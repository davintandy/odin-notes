# Elements and Tags

## What Is HTML?

**HTML (HyperText Markup Language)** is the standard markup language used to define the structure and content of webpages.

HTML uses predefined elements to tell the browser how content is organized, such as headings, paragraphs, lists, and links.

Web development commonly uses three core technologies:

- **HTML**: Defines the structure and content.
- **CSS**: Controls the appearance and layout.
- **JavaScript**: Adds interactivity and dynamic behavior.

HTML is a **markup language**, not a programming language. It describes and organizes content rather than implementing general programming logic.

## What Are HTML Tags?

**HTML tags** are keywords enclosed in angle brackets (`<>`) that mark the beginning or end of an HTML element.

Most HTML elements use two tags:

- **Opening tag**: Marks the beginning of an element.
- **Closing tag**: Marks the end of an element and includes a forward slash (`/`) before the tag name.

Example:

```html
<p>This is a paragraph.</p>
```

The code consists of:

- `<p>` - opening tag.
- `This is a paragraph.` - content.
- `</p>` - closing tag.

Tags tell the browser how to interpret the content they surround.

## What Are HTML Elements?

An **HTML element** consists of an opening tag, its content, and a closing tag, when applicable.

Using the previous example:

```html
<p>This is a paragraph.</p>
```

The entire expression is a paragraph element, while `<p>` and `</p>` are its opening and closing tags.

### Tags vs. Elements

| **Term** | **Meaning** | **Example** |
| --- | --- | --- |
| Opening tag | Marks the start of an element | `<h1>` |
| Closing tag | Marks the end of an element | `</h1>` |
| Content | The content inside the tags | `Hello World` |
| Element | The complete structure | `<h1>Hello World</h1>` |

**Remember**: A tag is part of an element. The element is the complete unit of markup.

## Common HTML Elements

HTML provides many predefined elements for different kinds of content.

### Headings

HTML has six heading levels, from `<h1>` to `<h6>`.

```html
<h1>Main Heading</h1>
<h2>Section Heading</h2>
<h3>Subsection Heading</h3>
```

Use headings to establish a meaningful content hierarchy, rather than choosing them only for their default visual size.

### Paragraphs

The `<p>` element represents a paragraph.

```html
<p>This is the first paragraph.</p>
<p>This is the second paragraph.</p>
```

### Lists

Unordered lists use `<ul>`, while ordered lists use `<ol>`. Each list item uses `<li>`

```html
<ul>
	<li>HTML</li>
	<li>CSS</li>
	<li>JavaScript</li>
</ul>
```

### Links

The `<a>` element creates a hyperlink.

```html
<a href="https://www.theodinproject.com/">The Odin Project</a>
```

The `href` attribute specifies the link destination.

## Void Elements

Most HTML elements have opening and closing tags, but some do not. These are called **void elements**.

Void elements cannot contain content and do not have closing tags.

Common examples include:

| **Element** | **Purpose** |
| --- | --- |
| `<br>` | Creates a line break |
| `<img>` | Embeds an image |
| `<hr>` | Represents a thematic break |
| `<meta>` | Provides metadata about the document |
| `<link>` | Links an external resource, often a CSS stylesheet |
| `<input>` | Creates an input control |

Example:

```html
<p>First line<br>Second line</p>
<img src="logo.png" alt="Company logo">
```

### What About Self-Closing Tags?

You may encounter syntax such as:

```html
<br />
<img src="logo.png" alt="Company logo" />
```

This is commonly called self-closing syntax. However, in HTML, void elements do not require a closing slash.

Prefer the standard HTML syntax.

```html
<br>
<img src="logo.png" alt="Company logo">
```

> **Important**: Do not confuse HTML void elements with elements that contain content. An element such as `<p>` still needs its closing tag.
> 

## Semantic HTML

**Semantic HTML** means choosing elements based on the meaning and purpose of their content.

For example:

- Use `<h1>` for a top-level heading.
- Use `<p>` for a paragraph.
- Use `<nav>` for a navigation section.
- Use `<main>` for the primary content of a page
- Use `<footer>` for footer content.

Using appropriate elements helps browsers and assistive technologies interpret the page structure. It can also improve accessibility and help search engines understand the content.

As you learn more HTML, focus on choosing elements for their meaning rather than their default appearance.