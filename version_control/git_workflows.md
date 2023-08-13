# Git Workflows

## Introduction

Git workflows are systematic approaches to using the Git version control system to manage code changes, collaborate with team members, and maintain a structured development process. Different workflows cater to varying team sizes, project complexities, and release strategies.

Here are some common Git workflows:

## Gitflow Workflow

- Suitable for projects with well-defined release cycles and multiple stages (e.g., development, testing, production).
- Main branches:
  - "master" or "main": Represents the production-ready code.
  - "develop": Integration branch for ongoing development.
- Feature branches, release branches, and hotfix branches are used for specific tasks.
- Follows a strict branching and merging strategy for controlled releases.

## Pull Request Workflow

- Commonly used on platforms like GitHub, GitLab, and Bitbucket.
- Developers fork the main repository or create feature branches in the main repository.
- Changes are made in these branches, and pull requests (PRs) are opened to propose merging them into the main codebase.
- PRs allow for discussion, code review, and automated testing before merging.
- Encourages collaboration, quality control, and transparency.

## Feature Branch Workflow

- Ideal for teams working on multiple features or bug fixes simultaneously.
- Each new feature or bug fix is developed in its own separate branch.
- Developers create feature branches from the main development branch (e.g., "master" or "main").
- Once a feature is complete, the branch is merged back into the main branch.
- Enables parallel development and isolates changes for easier testing and code review.

## Trunk-Based Development

- Favors frequent and small commits directly to the main branch (e.g., "master" or "main").
- Developers work on short-lived feature branches, aiming to merge them quickly into the main branch.
- Automated tests and code review play a significant role to ensure the main branch remains stable.
- Promotes continuous integration and rapid iteration.

## Forking Workflow (Not Commonly Used)

- Commonly used in open-source projects with large contributor communities.
- Contributors fork the main repository to their own remote repositories.
- They make changes in their forks and then create pull requests to propose changes to the main repository.
- Maintainers review and merge these pull requests if they meet the project's standards.
- Isolates contributors' changes and ensures a controlled review process.

## Centralised Workflow (Not Commonly Used)

- This simple workflow is suitable for smaller teams or projects.
- A central repository holds the main codebase, and all developers clone, commit, and push changes directly to this repository.
- Collaboration happens through commits, and conflicts are resolved directly on the central repository.
- Provides a linear history and is easy to understand.

## Conclusion

Each of these workflows has its own strengths and is best suited for specific development scenarios. Choosing the right workflow depends on factors like team size, project complexity, release frequency, and the desired level of control over the codebase.
