# Introduction

Coupling is the concept used to describe the degree to which different modules, components or classes in a software system depend on each other.

## Loose Coupling

Loose coupling refers to a situation where the components are independent of one another.

Generally this is the approach that is taken for OOP.

## Tight Coupling

Tight coupling refers to a situation where the components in a software system are strongly dependent on one another.

## Significance

Coupling is situational in development and it often depends on the design. The way to think about this is through aggregates and components. This approach will lead to better design.

In the context of what is being discussed...

### Aggregate

An aggregate can be seen as "loosely coupled". It is to put related systems together (through aggregation) whilst keeping them as separate concepts.

For example a Chimpanzee is a animal that can live in a location where that location the chimpanzee is assosiated could be a zoo or it could be the jungle.

The key point here is both the Zoo and Chimpanzee can exist together or separately and can therefore be described as an aggregate relationship.

### Component

Components meanwhile is to describe a "tightly coupled". It to put codependent systems together keeping them as a combined concept.

A good example of this can be seen in a computer. A computer runs as a sum of all of its parts and doesn't work properly if any one of those parts is faulty or missing.

For example a computer without RAM would have no fast access storage for running high demand modern programs and would likely crash.

Within this example we can see the strength and weakness of this concept... it is tightly coupled. This is to say if a single part of the whole was to go wrong the whole thing would collapse. This is why it is wise to be selective about when you apply this approach.

## Application

Applying the correct type of coupling is an important part of software design and there is no hard or fast rule just good judgement from expierence. TDD lends itself to helping decide upon which approach is best to take.

### Components > Aggregate

- View Models
- Large Models
- A zoo with animals (context matters)

### Aggregate > Components

- A zoo with animals (context matters)
