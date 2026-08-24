# Growing and Shrinking

## The `flex` Shorthand

Instead of writing three separate lines, we use the `flex` shorthand. It combines **Grow**, **Shrink**, and **Basis**.

**The “Magic” Number:** `flex: 1` is shorthand for `1 1 0`. It tells an item: “Grow to fill space, shrink if you must, and start from a baseline of zero.”

---

## The Three Components

### `flex-grow` (The Growth Factor)

This is a ratio that tells the item how much of the **remaining free space** it should take.

- **`flex-grow: 1` (on all items):** They all grow equally to fill the row.
- **`flex-grow: 2` (on one item):** That item grabs twice as much of the extra space as its siblings.

### `flex-shrink` (The Safety Valve)

This kicks in only when the items are **too big** for their container.

- **`flex-shrink: 1` (Default):** All items shrink at the same rate to prevent overflow.
- **`flex-shrink: 0`:** The “Don’t touch me” setting. Use this for icons or sidebars that **must** stay a fixed size.

### `flex-basis` (The Starting Line)

The “ideal” size of an item before growing or shrinking starts.

- `flex-basis: auto`: Looks at the item’s `width` or content size.
- `flex-basis: 0`: Ignores content size; the item starts with no initial width, letting `flex-grow` do the work.

---

## Practical Presets

| **Keyword** | **Equivalent** | **Behavior** |
| --- | --- | --- |
| `flex: initial;` | `0 1 auto` | **Default.** Shrinks if needed, but won’t grow to fill space. |
| `flex: auto;` | `1 1 auto` | **Fully Flexible.** Grows and shrinks based on content size. |
| `flex: none;`  | `0 0 auto`  | **Rigid.** Neither grows nor shrinks. Great for fixed sidebars. |
| `flex: <number>;`  | `<num> 1 0`  | **Proportional.** Sizes items strictly by the growth ratio. |

---

## Syntax Cheat Sheet

The browser interprets the `flex` shorthand based on how many values you provide:

- **1 Value:**
    - A number (e.g., `flex: 2`) → `flex-grow`. (Defaults to `2 1 0%`).
    - A width (e.g., `flex: 100px`) → `flex-basis`. (Defaults to `1 1 100px`)
- **2 Values:**
    - First is `flex-grow`, second is `flex-shrink` OR `flex-basis`.
- **3 Values:**
    - Must be in order: `[grow] [shrink] [basis]`.

---

## Workflow Pro-Tips

- **Width is a Suggestion:** When you use `flex-grow`, the browser may ignore your `width: 200px` setting to satisfy the flex rules.
- **The “Zero” Secret:** Using `flex-basis: 0` is the best way to ensure items are **exactly** the same size, even if one has more text than the other.
- **Minimum Content Size:** By default, flex items won’t shrink below their `min-content`. Use `min-width: 0` to allow them to shrink smaller.