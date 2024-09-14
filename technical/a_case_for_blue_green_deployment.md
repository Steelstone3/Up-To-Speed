# A Case For Blue Green Deployment

## Branching Strategy

Operating effectively in teams is critical to the success of projects in organizations. Branching strategy is one of the main ways in which features integrate with one another and the more seamless a process this is the more productive the team.

There are a number of approaches this article will explore and my reasoning for my favorite based on my own experience.

### Silos

Before we talk about the different branching strategies we need to "discuss working in silos".

When a developer works on a feature they will pick up on the domain language and other critical knowledge for the implementation of that feature.

This knowledge as a matter of priority should be documented in a publicly accessible place.

Larger teams may also want to ensure "code time" meetings or pair programming/ mobbing sessions are ran on a frequent basis to keep others in the loop of the work being done when implementing features.

This ensures that other members of the team could take over in such cases as someone leaves the company or becomes ill during a critical delivery phase.

### Feature Visibility

Keeping development work visible to other developers I believe is key to an effective branching strategy.

This will reduce the number of conflicts as it is obvious when a developer is working in an area.

The developers may then choose to pair program to eliminate the conflict all together or discuss a macro level strategy of how they will work around one another.

### Simplicity

Ensuring a branching strategy is easy to understand by all in the organization is key.

A Branching strategy chosen by an organization should be clear and simple to understand for any new developer being onboard-ed onto a project.

## Feature Branching

Feature branching seeks an iterative approach to the development branch.

Each developer creates a branch from develop to work on a feature then creates a pull request to merge the feature iteration into develop.

The pull request is reviewed by another developer as often the work is done in isolation.

As a result the development branch moves in feature based iterative steps.

### Problems With Feature Branching

#### Silos Using Feature Branching

The first main problem with feature branching is it is a very isolated approach to development meaning often other developers need to be brought fully up to speed with what you are working on and how they can help.

By the time the issue is explained likely some solutions are starting to form in the original author of the work's mind.

If a lack of relevant documentation is produced then no-one will be able to take over the area of work in the future.

#### Ineffective Quality Control

Code reviews are often ineffective as a means for properly reviewing the quality of the implementation and instead often focus on surface level details leading to fundamental design issues that will need to be resolved later in the codebase.

#### Slipping Development Standards

The developers own development standards may start to slip over time due to the isolated nature of this approach.

#### Long Branches

Long lived feature branches go stale and are then hard to merge with the ever shifting (with big changes) development branch.

Merge conflicts will be encountered and it can take days to weeks depending on the levels of stale-ness of the feature branch.

## Develop Only

Develop only is an approach where developer only push work to the development branch.

This branching strategy works really well for small teams.

It provides good visibility for work being done by developers to work around one another's changes and is simple to use.

When a milestone has been reached a branch is created and allowed to go stale for the release.

### Problems With Develop Only

#### Large Iterations

Not pushing work frequently in large iterations has the same issues as feature branching with a stale long lived branch.

Work should be pushed in small iterations regularly.

#### Features Not Working

There will be points in development where once working features will regress back into development.

This can make it difficult to integrate as a branching strategy with a test team.

#### Quality Control

Develop Only branching strategy requires unique approaches to ensuring code quality is maintained from the team.

This is due to a lack of code reviews so alternatives such XP practices might be used in its place.

## Blue Green Deployment

This approach combines the best bits of both Develop Only and Feature Branching (imho).

Blue is what is known as the old version where Green (possibly from green field project) is the new version.

Any work to any part of the system such as refactoring or a new version of a similar system gets created in new files/ projects.

The old system will be labelled as such in the files "blue_system" and the new system labelled as such "green_system".

When the old system can be replaced by the new system through a-b testing.

The old system is deleted, the new system is implemented as a commit which is pushed forming the deployment part of this branching strategy.

All work in progress commits keep the old system in place with the new system commented out when pushing to develop.

### Problems With Blue Green Deployment

#### Complexity

Explaining this concept is quite difficult when onboarding new developers onto a project and therefore mistakes are likely.

#### Large Iterations For Blue Green Deployment

Large iterations are another potential problem of this strategy however much more rare due to the fact that green code can be pushed in any compiling state so long as it isn't live.

#### Quality Control For Blue Green Deployment

Quality review processes can get complex with the strategy.

The best approach is "code time", "mobbing" and "pairing" sessions with a good testing strategy.

No-one should gate keep code quality however, it shouldn't be up to a sole individual either peer review is important and we need to be honest about this as developers.

### Benefits Of Blue Green Deployment

#### Role-back

Blue green deployment has options of role-back when the deployment commit is done back to the blue system.

This is highly beneficial in a live deployment environment.

#### Works For Large Teams

Blue green deployment can work really effectively in large teams.

Training on how to use this branching strategy however is paramount to ensuring its successful usage.

#### Stability With Visibility

Test teams will be happy as the blue systems will keep on working whilst the green systems are being visibly developed and pushed directly into the develop branch.

This makes changes easy to see and reduces merge conflicts like the Develop Only branching strategy.

## Conclusion

Branching strategies aren't a one size fits all solution.

Each organization will have their reasons for using the strategy they do from experience.

I argue however that if there was to be a "one size fits all" surely it must be blue green deployment.

It provides fast paced iterations with little system downtime for the trade offs of ensuring quality through alternative means to code reviews (XP practices) and initial complexity of the approach.
