# Block and Inline

## What Is Normal Flow?

**Normal flow** is the browser’s default layout behavior when CSS does not change how elements participate in the page layout.

By default, elements are arranged according to their display types and the order in which they appear in the HTML document.

There are two fundamental types of boxes:

- **Block boxes**: Typically start on a new line and stack vertically.
- **Inline boxes**: Flow alongside text and other inline content within a line.

Understanding normal flow helps you predict how elements will be positioned before using more advanced layout systems such as Flexbox and Grid.

### Example

```html
<h1>My Website</h1>
<p>This is the first paragraph.</p>
<p>This is the second paragraph.</p>
```

The heading and paragraphs appear on separate lines because they use block-level layout by default.

## Block Elements

A **block-level element** typically begins on a new line and occupies the available width of its containing block when its width is `auto`.

Block elements stack vertically in normal flow.

### Common Block Elements

| **Element** | **Purpose** |
| --- | --- |
| `<div>` | Generic container |
| `<p>` | Paragraph |
| `<h1>`-`<h6>` | Headings |
| `<section>` | Thematic section |
| `<article>` | Self-contained content |
| `<header>` | Introductory content |
| `<footer>` | Footer content |
| `<main>` | Main content of a document |

### Example

```html
<div class="box">First box</div>
<div class="box">Second box</div>
<div class="box">Third box</div>
```

```css
.box {
	background-color: lightblue;
	border: 1px solid blue;
	padding: 10px;
}
```

The three boxes appear on separate lines, with each box typically stretching across the available width of its container.

### Key Characteristics

- Start on a new line in normal flow.
- Typically occupy the available inline space when `width` is `auto`.
- Respect declared `width` and `height`.
- Respect padding, borders, and margins according to the box model.
- Stack vertically unless another layout method changes their behavior.

**Important**: A block element does not always fill the entire width of its parent. Explicit widths, maximum widths, margins, and other layout rules can change its dimensions.

## Inline Elements

An **inline element** flows within a line of text instead of automatically starting a new line.

Inline elements generally occupy only the space required by their content.

### Common Inline Elements

| **Element** | **Purpose** |
| --- | --- |
| `<span>` | Generic inline container |
| `<a>` | Hyperlink |
| `<strong>` | Strong importance |
| `<em>` | Stress emphasis |
| `<code>` | Inline code |
| `<label>` | Label for a form control |

### Example

```html
<p>
	Learn <strong>HTML</strong>, style with <em>CSS</em>
	<a href="https://www.theodinproject.com/">The Odin Project</a>.
</p>
```

The elements appear within the same paragraph rather than each starting on a new line.

### Key Characteristics

- Do not automatically start a new line.
- Flow alongside text and other inline content.
- Typically take up only the width needed for their content.
- Wrap onto subsequent lines when there is insufficient horizontal space.
- Ordinary inline elements do not respond to `width` and `height` in the same way as block elements.

### Padding, Margin, and Dimensions

For ordinary non-replaced inline elements:

- Horizontal padding and margins affect the space around the inline content.
- Vertical padding and borders can be visible but generally do not increase the line box height in the same way as block elements.
- Vertical margins do not push surrounding lines apart in the usual block-layout manner.
- `width` and `height` generally do not control the element’s dimensions.

Some inline-level elements, such as `<img>`, are **replaced elements** and can have their width and height controlled even when their display value remains `inline`.

## Inline-Block Elements

`display: inline-block` combines characteristics of inline and block layout.

An inline-block element sits alongside other inline-level content but behaves like a block box internally.

### Example

```html
<span class="badge">HTML</span>
<span class="badge">CSS</span>
<span class="badge">JavaScript</span>
```

```css
.badge {
	display: inline-block;
	width: 120px;
	padding: 10px;
	margin: 5px;
	border: 1px solid black;
	background-color: lightgray;
	text-align: center;
}
```

The badges can sit beside one another while respecting their specified dimensions, padding, borders, and margins.

### Key Characteristics

- Flows alongside text and other inline-level content.
- Respects declared `width` and `height`.
- Supports padding, borders, and margins on all sides.
- Can wrap to the next line when insufficient horizontal space remains.

### When to Use Inline-Block

Inline-block is useful for small components that need to appear side by side while maintaining control over their dimensions.

Examples include:

- Labels and badges.
- Small buttons or button-like elements.
- Compact navigation items.
- Small cards in a simple inline layout.

For more complex arrangements, Flexbox or Grid is often easier to manage.

## Comparing Block, Inline, and Inline-Block

| **Behavior** | **`block`** | **`inline`** | **`inline-block`** |
| --- | --- | --- | --- |
| Starts on a new line | Yes, in normal flow | No | No |
| Flows alongside inline content | No, by default | Yes | Yes |
| Width and height control | Yes | Generally no for ordinary inline elements | Yes |
| Horizontal padding and margins | Yes | Yes | Yes |
| Vertical padding and margins affect layout | Yes | Behaves differently from block boxes | Yes |
| Can wrap onto another line as inline-level content | No | Yes | Yes |

The distinctions are about layout behavior, not permanent categories attached to HTML tag names, CSS can change an element’s display behavior.

## The `display` Property

The CSS `display` property controls how an element participates in layout.

```css
div {
	display: inline;
}

span {
	display: block;
}

.badge {
	display: inline-block;
}
```

In this example:

- The `<div>` behaves as an inline element.
- The `<span>` behaves as a block element.
- Elements with the `badge` class behave as inline-block elements.

The HTML tags themselves have not changed. Only their CSS layout behavior has changed.

### Common Values

| **Value** | **Behavior** |
| --- | --- |
| `block` | Creates a block-level box |
| `inline` | Creates an inline-level box |
| `inline-block` | Flows inline while behaving like a block box internally |
| `flex` | Establishes a Flexbox layout for its children |
| `grid` | Establishes a Grid layout for its children |
| `none` | Removes the element from layout and prevents it from being rendered |

`display: none` is different from `visibility: hidden`. The latter hides an element while normally preserving its layout space.

## Understanding `<div>` and `<span>`

`<div>` and `<span>` are generic containers. They are useful when you need to group content for styling or layout but no more meaningful HTML element is appropriate.

### The `<div>` Element

A `<div>` is a generic container that behaves as a block-level box by default.

It is commonly used to group larger sections of content.

```html
<div class="card">
	<h2>Learn HTML</h2>
	<p>Start with the fundamentals of HTML.</p>
</div>
```

```css
.card {
	background-color: lightgray;
	padding: 20px;
	margin-bottom: 16px;
}
```

The `<div>` gives the heading and paragraph a shared container that can be styled as one component.

### The `<span>` Element

A `<span>` is a generic inline container. It is useful for styling or identifying a small part of text without creating a new block.

```html
<p>
	CSS makes webpages
	<span class="highlight">visually appealing</span>.
</p>
```

```css
.highlight {
	color: red;
	font-weight: bold;
}
```

Only the text inside the `<span>` receives the specified style, while the sentence remains part of the same paragraph.

### `<div>` vs. `<span>`

| **`<div>`** | **`<span>`** |
| --- | --- |
| Block-level by default | Inline by default |
| Commonly groups sections or components | Commonly targets a portion of text |
| Starts on a new line in normal flow | Flows with surrounding text |
| Often used for layout containers | Often used for small styling hooks |

### Use Semantic HTML When Appropriate

Although `<div>` and `<span>` are useful, do not use them when a more meaningful element fits the content.

For example, prefer:

```html
<nav>
	<a href="/">Home</a>
	<a href="/about">About</a>
</nav>
```

over using generic `<div>` elements for everything.

Semantic elements help communicate the purpose and structure of the content.

## Normal Flow and the Box Model

Block and inline behavior works together with the CSS box model.

```css
p {
	width: 400px;
	padding: 10px;
	border: 2px solid black;
	margin: 20px;
}
```

In the default `content-box` model, the declared width describes the content area. Padding and borders are added to the rendered width, while margins sit outside the border.

The type of box affects how these dimensions interact with the surrounding layout.

- Block elements typically stack vertically.
- Inline elements participate in line layout.
- Inline-block elements participate in line layout while retaining block-style dimensions.

When spacing or sizing looks unexpected, inspect both the element’s display behavior and its box-model properties.

## When to Use Each Display Type

Choose a display type based on the layout you need.

### Use `block` when:

- An element should start on a new line.
- You need to control its width or height.
- You are creating a container or section.

### Use `inline` when:

- Content should flow naturally within a line of text.
- You are styling a word or phrase.
- The element should not automatically start a new line.

### Use `inline-block` when:

- Elements should sit next to one another.
- You need to control their width and height.
- You need block-style padding and margins without forcing each element onto a separate line.

### Use Flexbox or Grid when:

- You need to align groups of elements systematically.
- You need consistent spacing between items.
- You are building more complex component layouts.

Flexbox and Grid provide more explicit layout controls than relying on inline-block elements alone.