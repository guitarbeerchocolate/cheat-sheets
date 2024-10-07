# Jest Cheat Sheet

Jest is a JavaScript testing framework, commonly used to test React applications, but it can be used for any JavaScript codebase. It provides powerful features such as test runners, matchers, and mock functions.

---

## Table of Contents

- [Installation](#installation)
- [Running Tests](#running-tests)
- [Writing Tests](#writing-tests)
- [Matchers](#matchers)
  - [Basic Matchers](#basic-matchers)
  - [Truthiness](#truthiness)
  - [Numbers](#numbers)
  - [Strings](#strings)
  - [Arrays and Iterables](#arrays-and-iterables)
  - [Exceptions](#exceptions)
- [Mock Functions](#mock-functions)
- [Testing Asynchronous Code](#testing-asynchronous-code)
- [Setup and Teardown](#setup-and-teardown)
- [Snapshot Testing](#snapshot-testing)
- [Best Practices](#best-practices)

---

## Installation

Install Jest via npm or yarn:

```bash
npm install --save-dev jest
# or
yarn add --dev jest
```

Add a script to your `package.json`:

```json
{
  "scripts": {
    "test": "jest"
  }
}
```

Run your tests with:

```bash
npm test
```

---

## Running Tests

You can run Jest tests using different options:

- Run all tests:

  ```bash
  npm test
  ```

- Run tests in watch mode:

  ```bash
  npm test -- --watch
  ```

- Run a specific test file:

  ```bash
  npm test -- myTestFile.test.js
  ```

---

## Writing Tests

Jest uses `test` or `it` to define a test case, and `expect` to define assertions.

```js
test("adds 1 + 2 to equal 3", () => {
  expect(1 + 2).toBe(3);
});
```

You can also use `describe` to group related tests:

```js
describe("Math functions", () => {
  test("adds 1 + 2 to equal 3", () => {
    expect(1 + 2).toBe(3);
  });

  test("subtracts 5 - 2 to equal 3", () => {
    expect(5 - 2).toBe(3);
  });
});
```

---

## Matchers

Jest provides a variety of matchers to assert different types of values.

### Basic Matchers

- **`toBe`**: Checks if two values are the same (uses `===`).

  ```js
  expect(2 + 2).toBe(4);
  ```

- **`toEqual`**: Deep equality check (works for objects and arrays).

  ```js
  expect({ name: "Alice" }).toEqual({ name: "Alice" });
  ```

- **`not`**: Inverts the matcher.

  ```js
  expect(2 + 2).not.toBe(5);
  ```

### Truthiness

Jest has matchers to check for truthy and falsy values:

- **`toBeNull`**: Checks if the value is `null`.

  ```js
  expect(null).toBeNull();
  ```

- **`toBeUndefined`**: Checks if the value is `undefined`.

  ```js
  expect(undefined).toBeUndefined();
  ```

- **`toBeTruthy`**: Checks if the value is truthy.

  ```js
  expect(true).toBeTruthy();
  ```

- **`toBeFalsy`**: Checks if the value is falsy.

  ```js
  expect(false).toBeFalsy();
  ```

### Numbers

Jest also supports comparisons with numbers:

- **`toBeGreaterThan`**: Checks if a value is greater than a given number.

  ```js
  expect(10).toBeGreaterThan(5);
  ```

- **`toBeGreaterThanOrEqual`**: Checks if a value is greater than or equal to a given number.

  ```js
  expect(10).toBeGreaterThanOrEqual(10);
  ```

- **`toBeLessThan`**: Checks if a value is less than a given number.

  ```js
  expect(5).toBeLessThan(10);
  ```

- **`toBeCloseTo`**: Useful for comparing floating-point numbers.

  ```js
  expect(0.2 + 0.1).toBeCloseTo(0.3);
  ```

### Strings

- **`toMatch`**: Checks if a string matches a regular expression.

  ```js
  expect("Hello, world!").toMatch(/world/);
  ```

### Arrays and Iterables

- **`toContain`**: Checks if an array or iterable contains a specific value.

  ```js
  expect(["apple", "banana", "orange"]).toContain("banana");
  ```

### Exceptions

- **`toThrow`**: Checks if a function throws an error.

  ```js
  function throwError() {
    throw new Error("Something went wrong!");
  }

  expect(throwError).toThrow("Something went wrong!");
  ```

---

## Mock Functions

Mock functions are used to simulate and track calls to functions.

- **Basic Mock**:

  ```js
  const mockFn = jest.fn();
  mockFn();
  expect(mockFn).toHaveBeenCalled();
  ```

- **Mock Implementation**:

  ```js
  const mockFn = jest.fn().mockImplementation(() => "mocked value");
  expect(mockFn()).toBe("mocked value");
  ```

- **Mocking Return Values**:

  ```js
  const mockFn = jest.fn().mockReturnValue(42);
  expect(mockFn()).toBe(42);
  ```

- **Mocking Modules**:

  ```js
  jest.mock("./module"); // Auto-mocks the './module' module
  ```

---

## Testing Asynchronous Code

Jest supports testing asynchronous code using callbacks, promises, and `async`/`await`.

### Using Callbacks

```js
test("callback example", (done) => {
  function fetchData(callback) {
    callback("data");
  }

  fetchData((data) => {
    expect(data).toBe("data");
    done(); // Indicate the test is complete
  });
});
```

### Using Promises

```js
test("promise example", () => {
  return fetchData().then((data) => {
    expect(data).toBe("data");
  });
});
```

### Using Async/Await

```js
test("async/await example", async () => {
  const data = await fetchData();
  expect(data).toBe("data");
});
```

---

## Setup and Teardown

You can run setup and teardown logic with these Jest functions:

- **`beforeEach`**: Runs before each test.
- **`afterEach`**: Runs after each test.
- **`beforeAll`**: Runs once before all tests.
- **`afterAll`**: Runs once after all tests.

Example:

```js
beforeEach(() => {
  initializeDatabase();
});

afterEach(() => {
  clearDatabase();
});

test("example test", () => {
  expect(1 + 1).toBe(2);
});
```

---

## Snapshot Testing

Jest can generate **snapshots** to verify that UI components do not change unexpectedly.

1. Create a snapshot test:

   ```js
   test("renders correctly", () => {
     const tree = renderer.create(<MyComponent />).toJSON();
     expect(tree).toMatchSnapshot();
   });
   ```

2. Jest will generate a snapshot file if one does not exist or compare the output with the existing snapshot.

3. Update snapshots with:

   ```bash
   jest --updateSnapshot
   ```

---

## Best Practices

1. **Write Independent Tests**: Ensure that tests do not depend on each other.
2. **Use Mocks Carefully**: Mock functions and modules sparingly, only when needed.
3. **Test Asynchronous Code Properly**: Always return or use `async`/`await` to avoid false positives in async tests.
4. **Use `beforeEach` and `afterEach` for Cleanup**: Clean up resources between tests to avoid side effects.
5. **Keep Tests Small and Focused**: Each test should check a single behavior or feature.

---

## Resources

- [Jest Documentation](https://jestjs.io/docs/en/getting-started)
- [Matchers API](https://jestjs.io/docs/en/expect)
