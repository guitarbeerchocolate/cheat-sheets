# Vitest Cheat Sheet

Vitest is a fast unit testing framework built for Vite projects. It provides a Jest-compatible API and is designed to work with Vite's fast and efficient build process.

---

## Table of Contents

- [Installation](#installation)
- [Running Tests](#running-tests)
- [Writing Tests](#writing-tests)
- [Matchers](#matchers)
- [Mocking](#mocking)
- [Snapshot Testing](#snapshot-testing)
- [Asynchronous Tests](#asynchronous-tests)
- [Setup and Teardown](#setup-and-teardown)
- [Coverage](#coverage)
- [Best Practices](#best-practices)

---

## Installation

First, install Vitest in your Vite project:

```bash
npm install vitest --save-dev
```

Add a test script to your `package.json`:

```json
{
  "scripts": {
    "test": "vitest"
  }
}
```

---

## Running Tests

You can run Vitest tests in different modes:

- Run all tests:

  ```bash
  npm run test
  ```

- Run tests in watch mode:

  ```bash
  npm run test -- --watch
  ```

- Run a specific test file:

  ```bash
  npm run test -- src/tests/myTestFile.test.js
  ```

- Run with coverage:

  ```bash
  npm run test -- --coverage
  ```

---

## Writing Tests

Vitest follows a similar structure to Jest, using `test` or `it` to define test cases.

```js
import { describe, it, expect } from "vitest";

describe("Math operations", () => {
  it("adds two numbers", () => {
    expect(1 + 1).toBe(2);
  });
});
```

---

## Matchers

Vitest provides a set of matchers for assertions. These matchers are similar to Jest’s, allowing you to assert values in your tests.

### Common Matchers

- **`toBe`**: Checks strict equality (like `===`).

  ```js
  expect(1 + 1).toBe(2);
  ```

- **`toEqual`**: Deep equality check (useful for objects and arrays).

  ```js
  expect({ a: 1 }).toEqual({ a: 1 });
  ```

- **`toBeTruthy` / `toBeFalsy`**: Checks if a value is truthy or falsy.

  ```js
  expect(true).toBeTruthy();
  expect(false).toBeFalsy();
  ```

- **`toContain`**: Checks if an array or string contains a value.

  ```js
  expect([1, 2, 3]).toContain(2);
  ```

- **`toThrow`**: Checks if a function throws an error.

  ```js
  const throwError = () => {
    throw new Error("Oops!");
  };
  expect(throwError).toThrow("Oops!");
  ```

---

## Mocking

Vitest has built-in mocking capabilities similar to Jest. You can mock functions, modules, and timers.

### Mocking Functions

Mock a function with `vi.fn()`:

```js
const mockFn = vi.fn();

mockFn();
expect(mockFn).toHaveBeenCalled();
```

Mock an implementation:

```js
const mockFn = vi.fn(() => "mocked");
expect(mockFn()).toBe("mocked");
```

### Mocking Modules

Mock a module with `vi.mock()`:

```js
vi.mock("./module", () => ({
  default: vi.fn(() => "mocked module"),
}));
```

---

## Snapshot Testing

Vitest supports snapshot testing, allowing you to capture and compare the rendered output of components or other values.

### Example

```js
import { expect, test } from "vitest";

test("renders correctly", () => {
  const component = "<div>Hello World</div>";
  expect(component).toMatchSnapshot();
});
```

Run tests with `--update` to update snapshots:

```bash
npm run test -- --update
```

---

## Asynchronous Tests

Vitest allows you to write tests for asynchronous code using promises or `async`/`await`.

### Async Example

```js
import { test, expect } from "vitest";

test("fetches data", async () => {
  const data = await fetchData();
  expect(data).toBe("result");
});
```

### Promise Example

```js
test("resolves a promise", () => {
  return fetchData().then((data) => {
    expect(data).toBe("result");
  });
});
```

---

## Setup and Teardown

You can use `beforeAll`, `beforeEach`, `afterEach`, and `afterAll` for setting up and cleaning up between tests.

### Example

```js
import { beforeEach, afterEach, test, expect } from "vitest";

beforeEach(() => {
  console.log("Setup before each test");
});

afterEach(() => {
  console.log("Cleanup after each test");
});

test("example test", () => {
  expect(1 + 1).toBe(2);
});
```

---

## Coverage

Vitest can generate coverage reports with the `--coverage` flag. You need to install a coverage provider (like `c8`):

```bash
npm install c8 --save-dev
```

Run tests with coverage:

```bash
npm run test -- --coverage
```

This will generate a coverage report in the `coverage` directory.

---

## Best Practices

1. **Write Isolated Tests**: Ensure that each test is independent and does not rely on the state of other tests.
2. **Use Descriptive Test Names**: Your test names should clearly describe what you are testing.
3. **Avoid Mocking Too Much**: Mock only what is necessary. Over-mocking can lead to fragile tests.
4. **Test Asynchronous Code Correctly**: Always return a promise or use `async/await` in asynchronous tests.
5. **Run Tests Frequently**: Running your test suite often will help catch issues early.
6. **Snapshot Testing**: Use snapshots sparingly for dynamic content, as they can become brittle.

---

## Resources

- [Vitest Documentation](https://vitest.dev/)
- [Matchers API](https://vitest.dev/api/expect.html)
- [Mocking in Vitest](https://vitest.dev/guide/mocking.html)
