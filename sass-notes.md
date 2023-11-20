# Sass (Syntactically Awesome Style Sheets) Cheat Sheet

# Introduction to Sass

What is Sass? Sass is a CSS preprocessor that extends CSS with additional features, such as variables, nesting, mixins, and more. It makes writing and maintaining CSS easier and more efficient.

File Extension: Sass files typically have a .scss extension.

## Variables

Declaration: Define variables to store values for reuse.

```
$primary-color: #007bff;
```

Usage: Use variables to set properties.

```
.button {
  background-color: $primary-color;
}
```

## Nesting

Nesting Selectors: Nest child selectors inside parent selectors to improve readability.

```
.container {
  h1 {
    font-size: 24px;
  }
  p {
    font-size: 16px;
  }
}
```

## Mixins

Mixin Declaration: Define reusable blocks of CSS with mixins.

```
@mixin button-styles {
  background-color: $primary-color;
  color: #fff;
  padding: 10px 20px;
}
```

Mixin Usage: Include mixins in selectors.

```
.button {
  @include button-styles;
}
```

## Partials

Partial Files: Create partial Sass files with \_ prefix (e.g., \_variables.scss) to modularize your code.

Import Partials: Import partials into main Sass files using @import.

```
@import 'variables';
```

## Operators

Mathematical Operators: Use operators for calculations.

```
$width: 100px;
.element {
  width: $width * 2;
}
```

## Functions

Built-in Functions: Sass provides built-in functions for various operations.

```
$color: #007bff;
.element {
  background-color: darken($color, 10%);
}
```

## Control Directives

Conditional Statements: Use @if, @else if, and @else for conditional styling.

```
$theme: 'light';

.element {
  @if $theme == 'light' {
    background-color: #fff;
  } @else {
    background-color: #000;
    color: #fff;
  }
}
```

Loops: Use @for and @each to create loops for repetitive styles.

## Extend/Inheritance

Extend Directive: Use @extend to share styles among selectors.

```
.error {
  border: 1px solid red;
}

.input-error {
  @extend .error;
  background-color: pink;
}
```

## Comments

Single-line Comments: Use // for single-line comments (not included in compiled CSS).

```
// This is a single-line comment
```

Multi-line Comments: Use /\* \*/ for multi-line comments (included in compiled CSS).

```
/*
  This is a
  multi-line comment
*/
```

## Output Style

Output Style: Set the output style for the compiled CSS.

```
// Options: nested (default), expanded, compact, compressed
$output-style: compressed;
```

## Importing CSS

Import CSS: Import regular CSS files into Sass.

```
@import 'styles.css';
```

## Resources

Sass Official Documentation
SassMeister: Online Sass compiler and playground.
