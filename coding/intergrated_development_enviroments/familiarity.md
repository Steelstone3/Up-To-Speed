# Familiarity With Intergrated Development Enviroments

## Introduction

Familiarity with an Integrated Development Environment (IDE) is crucial for developers as it provides a comprehensive software development environment with various tools and features that aid in creating and debugging code. IDEs offer a one-stop solution that includes features such as code editors, debuggers, version control systems, and build automation tools, allowing developers to increase their productivity and efficiency.

## Code Editor

A code editor is a software application that allows developers to create and modify software code that is a core part of any IDE.

Code editors provide a variety of features to make coding more efficient, such as syntax highlighting, code completion, and debugging tools. They also support multiple programming languages and allow developers to customize the editor to suit their needs.

In Visual Studios case during the installation process there are many different packages that can be picked from based on the specific needs of the project such as ASP.net tooling for web development with Razor and C++ 20 libraries for C++ development in addition to the typical C# with .net.

## Version Control

Version control is a system that tracks changes made to software code or any other set of files over time. It allows for multiple developers to collaborate on a project, track changes made to the codebase, and maintain a history of all versions of the code.

Version control provides many features including

> - Revision Tracking
>
> - Branching
>
> - Merging

The most commonly used version control system is "Git". This tool is both powerful and modern and contains the following features:

> - Committing local work
>
> - Pushing local work to a remote repository
>
> - Pulling changes down from a remote repository
>
> - Branching
>
> - Merging work into a branch
>
> - Fetching remote updates of a branch
>
> - Rebasing to the latest changes on a branch

This is covered in more depth under [version_control.md](../../version_control/version_control.md).

IDEs often have plugins for or directly integrate "Git frontends" within the tooling options it provides developers. Often these frontends aim to simplify the power and complexity of "Git" with shorthands such as "git sync" which usually fetches the latest of a branch and pushes changes to the remote.

Within this tooling also often comes the means to resolve merge conflicts. Within "Visual Studio 2022" this can be found under view/git changes (see [sources.md](../../sources.md)).

## Debugging

Debugging is a process of identifying and fixing errors, bugs, or defects in software code to ensure that the program works as intended.

This process involves

> - Reproducing the issue
>
> - Finding the issue from within the code
>
> - Fixing the issue
>
> - Testing the program to check that it now behaves as intended as described in the specification

There are many technequies that can be used within this process to help track down and fix the issue. These include:

> - Layers of testing
>
> - Logging
>
> - Tracing
>
> - Breakpoints

Breakpoints specifically are a tool used in IDEs. They allow developers to pause the execution of a program at a specific point and inspect the state of the program. Once a breakpoint is set, the program will stop running at that point, allowing the developer to examine the values of variables, data structures, and other program elements.

Breakpoints can be set in several ways, including by clicking on the line number in the code editor, by inserting a debugging statement in the code, or through the use of a debugging API. They can also be conditional, meaning that the program will only stop if a particular condition is met.

When supported by the testing pyramid this is a good means for routing out unexpected behaviours with a program being developed; However it is a time consuming process so should not substitue the various layers of testing that provide code confidence.
