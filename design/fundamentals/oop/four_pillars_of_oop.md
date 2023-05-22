# Four Pillars Of Object Oriented Programming

## Introduction

The four pillars of Object-Oriented Programming (OOP) are the fundamental principles that guide the design and implementation of object-oriented systems.

## The 4 Pillars

> * Encapsulation
>
> * Inheritance
>
> * Polymorphism
>
> * Abstraction

## Inheritance

Dog is-a Animal and can therefore do what all animals can and whatever a Dog can do on top.

Inheritance enables the creation of new classes (derived classes or subclasses) based on existing classes (base classes or superclasses). Subclasses inherit the properties (attributes and methods) of their superclasses and can add new or modify existing behavior. Inheritance promotes code reuse, as common attributes and methods can be defined in a superclass and inherited by multiple subclasses. It facilitates the creation of class hierarchies, where subclasses specialize or extend the behavior of their superclasses.

## Encapsulation

Hide internal state and provide a publically accessible means for the class to control its own state.

This

```cs
Ninja.TakesDamage(IWeapon);
```

Not this...

```cs
Ninja.Health -= Weapon.Damage;
```

Encapsulation is the principle of bundling data and related behaviors (methods) into a single unit called an object. An object encapsulates its internal state (data) and exposes a set of well-defined interfaces (methods) to interact with that state. Encapsulation promotes data hiding, where the internal details of an object are hidden from external entities, and access to the object's state is controlled through its methods. This allows for better control, security, and maintainability of the codebase.

## Abstraction

Abstraction allows for concepts of behaviour to be used whilst the details is left to the concrete type.

In the below example sword and mace can be used to damage the player's ninja. They both calculate damage differently but are both valid code that can be written DRY.

```cs
interface IWeapon {
   uint CalculateDamage();
}

// Sword is-a weapon
class Sword : IWeapon {
    uint damage = 50;
    uint numberOfAttacks = 3;
    uint CalculateDamage() {
        return damage * numberOfAttacks;
    }
}

// Mace is-a weapon
class Mace : IWeapon {
    uint damage = 30;
    uint numberOfAttacks = 6;
    uint CalculateDamage() {
        return damage * numberOfAttacks + numberOfAttacks;
    }
}

class Ninja {
    uint health = 100;
    
    void TakeDamage(IWeapon weapon) {
        health -= weapon.CalculateDamage();
    }
}

class CombatSystem {
    ...

    void Turn(IWeapon weapon) {
        player.TakeDamage(weapon)    
    }
}
```

and NOT the following example which violates abstraction and polymorphism. This is known as structural code...

```cs
class Sword {
    uint damage = 50;
    uint numberOfAttacks = 3;
    uint CalculateDamage() {
        return damage * numberOfAttacks;
    }
}

class Mace {
    uint damage = 30;
    uint numberOfAttacks = 6;
    uint CalculateDamage() {
        return damage * numberOfAttacks + numberOfAttacks;
    }
}

class Ninja {
    uint health = 100;
    
    void TakeMaceDamage(Mace mace) {
        health -= mace.CalculateDamage();
    }

    void TakeSwordDamage(Sword sword) {
        health -= sword.CalculateDamage();
    }
}

class CombatSystem {
    ...

    // TODO Use polymorphism and abstraction here
    void Turn(Mace mace) {
        player.TakeMaceDamage(mace)    
    }

     // TODO and here
    void Turn(Sword mace) {
        player.TakeSwordDamage(mace)    
    }
}
```

Abstraction focuses on representing the essential characteristics and behavior of an object while hiding the unnecessary details. It allows developers to create abstract classes and interfaces that define a common set of properties and methods that can be shared by multiple objects. Abstract classes provide a partial implementation, leaving specific details to be defined by subclasses, while interfaces define a contract that classes must adhere to. Abstraction enables the modeling of complex systems by breaking them down into manageable and understandable components, promoting modularity, and facilitating code maintenance and evolution.

## Polymorphism

Poly to mean many.

Morph to mean form.

Polymorphism is therefore the same code taking many forms.

Polymorphism means the ability of objects to take on multiple forms. In the context of OOP, polymorphism allows objects of different classes to be treated as objects of a common superclass. This is achieved through method overriding and method overloading. Method overriding enables a subclass to provide its own implementation of a method defined in its superclass, allowing different objects to exhibit different behavior while being accessed through a common interface. Method overloading allows multiple methods with the same name but different parameters to be defined in a class, providing different ways to perform an operation based on the type or number of arguments.

## Conclussion

By leveraging these four pillars, developers can create modular, reusable, and extensible code that models real-world entities and promotes good software design practices. These principles help improve code organization, maintainability, and scalability, making OOP a popular paradigm in modern software development.
