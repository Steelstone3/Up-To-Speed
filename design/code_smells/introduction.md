# Code Smells

## Introduction

Code smells are a set of common programming issues that can indicate a deeper problem in the design or structure of code. They are called "smells" because they are often symptoms of larger issues, just as a bad odor can be a symptom of a larger problem.

Identifying and addressing code smells can help improve the maintainability, readability, and overall quality of code. Refactoring the code to address these smells can also make it easier to extend and modify the code in the future.

## Types

Code smells can be subdivided into types as follows:

### Bloaters

Bloaters are code, methods and classes that have increased to such gargantuan proportions that they are hard to work with. Usually these smells do not crop up right away, rather they accumulate over time as the program evolves (and especially when nobody makes an effort to eradicate them).

### Object Oriented (OOP) Abusers

These smells are incomplete or incorrect application of object-oriented programming principles.

### Change Preventers

These smells mean that if you need to change something in one place in your code, you have to make many changes in other places too. Program development becomes much more complicated and expensive as a result.

### Dispensables

A dispensable is something pointless and unneeded whose absence would make the code cleaner, more efficient and easier to understand.

### Couplers

The smells in this group contribute to excessive coupling between classes or show what happens if coupling is replaced by excessive delegation.
