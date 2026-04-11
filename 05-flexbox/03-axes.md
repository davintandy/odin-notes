# Axes

## The Two Axes

Flexbox is a “one-dimensional” layout tool. You work along one axis at a time.

### The Main Axis

This is the **primary direction** in which your items are laid out.

- Controlled by `flex-direction`.

### The Cross Axis

The axis **perpendicular** to the main axis.

- If your main axis is horizontal, the cross axis is vertical (and vice versa).

---

## Flex Direction Values

The `flex-direction` property defines the direction of the main axis and the flow of content.

| **Property Value** | **Main Axis Direction** | **Visual Flow** |
| --- | --- | --- |
| `row` (Default) | Horizontal | Left → Right (in LTR) |
| `row-reverse` | Horizontal | Right → Left (in LTR) |
| `column` | Vertical | Top → Bottom |
| `column-reverse` | Vertical | Bottom → Top |

---

## The `column` + `flex: 1` Trap

A common point of confusion is using the shorthand `flex: 1` inside a `column` container.

- **The Problem:** `flex: 1` expands to `flex-grow: 1`, `flex-shrink: 1`, and `flex-basis: 0`.
- **The Result:** Because `flex-basis` is `0`, items start with **zero height**. If the parent container doesn’t have a defined height (like `height: 500px`), there is no “free space” to grow into, and items may stay collapsed.

**The Fixes:**

1. **Define Container Height:** Give the parent a height so the items have space to fill.
2. **Use `auto` Basis:** Use `flex: 1 1 auto` to respect natural content height before growing.
3. **Use Grow Only:** Use `flex-grow: 1` to keep the default `flex-basis: auto`.

---

## Writing Modes & RTL

Flexbox is **direction-agnostic**. The spec avoids “left” and “right” in favor of **flex-start** and **flex-end**.

- **Right-to-Left (RTL):** In languages like Arabic, `flex-start` is on the **right**.
- **Vertical Writing:** In some layouts, the main axis for a `row` might flow top-to-bottom.
- **Key Takeaway:** Always think in **Start** and **End.** It makes your layouts compatible across all languages.

---

## Accessibility Warning

Be careful with `row-reverse` and `column-reverse`.

Reversing the direction creates a disconnect between the **visual order** and the **DOM order**. Screen readers follow the DOM order, so a user might hear “Contact, About, Home” while seeing “Home, About, Contact.” Only use reverse values if the visual sequence does not change the meaning of the content.