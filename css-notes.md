# CSS Cheat Sheet

## Selectors

```
p {
    color: blue;
}
```

Class Selector: Selects elements with a specific class attribute.

```
.highlight {
    background-color: yellow;
}
```

ID Selector: Selects a single element with a specific ID attribute.

```
#header {
    font-size: 24px;
}
```

Universal Selector: Selects all elements on the page.

```
- {
  margin: 0;
  padding: 0;
}
```

Attribute Selector: Selects elements with a specific attribute.

```
input[type="text"] {
    border: 1px solid #ccc;
}
```

## Properties

Color: Set text or background color.

```
color: #FF5733;
background-color: #F4A460;
```

Font: Define font properties.

```
font-family: Arial, sans-serif;
font-size: 16px;
font-weight: bold;
```

Margin & Padding: Control spacing around elements.

```
margin: 10px;
padding: 5px;
```

Border: Customize element borders.

```
border: 1px solid #000;
border-radius: 5px;
```

Text: Style text content.

```
text-align: center;
text-decoration: underline;
```

Background: Set background properties.

```
background-image: url('bg.jpg');
background-size: cover;
```

Display: Define how elements are displayed.

```
display: block;
display: inline-block;
```

Positioning: Control element positioning.

```
position: relative;
top: 10px;
left: 20px;
```

Flexbox: Layout elements in a flexible container.

```
display: flex;
justify-content: center;
align-items: center;
```

## Pseudo-classes & Pseudo-elements

:hover: Style an element when the mouse hovers over it.

```
a:hover {
    color: #FF0000;
}
```

:nth-child: Select elements based on their position in a parent.

```
li:nth-child(odd) {
    background-color: #F0F0F0;
}
```

::before & ::after: Insert content before or after an element.

```
.quote::before {
    content: "“";
}
```

## Media Queries

Responsive Design: Adjust styles based on screen size.

```
@media screen and (max-width: 768px) {
    body {
        font-size: 14px;
    }
}
```

## Box Model

- Content: The actual content area of an element.
- Padding: Space between the content and the border.
- Border: A border around the padding.
- Margin: Space outside the border.

## Specificity

- Inline Styles: Highest specificity.
- ID Selectors: Higher specificity.
- Class Selectors: Medium specificity.
- Element Selectors: Lowest specificity.

## Tips

- CSS Comments: Use /_ Comment _/ for comments.
- Keep it Simple: Avoid unnecessary complexity.
- Consistency: Maintain a consistent naming convention.
- CSS Resets: Use a CSS reset to remove default styles.
- External Stylesheets: Separate CSS from HTML for reusability.
- Browser Compatibility: Test in multiple browsers.
