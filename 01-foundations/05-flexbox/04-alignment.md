# Alignment

## Understanding Flexbox Alignment

Flexbox provides several CSS properties for positioning and distributing items inside a flex container.

The two most important properties are:

- **`justify-content`** - Controls how items are positioned and distributed along the main axis.
- **`align-items`** - Controls how items are aligned along the cross axis.

Other useful properties include:

- `align-self` - Overrides the cross-axis alignment of an individual flex item.
- `align-content` - Controls the distribution of multiple flex lines along the cross axis.
- `gap` - Creates consistent spacing between flex items.

Before using these properties, remember that their behavior depends on the container’s `flex-direction`.

## The Main Axis and Cross Axis

Flexbox uses two axes to determine the direction of alignment.

| **Property** | **Main axis** | **Cross axis** |
| --- | --- | --- |
| `flex-direction: row` | Horizontal | Vertical |
| `flex-direction: column` | Vertical | Horizontal |

The main axis follows the `flex-direction`, while the cross axis runs perpendicular to it.

### Example: Row Direction

```css
.container {
	display: flex;
	flex-direction: row;
}
```

In a typical left-to-right writing environment:

- Main axis: Left to right.
- Cross axis: Top to bottom

### Example: Column Direction

```css
.container {
	display: flex;
	flex-direction: column;
}
```

- Main axis: Top to bottom.
- Cross axis: Left to right.

**Important**: `justify-content` always works along the main axis, while `align-items` always works along the cross axis. They do not permanently represent horizontal and vertical alignment.

## `justify-content`

The `justify-content` property controls how flex items are positioned and how remaining free space is distributed along the main axis.

It is applied to the **flex container**.

```css
.container {
	display: flex;
	justify-content: center;
}
```

### Common Values

| **Value** | **Behavior** |
| --- | --- |
| `flex-start` | Packs items at the start of the main axis |
| `flex-end` | Packs items at the end of the main axis |
| `center` | Groups items at the center of the main axis |
| `space-between` | Distributes items evenly, with the first and last items at the edges |
| `space-around` | Gives each item equal space around it |
| `space-evenly` | Distributes equal spacing between items and the container edges |

### Visual Comparison

Assume the container has available free space and the items do not grow to consume it.

**`flex-start`**

```
┌──────────────────────────────┐
│ [1] [2] [3]                  │
└──────────────────────────────┘
```

Items are grouped at the start.

**`flex-end`**

```
┌──────────────────────────────┐
│                  [1] [2] [3] │
└──────────────────────────────┘
```

Items are grouped at the end.

**`center`**

```
┌──────────────────────────────┐
│          [1] [2] [3]         │
└──────────────────────────────┘
```

Items are grouped in the center.

**`space-between`**

```
┌──────────────────────────────┐
│ [1]        [2]           [3] │
└──────────────────────────────┘
```

The first item touches the start, the last item touches the end, and the remaining space is distributed between them.

**`space-around`**

```
┌──────────────────────────────┐
│   [1]       [2]        [3]   │
└──────────────────────────────┘
```

Each item receives equal space on both sides. The visible space between items is twice the space at either outer edge.

**`space-evenly`**

```
┌──────────────────────────────┐
│    [1]      [2]       [3]    │
└──────────────────────────────┘
```

The space between every item and the space at both edges are equal.

### Important Notes

- `justify-content` distributes remaining free space; it does not automatically make items grow.
- If items already occupy all available space, there may be no extra space to distribute.
- `flex-start` and `flex-end` follow the flex direction.
- Changing `flex-direction` changes the physical direction in which these values operate.

## `align-items`

The `align-items` property controls how all flex items are aligned along the cross axis.

It is applied to the **flex container**.

```css
.container {
	display: flex;
	align-items: center;
}
```

### Common Values

| **Value** | **Behavior** |
| --- | --- |
| `stretch` | Stretches items to fill the available cross-axis space |
| `flex-start` | Aligns items at the start of the cross axis |
| `flex-end` | Aligns items at the end of the cross axis |
| `center` | Centers items along the cross axis |
| `baseline` | Aligns items according to their text baselines |

The default value is `stretch`.

### Visual Comparison

Assume the container has a larger cross-axis size than its items need.

**`stretch` (default)**

```
┌──────────────────────────────┐
│ [   1   ] [   2   ] [   3   ]│
│ [       ] [       ] [       ]│
└──────────────────────────────┘
```

Items stretch to fill the available cross-axis space when their cross sizes are automatic and other constraints do not prevent it.

**`flex-start`**

```
┌──────────────────────────────┐
│ [1]     [2]     [3]          │
│                              │
│                              │
└──────────────────────────────┘
```

Items align at the start of the cross axis.

**`flex-end`**

```
┌──────────────────────────────┐
│                              │
│                              │
│ [1]     [2]     [3]          │
└──────────────────────────────┘
```

Items align at the end of the cross axis.

**`center`**

```
┌──────────────────────────────┐
│                              │
│ [1]     [2]     [3]          │
│                              │
└──────────────────────────────┘
```

Items are centered along the cross axis.

### Example: Centering Items Vertically

With the default `row` direction:

```css
.container {
	display: flex;
	align-items: center;
	height: 200px;
}
```

The items are vertically centered inside the container.

For `flex-direction: column`, the same declaration centers items horizontally instead.

### Understanding `baseline`

Baseline alignment is useful when elements contain text with different font sizes.

```css
.container {
	display: flex;
	align-items: baseline;
}
```

Instead of centering the entire boxes, the browser aligns their text baselines.

This is particularly useful when arranging headings, labels, and text with different font sizes.

## `align-self`

The `align-self` property allows you to change the cross-axis alignment of an individual flex item without affecting the other items.

Unlike `align-items`, which is applied to the container, `align-self` is applied directly to a flex item.

### Example

```html
<div class="container">
	<div class="item">Item 1</div>
	<div class="item special">Item 2</div>
	<div class="item">Item 3</div>
</div>
```

```css
.container {
	display: flex;
	align-items: center;
	height: 200px;
}

.special {
	align-self: flex-start;
}
```

The result:

- Item 1 is centered along the cross axis.
- Item 2 is aligned at the start of the cross axis.
- Item 3 is centered along the cross axis.

### Common Values

| **Value** | **Behavior** |
| --- | --- |
| `auto` | Uses the parent’s `align-items` value; this is the default |
| `flex-start` | Aligns the individual item at the cross-axis start |
| `flex-end` | Aligns the individual item at the cross-axis end |
| `center` | Centers the individual item |
| `stretch` | Stretches the individual item when permitted |
| `baseline` | Aligns the item according to the baseline |

**Remember**: `align-items` controls the default alignment for all items, while `align-self` overrides that alignment for a specific item.

## `align-content`

The `align-content` property controls how multiple flex lines are distributed along the cross axis.

It becomes relevant when flex items wrap into multiple rows or columns.

### Why Do We Need `align-content`?

Consider a flex container with several items:

```css
.container {
	display: flex;
	flex-wrap: wrap;
}
```

When the container becomes too narrow, items can move onto additional rows.

Now there are two levels of alignment:

1. Aligning individual items within each flex line.
2. Distributing the flex lines themselves within the container.

The first is handled by `align-items`, while the second is handled by `align-content`.

### Example

```css
.container {
	display: flex;
	flex-wrap: wrap;
	align-content: center;
	height: 400px;
}
```

The multiple flex lines are grouped in the center of the cross axis.

### Common Values

| **Value** | **Behavior** |
| --- | --- |
| `flex-start` | Packs all flex lines at the cross-axis start |
| `flex-end` | Packs all flex lines at the cross-axis end |
| `center` | Groups all flex lines in the center |
| `space-between` | Distributes equal space between flex lines |
| `space-around` | Distributes equal space around each flex line |
| `space-evenly` | Distributes equal space between lines and container edges |
| `stretch` | Stretches flex lines to use the available cross-axis space |

### Important Notes

- `align-content` is relevant when there are multiple flex lines.
- It has no effect on a single-line flex container.
- Use `flex-wrap: wrap` when you want items to create multiple lines.
- The container needs available cross-axis space for alignment and distribution to be noticeable.

### `align-items` vs. `align-content`

This is an important distinction.

| `align-items` | `align-content` |
| --- | --- |
| Aligns individual items within a flex line | Aligns the flex lines as a group |
| Works with single-line and multi-line containers | Requires multiple flex lines to have an effect |
| Controls item alignment on the cross axis | Controls distribution of lines on the cross axis |

## The Difference Between `justify-content` and `align-items`

These properties are often confused because their physical direction changes with `flex-direction`.

### With `flex-direction: row`

```css
.container {
	display: flex;
	flex-direction: row;
	justify-content: center;
	align-items: center;
}
```

- `justify-content` centers items horizontally.
- `align-items` centers items vertically.

### With `flex-direction: column`

```css
.container {
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
}
```

- `justify-content` centers items vertically.
- `align-items` centers items horizontally.

### Quick Reference

| **Flex direction** | **`justify-content`** | **`align-items`** |
| --- | --- | --- |
| `row` | Horizontal alignment | Vertical alignment |
| `column` | Vertical alignment | Horizontal alignment |

The easiest way to remember:

- **Justify = Main axis**
- **Align = Cross axis**

Always identify the main axis before deciding which property to use.

## Using `gap` for Spacing

The `gap` property creates consistent spacing between flex items.

```css
.container {
	display: flex;
	gap: 16px;
}
```

This adds 16 pixels of space between adjacent items.

Unlike margins, `gap` only creates space between items, not between the items and the container’s outer edges.

### Different Gap Values

You can also specify row and column gaps separately.

```css
.container {
	display: flex;
	flex-wrap: wrap;
	row-gap: 20px;
	column-gap: 10px;
}
```

- `row-gap` controls spacing between rows.
- `column-gap` controls spacing between columns.

With `flex-direction: row`, `column-gap` typically separates items horizontally, while `row-gap` separates wrapped lines vertically.

### `gap` vs. `justify-content`

These properties serve different purposes.

| **`gap`** | **`justify-content`** |
| --- | --- |
| Sets a specified distance between items | Distributes available free space along the main axis |
| Does not distribute leftover space | Changes how leftover space is allocated |
| Useful for consistent spacing | Useful for positioning and distributing groups of items |

They can be used together:

```css
.container {
	display: flex;
	justify-content: center;
	gap: 20px;
}
```

The items are grouped in the center with 20 pixels between them.

## Auto Margins in Flexbox

Margins can also be used to position individual flex items by absorbing available free space.

For example, consider a navigation bar with a logo on the left and navigation links on the right.

```html
<nav class="navbar">
	<div class="logo">My Website</div>
	
	<div class="links">
		<a href="#">Home</a>
		<a href="#">About</a>
		<a href="#">Contact</a>
	</div>
</nav>
```

```css
.navbar {
	display: flex;
	align-items: center;
}

.logo {
	margin-right: auto;
}

.links {
	display: flex;
	gap: 16px;
}
```

The `margin-right: auto` on the logo absorbs the available horizontal space, pushing the navigation links toward the right.

This is an alternative to using `justify-content: space-between` when you want to control spacing around a particular item.

### When to Use Auto Margins

- Push one item to the opposite side of a container.
- Separate groups of items.
- Create navigation layouts.
- Absorb remaining free space before alignment properties distribute it.

## Practical Flexbox Alignment Examples

### Example 1: Center an Element Both Horizontally and Vertically

```css
.container {
	display: flex;
	justify-content: center;
	align-items: center;
	min-height: 400px;
}
```

This centers the child along both axes, assuming the container has sufficient available space.

### Example 2: Navigation Bar

```css
.navbar {
	display: flex;
	justify-content: space-between;
	align-items: center;
	padding: 16px;
}
```

This places the main navigation groups at opposite ends and aligns them along the cross axis.

### Example 3: Card Layout

```css
.cards {
	display: flex;
	justify-content: center;
	align-items: stretch;
	gap: 20px;
}

.card {
	flex: 1;
	max-width: 300px;
}
```

This creates a row of cards with consistent spacing and flexible widths.

### Example 4: Wrapping Cards

```css
.cards {
	display: flex;
	flex-wrap: wrap;
	justify-content: center;
	align-items: stretch;
	gap: 20px;
}
```

The cards can wrap onto additional rows when there is insufficient horizontal space.

## Common Mistakes

| **Mistake** | **Explanation** | **Solution** |
| --- | --- | --- |
| Using `align-items` when you want horizontal alignment | With the default `row`, it works vertically | Use `justify-content` |
| Using `justify-content` when you want vertical alignment | With the default `row`, it works horizontally | Use `align-items` |
| Expecting `align-content` to work with one row | It distributes multiple flex lines | Use `align-items` for individual items |
| Expecting `gap` to create space around the container edges | Gap only separates adjacent items | Use padding on the container if outer spacing is needed |
| Using `flex: 1` when you only want alignment | Items may grow and consume the available space | Remove `flex: 1` when fixed-sized items are desired |
| Using margins for every item to create spacing | Can make spacing inconsistent | Consider using `gap` |