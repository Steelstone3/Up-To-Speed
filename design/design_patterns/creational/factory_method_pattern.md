# Factory Method

## Introduction

Factory Method is a creational design pattern that provides an interface for creating objects in a superclass, but allows subclasses to alter the type of objects that will be created.

## Problem

Imagine that you’re creating a logistics management application. The first version of your app can only handle transportation by trucks, so the bulk of your code lives inside the "Truck" class.

After a while, a new requirement comes from sea transportation to support sea logistics.

But how will the code handle this? At present, most of your code is coupled to the "Truck" class. Adding "Ships" into the app would require making changes to the entire codebase. Additionally the code at present isn't extendable so would require complete reworks for each new requirement.

As a result, the code will be riddled with conditionals that switch the app’s behavior depending on the class of transportation objects.

## Solution

The Factory Method pattern suggests that you replace direct object construction calls with calls to a special factory method. This abstracts the construction of the object to within the factory method. Objects returned by a factory method are often referred to as products.

## UML

![Alt text](../../../../assests/factory_pattern.svg)
