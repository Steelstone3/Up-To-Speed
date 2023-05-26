# Object Calisthenics

## The Rules

> 1. One level of indentation per method
> 2. Don’t use the ELSE keyword
> 3. Wrap all primitives and Strings
> 4. First class collections
> 5. One dot per line
> 6. Don’t abbreviate
> 7. Keep all entities small
> 8. No classes with more than two instance variables
> 9. No getters/setters/properties
> 10. Skippy's Custom Rule 9: No Public Setters On Properties

## Rule 1: One Level Of Indentation Per Method

What is allowed

```cs
if(someCondition1 && someCondition2)
{
    DoTheThing();
}
```

What is not allowed

```cs
if(someCondition1)
{
    if(someCondition2) 
    {
        DoTheThing();
    }
}
```

This is to ensure simpler and more understandable flow within methods

## Rule 2: Don’t Use The ELSE Keyword

What is allowed

```cs
Job BobJobChoice(bool isEmployed) {
    if (isEmployed) {
        return BobMakesCandles();
    }

    return BobMakesFireworks()
}
```

What is not allowed

```cs
Job BobJobChoice(bool isEmployed) {
    if (isEmployed) {
        return BobMakesCandles();
    }
    else {
        return BobMakesFireworks();
    }
}
```

This is to enforce the power of polymoriphism and to remove un-needed else statements.

## Rule 3: Wrap All Primitives and Strings (Value Objects)

Can return primatives from methods but must use abstract wrapped types for parameters

What is allowed

```cs
interface IWeapon {
    uint CalculateDamage()
}

class Sword : IWeapon {
    private uint damage = 10;
    private uint numberOfAttacks = 2

    public uint CalculateDamage() {
        return damage * numberOfAttacks
    }
}

class Ninja {
    uint health = 100;

    void TakeDamage(IWeapon weapon) {
        health -= weapon.CalculateDamage()
    }
}
```

What is not allowed

```cs
class Ninja {
    uint health = 100;

    void TakeDamage(uint damage, uint numberOfAttacks) {
        health -= damage * numberOfAttacks
    }
}
```

This deals with a code smell called primative obsession.

## Rule 4: First Class Collections

What is allowed

```cs
class Inventory{
    private readonly List<IItem> items = new();

    public void AddItem(IItem item) {...}
}
```

What is not allowed

```cs
class Inventory{
    private readonly List<IItem> items = new();

    // Random other class member just to make the point
    private IWeapon weapon = new Sword()
}
```

Any collection gets wrapped within its own class. Therefore any behaviours related to that collection are treated as a single responsibilty boundary.

## Rule 5: One Dot Per Line

What is allowed

```cs
Dog.WagsTail();
```

What is not allowed

```cs
Dog.HappinessDetector.Tail.WagsTail();
```

Protects from open closed principle violation

## Rule 6: Don’t Abbreviate

What is allowed

```cs
private Coordinate coordinate

public Coordinate FindCoorinatesOfTheTreasure() {...}
```

What is not allowed

```cs
private Coordinate xY

public Coordinate FindXY() {...}
```

Explaining what the code is doing with method and variable declarations can save time writing and maintaining comments (that do go stale in codebases)

## Rule 7: Keep All Entities Small

No class should be over 50 lines

No method should be over 10 lines

No folder should be over 10 files

This rule is extreme for the purposes of this exercise but the point being large methods and classes are unwieldy

(Realistically 100 lines of code (ignore using statements in the count) for classes 15 lines for methods)

## Rule 8: No Classes With More Than Two Instance Variables

What is allowed

```cs
class Name {
    private GivenNames givenNames = new GivenNames();

    public void AddName(GivenName givenName) {...}
    public void DisplayGivenNames() {...}
}

class GivenNames {
    List<GivenName> names = new();

    public void AddName(GivenName name) {...}
}

class GivenName {
    private string name;

    public GivenName(string name) {
        this.name = name
    }
}
```

What is not allowed

```cs
class Name {
    string firstName;
    string middleName;
    string lastName;
}
```

A class responsible for lots of internal state cannot claim to be single responsiblity

## Rule 9: No Getters/ Setters/ Properties

What is allowed

```cs
class Ninja {
    private IHealth health = new Health();

    void TakeDamage(IWeapon weapon) {...}
}
```

What is not allowed

```cs
class Ninja {
    private IHealth health = new Health();

    void SetHealth(IHealth health) {...}
}
```

OR

```cs
class Ninja {
    public IHealth Health {get; set;} = new Health();
}
```

This is to enforce encapsulation in all value objects

## Skippy's Custom Rule 10: No Public Setters On Properties

The previous rule 9 is near impossible to not violate at some point. Therefore with the exception of patterns that demand public setters on properies such as MVVM public setters are not to be used to keep in the overall spirit of the previous rule whilst making it workable for the actual codebase. Where possible the previous rule 9 still applies.

What is allowed

```cs
public int Damage {get; private set;}

public int NumberOfAttacks {get; protected set;}
```

What is not allowed

```cs
public int Damage {get; set;}
```
