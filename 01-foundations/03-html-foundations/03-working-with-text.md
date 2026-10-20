# Working with Text

## Creating Paragraphs

The `<p>` element defines a paragraph of text.

```html
<p>This is the first paragraph.</p>
<p>This is the second paragraph.</p>
```

Each paragraph is treated as a separate block of content and is typically displayed on a new line with spacing around it.

### Why Use Paragraph Elements?

HTML does not treat line breaks and repeated spaces in the source code as paragraph separators. Browsers generally collapse consecutive whitespace characters into a single space.

For example:

```html
<body>
	This is the first sentence.
	This is the second sentence.
</body>
```

The browser generally displays this as one continuous line of text rather than two separate paragraphs.

Use `<p>` to define separate paragraphs explicitly.

```html
<body>
	<p>This is the first paragraph.</p>
	<p>This is the second paragraph.</p>
</body>
```

**Key takeaway**: Use HTML elements to define the structure of your content instead of relying on how the code is spaced in the editor.

## Creating Headings

HTML provides six levels of headings, from `<h1>` to `<h6>`.

```html
<h1>Main Heading</h1>
<h2>Section Heading</h2>
<h3>Subsection Heading</h3>
<h4>Fourth-Level Heading</h4>
<h5>Fifth-Level Heading</h5>
<h6>Sixth-Level Heading</h6>
```

Browsers typically display higher-level headings in larger, bolder text by default.

### Organizing Headings

Use headings to create a logical hierarchy for your content.

```html
<h1>My First Blog</h1>

<h2>Introduction</h2>
<p>Welcome to my blog.</p>

<h2>My Learning Journey</h2>
<p>I am learning HTML and CSS.</p>

<h3>What I Learned Today</h3>
<p>I learned how to structure text using HTML.</p>
```

The hierarchy looks like this:

```
My First Blog (h1)
├── Introduction (h2)
└── My Learning Journey (h2)
    └── What I Learned Today (h3)
```

### Best Practices

- Use headings according to their semantic hierarchy, not just their visual size.
- Use `<h1>` for the main heading of the page.
- Use lower-level headings to organize sections and subsections.
- Avoid choosing a heading level simply because its default font size looks better. Use CSS to change appearance when necessary.

## Making Text Important: `<strong>`

The `<strong>` element indicates that its content has strong importance, seriousness, or urgency.

Browsers typically display `<strong>` text in bold.

```html
<p>
	<strong>Warning:</strong> Save your work before closing the editor.
</p>
```

The opening and closing tags identify the important portion of the sentence.

### Why Use `<strong>`?

`<strong>` provides semantic meaning in addition to its typical bold appearance. Assistive technologies, such as screen readers, may communicate this importance to users.

Use `<strong>` when the text is genuinely important, rather than simply to make it visually bold.

## Emphasizing Text: `<em>`

The `<em>` element indicates stress emphasis within a sentence.

Browsers typically display `<em>` text in italic.

```html
<p>
	I <em>really</em> enjoy learning web development.
</p>
```

The emphasis changes which word receives stress when the sentence is read.

### Why Use `<em>`?

- It communicates emphasis and meaning.
- Assistive technologies may convey the emphasis.
- It is useful when the intended meaning depends on which words are stressed.

Use `<em>` when you want to emphasize a word or phrase semantically, not merely to apply italic styling.

## `<strong>` vs. `<em>`

Although both elements commonly change the appearance of text, they serve different purposes.

| **Element** | **Semantic meaning** | **Default appearance** |
| --- | --- | --- |
| `<strong>` | Strong importance | Bold |
| `<em>` | Stress emphasis | Italic |

### What About Bold and Italic Styling Without Emphasis?

Semantic meaning and visual appearance are different concerns.

If you need to change how text looks without changing its meaning, CSS is generally the appropriate tool.

```html
<p class="highlight">This text has a custom appearance.</p>
```

```css
.highlight {
	font-weight: bold;
}
```

The CSS changes the visual appearance without marking the text as semantically important.

## Nesting HTML Elements

**Nesting** means placing one HTML element inside another.

```html
<p>
	This is a paragraph with <strong>important text</strong>
</p>
```

Here, the `<strong>` element is nested inside the `<p>` element.

### Parent, Child, and Sibling Relationships

- **Parent**: An element that directly contains another element.
- **Child**: An element directly contained by another element.
- **Sibling**: Elements that share the same direct parent.

Example:

```html
<body>
	<p>First paragraph.</p>
	<p>Second paragraph.</p>
</body>
```

In this example:

- `<body>` is the parent of both paragraphs.
- Each `<p>` element is a child of `<body>`.
- The two paragraphs are siblings.

These relationships become important when applying CSS and manipulating elements with JavaScript.

### Correct Nesting

When elements are nested, close them in the reverse order in which they were opened.

Correct:

```html
<p>This is <strong>important text</strong>.</p>
```

Incorrect:

```html
<p>This is <strong>important text.</p></strong>
```

The incorrect example closes the paragraph before closing the nested `<strong>` element.

### Indentation

Indentation makes nested structures easier to read.

```html
<body>
	<h1>My Blog</h1>
	
	<p>
		I am learning <strong>HTML</strong>
		and <em>web development</em>
	</p>
</body>
```

Consistent indentation helps you understand the document structure and identify mistakes.

## HTML Comments

HTML comments allow you to leave notes in your source code for yourself or other developers.

```html
<!-- This is an HTML comment. -->
<p>This paragraph is visible in the browser.</p>
```

### Important Characteristics

- Comments are not rendered as visible webpage content.
- They can explain why a particular section of code exists.
- They can help organize or annotate complex markup.
- They remain visible to anyone who can inspect the HTML source, so never use comments to store passwords, secrets, or sensitive information.

### Commenting Out Code

You can temporarily hide a section of HTML from the rendered page by commenting it out.

```html
<!--
<p>This paragraph is not rendered while commented out.</p>
-->
```

Use this technique for temporary testing, but remove unnecessary commented-out code when it is no longer needed.

### VS Code Shortcut

The standard comment-toggle shortcut in VS Code is `Ctrl + /`.

The shortcut can comment or uncomment selected lines when supported by the editor and keyboard layout.

## Generating Placeholder Text with Lorem Ipsum

When creating a webpage, you may want to test the layout before writing the final content.

**Lorem Ipsum** is placeholder text commonly used for this purpose.

In VS Code, type:

```html
lorem
```

Then press `Enter` to trigger the Emmet abbreviation, provided the editor recognizes it in the current context.

VS Code can generate placeholder text that you can place inside paragraphs.

```html
<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
```

Placeholder text is useful when practicing paragraph structure, heading hierarchy, and text formatting. Replace it with meaningful content when the page is ready for its intended audience.