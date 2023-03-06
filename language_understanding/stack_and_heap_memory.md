# Stack & Heap Memory

## Introduction

Stack and heap are two regions of memory in computer systems that are used for different purposes:

## Value Types

Value types are primative types being used as pass-by-value. The parameters passed in by value create an enviroment that is destroyed at the end of the method's execution. The enviroment contains a value copy of the values passed into the method.

```cs
// In this example points creates an enviroment on the stack
// This enviroment is destroyed at the return of this method
// The values are passed in by value as a copy of the memory is created on the stack
// The result is returned
public uint CalculateGraph(uint points)
{
    ...

    return points
}
```

## Reference Types

Reference types are primative types being used as pass-by-reference, data structures and objects. The parameters passed in by reference create an enviroment that is destroyed at the end of the method's execution. The enviroment contains a pointer to the values stored on the heap updating the original store of memory.

```cs
// In this example points creates an enviroment on the stack
// This enviroment is destroyed at the return of this method
// The values are passed in as parameters by reference as a pointer to  the memory on the heap is created
// The result is returned
public void CalculateGraph(ref uint points)
{
    ...
}
```

## Stack

The stack is a region of memory used for the execution of functions or methods in a program. It operates in a Last-In-First-Out (LIFO) manner. Each time a function or method is called, a new stack frame, also known as an activation record, is created and pushed onto the stack. The stack frame contains information such as local variables, function parameters, return addresses, and other execution context data and is accessed through value types (primatives).

Key characteristics of the stack include:

### Fixed size

The size of the stack is predetermined and limited, usually defined during the compilation or runtime configuration.

### Fast access

Accessing and deallocating memory on the stack is fast since it involves adjusting the stack pointer.

### Automatic memory management

Memory allocation and deallocation on the stack are managed automatically by the compiler or runtime system.

### Limited lifespan

Variables allocated on the stack have a limited lifespan and are deallocated when they go out of scope or when the function or method returns.

## Heap

The heap is a region of memory used for dynamic memory allocation. It is a more flexible memory space where objects and data can be dynamically allocated and deallocated as needed. Memory allocation on the heap is done when passing by reference (objects, data structure, primatives passed as reference types (ref))

Key characteristics of the heap include:

### Dynamic size

The heap can grow or shrink based on the memory allocation and deallocation operations.

### Slower access

Accessing memory on the heap is relatively slower compared to the stack as it involves searching for available memory blocks and managing the allocation and deallocation processes.

### Manual memory management

Memory allocation and deallocation on the heap are managed manually by the programmer. It is the responsibility of the programmer to allocate memory when needed and explicitly deallocate it when no longer required.

### Extended lifespan

Objects or data allocated on the heap can persist beyond the scope of a function or method. They need to be explicitly deallocated to free up memory resources.

## Conclusion

In most programming languages, value types are stored on the stack and reference types are stored as pointers on the stack aimed at memory on the heap. It is important to manage memory usage efficiently to avoid issues like memory leaks (unreleased memory) or accessing deallocated memory, which can lead to unpredictable behavior or program crashes.
