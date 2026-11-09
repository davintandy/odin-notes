# Axes

## Understanding the Axes in Flexbox

Flexbox uses two axes to determine how items are arranged inside a flex container:

- **Main axis**: The primary direction in which flex items are laid out.
- **Cross axis**: The direction perpendicular to the main axis.

The direction of these axes is controlled by the `flex-direction` property.

### Why Are Axes Important?

Understanding the axes helps you determine:

- Whether items are arranged horizontally or vertically.
- How `flex-grow`, `flex-shrink`, and `flex-basis` affect item sizing.
- How alignment properties such as `justify-content` and `align-items` behave.

The main axis is not always horizontal. Its direction depends on `flex-direction`.

## The Main Axis and Cross Axis

### `flex-direction: row`

The default value of `flex-direction` is `row`.

```css
.container {
	display: flex;
	flex-direction: row;
}
```

In a typical left-to-right writing environment:

- The **main axis** runs horizontally, from left to right.
- The **cross axis** runs vertically, from top to bottom.

```
Cross axis
    ↓
┌─────────────────────────────┐
│  Item 1   Item 2   Item 3   │ → Main axis
└─────────────────────────────┘
```

### `flex-direction: column`

The `column` value arranges flex items vertically.

```css
.container {
	display: flex;
	flex-direction: column;
}
```

In a typical horizontal writing environment:

- The **main axis** runs vertically, from top to bottom.
- The **cross axis** runs horizontally.

```
       Main axis
           ↓
    ┌─────────────┐
    │   Item 1    │
    ├─────────────┤
    │   Item 2    │
    ├─────────────┤
    │   Item 3    │
    └─────────────┘
           →
       Cross axis
```

### Comparison

| **Property** | **Main axis** | **Cross axis** |
| --- | --- | --- |
| `flex-direction: row` | Horizontal in typical writing modes | Vertical |
| `flex-direction: column` | Vertical in typical writing modes | Horizontal |

**Important**: These horizontal and vertical descriptions assume a typical horizontal writing mode. In languages and layouts using different writing modes or text directions, the axes can correspond to different physical directions.

## The Four Values of `flex-direction`

The `flex-direction` property accepts four main values.

| **Value** | **Behavior** |
| --- | --- |
| `row` | Arranges items along the main axis in the inline direction; the default |
| `row-reverse` | Arranges items in the opposite inline direction |
| `column` | Arranges items along the block axis |
| `column-reverse` | Arranges items in the opposite block direction |

### Example

```css
.container {
	display: flex;
	flex-direction: row;
}
```

To arrange the items vertically:

```css
.container {
	display: flex;
	flex-directoin: column;
}
```

To reverse the visual direction of the items:

```css
.container {
	display: flex;
	flex-direction: row-reverse;
}
```

Or:

```css
.container {
	display: flex;
	flex-direction: column-reverse;
}
```

### Understanding Reverse Directions

Consider the following HTML:

```html
<div class="container">
	<div>Item 1</div>
	<div>Item 2</div>
	<div>Item 3</div>
</div>
```

With `flex-direction: row`, the visual order in a typical left-to-right environment is:

```
Item 1 → Item 2 → Item 3
```

With `flex-direction: row-reverse`, the visual order becomes:

```
Item 3 → Item 2 → Item 1
```

Similarly, `column-reverse` reverses the visual direction of a vertical layout.

**Accessibility note**: Reversing items with CSS changes their visual presentation, not their underlying DOM order. Screen readers and keyboard navigation may still follow the original document order, so use reverse directions carefully when the sequence of content matters.

## How the Axes Affect `flex-basis`

The `flex-basis` property specifies a flex item’s initial main size before free space is distributed through growing or shrinking.

Because the main axis changes with `flex-direction`, the dimension controlled by `flex-basis` changes as well.

### With `flex-direction: row`

```css
.container {
	display: flex;
	flex-direction: row;
}

.item {
	flex-basis: 200px;
}
```

In a typical horizontal writing mode, `flex-basis: 200px` establishes an initial main size of 200 pixels horizontally.

It behaves like a starting width, subject to Flexbox sizing rules.

### With `flex-direction: column`

```css
.container {
	display: flex;
	flex-direction: column;
}

.item {
	flex-basis: 200px;
}
```

Now the initial main size is 200 pixels vertically. In a typical horizontal writing mode, this corresponds to the item’s starting height.

### Comparison

| **`flex-direction`** | **Main dimension** | **Meaning of `flex-basis: 200px`** |
| --- | --- | --- |
| `row` | Width | Initial main size of 200px horizontally |
| `column` | Height | Initial main size of 200px vertically |

**Key takeaway**: `flex-basis` follows the main axis, not a permanently fixed width or height.

## Why `flex: 1` Can Behave Unexpectedly in a Column

The shorthand:

```css
.item {
	flex: 1;
}
```

Commonly expands to:

```css
.item {
	flex-grow: 1;
	flex-shrink: 1;
	flex-basis: 0%;
}
```

This means the item starts with a zero-percentage flex basis and can grow or shrink.

### Example

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
	flex-direction: column;
}

.item {
	flex: 1;
	height: 100px;
}
```

You might expect each item to be 100 pixels tall, but the declared height may not determine the starting main size because `flex-basis: 0%` takes precedence over the main-size property when calculating the flex basis.

If the container also has no definite height, its height can be determined by its contents. Since the flex items start from a zero basis and there is no definite extra vertical space to distribute, they may collapse instead of growing to the expected heights.

### Solution 1: Use `flex-basis: auto`

```css
.container {
	display: flex;
	flex-direction: column;
}

.item {
	flex: 1 1 auto;
	height: 100px;
}
```

Here, `flex-basis: auto` uses the specified height as the starting main size. Each item can still grow or shrink according to available space.

### Solution 2: Give the Container a Height

```css
.container {
	display: flex;
	flex-direction: column;
	height: 500px;
}

.item {
	flex: 1;
}
```

With a definite container height, Flexbox has a vertical size against which it can calculate and distribute free space. The items can grow to share that space, subject to their minimum-size constraints.

### Solution 3: Use `flex-grow` Instead

```css
.container {
	display: flex;
	flex-direction: column;
}

.item {
	height: 100px;
	flex-grow: 1;
}
```

This keeps the `auto` basis behavior while allowing items to grow when positive free space is available.

The appropriate solution depends on whether you want the items to retain their preferred heights or fill a container with a defined height.

## Relationship Between Axes Alignment

The main and cross axes also determine how Flexbox alignment properties behave.

- `justify-cnotent` distributes or positions items along the **main axis**.
- `align-items` aligns items along the **cross axis**.

For example

```css
.container {
	display: flex;
	flex-direction: row;
	justify-content: center;
	align-items: center;
}
```

With the default `row` direction in a typical horizontal writing mode:

- `justify-content: center` centers items horizontally.
- `align-items: center` centers items vertically.

If you change the direction to `column`:

```css
.container {
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
}
```

The axes change, so the same alignment properties now work in the opposite physical directions:

- `justify-content: center` centers items vertically.
- `align-items: center` centers items horizontally.

This is why understanding axes before learning alignment is so useful.