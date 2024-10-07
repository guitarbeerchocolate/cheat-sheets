# Testing Library Cheat Sheet

Testing Library is a family of libraries that help you test UIs in a way that mimics user behavior. It provides utilities to query DOM elements, interact with them, and assert their states.

---

## Table of Contents

- [Installation](#installation)
- [Basic Setup](#basic-setup)
- [Render and Queries](#render-and-queries)
  - [Queries](#queries)
    - [Types of Queries](#types-of-queries)
    - [Common Query Methods](#common-query-methods)
- [User Interaction](#user-interaction)
- [Assertions](#assertions)
- [Async Utilities](#async-utilities)
- [Custom Render Function](#custom-render-function)
- [Debugging](#debugging)
- [Best Practices](#best-practices)

---

## Installation

Install the core Testing Library package for React:

```bash
npm install --save-dev @testing-library/react
```

For DOM-based projects, install the core DOM library:

```bash
npm install --save-dev @testing-library/dom
```

---

## Basic Setup

Import the necessary functions for your tests:

```js
import { render, screen } from "@testing-library/react";
import "@testing-library/jest-dom"; // For custom matchers like toBeInTheDocument
import MyComponent from "./MyComponent"; // Component under test
```

Basic example:

```js
test("renders the component", () => {
  render(<MyComponent />);
  const element = screen.getByText(/hello world/i);
  expect(element).toBeInTheDocument();
});
```

---

## Render and Queries

The `render` function mounts a React component to the DOM, and then you can query the DOM using different methods provided by Testing Library.

```js
render(<MyComponent />);
```

### Queries

- **Queries** are functions used to find elements in the DOM.
- They are available on `screen` or returned by `render` result.

#### Types of Queries

1. **getBy**: Throws an error if the element is not found (use when element must be present).
2. **queryBy**: Returns `null` if the element is not found (use when the element may not be present).
3. **findBy**: Returns a promise and waits for the element to appear (use for async elements).

#### Common Query Methods

| **Query Method**               | **Description**                                             |
| ------------------------------ | ----------------------------------------------------------- |
| `getByText(/text/i)`           | Finds an element by its text content (supports regex).      |
| `getByRole('button')`          | Finds an element by its ARIA role.                          |
| `getByLabelText('Label')`      | Finds an element associated with a label (like `<input>`).  |
| `getByPlaceholderText('text')` | Finds an element by its placeholder text (e.g., `<input>`). |
| `getByAltText('alt text')`     | Finds an element by the alt text of an image.               |
| `getByTestId('custom-id')`     | Finds an element by `data-testid` attribute.                |

Example:

```js
const button = screen.getByRole("button", { name: /submit/i });
expect(button).toBeInTheDocument();
```

---

## User Interaction

Testing Library provides a `userEvent` API to simulate user interactions like clicking, typing, and hovering.

First, install the `user-event` library:

```bash
npm install --save-dev @testing-library/user-event
```

Then use it in your tests:

```js
import userEvent from "@testing-library/user-event";

test("clicks the button", () => {
  render(<MyComponent />);
  const button = screen.getByRole("button", { name: /submit/i });
  userEvent.click(button);
  expect(button).toBeDisabled(); // Example of checking state after interaction
});
```

Other common user interactions:

- **Typing into inputs**:

  ```js
  userEvent.type(inputElement, "Hello");
  ```

- **Selecting from dropdowns**:

  ```js
  userEvent.selectOptions(selectElement, ["optionValue"]);
  ```

- **Hovering**:

  ```js
  userEvent.hover(element);
  ```

---

## Assertions

Testing Library is typically used with Jest for assertions. You can use Jest's built-in matchers, or the extended ones provided by the `jest-dom` library:

### Common Assertions (from `@testing-library/jest-dom`)

- **`toBeInTheDocument`**: Asserts that an element exists in the DOM.

  ```js
  expect(button).toBeInTheDocument();
  ```

- **`toBeVisible`**: Asserts that an element is visible to the user.

  ```js
  expect(modal).toBeVisible();
  ```

- **`toHaveTextContent`**: Checks the text content of an element.

  ```js
  expect(paragraph).toHaveTextContent("Hello World");
  ```

- **`toBeDisabled` / `toBeEnabled`**: Asserts whether an element is disabled or enabled.

  ```js
  expect(button).toBeDisabled();
  ```

- **`toHaveAttribute`**: Checks for the presence of a specific attribute on an element.

  ```js
  expect(link).toHaveAttribute("href", "/home");
  ```

---

## Async Utilities

When testing components that have asynchronous actions, such as loading or fetching data, use `findBy` queries or Jest's `waitFor`.

### Using `findBy`

```js
test("displays data after fetch", async () => {
  render(<MyComponent />);
  const dataElement = await screen.findByText(/data loaded/i);
  expect(dataElement).toBeInTheDocument();
});
```

### Using `waitFor`

```js
import { waitFor } from "@testing-library/react";

test("shows loader before data", async () => {
  render(<MyComponent />);
  const loader = screen.getByTestId("loader");
  await waitFor(() => expect(loader).not.toBeInTheDocument());
});
```

---

## Custom Render Function

You can create a custom `render` function for tests that require shared logic, like wrapping your component in a provider (e.g., Redux or Theme provider).

```js
import { render as rtlRender } from "@testing-library/react";
import { Provider } from "react-redux";
import store from "./store";

function render(ui, { ...options } = {}) {
  return rtlRender(<Provider store={store}>{ui}</Provider>, options);
}

// Use your custom render function in tests
render(<MyComponent />);
```

---

## Debugging

Testing Library provides several ways to debug your tests and the DOM.

- **`screen.debug()`**: Prints the current state of the DOM in the console.

  ```js
  screen.debug(); // Logs the entire DOM to the console
  ```

- **`logRoles()`**: Prints out the accessible roles of all elements in the rendered output.

  ```js
  import { logRoles } from "@testing-library/dom";
  logRoles(container); // Prints available roles
  ```

---

## Best Practices

1. **Test Behavior, Not Implementation**: Focus on how the user interacts with the component, not the internal details.
2. **Use `getByRole` When Possible**: This ensures accessibility and matches how real users interact with elements.
3. **Prefer `findBy` for Async Queries**: Use `findBy` when querying elements that appear after asynchronous operations.
4. **Avoid `querySelector`**: Use Testing Library's query methods (like `getByText`, `getByRole`) instead of low-level DOM selectors.
5. **Use `screen` for Readability**: `screen` makes queries easier to read and avoids needing to pass the `container` around.

---

## Resources

- [Testing Library Docs](https://testing-library.com/docs/)
- [Jest DOM Matchers](https://github.com/testing-library/jest-dom)
