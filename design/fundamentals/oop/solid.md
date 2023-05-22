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

### Example

As a brief overview take the "Dog" class example. Lets say our Dog can walk, run, crawl, breath, play fetch, swim, wag tail and a few other things like that. 

All of these behaviours relate to the being a dog concept. 

If this class is within 100 lines it is reasonable to say this class follows single responsilbity. 

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
  Mobility{get;}
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

### Example

Imagine we are 
