# All Systems Are Real Time Systems

## Introduction

> What are real time systems?

Real time systems are time critical systems that perform real-time application functions. Normal examples include autonomous driving or air traffic control systems.

Without meeting strict time constraints of application execution these systems would fail to function safely.

## Loose Time Constraints

Typically "non" real time systems, a typical application, are created with a loose ideal of general acceptable user performance. The difference here is in these systems time is not of critical importance... or is it?

Just because there is a loose constraint to fufil a user's expected performance doesn't mean it shouldn't hold value. For instance take a e-commerce site, a user who is waiting over a second to view a product would likely get fed up waiting for that particular companies site where better performing ones are avaliable.

So from this we can extrapolate that where time is a loose constraint it still holds importance to the user expierence and therefore does have a strict time constrant of user acceptability. This therefore makes every system a real time system (from a certain point of view).

## Measuring Performance

There are many ways to measure the performance of code and not all are obvious. It is incredibly important when optimising code to measure first.

### Profiling

Profiling is a measurement of code performance taken through a tool known as a profiler.

Using a profiler allows us to assertain the time taken and how often the method is executed. This allows us to determine where to focus code optimising development efforts.

### User Acceptance

Users are a valuable asset and an important stakeholder when it comes to software development. Sometimes just simply asking a user to report any sub-optimal expierence of a program allows for a development team to better focus efforts towards improving the end user's expierence.

Like before there are some important measurements we can take from user feedback

> - Parts of the program that are unresposive from over a second. It may be a visual indicator is required or backend optimisations/ code to be written in a non-blocking way
>
> - Parts of the program that feel slow. It is important to work out how often the user uses this feature before putting in the development effort.

## Common Occurances

The first thing we should analyse when it comes to code performance is "the easy wins". Whilst ["Molly Rocket"](<>) brings up excellent points about how code can be optimised by breaking well established coding standards his example is both contrived and not the place anyone should start when looking at enterprise systems.

### I/O

Reading and wrtitting to files is one of the slower tasks any system can perform. Testing around this area comes under the category of integration testing due to the fact these tests run 100x upwards slower of a standard unit tests.

Data access layers are usually written asynchronously for CRUD operations. This is really important not for outright speed and performance but to ensure the user expierence isn't blocked by CRUD operations.

Nested data structures can also take a database a longer time to write than flattened data structures. Consider how the data is being entered and where you might want to nest, flatten, merge or have separate data structures. The less write/ read calls the faster the database performance and small gains here will lead to massive gains when scaled.

Most database technologies have optimisations for better vertical or horizontal scaling examples include indexing and sharding. For searches of large data indexing can significantly improve data retrival times.

Consideration for the database technology or if a database should be used. Switching out a database technology can be an extreme step however certain database technologies may be more fit for purpose for the application being built. Principally a well written data access layer should have a near seemless translation from one to the other once the CRUD operations are re-written.

### Architectural Bottlenecks/ Latency

Latency between two systems communicating can very occasionally be a lack of capacity but often is more likely coming from poor aritectural design.

Micro-services as an example have larger latency than monolith architectural structures along with repition at the bounds of the system.

Additionally bottlenecks can form from service to service communication even with sufficient load testing before a system goes live. Testing a system's scalability is important and ensuring data passes through the system in an optimised way is mission critical.

### Mission Critical Services

Code that gets run a lot and takes time to execute is the first order of business once the other issues listed above have been addressed.

The two important factors are:

> - The time taken to run a method
>
> - How often is that method executed

It is from this we can reason that code executed a lot that takes a long time to run is the starting point for any code optimisation work to take place.

> For example is method A takes 6 seconds to run and method B takes 500ms to run in a vacuum you would maybe put your attention on method A. However, if method B is run over 10,000 times more often than method A there is a larger performance benefit for speeding up method B to the application.

### Language Quirks

Certain languages have certain performance gotchas. However it is important not to focus on the minusha that gets optimised away on compilation. Instead the focus on optimisations should come from measured evidence.

> For example C# uses garbage collection memory management and a unique case at work found strings created for the express purpose of construction needed repeated garbage collection as many of these objects were being created. The solution was to inline the variable and this saw significantly less calls to the garbage collector and therefore significantly better performance (as well as new coding standards).

The point isn't to know all this stuff up front but to be aware that it will occur regardless of the language and to learn from each expierence.

## Optimising Code

The main takeaway from all of this is the following. When optimising code on all parts of the system

> Discover the performance issues and bottlenecks with the program
>
> Organise the work for the easiest wins that will provide the most performance improvements to the most users first

Then

> Measure the current performance
>
> Assertain the desired performance
>
> Make a change
>
> Re-measure the performance
>
> Check for bugs/ regressions
>
> Version the change
>
> Repeat

It is also important to note that completing the features for a system normally takes a higher prority unless the unoptimised code is mission critical.

## Conclusion

Admission that all systems are real time systems is important in my view as it constrains us to considering how well optimised our deployed code is to the end user using it.

Consideration for the user expierence is important and is often overlooked in enterprise applications. Putting the user as the judge of a programs performance keeps us developers honest and able to create better applications in the long run.
