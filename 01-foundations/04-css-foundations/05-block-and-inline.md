# Block and Inline

## Normal Layout Flow

**Normal Flow** is the default system browsers use to place elements in the viewport. Starting with a solid structure here ensures your site remains accessible to screen readers and works even in limited browsers.

### The Default Rules:

- **The Box Model:** Every element is a box. Padding, borders, and margins are added to the content size.
- **Direction:** By default, elements flow based on the parent’s writing mode (usually horizontal, top-to-bottom)
- **Accessibility:** Normal flow is designed for readability; working with it is easier than struggling against it.

---

## Display Types: Block vs. Inline vs. Inline-Block

The `display` property is the primary way we categorize how boxes behave in the flow of a page.

| **Feature** | **Block (`div`, `p`, `h1`)** | **Inline (`span`, `a`, `strong`)** | **Inline-Block** |
| --- | --- | --- | --- |
| **New Line** | Starts on a new line. | Stays on the same line. | Stays on the same line. |
| **Width** | Stretches to fill parent. | Only as wide as content. | Only as wide as content. |
| **Height/Width** | Fully respected. | **Ignored** (except `<img>`). | **Fully respected**. |
| **Spacing** | Pushes others away. | **Ignored** (causes overlap). | **Pushes others away**. |
| **Contains** | Block or inline. | **Inline only**. | Block or inline. |

### The “Hybrid” Advantage: `inline-block`

`display: inline-block` provides a middle ground. It is the modern successor to “floats” for creating side-by-side boxes because:

- It allows for specific `width` and `height`.
- It respects top/bottom `padding` and `margin`.
- It wraps naturally to a new line if space runs out, without needing to “clear” floats.

---

## Generic Containers: Divs and Spans

When semantic elements (like `<nav>` or `<article>`) don’t fit, we use “meaningless” containers as **hooks** for CSS or for grouping elements.

### `<div>` (Block)

- **Purpose:** A generic container for sections of a document.
- **Usage:** Groups related elements to apply layout or styling to a whole block.

### `<span>` (Inline)

- **Purpose:** An inline container for marking up a specific part of a text.
- **Usage:** Styles a word or phrase inside a paragraph without breaking the line.

---

## The “Gotcha”: Margin Collapsing

In normal flow, vertical margins that touch each other **collapse** into a single margin. The smaller margin disappears, and the larger one remains.

- **The Math:** If a `h2` has `margin-bottom: 20px` and the `p` below has `margin-top: 10px`, the gap is **20px**, not 30px.
- **The Scope:** This **only** happens vertically. Horizontal margins never collapse.

---

## Overriding Normal Flow

Once you master the defaults, you can use these methods to bend the rules:

1. **Display Property:** Switch to `flex` or `grid` for advanced internal layouts.
2. **Positioning:** Use `relative`, `absolute`, or `fixed` to pluck elements out of the flow.
3. **Floats:** Use `float: left/right` to wrap text around images (classic magazine style).
4. **Responsive Design:** Use `@media` queries to change layouts based on screen size.

Always ensure your HTML looks good in **Normal Flow** before adding complex CSS. It makes your site more robust and easier to maintain.