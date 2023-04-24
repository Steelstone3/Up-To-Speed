# Outside-In

## Introduction

Outside-in test driven development is the process of developing software from the overarching design architecture to the detail. This test driven approach uses test doubles to check component interactions within a tested unit.

## Design Using Outside-In TDD

In order to design code using outside-in TDD we must ensure we use the same test double reference; we must also make sure that we depend on abstractions rather than concretes through the use of interfaces that can be overriden by mocking libraries.

For this to be the case the object in question must override an interface passed in as a parameter through the constructor or method being tested.

### Example Of Structure Using Constructor Parameters

```cs
public class ExampleClass : IExampleClass
{
    // Private field created that will use the same reference as in the tests
    private readonly IComponentInterface component;

    // Test doubles can override "component" and use the same reference as in the tests
    public ExampleClass(IComponentInterface component)
    {
        this.component = component;
    }

    public void SomeMethod() 
    {
        // Using the same reference we are then able to test this behaviour is executed
        component.SomeActionFromTheComponent();
    }
}
```

### Example Of Structure Using Method Parameters

```cs
public class ExampleClass : IExampleClass
{
    // Test doubles can override "component" and use the same reference
    public void SomeMethod(IComponentInterface component) 
    {
        // Using the same reference we are then able to test this behaviour is executed
        component.SomeActionFromTheComponent();
    }
}
```

### Poor Design

This may at first seem restricting at first however, oop code design principles state to depend upon abstractions.

In the example below "SomeMethod()" is tightly coupled to the "Component" class which means that testing "SomeMethod()" would also be testing "Component" which is also poor test design and an approach that can be often taken (by accident) from doing "Test After Development" (TAD).

In the example below any changes made to how the component class works will have a direct impact on "ExampleClass"

```cs
public class ExampleClass : IExampleClass
{
    public void SomeMethod() 
    {
        // Using the concrete directly couples the behaviour of "Component" to "ExampleClass"
        // This violates the D in SOLID 
        new Component().SomeActionFromTheComponent();
    }
}
```

## Best Practise

* Focus on covering the public interface of each class (public methods)
* Ensure edge case behaviours are covered in the tests by thinking about the ways in which the method can be used and abused through stubbing.
* Ensure components are making expected method calls usings mocks.
* Create fakes for complex external systems (mainly).
* Use a mocking library.

## Example

