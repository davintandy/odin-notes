# Intro to CSS

## What Is CSS?

**CSS (Cascading Style Sheets)** is a stylesheet language used to control the appearance and layout of HTML documents.

HTML defines the structure and content of a webpage, while CSS determines how that content looks.

### HTML vs. CSS

| **HTML** | **CSS** |
| --- | --- |
| Defines webpage structure | Controls visual presentation |
| Creates headings, paragraphs, links, and images | Controls colors, fonts, sizes, and spacing |
| Uses elements and attributes | Uses selectors, properties, and values |

Example:

```html
<h1>Hello World!</h1>
<p>This is my first webpage.</p>
```

```css
h1 {
	color: blue;
}

p {
	color: gray;
}
```

The HTML defines the content, while the CSS changes how that content appears in the browser.

## Adding CSS to HTML

There are three ways to apply CSS to an HTML document:

1. External CSS
2. Internal CSS
3. Inline CSS

### External CSS

External CSS stores styles in a separate `.css` file and links it to the HTML document.

HTML:

```html
<head>
	<link rel="stylesheet" href="styles.css">
</head>
```

CSS:

```css
h1 {
	color: blue;
}
```

The `<link>` element connects the HTML document to the stylesheet.

- `rel="stylesheet"` specifies the relationship between the HTML document and the linked resource.
- `href="styles.css"` specifies the stylesheet’s location relative to the HTML file.

The `<link>` element belongs inside `<head>` and is a void element, so it does not require a closing tag.

### Advantages

- Keeps HTML and CSS separate, making both easier to read and maintain.
- Allows multiple HTML pages to share the same stylesheet.
- Makes global style changes easier because the styles can be updated in one file.

**Best practice**: Use external CSS for most projects.

### Internal CSS

Internal CSS places stylesheet rules inside a `<style>` element in the HTML document’s `<head>`.

```html
<head>
	<style>
		h1 {
			color: blue;
		}
		
		p {
			color: gray;
		}
	</style>
</head>
```

Internal CSS can be useful for a single page or a small demonstration, but it combines presentation with the HTML document and is less convenient when styles need to be reused across pages.

### Inline CSS

Inline CSS applies styles directly to an HTML element using the `style` attribute.

```html
<h1 style="color: blue;">Hello World!</h1>
```

Inline styles are useful for limited, specific cases but are generally discouraged as the primary styling method because they:

- Mix presentation with HTML content.
- Make styles harder to maintain.
- Encourage repeated declarations across multiple elements.
- Typically take precedence over ordinary external and internal author styles in the CSS cascade.

### Comparison

| **Method** | **Where CSS is written** | **Best use** |
| --- | --- | --- |
| External | Separate `.css` file | Most projects are reusable styles |
| Internal | `<style>` inside `<head>` | Page-specific demonstrations or small pages |
| Inline | `style` attribute on an element | Occasional element-specific styling |

## Basic CSS Syntax

A CSS rule consists of a **selector** and a declaration block.

```css
selector {
	property: value;
}
```

Example:

```css
p {
	color: red;
	font-size: 18px;
}
```

### Components of a CSS Rule

| **Component** | **Meaning** | **Example** |
| --- | --- | --- |
| Selector | Identifies the elements to style | `p` |
| Declaration block | Contains the style declarations, enclosed in `{}` | `{ color: red; }` |
| Property | Specifies what aspect to change | `color` |
| Value | Specifies the desired setting | `red` |
| Declaration | A property-value pair ending in a semicolon | `color: red;` |

A declaration follows this structure:

```css
property: value;
```

Multiple declarations can appear inside one rule:

```css
p {
	color: red;
	background-color: yellow;
	font-size: 18px;
}
```

### CSS Comments

Use comments to explain your styles or temporarily disable declarations.

```css
p {
	color: red;
	/* font-size: 18px; */
}
```

CSS comments begin with `/*` and end with `*/`.

## CSS Selectors

A **selector** determines which HTML elements receive a CSS rule.

### Universal Selector

The universal selector (`*`) selects all elements.

```css
* {
	color: purple;
}
```

This applies the specified text color to all elements unless another applicable rule overrides it.

### Type Selector

A type selector, also called an element selector, selects all elements of a specific HTML type.

```css
p {
	color: red;
}
```

All `<p>` elements receive the specified style, while elements of other types are not directly selected by this rule.

### Class Selector

A class selector selects elements with a particular `class` attribute. Its CSS syntax starts with a period (`.`).

HTML:

```html
<p class="alert-text">Please read this warning.</p>
<div class="alert-text">Important information.</div>
```

CSS:

```css
.alert-text {
	color: red;
}
```

Both elements receive the rule because they share the `alert-text` class.

### Multiple Classes

An element can have multiple classes, separated by spaces.

```html
<div class="alert-text severe-alert">
	Critical warning.
</div>
```

Each class can be targeted independently:

```css
.alert-text {
	color: red;
}

.severe-alert {
	font-weight: bold;
}
```

Use hyphens for multiword class names, such as `alert-text`, rather than spaces. Spaces separate distinct class names in HTML.

Classes are reusable and can be applied to multiple elements, making them the preferred choice for most reusable styling rules.

### ID Selector

An ID selector targets an element with a particular `id` attribute. Its CSS syntax starts with a hash (`#`).

HTML:

```html
<h1 id="main-title">My Website</h1>
```

CSS:

```css
#main-title {
	color: blue;
}
```

An ID should be unique within an HTML document. Unlike classes, IDs are intended to identify a particular element.

Use IDs when a unique identifier is needed, such as for linking to a section of a page. For reusable styling, classes are generally more flexible.

### Class vs. ID

| **Class (`.class-name`)** | **ID (`#id-name`)** |
| --- | --- |
| Can be reused across many elements | Should uniquely identify one element per page |
| An element can have multiple classes | An element should have only one ID value |
| Commonly used for reusable styles | Useful for unique identification and specific targets |
| Lower specificity than an ID selector | Higher specificity than a class selector |

Class and ID names are case-sensitive when matched by CSS. Prefer descriptive names beginning with letters and avoid whitespace.

## Grouping Selectors

**Grouping selectors** allows multiple selectors to share the same declarations. Separate them with commas.

```css
.read,
.unread {
	color: white;
	background-color: black;
}
```

You can still define additional styles separately:

```css
.read {
	font-weight: bold;
}

.unread {
	opacity: 0.7;
}
```

Grouping reduces repetition and makes shared styles easier to maintain.

**Remember**: A comma separates selectors and applies the rule to each of them independently.

## Chaining Selectors

**Chaining selectors** combines multiple selectors without spaces or commas. The resulting selector matches an element that satisfies all the specified conditions.

HTML:

```html
<div class="subsection header">Latest Posts</div>
<p class="subsection preview">Post preview..</p>
```

To select only the element that has both `subsection` and `header` classes:

```css
.subsection.header {
	color: red;
}
```

The selector matches the `<div>` but not the `<p>` because the paragraph does not have the `header` class.

You can also combine a class and an ID:

```html
<p class="subsection" id="preview">Post preview..</p>
```

```css
.subsection#preview {
	color: blue;
}
```

This matches an element with both the `subsection` class and the `preview` ID.

## Descendant Combinator

A **descendant combinator** selects elements nested anywhere inside another matching element. It is represented by a space between selectors.

HTML:

```html
<div class="ancestor">
	<div class="contents">
		<p class="contents">Nested paragraph</p>
	</div>
</div>

<div class="contents">Outside content</div>
```

CSS:

```css
.ancestor .contents {
	color: red;
}
```

The selector targets elements with the `contents` class that have an ancestor with the `ancestor` class.

In this example, the inner `<div>` and nested `<p>` are selected, while the final `<div>` is not.

Avoid unnecessarily complicated descendant selectors. Deeply nested selectors can make styles harder to understand and maintain.

## Basic CSS Properties

CSS properties control different visual aspects of HTML elements. The following are useful starting points.

### Color and Background Color

- `color` changes the text color.
- `background-color` changes the element’s background color.

```css
p {
	color: white;
	background-color: black;
}
```

Common color value formats include:

```css
h1 {
	color: red;
}

p {
	color: #1100ff;
}

div {
	color: rgb(100, 0, 127);
}

span {
	color: hsl(15, 82%, 56%);
}
```

Colors can be specified using named keywords, hexadecimal values, RGB, HSL, and other supported CSS color formats.

### Typography

| **Property** | **Purpose** | **Example** |
| --- | --- | --- |
| `font-family` | Specifies the typeface | `font-family: Arial, sans-serif;` |
| `font-size` | Controls text size | `font-size: 18px;` |
| `font-weight` | Controls font boldness | `font-weight: 700;` |
| `text-align` | Aligns inline content horizontally within a block | `text-align: center;` |

### Font Fallbacks

You can provide multiple fonts separated by commas. If the browser cannot use the first font, it tries the next one.

```css
body {
	font-family: "Times New Roman", serif;
}
```

- `"Times New Roman"` is a specific font family name.
- `serif` is a generic font family.

Specific font names containing spaces are usually quoted for readability. Generic family names do not need quotation marks.

### Image Height and Width

The `width` and `height` properties control an image’s rendered dimensions.

```css
img {
	width: 500px;
	height: auto;
}
```

Setting one dimension and using `auto` for the other preserves the image’s aspect ratio.

For example, if the original image is 1000 pixels wide and 500 pixels high, setting its width to `500px` and height to `auto` results in a rendered size of approximately 500 x 250 pixels.

For responsive images:

```css
img {
	max-width: 100%;
	height: auto;
}
```

This prevents an image from becoming wider than its container while preserving its proportions.

### HTML Dimensions and CSS

HTML can also specify an image’s intrinsic dimensions:

```html
<img
	src="images/photo.jpg"
	alt="A landscape"
	width="1000"
	height="500"
>
```

Providing accurate `width` and `height` attributes allows the browser to reserve space for the image before it finishes loading, reducing unexpected layout shifts. CSS can then control its responsive appearance.

## Semantic HTML and the `<div>` Element

A `<div>` is a generic container used to group content when no more appropriate semantic element fits.

```html
<div class="card">
	<h2>Introduction</h2>
	<p>Learn the basics of CSS.</p>
</div>
```

The class allows the container to be styled:

```css
.card {
	background-color: lightgray;
	color: black;
}
```

However, use meaningful HTML elements whenever possible.

For example:

- Use `<h1>-<h6>` for headings.
- Use `<p>` for paragraphs.
- Use `<nav>` for navigation.
- Use `<main>` for the page's primary content.
- Use `<div>` when a generic container is appropriate.

Semantic HTML communicates the meaning and structure of content, improving maintainability and supporting accessibility.