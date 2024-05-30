# Multi-Threaded Programming

## Introduction

Multi-threaded programming otherwise known as concurrent programming allows for the multi-core CPU architecture to be taken advantage of. For certain applications this speeds up code execution.

## Limitations

Multi-threading is prone to some well known pitfalls.

### Race Conditions

A race condition occurs when the outcome of a program depends on the unpredictable order in which threads execute. Proper synchronization is essential to prevent race conditions.

The most common example of this is two threads changing the value of one variable other code depends on.

For example in the "game of life" the next state would need to be determined from a immutable previous state in order to not create a race condition.

### Deadlocks

A deadlock happens when two or more threads are blocked indefinitely, waiting for each other to release the resources that they need. Careful design of resource allocation and synchronization is necessary to avoid deadlocks.

This is more likely to occur when utilizing lower level threading libraries.

### Starvation

Starvation occurs when a thread is perpetually denied access to a resource, preventing it from making progress. Fair scheduling algorithms and resource allocation policies can help prevent starvation.

## Best Practices

### Thread-Safe Data Structures

Employ data structures that are specifically designed to be used safely in a multithreaded environment. These data structures often have built-in synchronization mechanisms.

### Encapsulate Shared Data

Keep shared data and the code that accesses it within a well-defined module or class. This encapsulation makes it easier to manage synchronization and reason about the code's behavior.

### Test Thoroughly

Multithreaded code can be challenging to test. Use a variety of test cases to try to expose potential concurrency issues. Consider using tools that can help with concurrency testing.

### Keep It Simple

Multithreading adds complexity. Strive to keep your designs as simple as possible to reduce the risk of errors.

## Code Example

In C# some of these pitfalls are better handled in the high level wrapper of Task. Task provides a promise that wraps the existing low(er) level Thread library and is the modern approach to multi-threading.

```cs
public void ExampleOne() {
    // This runs a promise on a anonomous function with no return type
    Task task = Task.Run(() => {
        Console.WriteLine("Do a thing");
    
        for (int i = 0; i < 5; i++)
        {
            Console.WriteLine("Do a thing in a loop");
        }
    });
}

public void ExampleTwo() {
    // This runs a promise on a anonomous function with a int return type
    Task<int> task = Task.Run(() => {
        int result = 0;
        
        for (int i = 1; i <= 10; i++)
        {
            result += i;
        }

        return result;
    });

    // Wait for all tasks to complete.
    Task.WhenAll(task).Wait();

    // Gets the return of the task
    int result = task.Result;
}

public void ExampleThree() {
    // This runs a promise on a callback function with no return type
    Task task = Task.Run(ExampleThreeAction());
}

// Callback function where Action (a type of callback) stores a void method in an object
private Action ExampleThreeAction() {  
    Console.WriteLine("Do a thing");
    
    for (int i = 0; i < 5; i++)
    {
        Console.WriteLine("Do a thing in a loop");
    }
}

public void ExampleFour() {
    //  This runs a promise on a callback function with a int return type
    Task<int> task = Task.Run(ExampleFourFunc());

    // Wait for all tasks to complete.
    Task.WhenAll(task).Wait();

    // Gets the return of the task
    int result = task.Result;
}

// Callback function where Func (a type of callback) stores a method which returns an int datatype in an object
private Func<int> ExampleFourFunc() {
    int result = 0;
        
    for (int i = 1; i <= 10; i++)
    {
        result += i;
    }

    return result;
}
```
