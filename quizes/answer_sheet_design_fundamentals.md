# Up To Speed Quiz - Design Fundamentals: Answer Sheet

## I'm Too Young to Die Answer 1 (2.5)

* Single responsibility
* Open closed
* Listov's substitution
* Interface segregatoin
* Dependency inversion

## I'm Too Young to Die Answer 2 (2)

* Abstraction
* Encapsulation
* Inheritance
* Polymorphism

## I'm Too Young to Die Answer 3 (1.5)

* Don't
* Repeat
* Yourself

Subscore (6 / 6)

## Hey, Not Too Rough Answer 1 (0.75)

Abstractions hide unnecessary details so they can focus on main characteristics and behaviour

A: To increase code flexibility, extensibility, modularity and maintainability. To provide encapsulation and to not violate the D in SOLID

## Hey, Not Too Rough Answer 2 (0.75)

So they isolate one thing and prove if it works

## Hey, Not Too Rough Answer 3 (0 / 0.75)

Can reuse lots of code so not much code repetition

A: Safe polymorphism is the main advantage that OOP provides as a paradigm. Functional polymorphism is achieved with function pointers which is an unsafe practise.

## Hey, Not Too Rough Answer 4 (0.75)

Provides confidence that the code has the desired function and the implementation stays focused on what is necessary

## Hey, Not Too Rough Answer 5 (0.75)

Allows easy testing and debugging and suggestions help to write code quicker

Subscore ( 3 / 3.75)

## Hurt Me Plenty Answer 1 (2 / 3)

Composition means components are tightly coupled whereas aggregation means they are loosely coupled. With aggregation, related systems are put together whilst remaining separate, but in composition, the systems are kept as a combined concept and are codependent.

A: (For the extra point) For example a zoo can contain animals is an example of compisition however if those same animals also can live in the jungle then this is an example of aggregation.

## Hurt Me Plenty Answer 2 (2 / 3)

Testing pyramid has unit tests at the bottom, then integration tests and finally manual tests at the top (the smallest section). This is in order of time taken. Most of the tests should be unit tests as they take the shortest time and can be automated. Manual tests take a long time and require a human to complete, which is also more costly.

A: Unit tests, Acceptance tests, Integration tests, Automated UI Tests, Exploritory/ Manual testing

A: For example unit test suites complete in approximately 2 seconds where automated UI testing may be run once a day on a build server

## Hurt Me Plenty Answer 3 (2.5 / 3)

* List is a finite, ordered sequence of items. More flexible than stacks and queues as any element can be accessed.
* Stack is LIFO, elements are pushed onto the stack when they are added and popped from the stack when they are removed.
* Queue is FIFO, elements can only be inserted at the back and removed from the front.

A: Enqueue, Dequeue keywords

Subscore (6.5 / 9)

## Ultra Violence Answer 1 ( 10 / 30)

* Single responsibility: Classes and methods only deal with one concept
* Open closed: A class is open for extension but closed for modification
* Listov's substitution: Any subclass can be substituted for any of its base classes (most of the time)
* Interface segregatoin: Nothing should depend on an interface that it doesn't actually use
* Dependency inversion: Things should depend on abstractions and not concrete types, so any abstract type can use any concrete type that inherits from it

A: Explain the reasons behind each principle of SOLID to help SOLIDIFY... (pun intended) the purpose behind each

## Ultra Violence Answer 2 ( 8 / 24 )

* Abstraction: Details should be hidden so can focus on main characteristics and behaviour
* Encapsulation: Internal state should be hidden
* Inheritance: New classes should be created as subclasses based on existing classes, from which they inherit properties
* Polymorphism: Objects can take on multiple forms, through method overriding and overloading

A: Explain the reasoning behind each of the principles of 4 pillars

## Ultra Violence Answer 3 (4 / 6)

* Inside-out developement is where software is developed from the detail to the overarching design architecture using TDD and unit tests.
* Outside-in is where software is developed from overarching design architecture to the detail. Also a TDD approach but uses test doubles.
* The two can be used together in a reg -> green -> refactor TDD approach.

A: Close! Behaviour Driven Development Outside-In Inside-Out double loop for how the two techniques can be used together. Start with the behaviours you expect to be called on the outside writing an acceptance test and using test doubles. Move in to the inside and make steps towards the acceptance test using inside-out

Subscore (22 / 60)

Score (37.5 / 78.75 | 47.62%)

## Nightmare Difficulty Answer 1 (0 / 25)

Attempt these if you dare!

* 1 point for the error the code would produce
* 1 point for the term
* 3 points for why it is a bad practise
* 3 points for why the error would occur

## Nightmare Difficulty Answer 2 (0 / 90)

Attempt these if you dare!
