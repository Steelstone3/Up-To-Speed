# Gherkin Syntax

## Introduction

Gherkin syntax is a human-readable, structured language used in Behavior-Driven Development (BDD) to write executable specifications. It provides a way to describe the behavior and expected outcomes of a software system in a clear and concise manner. Gherkin syntax is designed to be easily understandable by both technical and non-technical stakeholders, fostering collaboration and shared understanding.

## Syntax

Gherkin syntax follows a specific format and uses keywords to describe scenarios and steps. The syntax is typically used in feature files, which serve as living documentation and automated test cases.

Here are the main components and keywords of Gherkin syntax:

### Feature

A feature represents a high-level business requirement or user capability that is being described. It is defined using the "Feature" keyword followed by a brief description of the feature.

### Scenario

A scenario represents a specific test case or example that illustrates the desired behavior of the system. It is defined using the "Scenario" keyword followed by a descriptive title.

### Given, When, Then

These keywords define the steps of a scenario and describe the sequence of events or actions. Each step provides context and sets up the preconditions for the test. The keywords are:

Given: Describes the initial state or preconditions of the system.
When: Describes the action or event that occurs.
Then: Describes the expected outcome or result.
These steps can be extended with additional keywords such as "And" or "But" to provide further clarity and structure.

### Background

The "Background" keyword is used to define steps that are common to all scenarios within a feature file. It helps in reducing repetition by defining preconditions that are shared across multiple scenarios.

### Examples

The "Examples" keyword is used to provide data tables or parameterized values that demonstrate different variations or inputs for a scenario. It allows for concise representation of multiple test cases within a single scenario.

### Tags

Tags are used to categorize and group related scenarios. They are specified using the "@" symbol followed by a tag name. Tags can be used to selectively run or exclude specific scenarios during test execution.

## Example

Here's an example scenario written in Gherkin syntax:

```gherkin
Feature: Login Functionality
  As a registered user
  I want to be able to log in to the system
  So that I can access my account and perform actions

  Scenario: Successful Login
    Given I am on the login page
    When I enter valid credentials
    And I click the "Login" button
    Then I should be redirected to the dashboard
    And I should see a welcome message

  Scenario: Invalid Login
    Given I am on the login page
    When I enter invalid credentials
    And I click the "Login" button
    Then I should see an error message
    And I should remain on the login page
```

In the example above, we have defined a feature called "Login Functionality" that describes the purpose of the feature. The feature includes two scenarios: "Successful Login" and "Invalid Login," each representing a specific test case.

The "Successful Login" scenario starts with the initial state defined by the "Given" step, where the user is on the login page. The "When" step describes the action of entering valid credentials, and the subsequent "And" step represents clicking the "Login" button. The "Then" steps define the expected outcomes, such as being redirected to the dashboard and seeing a welcome message.

The "Invalid Login" scenario follows a similar structure but represents the case where the user enters invalid credentials. The expected outcomes include seeing an error message and remaining on the login page.

These scenarios serve as executable specifications that can be automated and validated against the system's behavior. They provide clear guidance on the expected behavior of the login functionality and help ensure that the implemented software meets the specified requirements.

## Conclusion

By using Gherkin syntax, stakeholders can collaboratively write and review scenarios that describe the behavior of the software system in a structured and readable format. These scenarios can be transformed into automated tests, helping to validate the system's behavior against the specified requirements. Gherkin syntax promotes clarity, shared understanding, and effective communication between business experts, developers, and testers throughout the development process.
