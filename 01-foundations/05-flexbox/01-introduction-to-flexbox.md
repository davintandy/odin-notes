# Introduction to Flexbox

## What Is Flexbox?

**Flexbox (Flexible Box Layout)** is a CSS layout model designed to arrange elements in rows or columns and distribute space between them.

Unlike normal document flow, where block elements typically stack vertically, Flexbox allows elements to align and resize dynamically according to the available space and specified rules.

### Why Use Flexbox?

- Arrange elements horizontally or vertically.
- Align items within a container.
- Distribute available space between items.
- Allow items to grow or shrink based on layout requirements.
- Build reusable components and more complex page layouts.

Flexbox is especially useful for navigation bars, buttons, cards, and content sections.

## Enabling Flexbox

To use Flexbox, apply `display: flex` to the parent element.

### HTML

```html
<div class="flex-container">
	<div>Item 1</div>
	<div>Item 2</div>
	<div>Item 3</div>
</div>
```

### CSS

```css
.flex-container {
	display: flex;
}
```

By default, the three child elements are arranged horizontally in a row instead of stacking vertically.

### Before and After

Without Flexbox, block-level `<div>` elements typically stack vertically:

```
Item 1
Item 2
Item 3
```

With `display: flex`:

```
Item 1  Item 2  Item 3
```

The children become flex items, allowing Flexbox to control their layout.

## Flex Containers and Flex Items

Understanding the relationship between containers and items is fundamental to Flexbox.

### Flex Container

A **flex container** is an element with `display: flex` or `display: inline-flex`.

```css
.container {
	display: flex;
}
```

The container controls how its direct children are arranged.

### Flex Items

**Flex items** are the direct children of a flex container.

```html
<div class="container">
	<div>Item 1</div>
	<div>Item 2</div>
	<div>Item 3</div>
</div>
```

In this example:

- `.container` is the flex container.
- Each child `<div>` is a flex item.

### Important: Direct Children Only

Consider this nested structure:

```html
<div class="container">
	<div class="item">
		<p>Nested paragraph</p>
	</div>
</div>
```

If `.container` has `display: flex`:

- The outer `<div class="item">` is a flex item.
- The nested `<p>` is not a flex item of `.container`.
- The paragraph can still participate in the layout inside `.item` according to normal flow.

If `.item` also has `display: flex`, it becomes a flex container for its own direct children.

**Key concept**: An element can be both a flex item in its parent’s layout and a flex container for its own children.

Nesting flex containers is one of the main ways to build more complex layouts.

## How Flex Items Adapt to Available Space

Flexbox allows items to grow or shrink according to the space available in their container.

For example:

```css
.flex-container {
	display: flex;
}

.flex-container div {
	flex: 1;
}
```

The `flex: 1` declaration allows the items to share available space equally under typical conditions.

If you add another child to the container, Flexbox automatically includes it in the layout.

```html
<div class="flex-container">
	<div>Item 1</div>
	<div>Item 2</div>
	<div>Item 3</div>
	<div>Item 4</div>
</div>
```

```
┌──────────┬──────────┬──────────┬──────────┐
│  Item 1  │  Item 2  │  Item 3  │  Item 4  │
└──────────┴──────────┴──────────┴──────────┘
```

The items adjust to distribute the available space.

### Understanding `flex: 1`

The `flex` shorthand controls an item’s flexibility. The common declaration `flex: 1` allows the item to grow and shrink and generally uses a zero-percent flex basis.

When several items have the same `flex: 1` declaration, they normally share the available space equally, subject to their minimum sizes and other layout constraints.

### Experiment with Flexbox

Try the following changes in you CSS:

1. Add `display: flex` to the parent.
2. Add `flex: 1` to each child.
3. Add another child element.
4. Resize the browser window.
5. Observe how the items respond to the available width.

This helps demonstrate the difference between simply arranging elements in a row and allowing them to flex.

## Building Layouts with Nested Flex Containers

Flexbox layouts can be built by nesting containers.

```html
<div class="page">
	<header class="header">
		<div class="logo">My Website</div>
		<nav class="navigation">
			<a href="#">Home</a>
			<a href="#"<About</a>
		</nav>
	</header>
	
	<main class="content">
		<div class="card">Card 1</div>
		<div class="card">Card 2</div>
	</main>
</div>
```

```css
.header {
	display: flex;
}

.content {
	display: flex;
}

.card {
	flex: 1;
}
```

Here:

- `.header` arranges its direct children using Flexbox.
- `.content` independently arranges its direct children using Flexbox.
- Each `.card` can grow to share the space within `.content`.

Each flex container controls its own direct children. Applying Flexbox to one container does not automatically make every descendant a flex item of that container.

## Debugging Flexbox with DevTools

Flexbox can become more complicated as layouts grow. Chrome DevTools can help you understand what is happening.

When a layout does not behave as expected:

1. Right-click the element and select **Inspect**.
2. Select its parent element in the Elements panel.
3. Check whether the parent has `display: flex`.
4. Identify its direct children, which are the flex items.
5. Experiment with the relevant CSS declarations.
6. Apply the successful changes to your source files.

Chrome DevTools also provides Flexbox visualization controls for inspecting container boundaries and item alignment.

**Best practice**: Experiment with small examples first. Once you understand how the container and its items interact, apply the same concepts to larger layouts.