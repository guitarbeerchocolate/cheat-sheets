# Flexbox Cheat Sheet

## Introduction

Flexbox, short for "Flexible Box Layout," is a layout model in CSS designed to make it easier to design complex layouts and distribute space among items in a container. It provides a more efficient way to align and distribute space among items in a container, even when their sizes are unknown or dynamic.

## Flex Container

To create a flex container, you need to set the `display` property to `flex` on its parent element.

```css
.container {
  display: flex;
}
```

## Flex Direction

- flex-direction: row; (default): Items are arranged horizontally.
- flex-direction: row-reverse;: Items are arranged horizontally in reverse order.
- flex-direction: column;: Items are arranged vertically.
- flex-direction: column-reverse;: Items are arranged vertically in reverse order.

```
.container {
  flex-direction: column;
}
```

- ## Justify Content
- justify-content: flex-start; (default): Items are packed to the start of the container.
- justify-content: flex-end;: Items are packed to the end of the container.
- justify-content: center;: Items are centered within the container.
- justify-content: space-between;: Items are evenly distributed with space between them.
- justify-content: space-around;: Items are evenly distributed with space around them.

```
.container {
  justify-content: center;
}
```

## Align Items

- align-items: flex-start; (default): Items are aligned to the start of the cross axis.
- align-items: flex-end;: Items are aligned to the end of the cross axis.
- align-items: center;: Items are centered in the cross axis.
- align-items: baseline;: Items are aligned based on their baseline.
- align-items: stretch;: Items are stretched to fill the container.

```
.container {
  align-items: center;
}
```

## Flex Wrap

- flex-wrap: nowrap; (default): Items are in a single line.
- flex-wrap: wrap;: Items wrap onto multiple lines when necessary.
- flex-wrap: wrap-reverse;: Items wrap onto multiple lines in reverse order.

```
.container {
  flex-wrap: wrap;
}
```

## Flex Items

### Flex Grow

The flex-grow property specifies how much an item will grow relative to the rest of the items in the container. It takes a numeric value.

```
.item {
  flex-grow: 1;
}
```

### Flex Shrink

The flex-shrink property specifies how much an item will shrink relative to the rest of the items in the container. It takes a numeric value.

```
.item {
  flex-shrink: 1;
}
```

### Flex Basis

The flex-basis property specifies the initial size of an item before it is flexed. It takes a length or a keyword value.

```
.item {
  flex-basis: 100px;
}
```

### Flex

The flex property is a shorthand for flex-grow, flex-shrink, and flex-basis.

```
.item {
  flex: 1 1 auto;
}
```

### Align Self

The align-self property overrides the align-items value for a single item. It takes the same values as align-items.

```
.item {
  align-self: flex-start;
}
```
