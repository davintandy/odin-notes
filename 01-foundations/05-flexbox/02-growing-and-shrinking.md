# Growing and Shrinking

## Understand the `flex` Property

The CSS `flex` property controls how a flex item grows or shrinks to fit the available space inside its flex container.

It is a shorthand for three properties:

- `flex-grow`
- `flex-shrink`
- `flex-basis`

### Syntax

```css
.item {
	flex: <flex-grow> <flex-shrink> <flex-basis>;
}
```

Example:

```css
.item {
	flex: 1 1 200px;
}
```

This means:

- `flex-grow: 1` - allows the item to grow.
- `flex-shrink: 1` - allows the item to shrink.
- `flex-basis: 200px` - establishes an initial main size of 200 pixels.

Understanding these three properties separately makes the `flex` shorthand much easier to use.

## `flex-grow`

The `flex-grow` property determines how flex items share **positive free space** in their container.

```css
.item {
	flex-grow: 1;
}
```

A value of `1` allows the item to grow when additional space is available.

### Example: Equal Growth

```html
<div class="container">
	<div class="item">Item 1</div>
	<div class="item">Item 2</div>
	<div class="item">Item 3</div>
</div>
```

```css
.container {
	display: flex;
}

.item {
	flex-grow: 1;
}
```

Each item receives an equal share of the distributable positive free space because all three have the same growth factor.

### Example: Different Growth Factors

```css
.item-one {
	flex-grow: 1;
}

.item-two {
	flex-grow: 2;
}

.item-three {
	flex-grow: 1;
}
```

The growth factors are in a `1:2:1` ratio.

If there are 400 pixels of distributable positive free space, the items receive approximately:

| **Item** | **Growth factor** | **Additional space** |
| --- | --- | --- |
| Item 1 | 1 | 100px |
| Item 2 | 2 | 200px |
| Item 3 | 1 | 100px |

These amounts represent the additional free space distributed, not necessarily the final widths of the items. Their initial sizes and minimum-size constraints also affect their final dimensions.

### Important Notes

- `flex-grow: 0` prevents an item from growing to absorb positive free space.
- `flex-grow: 1` allows the item to participate in growth.
- Larger growth factors receive a proportionally larger share of the available positive free space.
- Growing occurs along the container’s main axis.

## `flex-shrink`

The `flex-shrink` property determines how flex items respond when their combined sizes exceed the available space in their container.

```css
.item {
	flex-shrink: 1;
}
```

The default `flex-shrink` value is `1`, meaning items can shrink when necessary.

### Example: Shrinking to Fit

```css
.container {
	display: flex;
	width: 300px;
}

.item {
	width: 150px;
	flex-shrink: 1;
}
```

With two items, their declared widths total 300 pixels. If borders, padding, margins, or additional items make the total required space exceed the available width, the items may shrink to accommodate the layout.

### Preventing an Item from Shrinking

```css
.item {
	flex-shrink: 0;
}
```

This prevents the item from participating in flex shrinking.

For example:

```css
.container {
	display: flex;
	width: 500px;
}

.item {
	width: 250px;
	flex-shrink: 1;
}

.item-fixed {
	width: 250px;
	flex-shrink: 0;
}
```

If the container becomes too small for both items `.item` can shrink while `.item-fixed` resists shrinking.

**Important**: Preventing an item from shrinking does not guarantee that everything will fit. The layout may overflow when insufficient space remains.

### Important Notes

- `flex-shrink: 1` allows shrinking.
- `flex-shrink: 0` prevents flex shrinking for that item.
- A larger shrink factor generally means a larger share of the negative free space is assigned to the item.
- Shrinking depends on the flex base sizes as well as the shrink factors; it is not simply a matter of subtracting equal pixel amounts.
- Minimum-size constraints can stop an item from shrinking as much as expected.

## `flex-basis`

The `flex-basis` property defines a flex item’s initial main size before the remaining free space is distributed through growing or shrinking.

```css
.item {
	flex-basis: 200px;
}
```

The main size depends on the container’s `flex-direction`:

- `row` - the main size is horizontal, so `flex-basis` corresponds to the initial width.
- `column` - the main size is vertical, so `flex-basis` corresponds to the initial height.

### Common Values

| **Value** | **Meaning** |
| --- | --- |
| `0` or `0%` | Starts from a zero flex basis, before growth and subject to minimum-size constraints |
| `200px` | Uses a 200-pixel initial main size |
| `50%` | Uses a percentage of the flex container’s inner main size when resolvable |
| `auto` | Looks to the item’s main-size property, such as `width` in a row layout |
| `content` | Bases the size on the item’s content |

### Example: Fixed Basis

```css
.item {
	flex-basis: 200px;
	flex-grow: 0;
	flex-shrink: 1;
}
```

The item starts with a 200-pixel main-size. It does not grow to consume extra space, but it can shrink if the container becomes too small.

### `flex-basis: 0` vs. `flex-basis: auto`

These values behave differently.

**With `flex-basis: 0`**:

```css
.item {
	width: 250px;
	flex: 1;
}
```

The shorthand `flex: 1` uses a zero-percentage flex basis in common browser implementations. The item’s declared width does not establish its flex base size in the same way it would with `flex-basis: auto`.

**With `flex-basis: auto`:**

```css
.item {
	width: 250px;
	flex: 1 1 auto;
}
```

The browser uses the declared width as the starting main size in this row layout, then distributes space through growing or shrinking.

**Key takeaway**: `flex-basis` determines the starting point for Flexbox sizing: `flex-grow` and `flex-shrink` determine how that size responds to available space.

## Combining the Three Properties

The `flex` shorthand makes it easier to configure an item’s sizing behavior in a single declaration.

```css
.item {
	flex: 1 1 200px;
}
```

The values are always interpreted in this order when all three are specified:

```
flex-grow | flex-shrink | flex-basis
```

### Common Shorthand Values

| **Declaration** | **Equivalent values** | **Behavior** |
| --- | --- | --- |
| `flex: 1` | `1 1 0%` in common implementations | Grow and shrink, starting from a zero-percentage basis |
| `flex: 2` | `2 1 0%` | Same basic behavior as `flex: 1`, but with a growth factor of 2 |
| `flex: auto` | `1 1 auto` | Grow and shrink, using the main-size property as the basis |
| `flex: initial` | `0 1 auto` | Do not grow, but allow shrinking from the automatic basis |
| `flex: none` | `0 0 auto` | Neither grow nor shrink; use the automatic basis |

The initial values of the individual longhand properties are `flex-grow: 0`, `flex-shrink: 1`, and `flex-basis: auto`. The shorthand `flex: 1` is not equivalent to setting only `flex-grow: 1`.

### `flex: 1`

```css
.item {
	flex: 1;
}
```

Use this when you want flexible items to share the available space, often equally when they all use the same value and have compatible minimum sizes.

### `flex: auto`

```css
.item {
	flex: auto;
}
```

Use this when items should be flexible while taking their existing main sizes into account.

### `flex: none`

```css
.item {
	flex: none;
}
```

Use this when an item should retain its preferred main size rather than growing or shrinking to fit.

Be aware that a fixed or inflexible item can cause overflow when the container is too small.

## Practical Example: Creating Unequal Columns

Consider a layout where the center column should occupy twice the distributable space of the other columns.

### HTML

```html
<div class="container">
	<div class="sidebar">Sidebar</div>
	<div class="main-content">Main Content</div>
	<div class="aside">Aside</div>
</div>
```

### CSS

```css
.container {
	display: flex;
	gap: 16px;
}

.sidebar {
	flex: 1;
	background-color: lightblue;
}

.main-content {
	flex: 2;
	background-color: lightgreen;
}

.aside {
	flex: 1;
	background-color: lightpink;
}
```

The flex factors establish a `1:2:1` distribution of the available free space. The main content receives twice the growth allocation of either side column.

Because each item uses `flex: 1` or `flex: 2`, they also start from a zero-percentage flex basis. Their final widths remain subject to minimum-size constraints, the container’s dimensions, and the space used by `gap`.

## Troubleshooting Flex Items That Refuse to Shrink

Sometimes an item remains wider than expected, even after you set `flex-shrink: 1`.

One reason is the automatic minimum size of a flex item. Its content may establish a minimum width that prevents further shrinking.

For example, a long unbreakable word or a wide image may force an item to remain wider than the available space.

A common solution for a row-layout item is:

```css
.container {
	display: flex;
}

.main-content {
	min-width: 0;
}
```

This allows the item’s minimum width to reach zero instead of being constrained by its automatic minimum size.

The content may still need additional handling - for example, text wrapping or responsive image sizing - to avoid overflowing the smaller item.

Before changing flex factors repeatedly, inspect the item’s `flex-basis`, `min-width`, content, and container dimensions.