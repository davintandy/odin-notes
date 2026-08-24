# Alignment

## Fundamentals: The Two Axes

Unlike traditional layouts (Block or Inline), Flexbox relies on two perpendicular axes. Their orientation depends on your `flex-direction`.

- **Main Axis:** The primary direction items are laid out.
- **Cross Axis:** The axis perpendicular to the main axis.
- **Start/End:** Flexbox uses “Start” and “End” instead of Left/Right to remain compatible with different writing modes (like RTL).

---

## Parent Properties (The Flex Container)

These properties are applied to the element with `display: flex;`.

### Direction & Flow

- `flex-direction`: Defines the main axis (`row`, `row-reverse`, `column`, `column-reverse`).
- `flex-wrap`: Controls if items should wrap to multiple lines (`nowrap`, `wrap`, `wrap-reverse`).
- `flex-flow`: A shorthand for direction and wrap. Default: `row nowrap`.

### Alignment & Distribution

| **Property** | **Axis** | **Description** |
| --- | --- | --- |
| `justify-content` | **Main** | Distributes the **group** of items (e.g., `center`, `space-between`, `space-evenly`). |
| `align-items` | **Cross** | Aligns items **on the current line** (e.g., `stretch`, `center`, `baseline`). |
| `align-content` | **Cross** | Aligns **rows/lines** (only works if `flex-wrap` is enabled). |
| `gap` | **Both** | Sets the gutter space between items without affecting edges. |

---

## Child Properties (The Flex Items)

These properties are applied to the direct children of a flex container.

### The `flex` shorthand

It is recommended to use the shorthand rather than individual properties

- `flex-grow`: Ability to grow if there is extra space (ratio). Default: `0`.
- `flex-shrink`: Ability to shrink if the container is too small. Default: `1`. Set `flex-shrink: 0` to keep icons or sidebars from squishing.
- `flex-basis`: The initial “Hypothetical Size” before growth/shrinkage occurs.

### Individual Overrides

- `align-self`: Allows a single item to override the container’s `align-items` setting.
- `order`: Changes the visual order of items without changing the underlying HTML/DOM structure.

---

## Key Logic & “Gotchas”

### Hypothetical vs. Minimum Size

- **Hypothetical Size:** The size an element wants to be (based on `width` or `flex-basis`).
- **The Minimum Size Trap:** Flexbox won’t shrink an item below its content’s minimum size (e.g., a long word). To force a shrink, set `min-width: 0`.

### Auto Margins

In Flexbox, `margin: auto` is incredibly powerful. An auto margin will “swallow” all available free space in its direction.

**Example:** Setting `margin-left: auto` on the last item of a navbar will push it all the way to the right side of the container.

### Accessibility Warning

Using `order` or `-reverse` directions creates a disconnect between the **visual order** and the **DOM/Screen Reader order**. Ensure the logical flow of information remains intact for assistive technology.