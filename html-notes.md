# HTML notes

## About HTML

HTML stands for HyperText Markup Language. It is the standard markup language used to create web pages and is a fundamental technology for building websites. HTML provides a way to structure the content of a web page by using various elements and tags to define the layout, text, images, links, forms, and other elements that make up a webpage.

HTML documents consist of a series of elements enclosed in tags. Tags are used to define the structure and appearance of content on a web page. For example, you can use HTML tags to create headings, paragraphs, lists, tables, links, and more. These tags are interpreted by web browsers to render web pages correctly.

## How to create HTML inside VS Code

To create a basic page

`! + tab`

To create an article with a paragraph and an aside with a table within a HTML body

`article>p+aside>table`

Basic HTML Structure: Set up the basic structure of an HTML document with `<html>`, `<head>`, and `<body>` elements.

### 1. Basic Structure

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Page Title</title>
  </head>
  <body>
    <!-- Content goes here -->
  </body>
</html>
```

Headings: Use `<h1>`, `<h2>`, `<h3>`, `<h4>`, `<h5>`, and `<h6>` elements to create headings of varying importance.

```
<h1>Heading 1</h1>
<h2>Heading 2</h2>
<h3>Heading 3</h3>
<h4>Heading 4</h4>
<h5>Heading 5</h5>
<h6>Heading 6</h6>
```

Create Paragraphs: Use the `<p>` element to structure and display text content in paragraphs.

```
<p>This is a paragraph.</p>
```

Insert Line Breaks: Use the `<br />` element to insert line breaks within text.

Create Lists: Use `<ul>` for unordered lists (bulleted lists) and `<ol>` for ordered lists (numbered lists), along with <li> for list items.

```
<ul>
    <li>Item 1</li>
    <li>Item 2</li>
</ul>
<ol>
    <li>Item 1</li>
    <li>Item 2</li>
</ol>
```

Create Links: Use the `<a>` element to create hyperlinks to other web pages or resources.

```
<a href="https://www.example.com">Visit Example.com</a>
```

Add Images: Use the `<img>` element to display images on a web page.

```
<img src="image.jpg" alt="Image Description">
```

Structure Text: Utilize elements like `<strong>`, `<em>`, `<u>`, `<s>`, `<sub>`, and `<sup>` to emphasize, underline, strike through, and format text.

Create Tables: Use `<table>`, `<thead>`, `<tbody>`, `<tr>`, `<th>`, and `<td>` elements to create structured tables of data.

```
<table>
    <thead>
        <tr>
            <th>Header 1</th>
            <th>Header 2</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Data 1</td>
            <td>Data 2</td>
        </tr>
    </tbody>
</table>
```

Create Forms: Use `<form>`, `<input>`, `<textarea>`, `<select>`, `<button>`, and other form elements to collect user input.

```
<form action="/submit" method="POST">
    <label for="name">Name:</label>
    <input type="text" id="name" name="name" required>
    <br>
    <label for="email">Email:</label>
    <input type="email" id="email" name="email" required>
    <br>
    <button type="submit">Submit</button>
</form>
```

Add Labels and Inputs: Use `<label>` elements to provide labels for form fields, improving accessibility.

Create Dropdown Menus: Use `<select>` elements with `<option>` elements to create dropdown menus in forms.

Set Page Titles: Use the `<title>` element within the `<head>` section to set the title of the webpage.

Add Metadata: Include metadata tags like `<meta>` for character encoding, `<meta>` for viewport settings, and `<meta>` for descriptions.

Link to External Resources: Use `<link>` and `<script>` elements to link to external CSS and JavaScript files.

```
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link rel="stylesheet" type="text/css" href="styles.css">
<link rel="icon" type="image/png" href="favicon.png">
<script>
    function greet() {
        alert("Hello, World!");
    }
</script>
<script src="script.js"></script>
```

Add Comments: Use `<!-- Comment Text -->` to insert comments within the HTML code for documentation and readability.

Nest Elements: Properly nest HTML elements to maintain a clear and valid document structure.

Use Semantic HTML: Choose semantic elements like `<header>`, `<nav>`, `<main>`, `<article>`, `<section>`, `<aside>`, `<footer>`, and `<figure>` to provide meaningful structure to your content.

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sample Page</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <header>
        <h1>Welcome to Our Website</h1>
        <nav>
            <ul>
                <li><a href="#home">Home</a></li>
                <li><a href="#about">About Us</a></li>
                <li><a href="#services">Services</a></li>
                <li><a href="#contact">Contact</a></li>
            </ul>
        </nav>
    </header>

    <main>
        <article>
            <h2 id="about">About Us</h2>
            <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla eget erat eu urna mollis congue.</p>
        </article>

        <article>
            <h2 id="services">Our Services</h2>
            <section>
                <h3>Service 1</h3>
                <p>Details about Service 1.</p>
            </section>
            <section>
                <h3>Service 2</h3>
                <p>Details about Service 2.</p>
            </section>
        </article>
    </main>

    <aside>
        <h2>Related Links</h2>
        <ul>
            <li><a href="#news">Latest News</a></li>
            <li><a href="#events">Upcoming Events</a></li>
        </ul>
    </aside>

    <footer>
        &copy; 2023 Our Company | All rights reserved.
    </footer>

    <figure>
        <img src="sample-image.jpg" alt="A sample image">
        <figcaption>Image Caption</figcaption>
    </figure>
</body>
</html>
```

Understand HTML5 Elements: Add HTML5 elements like `<video>`, `<audio>`, `<canvas>` and `<svg>` to add multimedia and interactive elements to your web pages.

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Media and Graphics Example</title>
</head>
<body>
    <h1>HTML Multimedia and Graphics Example</h1>

    <!-- Video -->
    <section>
        <h2>Video</h2>
        <video controls width="480" height="270">
            <source src="sample-video.mp4" type="video/mp4">
            Your browser does not support the video tag.
        </video>
    </section>

    <!-- Audio -->
    <section>
        <h2>Audio</h2>
        <audio controls>
            <source src="sample-audio.mp3" type="audio/mpeg">
            Your browser does not support the audio tag.
        </audio>
    </section>

    <!-- Canvas -->
    <section>
        <h2>Canvas</h2>
        <canvas id="myCanvas" width="200" height="100"></canvas>
        <script>
            const canvas = document.getElementById('myCanvas');
            const context = canvas.getContext('2d');
            context.fillStyle = 'blue';
            context.fillRect(10, 10, 150, 80);
        </script>
    </section>

    <!-- SVG -->
    <section>
        <h2>SVG</h2>
        <svg xmlns="http://www.w3.org/2000/svg" width="200" height="100">
            <rect x="10" y="10" width="150" height="80" fill="green" />
        </svg>
    </section>
</body>
</html>
```

## Auto-Completion and Formatting in VS Code

VS Code provides auto-completion for HTML tags and attributes. Start typing a tag and use Tab to complete it.

To format your HTML code, you can right-click and select "Format Document," or use the keyboard shortcut Shift + Alt + F (Windows/Linux) or Shift + Option + F (Mac).

Extensions: VS Code supports extensions for HTML development. You can install extensions like "HTML Snippets" or "Live Server" to enhance your HTML development experience.

Preview: To see a live preview of your HTML page, you can install the "Live Server" extension, which allows you to open a local development server and preview your page in your web browser.
