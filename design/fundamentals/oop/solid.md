# SOLID

## Introduction

SOLID in object oriented programming is a set of 5 principles to follow in order to create extendable and maintainable object oriented code.

## Acronym

The following letters correspond to the following principles:

> S - Single Responsibility
>
> O - Open Closed
>
> L - Listov's Substitution
>
> I - Interface Segregation
>
> D - Dependency Inversion

## Single Responsbility

The single responsibility principle is the idea of classes and behaviours (methods/ functions) dealing with 1 concept.

This is quite wooly as an OOP principle and requires some expierence to know where the approximate line to draw is in where one concept begins and another ends.

For example "Object Calisthenics" describes the case for 10 line maximum for methods and 50 lines maximum for classes. However the 50 lines for classes can be considered extreme by some developers who may choose 100 lines or to only consider the lines of functions.

For another example Lazy class smell may also need to be considered when deciding just how long to make a class or it will be accused of "not doing enough".

### Single Responsibility Example

As a brief overview take the "Dog" class example. Lets say our Dog can walk, run, crawl, breath, play fetch, swim, wag tail and a few other things like that.

All of these behaviours relate to the being a dog concept. If this class is within 100 lines it is reasonable to say this class follows single responsilbity.

However if this number starts to be pushed say the Dog class is at 1000 lines we need to consider putting groups of behaviours into sub-concept components with their own responsibility

So depending on context both

```cs
...

class Dog {
  void Walk(){...}
  void Run(){...}
  void Crawl(){...}

  ...
}
````

and

```cs
...

class Dog {
  IMobility Mobility{get;}

  ...
}

class Mobility {
  void Walk(){...}
  void Run(){...}
  void Crawl(){...}
}
```

are valid depending on how many behaviours and state both have as concepts

## Open Closed

Open closed principle is to state that a class is open for extension but closed for modification.

In simpler terms we want to provide classes with internal state that belongs to itself that it modifies

### Open Closed Example

Imagine we are creating a game

In this example the Ninja in our game is responsble for the means in which external classes modify its internal state. This is to say Ninja in this example is responsible for the way in which it takes damage.

```cs
class Ninja{
  private uint health;

  public Ninja() {
    health = 100;
  }

  // Ninja is responsible for the means in which it takes damage to health 
  // and enforces the use of weapons being the means by which it will take damage
  void TakeDamage(IWeapon weapon) {
    health -= (weapon.Damage * weapon.NumberOfAttacks);
  }
}
```

(primative obsession smell) We can also limit the scope of what can damage a ninja by wrapping primatives such as damage and number of attacks into a value object such as weapon.

Lets see how collaborators will now use this class

```cs
class CombatSystem {
  void Turn(INinja attackingNinja, INinja defendingNinja) {
    defendingNinja.TakeDamage(attackingNinja.EquipedWeapon);
  }
}
```

As we can see here the defending ninja is responsible for the means in which it takes damage from the attacking ninja's weapon

Now lets show a violation to drive home the point

```cs
class Ninja{
  public uint Health { get; set; }

  public Ninja() {
    Health = 100;
  }
}

class CombatSystem {
  void Turn(INinja attackingNinja, INinja defendingNinja) {
    defendingNinja.Health -= attackingNinja.EquipedWeapon.Damage * attackingNinja.EquipedWeapon.NumberOfAttacks;
  }
}
```

The above example violates the O in SOLID as Health is now exposed for external collborators to modify the internal state of Ninja.

This means the combat system is now responsible for the concept of how a Ninja takes damage which violates the S in SOLID as well. This is due to the game's combat system being responsible for the flow of combat and not the details of how ninjas attack and defend one another explicitly.

## Listov's Substitution

Annoyingly difficult to remember this one as it is forced to fit the SOLID acyronm.

Listov's Substitution principle is to state that any sub-class should be able to be substituted (swapped) for any base class.

```cs
class Animal {
  void Walk() {...}
  void Crawl() {...}
  void Run() {...}
  void Breath() {...}
  void MakeNoise() {...}
}

class Dog : Animal {
  void PlayFetch() {...}
}

class Cat : Animal {
  void Scratch() {...}
}
```

In the example above both dog and cat can be substitued under L for any of their behaviours besides "play fetch" specific to Dog and "scratch" specific to Cat.

Therefore...

```cs
class AnimalKingdomController {
  void PlayOutside(Dog dog) {
    dog.Run()
    dog.MakeNoise()
    dog.Breath()
  }
}
```

can become...

```cs
class AnimalKingdomController {
  void PlayOutside(Animal animal) {
    animal.Run()
    animal.MakeNoise()
    animal.Breath()
  }
}
```

Where both Cat and Dog are valid objects that can be passed into this class' method of "play outside"

## Interface Segregation

The interface segregation principle states "Clients should not be forced to depend upon interfaces that they do not use."

This is to state that when a sub-class is not using a method on the base class then it should only apply to the sub-classes that do use it.

For example

```cs
class Animal {
  void Walk() {...}
  void Crawl() {...}
  void Run() {...}
  void Breath() {...}
  void MakeNoise() {...}
  void PlayFetch() {...}
}

class Dog : Animal {
}

class Cat : Animal {
  void Scratch() {...}
}
```

Cat's don't play fetch so in this case we would want to move "play fetch" to the first place it becomes relevant to all sub-classes

In this case Dog is the only animal that "plays fetch"

```cs
class Animal {
  void Walk() {...}
  void Crawl() {...}
  void Run() {...}
  void Breath() {...}
  void MakeNoise() {...}
}

class Dog : Animal {
  void PlayFetch() {...}
}

class Cat : Animal {
  void Scratch() {...}
}
```

This can also apply to interfaces for example

```cs
interface IFile {
  void Load();
  void Save();
  void Print();
  void SendByEmail();
}

class Png : IFile {...}
class Exe : IFile {...}
```

In the example above many email providers don't allow executables to be sent as it may compromise their servers that provide email services

```cs
interface IFile {
  void Load();
  void Save();
  void Print();
}

interface ISendable {
  void SendByEmail();
}

class Png : IFile, ISendable {...}
class Exe : IFile {...}
```

and now this no longer violates I as Exe can use the entire IFile interface

## Dependency Inversion

Depend on abstractions and not on concrete types

The idea here being any abstract type can use any concrete type that inherits from the abstract type.

```cs
interface IFile {
  void Load();
  void Save();
  void Print();
}

class Png : IFile {...}
class Jpeg : IFile {...}

class FileController {
  void Save(IFile file) {
    file.Save();
  }
}
```

In this example anything that inherits from the abstract type of IFile can be used on the "save" method of file controller. This means that we have flexibilty such as to provide a new png implementation concurrently to safely refactor away the old type or implement a completely new sub-class that fufils the contract of IFile.

We can also use dependency injection to override IFile with a test double (dedicated section exists on test doubles).

```cs
class Png {
  void Load();
  void Save();
  void Print();
}

class Jpeg : IFile {
  void Load();
  void Save();
  void Print();
}

class FileController {
  void SavePng(Png png) {
    png.Save();
  }

  void SaveJpeg(Jpeg jpeg) {
    jpeg.Save();
  }
}
```

In this above example there are three main issues. Firstly save png and save jpeg can't have there respective parameters overriden with test doubles meaning both these methods within file controller are "untestable".

Secondly the fact file controller has two methods that both save is an indicator that we should use polymorphism and abstract away the concrete types being used.

Thirdly as a direct result of having two methods that both save our code is WET.
