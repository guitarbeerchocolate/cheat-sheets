# PHPUnit Cheat Sheet

PHPUnit is a popular testing framework for PHP. It is used to write and run unit tests to verify that individual parts of an application work as expected.

---

## Table of Contents

- [Installation](#installation)
- [Writing Your First Test](#writing-your-first-test)
- [Assertions](#assertions)
- [Test Annotations](#test-annotations)
- [Testing Exceptions](#testing-exceptions)
- [Setup and Teardown](#setup-and-teardown)
- [Mocking with PHPUnit](#mocking-with-phpunit)
- [Data Providers](#data-providers)
- [Best Practices](#best-practices)

---

## Installation

To install PHPUnit, you can use Composer:

```bash
composer require --dev phpunit/phpunit
```

You can also install it globally:

```bash
composer global require phpunit/phpunit
```

Run your tests using the following command:

```bash
./vendor/bin/phpunit
```

---

## Writing Your First Test

A PHPUnit test case is a class that extends `PHPUnit\Framework\TestCase`. Each test method should begin with `test`.

```php
use PHPUnit\Framework\TestCase;

class ExampleTest extends TestCase {
    public function testAddition() {
        $this->assertEquals(4, 2 + 2);
    }
}
```

To run the test, use:

```bash
./vendor/bin/phpunit ExampleTest
```

---

## Assertions

Assertions are methods used to test that specific conditions are met.

| **Assertion**                                | **Description**                                                |
| -------------------------------------------- | -------------------------------------------------------------- |
| `$this->assertTrue($condition)`              | Asserts that the condition is true.                            |
| `$this->assertFalse($condition)`             | Asserts that the condition is false.                           |
| `$this->assertEquals($expected, $actual)`    | Asserts that two values are equal.                             |
| `$this->assertNotEquals($expected, $actual)` | Asserts that two values are not equal.                         |
| `$this->assertNull($variable)`               | Asserts that a variable is null.                               |
| `$this->assertNotNull($variable)`            | Asserts that a variable is not null.                           |
| `$this->assertCount($count, $array)`         | Asserts that an array has the expected number of elements.     |
| `$this->assertInstanceOf($class, $object)`   | Asserts that an object is an instance of a particular class.   |
| `$this->assertSame($expected, $actual)`      | Asserts that two variables reference the same object or value. |

Example:

```php
public function testStringEquals() {
    $expected = 'Hello World';
    $actual = 'Hello ' . 'World';
    $this->assertEquals($expected, $actual);
}
```

---

## Test Annotations

Annotations in PHPUnit provide additional information or configure the behavior of the test. Common annotations include:

| **Annotation**  | **Description**                                              |
| --------------- | ------------------------------------------------------------ |
| `@test`         | Marks a method as a test.                                    |
| `@dataProvider` | Links a method as a data provider for a test.                |
| `@depends`      | Specifies that a test depends on the result of another test. |
| `@group`        | Assigns the test to a specific group of tests.               |
| `@covers`       | Specifies which method or class is covered by this test.     |

Example:

```php
/**
 * @group math
 */
public function testMultiplication() {
    $this->assertEquals(6, 2 * 3);
}
```

---

## Testing Exceptions

To test that an exception is thrown, you can use the `expectException` method.

Example:

```php
public function testException() {
    $this->expectException(InvalidArgumentException::class);

    // Code that triggers the exception
    throw new InvalidArgumentException("Invalid argument");
}
```

You can also check for specific exception messages:

```php
$this->expectExceptionMessage("Invalid argument");
```

---

## Setup and Teardown

You can use the `setUp()` and `tearDown()` methods to set up a test environment before each test and clean it up after each test.

- `setUp()` is executed before each test method.
- `tearDown()` is executed after each test method.

Example:

```php
use PHPUnit\Framework\TestCase;

class ExampleTest extends TestCase {
    protected $stack;

    protected function setUp(): void {
        $this->stack = [];
    }

    public function testPush() {
        array_push($this->stack, 'foo');
        $this->assertEquals('foo', $this->stack[count($this->stack) - 1]);
    }

    protected function tearDown(): void {
        $this->stack = [];
    }
}
```

---

## Mocking with PHPUnit

Mocking allows you to create dummy objects that simulate the behavior of real objects. This is useful when testing components that depend on external services, databases, or other objects.

Example of a mock object:

```php
public function testMockExample() {
    $mock = $this->createMock(SomeClass::class);
    $mock->method('someMethod')
         ->willReturn('expectedValue');

    $this->assertEquals('expectedValue', $mock->someMethod());
}
```

Mocking can also simulate behavior like throwing exceptions or calling specific methods a number of times.

---

## Data Providers

A **data provider** supplies different sets of data to a test. This allows you to test the same logic with multiple inputs.

Example:

```php
/**
 * @dataProvider additionProvider
 */
public function testAddition($a, $b, $expected) {
    $this->assertEquals($expected, $a + $b);
}

public function additionProvider() {
    return [
        [1, 2, 3],
        [0, 0, 0],
        [-1, 1, 0],
    ];
}
```

---

## Best Practices

1. **Test Single Responsibility**: A test method should test only one thing.
2. **Use Meaningful Names**: Test method names should describe what the test is verifying.
3. **Test Edge Cases**: Test cases should cover typical, edge, and error conditions.
4. **Use Mocks Sparingly**: Mock dependencies when necessary, but try to avoid overusing them.
5. **Run Tests Frequently**: Running your test suite often will help catch bugs early in the development process.
6. **Automate Testing**: Integrate PHPUnit tests with Continuous Integration (CI) tools to run automatically on every commit or push.
7. **Test Coverage**: Ensure that critical parts of your application are covered by unit tests to maintain reliability.

---

This cheat sheet provides a basic overview of how to use PHPUnit to write and run unit tests. It covers installation, key assertions, testing exceptions, setup/teardown, and mocking, as well as best practices for effective testing.
