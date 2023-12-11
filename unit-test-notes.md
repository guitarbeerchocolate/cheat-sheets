# PHPUnit Unit Testing Cheat Sheet

## Introduction to PHPUnit

PHPUnit is a popular unit testing framework for PHP. It allows you to write and execute unit tests to ensure the correctness of your code.

## Installation

To use PHPUnit, you need to install it. You can install it globally or as a development dependency for your project using Composer.

### Globally (recommended):

```
composer global require phpunit/phpunit
```

As a development dependency (in your project's composer.json):

```
composer require --dev phpunit/phpunit
```

## Writing Your First Test

Create a test class for your code. Test classes must be named \*Test.php and extend PHPUnit\Framework\TestCase.

```
use PHPUnit\Framework\TestCase;

class MyTest extends TestCase {
    // Your test methods go here
}
```

## Writing Test Methods

Write test methods with the test prefix. Use assertions to check the expected behavior of your code.

```
public function testAddition() {
    $result = 2 + 2;
    $this->assertEquals(4, $result);
}
```

## Running Tests

You can run tests using the phpunit command followed by the test class filename:

```
phpunit MyTest.php
```

## Assertions

PHPUnit provides various assertion methods to validate your code's behavior. Here are some common assertions:

```
assertEquals($expected, $actual): Asserts that two values are equal.
assertTrue($condition): Asserts that a condition is true.
assertFalse($condition): Asserts that a condition is false.
assertNull($value): Asserts that a value is null.
assertNotNull($value): Asserts that a value is not null.
assertArrayHasKey($key, $array): Asserts that an array has a specific key.
```

## Test Fixtures

Use fixtures to set up the environment for your tests. PHPUnit provides setUp and tearDown methods for this purpose.

```
public function setUp() {
    // Set up before each test
}

public function tearDown() {
    // Clean up after each test
}
```

## Data Providers

You can use data providers to run the same test with multiple sets of data.

```
/**
 * @dataProvider additionDataProvider
 */
public function testAddition($a, $b, $expected) {
    $result = $a + $b;
    $this->assertEquals($expected, $result);
}

public function additionDataProvider() {
    return [
        [2, 2, 4],
        [3, 5, 8],
        [1, 1, 2],
    ];
}
```

## Mocking

Use PHPUnit's mocking features to simulate objects or dependencies.

```
$mock = $this->getMockBuilder(MyClass::class)
             ->setMethods(['methodToMock'])
             ->getMock();

$mock->expects($this->once())
     ->method('methodToMock')
     ->willReturn('mockedReturnValue');
```

## Code Coverage

PHPUnit can generate code coverage reports to show which parts of your code were tested.

```
phpunit --coverage-html coverage-report/
```
