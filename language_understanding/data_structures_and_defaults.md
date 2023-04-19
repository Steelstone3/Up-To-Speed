# Data Structures & Defaults

## Introduction

In C#, data structures are used to organize and store data in a way that enables efficient manipulation and retrieval. Some of the most commonly used data structures in C# include:

> - Arrays: Arrays are used to store a collection of elements of the same type. They are fixed in size and can be multidimensional.
>
> - Lists: Lists are used to store a collection of elements of any type. They can dynamically grow or shrink in size.
>
> - Stacks: Stacks are used to store a collection of elements in a Last-In-First-Out (LIFO) order. Elements can only be added or removed from the top of the stack.
>
> - Queues: Queues are used to store a collection of elements in a First-In-First-Out (FIFO) order. Elements can only be added to the back of the queue and removed from the front.
>
> - Dictionaries: Dictionaries are used to store a collection of key-value pairs. Each key must be unique, and values can be of any type.
>
> - Linked Lists: Linked lists are used to store a collection of elements that are connected through a series of nodes. Each node contains an element and a reference to the next node in the list.
>
> - Trees: Trees are used to store a collection of elements in a hierarchical structure. Each element is called a node, and nodes are connected through parent-child relationships.

## Data Structures

T represents a generic meaning these data structures can take any type with the same behaviours for the data structure itself.

Type | Represents | Default Value
:-- | :--: | :--:
int[] | Array | null
List\<T> | List collection | null
Stack\<T> | Stack | null
Queue\<T> | Queue | null
Dictionary\<TKey, TValue> | Dictionary of key-value pairs where TKey represents the key and TValue the value | null
LinkedList\<T> | LinkedList | null
Tree\<T> | Tree | null
