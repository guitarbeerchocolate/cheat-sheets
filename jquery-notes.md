# jQuery Cheat Sheet

## Introduction to jQuery

What is jQuery? jQuery is a fast, small, and feature-rich JavaScript library that simplifies HTML document traversal and manipulation, event handling, and animation.

Why jQuery? jQuery makes it easier to write cross-browser JavaScript code and simplifies common tasks in web development.

## Getting Started

Include jQuery: Add jQuery to your HTML file using a script tag.

```
<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
```

Document Ready: Execute code when the DOM is fully loaded.

```
$(document).ready(function() {
  // jQuery code here
});
```

Shorthand for Document Ready:

```
$(function() {
  // jQuery code here
});
```

## Selecting Elements

ID Selector:

```
$('#myId');
```

Class Selector:

```
$('.myClass');
```

Element Selector:

```
$('p');
```

Attribute Selector:

```
$('input[type="text"]');
```

Multiple Selectors:

```
$('#myId, .myClass, p');
```

## Manipulating Elements

Get/Set Text Content:

```
$('#myElement').text();          // Get text
$('#myElement').text('New Text'); // Set text
```

Get/Set HTML Content:

```
$('#myElement').html();             // Get HTML
$('#myElement').html('<p>HTML</p>'); // Set HTML
```

Get/Set Attribute:

```
$('#myElement').attr('href');          // Get attribute
$('#myElement').attr('href', 'newurl'); // Set attribute
```

Add/Remove Class:

```
$('#myElement').addClass('newClass');
$('#myElement').removeClass('oldClass');
```

Show/Hide Elements:

```
$('#myElement').show();
$('#myElement').hide();
```

## Events

Click Event:

```
$('#myElement').click(function() {
  // Code to run on click
});
```

Mouse Enter/Leave Event:

```
$('#myElement').mouseenter(function() {
  // Code to run on mouse enter
});
$('#myElement').mouseleave(function() {
  // Code to run on mouse leave
});
```

Form Submit Event:

```
$('form').submit(function(event) {
  event.preventDefault(); // Prevent form submission
  // Code to handle form submission
});
```

## Animations

Fade In/Fade Out:

```
$('#myElement').fadeIn();
$('#myElement').fadeOut();
```

Slide Down/Slide Up:

```
$('#myElement').slideDown();
$('#myElement').slideUp();
```

Animate Custom Properties:

```
$('#myElement').animate({ width: '200px', height: '200px' }, 1000);
```

## AJAX

Load Content:

```
$('#myElement').load('url-to-load');
```

AJAX GET Request:

```
$.get('url', function(data) {
  // Handle data
});
```

AJAX POST Request:

```
$.post('url', { key: 'value' }, function(data) {
  // Handle data
});
```
