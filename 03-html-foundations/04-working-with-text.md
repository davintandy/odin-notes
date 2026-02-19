# Working with Text

In HTML, text doesn’t always appear the way you type it in your editor. Browsers follow specific rules for spacing and hierarchy.

---

## Structural Text Elements

### The Whitespace “Problem”

If you type two separate paragraphs in HTML without tags, the browser will compress the newline into a single space, clumping your text together.

To create separate blocks of text, you **must** wrap them in `<p>` tags.

### Paragraphs (`<p>`)

The `<p>` element defines a paragraph. Browsers automatically add a small amount of space (margin) before and after each one.

### Headings (`<h1>` - `<h6>`)

Headings create a visual and structural hierarchy.

- `<h1>`: The most important (the “Title” of the page). Use only one per page!
- `<h6>`: The least important.

| **Tag** | **Purpose** | **SEO/Accessibility Impact** |
| --- | --- | --- |
| `<h1>` | Main Page Heading | High (defines the topic) |
| `<h2>` - `<h3>` | Section Sub-Headings | Medium (organizes content) |
| `<h4>` - `<h6>` | Minor Sub-Sections | Low (fine-grained detail) |

---

## Adding Meaning (Semantics)

Don’t just use tags for looks-use them for **meaning**. This helps screen readers and search engines understand your content.

- `<strong>`: Makes text **bold** and marks it as “important.”
- `<em>`: Makes text *italic* and adds “emphasis.”

```html
<p>This is <strong>very importang</strong> and this is <em>emphasized</em>.</p>
```

---

## Nesting & Code Organization

### The “Family Tree” Analogy

When you put one element inside another, you create a **Parent/Child** relationship.

- **Parent:** The outer element.
- **Child:** The inner element.
- **Siblings:** Elements at the same level (under the same parent).

### Indentation

Always indent your child elements. It doesn’t change how the website looks to the user, but it makes the code readable for you and your team.

```html
<body>
	<header>
		<h1>Welcome</h1>
		<p>Hello world</p>
	</header>
</body>
```

---

## HTML Comments

Comments are for humans, not browsers. Use them to leave notes or “turn off” code temporarily.

- **Syntax:** `<!--` and `-->`.
- **Shortcut:** `Ctrl + /`.