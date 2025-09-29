# How To Do A Proper Code Review

## Introduction

Pull requests don't form part of every development approach. However, it is an important ceremony used for peer reviewed quality assurance. Other development approaches may use something else in place such as pair programming. If you are however asked to conduct a code review this blog can serve as a guide.

## Process

Very importantly a process for reviewing code needs to be established.

This documentation needs to be readily accessible in a common easy to find location and will act as a kernel of truth for when (not if) conflicts arises.

All members of the team should be involved in generating this process as it will act as the agreed upon standard.

If the standards are not being upheld this can be discussed in the retrospective ceremony.

### Example Process

An example of process may be the following:

- Code reviews to be conducted within 3 hours of being received
- All code reviews require 1 developer's approval
- Larger changes require more than 1 developer's approval
- Fundamental architectural changes require 1 principle developer's approval
- Changes to the develop branch must be made via pull request
- Changes to the develop branch must compile, pass all existing tests and pass all new tests added

With some standards in place for what is expected from developers

- All code reviews where possible should have accompanying test suites
- Review tone must be constructive
- Developers must not gate-keep the code review process
- Domain knowledge should be valued and considered when choosing a reviewer

and so on

## Review Tone

Criticism even when constructively delivered is difficult to receive. This needs to be the primary understanding before even touching the keyboard to write your first comment.

Review tone needs to be collaborative and the person's code that is being reviewed needs to be receptive to the feedback.

### As The Reviewer

Take the approach of politely questioning decisions rather than making outright accusations on approaches taken. Be prepared for push back as you were likely not involved in the process that ultimately lead to that design decision. You as the reviewer may be missing key details that the author of the code changes has.

Be considerate to the effort that has been put in to the work. Remember the end goal of a code review is to polish the submitted work up to a standard that all have agreed to upfront by the development team.

### As The Code Author

Remember the reviewer is trying to help improve the quality of the code.

Any suggestions that are made are (in most cases) feedback and not a personal attack.

Back the decisions you have taken to reach the outcome whilst being open to other reasonable suggestions.

Remember the reviewer may not be familiar with the area of the domain.

## What Not To Do

A lot of the time in code reviews developers quibble over semantics. For instance a common "review" of code could look something like:

```cs
// Version A
if(hasBeenDeleteed)
  item.DoesNotExist();

// Version B
if(isDeleted)
{
  item.DoesNotExist();
}
```

In this example the semantics obsessed reviewer will argue Version A looks worse than Version B and contains a spelling mistake "Deleteed".

This type of review is nitpicking where neither the quality or performance of the code is improved and most critically wastes time better spent finding more fundamental issues with the submitted code.

Point the developer to the styling guidelines of either the language or the organization. Raise this in retrospective if one does not exist whereby you would agree to disagree on the code style that should be left out of code reviews.

Make a quick comment to note the spelling mistake "hasBeenDeleted" will suffice you are not marking English homework here.

The only exception to the "variable name" "method name" "code style" semantic review is where it affects other developers ability to interpret the code significantly. This is rare and should still be the last thing addressed in a code review.

## What To Look For

Look for fundamental issues with the code. I cannot extensively cover every single example but here are a few common mistakes to look out for.

### DTO/ UI Mapping

Controllers should only be used to determine state on user actions such as "update" "replace" and so on. Variable assignment in data transfer object mappers, UI elements and so on should be done on construction of the type.

This pattern will cause out of sync data and unnecessary computational cycles on draw calls.

```cs
public ShoppingListDto ShoppingListDtoMapper(ShoppingList shoppingList) {
  return ShoppingListDto {
    FruitList = _listController.GetFruitList(),
    MeatList = shoppingList.MeatList
  }
}
```

Should be

```cs
public ShoppingListDto ShoppingListDtoMapper(ShoppingList shoppingList) {
  return ShoppingListDto {
    FruitList = shoppingList.FruitList,
    MeatList = shoppingList.MeatList
  }
}
```

### Variable Order

Variable order is another common bug

```cs
public class OrderService {
  public void PlaceOrder(Address shippingAddress, Address billingAddress) {
    _orderController.PlaceOrder(billingAddress, shippingAddress);
  }
}

public class OrderController {
  pubic void PlaceOrder(Address shippingAddress, Address billingAddress) {
    ...
  }
}
```

In this example the placed order in the service will send the item to the billing address and bill the item to the shipping address. These may be different from one another.

A good solution to this can be type restriction. This is known as smart construction. When providing feedback it is important to consider design patterns and concepts that make it harder for the next developer to repeat the mistake.

```cs
// Domain Layer

// Wrapper type of Address
public class BillingAddress {
  public Address { get; }
}


// Wrapper type of Address
public class ShippingAddress {
  public Address { get; }
}

// Internal class to the domain project in hexagonal architecture
// This ensures Address can't be used as a variable in other areas of the program outside of the domain model layer
internal class Address {
  ...
}

// Application Layer
public class OrderService {
  public void PlaceOrder(ShippingAddress shippingAddress, BillingAddress billingAddress) {
    // This line won't compile
    _orderController.PlaceOrder(billingAddress, shippingAddress);

    // This line however will compile
    _orderController.PlaceOrder(shippingAddress, billingAddress)
  }
}

public class OrderController {
  pubic void PlaceOrder(ShippingAddress shippingAddress, BillingAddress billingAddress) {
    ...
  }
}
```

### Non-Atomic Database Calls

Non atomic database calls are wasteful to computing resources and often breaks database normalization.

```cs
public void UpsertRace(DatabaseConnection database, Race race) {
  string raceStatistics = _raceSerializer(race.Statistics);
  string raceResult = _raceSerializer(race.Result);

  database.Upsert(raceStatistics);
  database.Upsert(raceResult);
}
```

In this case there is no reason a race can't be upserted to the database as a single call to the database.

This is often the first place to check when wanting to optimize an application.

```cs
public void UpsertRace(DatabaseConnection database, Race race) {
  string raceString = _raceSerializer(race);

  database.Upsert(raceString);
}
```

### Other Areas To Check

- [Code smells](<https://refactoring.guru/refactoring/smells>)
  - Speculative generality
  - Anemic domain models/ Lazy class
  - Large classes
  - Long methods
  - Long parameter lists
  - Feature envy
  - Middle man
  - Alternative classes with different inheritance
- [Poor usage of patterns](<https://refactoring.guru/design-patterns>)
  - Repeats in code that need refactoring
  - Factory method over builder pattern
  - Builder pattern over factory method
  - Singleton anti-pattern
  - Needless use of prototypes/ clone/ deep clone pattern
  - Inheritance over composition
  - Creating patterns that exist in the language
    - C# for [example](<https://www.youtube.com/watch?v=4rQ0jFmKSgk>)
    - Iterator
    - Chain of responsibility

## Common Problems With Code Reviews

### Semantic Code Reviews

Mentioned above these code reviews don't address points of quality but instead obsess around how pretty the code looks. Train, educate, use documentation where necessary to ensure a good standard of code review is being conducted.

### Time

Code reviews take significant time to complete properly. This should be accounted for in the size of the change request.

Take a hard zero-tolerance stance on large change requests. Ensure all members of the team do the same to prevent bad actors on the team from chucking in large balls of un-reviewable mud.

### Gate-Keeping

Don't be a gate-keeper and don't allow others to gate-keep when it comes to code reviews. What do I mean by gate-keeping in this context.

- A junior should be allowed to review a principle developers work as the main reviewer
- A junior should be allowed to review another juniors' work as the main reviewer
  - A principle should not be conducting the main review if they are an optional reviewer on a junior reviewing junior code review
  - A principle should pick up anything that has been missed by the reviewing junior once the junior has finished conducting their code review
- A principle should not be allowed to prevent a juniors' work from being merged just because they have less experience
- Good code is good code

By not sticking to these principles as a more experienced developer you will be stifling growth of up and coming talented junior developers that one day may be in a similar position to you and a better person for anything you put them through at this point in their career.

### Poor Review Tone

Criticism can be levelled in ways that is very hurtful to the author of the code as a form of belittling, bullying, elitism or superiority. Don't stand for this. Put the review process on hold be prepared to speak to the individual about their conduct in a calm and professional way. Escalate where necessary.

See guidance above for correct conduct.

## Conclusion

You will often find throughout your career that code reviews boil down to box ticking exercise as part of some agile process of "quality assurance". This is wrong. Code reviews must be conducted properly or there is no point to the ceremony. If one fails to do the process correctly the team fails to do the process correctly.

Lets make a start in doing better code reviews from today.
