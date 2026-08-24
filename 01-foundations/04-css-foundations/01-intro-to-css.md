# Intro to CSS

## Basic syntax

A CSS **Rule** consists of a **Selector** (who is being styled) and a **Declaration Block** (what the style is).

```css
selector {
	property: value;
}
```

---

## Adding CSS to HTML

There are three ways to link your styles. **External** is the gold standard for real projects.

| **Method** | **Where it lives** | **Best for…** |
| --- | --- | --- |
| **External** | A separate `.css` file linked in `<head>`. | **Whole websites**. Cleanest and most reusable. |
| **Internal** | Inside `<style>` tags in the `<head>`. | Single-page unique styles. |
| **Inline** | Directly in the HTML tag via `style` attribute. | Quick fixes (Generally avoided). |

**External Link Example:**

```html
<link rel="stylesheet" href="style.css">
```

---

## Selectors: Choosing Your Target

Selectors tell the browser exactly which HTML elements to paint.

### Basic Selectors

- **Universal (`*`):** Targets every single element on the page.
- **Type:** Targets elements by tag name (e.g., `h1`, `div`, `p`).
- **Class (`.className`):** Targets elements with a specific class attribute. Can be used many times.
- **ID (`#idName`):** Targets a unique element. **Can only be used once per page.**

### Advanced Selection

- **Grouping (`.one, .two`):** Applies the same styles to multiple selectors at once (separated by a **comma**).
- **Chaining (`.class1.class2`):** Targets an element that has **both** classes (no space).
- **Descendant Combinator (`.parent .child`):** Targets a child element only if it is inside a specific parent (separated by a **space**).

---

## Key Properties to Master

### Colors

Colors can be defined by name (`red`), **HEX** (`#ff0000`), **RGB** (`rgb(255, 0, 0)`), or **HSL**.

Use an “Alpha” value (RGBA/HSLA) to adjust transparency.

### Typography

- `font-family`: Always provide a “fallback” list. If the browser doesn’t have your first choice, it moves to the next.
    
    Example: `font-family: "Times New Roman", Arial, sans-serif;`
    
- `font-size`: Usually set in pixels (`px`).
- `font-weight`: Boldness (numbers 100-900 or keywords like `bold`).
- `text-align`: Horizontal alignment (`left`, `center`, `right`).

### Image Sizing

To prevent “layout shift” (where the page jumps as images load), always define width and height in HTML.

**Maintain Proportions:** Set `width` to a specific size and `height: auto`.

```css
img {
	width: 300px;
	height: auto;
}
```

---

## The `<div>` vs. Semantic Tags

The `<div>` is a generic container. While useful for grouping things for CSS, always try to use **Semantic HTML** (like `<header>`, `<main>`, or `<footer>`) first. It’s better for SEO and accessibility!