# Inspecting HTML and CSS

## What Is Chrome DevTools?

**Chrome DevTools** is a collection of web development tools built into Google Chrome. It helps developers inspect webpages, experiment with changes, and troubleshoot HTML and CSS issues.

### Why Use DevTools?

- Inspect the HTML structure of a webpage.
- Identify the CSS rules applied to an element.
- Determine why a CSS declaration is overridden.
- Experiment with HTML and CSS changes in real time.
- Test different styling values without repeatedly editing and reloading source files.

### Important Panels

Chrome DevTools contains several panels, each designed for different tasks.

| **Panel** | **Main purpose** |
| --- | --- |
| **Elements** | Inspect and modify the page’s DOM and CSS |
| **Console** | View messages and interact with JavaScript |
| **Sources** | Inspect source files and debug code |
| **Network** | Inspect network requests and resource loading |
| **Performance** | Investigate page loading and runtime performance |
| **Application** | Inspect resources such as storage, cookies, and loaded assets |
| **Device Mode** | Simulate different screen sizes and mobile devices |

For this lesson, focus primarily on the **Elements panel** and its **Styles section**.

## Opening Chrome DevTools

There are several ways to open DevTools.

### Method 1: Inspect an Element

1. Open a webpage in Chrome.
2. Right-click an element, such as a heading or paragraph.
3. Select **Inspect**.
4. DevTools opens with the selected element highlighted in the Elements panel.

This is usually the fastest method when you want to investigate a specific part of a webpage.

### Method 2: Keyboard Shortcuts

| **Action** | **Keyboard Shortcuts** |
| --- | --- |
| Open element inspector | `Ctrl + Shift + C` |
| Open DevTools | `Ctrl + Shift + I` or `F12` |
| Open the previously used panel | `F12` |

Keyboard behavior may vary depending on the operating system, keyboard, and browser configuration.

### Method 3: Chrome Menu

1. Open Chrome’s three-dot menu.
2. Select **More tools** → **Developer tools**.

### Element Selection Tool

The element selection tool lets you hover over elements on the webpage and select the one you want to inspect.

This is useful when you do not know which HTML element corresponds to a particular visual component.

## Understanding the Elements Panel

The **Elements panel** displays the page’s DOM tree and allows you to inspect its structure.

### What Is the DOM?

**DOM (Document Object Model)** is the browser’s structured representation of an HTML document.

HTML defines the document’s markup. The browser parses that markup and constructs a DOM tree representing the elements and their relationships.

For example, consider this HTML:

```html
<body>
	<h1>My Website</h1>
	<p>Welcome to my website.</p>
</body>
```

The DOM tree can be represented as:

```
body
├── h1
│   └── "My Website"
└── p
    └── "Welcome to my website."
```

Each element is represented as a node in the tree, and text inside elements is represented by text nodes.

### Navigating the DOM Tree

In the Elements panel, you can:

- Click an element to select it.
- Expand or collapse elements to view or hide their children.
- Inspect the attributes and content of an element.
- Hover over DOM nodes to highlight their corresponding elements on the webpage.
- Search the DOM tree for text or elements using CSS selectors.

### Searching for Elements

1. Focus the Elements panel.
2. Press `Ctrl + F`.
3. Enter text, a CSS selector, or an XPath expression.
4. DevTools highlights matching results in the DOM tree.

For example, searching for `.card` helps locate elements with the `card` class.

This is especially useful when working with large or deeply nested HTML documents.

## Inspecting CSS in the Styles Section

When you select an element in the DOM tree, the **Styles** section displays the CSS rules that affect that element.

For example:

```html
<p class="description">Hello World!</p>
```

```css
p {
	color: red;
}

.description {
	font-size: 18px;
}
```

When you inspect the paragraph, you can find both rules in the Styles section.

### What Can You Learn from the Styles Section?

- Which selectors target the element.
- Which CSS properties and values are declared.
- Which declarations are overridden.
- Which styles are inherited from parent elements.
- Where a stylesheet rule originates, when the source information is available.

### Overridden CSS Declarations

Suppose your stylesheet contains:

```css
p {
	color: red;
}

.description {
	color: blue;
}
```

For a paragraph with the `description` class, the Styles section shows both declarations, but the `color: red` declaration is crossed out because the more specific class rule wins.

A crossed-out declaration is a useful clue when diagnosing unexpected styling.

Instead of adding more CSS immediately, inspect the existing rules to understand why the declaration is not taking effect.

## Testing CSS Changes in DevTools

One of the most useful features of DevTools is the ability to experiment with CSS directly in the browser.

These changes appear immediately, allowing you to test different values without constantly editing your stylesheet.

### Modifying Existing Declarations

1. Inspect the element you want to change.
2. Find the relevant rule in the Styles section.
3. Click the property value you want to modify.
4. Enter a new value and press `Enter`.
5. Observe the updated webpage.

For example, change:

```css
color: red;
```

to:

```css
color: blue;
```

The selected element’s text changes to blue immediately.

### Adding a New Declaration

You can also add a new CSS property to an existing rule or to be selected element’s inline styles.

For example:

```css
background-color: lightyellow;
```

This makes it easy to test background colors, font sizes, margins, padding, and other properties.

### Adding a CSS Rule

You can create a new rule in the Styles section to experiment with styling an element using a selector.

For example:

```css
.description {
	font-size: 20px;
	color: darkblue;
}
```

This is useful when testing an idea before adding the rule to your actual stylesheet.

### Toggling Declarations

DevTools lets you disable or re-enable individual declarations, commonly using a checkbox beside the declaration.

This helps you determine which property is responsible for a particular visual effect without deleting the declaration.

### Important Limitation

**Changes made in DevTools are temporary by default.**

They modify the current page in the browser, not automatically the HTML or CSS files in your code editor. Reloading the page generally discards these experimental changes unless you have configured a persistence workflow.

Once you are satisfied with a change, make it in the actual source file and save it.

## Editing HTML in DevTools

The Elements panel also lets you modify the DOM directly.

### Edit Text Content

1. Inspect the element.
2. Double-click its text content in the DOM tree.
3. Replace the existing text.
4. Press `Enter` to apply the change.

### Edit Attributes

You can double-click an element’s attribute name or value to modify it.

For example, change:

```html
<p class="description">Hello World!</p>
```

to:

```html
<p class="highlight">Hello World!</p>
```

This lets you test different classes and attributes without editing the original HTML file.

### Edit as HTML

For larger changes:

1. Right-click a DOM node.
2. Select **Edit as HTML**.
3. Modify the markup.
4. Apply the changes.

DevTools supports editing a sectoin of HTML with syntax highlighting and autocomplete.

### Other DOM Operations

The Elements panel also allows you to:

1. Duplicate an element.
2. Reorder nodes.
3. Hide an element.
4. Delete an element.
5. Change an element’s tag name.

These features are useful for experimenting with page structure and identifying which elements affect the layout.

As with CSS changes, these DOM modifications are temporary by default.

## Working with Classes and Pseudo-Classes

DevTools makes it easy to test how an element behaves when classes or pseudo-classes are applied.

### Adding and Removing Classes

The Styles section includes a class editor, commonly accessed through the `.cls` control.

For example, suppose your stylesheet contains:

```css
.highlight {
	background-color: yellow;
	color: black;
}
```

You can temporarily and the `highlight` class to a selected element and see how it looks.

You can also toggle classes on and off to compare different styles.

### Testing Pseudo-Classes

Pseudo-classes describe particular states of an element.

One common example is `:hover:`

```css
button:hover {
	background-color: blue;
	color: white;
}
```

Normally, this rule applies when the pointer hovers over the button.

DevTools lets you force a pseudo-class state, even when the pointer is not actually hovering over the element.

To test it:

1. Inspect the element.
2. Find the `:hov` control in the Styles section.
3. Enable `:hover`.
4. Observe the applied styling.

This is helpful for testing interactive styles consistently.

## Understanding the CSS Box Model

DevTools provides a visual **Box Model** diagram for inspecting an element’s dimensions and spacing.

The box model consists of four layers:

```
┌───────────────────────────────┐
│            Margin             │
│  ┌─────────────────────────┐  │
│  │          Border         │  │
│  │  ┌───────────────────┐  │  │
│  │  │      Padding      │  │  │
│  │  │  ┌─────────────┐  │  │  │
│  │  │  │   Content   │  │  │  │
│  │  │  └─────────────┘  │  │  │
│  │  └───────────────────┘  │  │
│  └─────────────────────────┘  │
└───────────────────────────────┘
```

### Box Model Components

| **Component** | **Purpose** |
| --- | --- |
| Content | The text, image, or other content inside the element |
| Padding | Space between the content and the border |
| Border | The boundary surrounding the padding and content |
| Margin | Space outside the border, separating the element from others |

### Inspecting Dimensions

1. Select an element in the DOM tree.
2. Find the Box Model diagram in the Styles section.
3. Hover over a region to highlight the corresponding area on the webpage.
4. Double-click a dimension to modify it.

You can experiment with values for width, height, padding, margin, and border dimensions.

The diagram commonly uses pixels by default, but it can accept other CSS units, such as percentages and viewport units.

This provides a visual way to understand how spacing changes affect an element’s position and size.

## A Practical CSS Debugging Workflow

When an element does not look as expected, follow this process.

1. **Inspect the element**. Right-click it and select inspect.
2. **Check the DOM tree**. Confirm that you selected the correct element and examine its classes and attributes.
3. **Review the Styles section**. Look for the declarations affecting its appearance.
4. **Investigate overridden properties**. Check crossed-out declarations and compare selectors, specificity, and rule order.
5. **Experiment in DevTools**. Change values, toggle declarations, or test classes.
6. **Check the box model**. Investigate margin, padding, borders, and dimensions if the problem involves spacing or layout.
7. **Update the source files**. Once you identify the correct fix, implement it in your editor and save the changes.
8. **Reload and verify**. Confirm that the saved HTML and CSS produce the expected result.

This workflow is faster and more systematic than repeatedly changing CSS without understanding the cause of a problem.

## Common Mistakes

| **Mistake** | **Better approach** |
| --- | --- |
| Changing CSS without inspecting existing rules | Select the element and review its Styles section first |
| Ignoring crossed-out declarations | Identify which competing rule takes precedence |
| Confusing the DOM with the original HTML file | Remember that the DOM is the browser’s live document representation |
| Assuming browser edits are saved automatically | Apply successful changes to your actual source files |
| Adding increasingly specific selectors without investigating the conflict | Use DevTools to identify the original rule and understand the cascade |
| Ignoring padding and margin when debugging layout | Inspect the Box Model diagram |