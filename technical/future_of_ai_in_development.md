# Future Of AI In Development

## Disclaimer

This is just subjective opinion from a lay-person. I don't claim to be an expert in AI but have had experience in using them to generate images and have experimented with using them to assist with personal development projects.

## As Assistive Tools

Similar to the current state of generative AI tools now with more integration.

Picture the current work flow of a typical generative AI tool.

> You enter a prompt
>
> You get a response
>
> You copy the response into the project
>
> You compile the project
>
> You find the compilation errors
>
> You run the solution
>
> You find the bugs and fix them
>
> You write some tests and refactor the solution

The current state of generative AI isn't all that useful (dare I say) versus working the solution out for yourself or finding similar solutions on developer focused forums/ chat rooms (likely where the AI scraped it from).

Imagine a future scenario where an AI tool sends it output into a compiler and adjusts the code until it compiles.

Continuing down this logical path. Imagine writing the desired behaviors through unit tests then getting an AI to do the green then refactor steps in a test driven development like workflow.

This may be possible in the future on a local system with improvements to the number of generations required for the desired outcome (currently something near several million) and it might not be used in all scenarios. However, consider how many development tasks are tedious the developer equivalent of "washing the dishes" that a "washing machine" could do instead.

The future workflow might look something like:

> Write a series of unit tests
>
> Produce a basic skeleton of the code using the IDE/ AI
>
> Run the failing unit tests
>
> Run the AI tool to complete the green and refactor step
>
> Re-run the now passing unit tests
>
> Run the solution
>
> Encounter edge-cases and bugs
>
> Write some additional unit tests covering the edge cases
>
> Re-run the AI tool and unit tests which pass

## As "Next Generation" Compilers

There is a near industry wide acceptance of the trade off of absolute control that writing code in assembly provides is worth it for the readability, maintainability and scalability that compiled high level languages provide.

The main reason for this is the quality of the end product is of an acceptable standard to the end user. In other words languages like C and Rust compile down to near assembly levels of performance where more flexible languages with further abstractions such as weak typed, garbage collection or interpreters provide performance 2x to 5x worse than the best case scenario for the hardware it is running which with modern computer hardware still provides adequate performance in lots of cases.

It is with this in mind an AI generated program may one day fit an acceptance of the end user's needs.

Such AI generated programs may rely on a gherkin syntax prompt interface where a product owner could define how the program is intended to work, technologies to use, how to deploy it and so on. These requirements would then generate the tests and the AI would then generate high level code to meet these tests.

An example of this might look like:

> Given: a "library" of "books" from an "SQL database"
>
> When: a "customer" takes a "book" from the "library"
>
> Then: the "library" should move the "book" entry into the "lent books" table

A prompt like above should serve to create CRUD statements for the library's book management system and integrate the feature as described above.

### Levels Of Abstraction

In the example above without being able to see the internals of the high level code being generated (one layer of abstraction down) the application may have poor performance or security neither of which are ideal for a mission critical system.

From the example above therefore we would need to rethink the means by which the current layers of programming work.

Returning to the point about compilers being an accepted compromise; a programmer cannot make meaningful change to the performance of an application by changing the assembly. This is to say any changes to the assembly (which is further compiled down to machine code) are not reflected in the high level language. If a developer was to change the assembly they would have to endlessly continue to do so integrating their changes with the constantly compiling and changing code of the high level programming language.

This is not the case with some UI frameworks where changes in the graphical interface can be reflected back in the IDE and vice versa. This is a model proposed and one I think would need to be adopted if we were to go down the path I suggested above. Whilst an integrated assistant keeps the status quo of access to the high level language the program is being written in, the prompted AI "compiler" should allow developers access to the internal code being generated and in turn this should update the behavioral prompts for the features, deployment, dependencies/ technologies and so on.

To not use a model like the one suggested I think risks having "AI compilers" in a "build your own website" box separate from "real development" which is to say a limited tool separate from the core craft of software development. In the shortest words possible a fad.

## As Testers

The nature of the way in which AI is built means it sees thousands upon thousands of examples of code. It is therefore entirely possible for AI to become a "white box" tester (a tester who knows the internals of the system). There are many standards that developers have to follow and I am not just referring to standard paradigm rules.

AI could be used to detect breaches in security within WASM's guidelines, industry specific guidelines or just simply hunting down bugs in code with an integrated compiler and unit tests with possible suggestions for additional unit tests that need to be written like I described before.

Additionally AI could perform rapid "black box" (where the tester is unaware of the internals of the system) testing for an application. Providing the AI with parameters and control of a sandbox to run the application in through multiple hosted virtual machines an AI could be tasked with running exploratory testing of an application. The AI could then write the bug reports for a human to approve and place into the backlog of the project.

## As A Colleague

Pull requests and pair programming exercises could be another role that AI could fulfill.

Pair programming touches upon what I was discussing before when it comes to AI as an assistive tool. However in addition the AI could play the role of driver/ navigator and allow the developer wear "tactical" or "big picture" hats.

Pull requests are another potential area an AI tool could be useful in either pointing towards key changes for discussion for humans to then discuss or in directly conducting the code review itself and providing a score/ suggestions.

## Conclusion

AI has many potential roles it could play in the future but don't get sold on the cool-ade too much. Whilst a lot of AI tools right now have promise they are a long way from being truly scalable and take a lot more resource than a few humans and their grey matter do to solve even the most basic of tasks.

For right now AI barely contributes to my current work/ workflow but being open to reasonable change and questioning our approaches scientifically and on the merits of new approaches should always be considered.

Do I think AI will replace us... honestly no. Do I think AI will have a role to play in development work of the future? Absolutely and only time will tell as to which of the ideas I've presented in this blog post will come to fruition.
