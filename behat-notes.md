# Behat Cheat Sheet

Behat is a PHP framework for behavior-driven development (BDD). It allows you to define test cases in a human-readable language (Gherkin) and ensures your application's behavior matches expectations.

---

## Table of Contents

- [Installation](#installation)
- [Behat Structure](#behat-structure)
- [Gherkin Syntax](#gherkin-syntax)
  - [Feature Files](#feature-files)
  - [Basic Syntax](#basic-syntax)
  - [Scenario Outline](#scenario-outline)
  - [Background](#background)
- [Running Behat](#running-behat)
- [Writing Step Definitions](#writing-step-definitions)
  - [Basic Example](#basic-example)
  - [Using Regular Expressions](#using-regular-expressions)
- [Tags and Filtering](#tags-and-filtering)
- [Contexts](#contexts)
- [Best Practices](#best-practices)

---

## Installation

Install Behat via Composer:

```bash
composer require --dev behat/behat
```

Initialize Behat in your project:

```bash
vendor/bin/behat --init
```

---

## Behat Structure

When you initialize Behat in your project, the following directory structure is created:

```
/features
  |-- bootstrap/
  |-- FeatureContext.php
  |-- *.feature
```

- **Feature Files (`*.feature`)**: Where Gherkin scenarios are written.
- **FeatureContext.php**: Contains PHP code that maps to Gherkin steps (step definitions).
- **bootstrap/**: Where additional context or helper classes can be placed.

---

## Gherkin Syntax

Gherkin is a business-readable, domain-specific language used in Behat to describe behaviors.

### Feature Files

Each feature file represents a feature of your application and includes a series of scenarios (test cases).

Example structure:

```gherkin
Feature: User authentication
  In order to use the application
  As a registered user
  I want to log in

  Scenario: Successful login
    Given I am on the login page
    When I fill in "username" with "john"
    And I fill in "password" with "123456"
    And I press "Login"
    Then I should see "Welcome, John"
```

### Basic Syntax

- **Feature**: Describes a high-level feature of the application.
- **Scenario**: Represents a test case that defines the steps for a specific behavior.
- **Steps**: The actual actions within the scenario, written as `Given`, `When`, `Then`, `And`, or `But`.

---

### Scenario Outline

A **Scenario Outline** is used to run the same scenario with different sets of data.

```gherkin
Scenario Outline: Logging in with valid credentials
  Given I am on the login page
  When I fill in "<username>" with "<password>"
  And I press "Login"
  Then I should see "<message>"

  Examples:
    | username | password | message       |
    | alice    | 123456   | Welcome, Alice |
    | bob      | abcdef   | Welcome, Bob   |
```

### Background

The **Background** keyword allows you to define steps that are common to all scenarios in the feature.

```gherkin
Feature: User dashboard

Background:
  Given I am logged in as a user

Scenario: Viewing the dashboard
  When I go to the dashboard
  Then I should see "Dashboard"
```

---

## Running Behat

Run all tests:

```bash
vendor/bin/behat
```

Run a specific feature file:

```bash
vendor/bin/behat features/login.feature
```

Run tests with a specific tag:

```bash
vendor/bin/behat --tags=@login
```

---

## Writing Step Definitions

Each Gherkin step must be mapped to a corresponding PHP method in the `FeatureContext.php` file.

### Basic Example

```php
/**
 * @Given I am on the login page
 */
public function iAmOnTheLoginPage() {
    // Navigate to the login page
    $this->visitPath('/login');
}

/**
 * @When I fill in :field with :value
 */
public function iFillInWith($field, $value) {
    // Fill the form field with the specified value
    $this->getSession()->getPage()->fillField($field, $value);
}

/**
 * @Then I should see :text
 */
public function iShouldSee($text) {
    // Assert that the page contains the text
    assert($this->getSession()->getPage()->hasContent($text));
}
```

### Using Regular Expressions

You can use regular expressions to capture dynamic parts of steps.

```php
/**
 * @When /^I press "(.*)"$/
 */
public function iPress($button) {
    $this->getSession()->getPage()->pressButton($button);
}
```

---

## Tags and Filtering

You can organize and run specific tests using tags.

1. Tag a scenario or feature:

```gherkin
@login
Scenario: User logs in with valid credentials
  ...
```

2. Run tests by tag:

```bash
vendor/bin/behat --tags=@login
```

3. Use multiple tags with logical operators:

```bash
vendor/bin/behat --tags="@login&&~@slow"
```

---

## Contexts

- **Context classes** define the environment in which your steps are executed.
- **FeatureContext.php** is the default context file, but you can create additional context classes for better organization.

### Creating Custom Contexts

You can create a custom context for managing different domains of your application:

```bash
vendor/bin/behat --init --context=AuthContext
```

---

## Best Practices

1. **Write Readable Tests**: Make sure your Gherkin scenarios are written in plain, business-readable language.
2. **Reusability**: Write reusable step definitions to reduce duplication across scenarios.
3. **Use Tags Wisely**: Use tags to categorize tests, allowing you to run subsets of scenarios.
4. **Scenario Scope**: Keep your scenarios small and focused on a single behavior or feature.
5. **Keep Contexts Clean**: Split step definitions into multiple context classes if they serve different domains.
6. **Background Usage**: Use `Background` to set up common steps for multiple scenarios in a feature file.

---

## Resources

- [Behat Documentation](https://docs.behat.org/en/latest/)
- [Gherkin Syntax](https://cucumber.io/docs/gherkin/)
- [Mink (Browser Automation)](http://mink.behat.org/en/latest/)
