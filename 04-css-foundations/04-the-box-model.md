# The Box Model

## The Four Layers

Every element consists of four parts, layered from the inside out. When debugging in **DevTools**, look for these specific colors:

- **Content (Blue):** Where your text or images live. Size with `width` and `height`.
- **Padding (Green):** Transparent space **inside** the border. It pushes content away from the edge.
- **Border (Yellow):** The line wrapped around the padding and content.
- **Margin (Orange):** Invisible space **outside** the border. It pushes other elements away.

---

## Block vs. Inline Boxes

The `display` property determines how a box sits in the “flow” of the page.

| **Feature** | **Block (`h1`, `p`, `div`)** | **Inline (`a`, `span`, `strong`)** |
| --- | --- | --- |
| **New Line** | Always breaks to a new line. | Stays on the same line. |
| **Sizing** | Respected `width` and `height`. | Ignored. Sized by content only. |
| **Spacing** | Pushes all neighbors away. | Top/Bottom are ignored (causes overlap). |
| **Default** | Fills 100% width of container. | Only takes up necessary space. |

`display: inline-block` allows an element to stay on the same line while still respecting `width`, `height`, and vertical padding/margins.

---

## Sizing Models: The “Math” Problem

By default, CSS adds padding and borders **on top** of your width, which can break layouts.

### Standard Model (`content-box`)

If you set `width: 300px` + `20px` padding + `5px` border, the box is actually **350px** wide.

**Formula:** Total Visible Width = `width` + `left padding` + `right padding` + `left border` + `right border`

### Alternative Model (`border-box`)

The width you set is the **final** width. Padding and borders grow **inward**, shrinking the content area instead of expanding the box.

```css
html {
	box-sizing: border-box;
}

*, *::before, *::after {
	box-sizing: border-box;
}
```

---

## Deep Dive: Margins

Margins create space around elements. They can be positive (pushing away) or negative (pulling closer).

### Shorthand Syntax

The `margin` property can take 1 to 4 values:

- `10px` (All sides)
- `10px 20px` (Top/Bottom, Left/Right)
- `10px 5px 15px` (Top, Left/Right, Bottom)
- `10px 5px 15px 20px` (Top, Right, Bottom, Left)

### Horizontal Centering with `auto`

To center a block element within its parent, you must provide a **width** and set side margins to **auto**:

```css
.centered-box {
	width: 50%;
	margin: 0 auto;
}
```

### Vertical Margin Collapsing

When two vertical margins touch, they don’t add up; they **collapse** into a single gap equal to the **largest** individual margin.

- **Example:** If `h2` has `margin-bottom: 20px` and the following `p` has `margin-top: 10px`, the gap is **20px**, not 30px.
- **Why?** This prevents double-spacing between paragraphs and keeps headings consistently spaced.

---

## Inner vs. Outer Display

Elements have two “faces” that define their behavior:

1. **Outer Display:** (`block`, `inline`) How the box sits next to its neighbors.
2. **Inner Display:** (`flex`, `grid`) How the box organizes the children **inside** of it.
    - Example: `display: flex;` keeps the box behaving like a **block** on the outside but turns the interior into a Flexbox layout.