# The Cascade

## What Is the CSS Cascade?

The **CSS cascade** is the process browsers use to determine which CSS declarations apply when multiple rules could affect the same element.

For example:

```css
p {
	color: red;
}

p {
	color: blue;
}
```

The paragraph appears blue because both rules target the same element, have equal specificity, and the blue declaration comes later.

Understanding the cascade helps you identify why a particular style is applied and how to resolve unexpected styling conflicts.

### What Determines Which Rule Wins?

For the basic concepts, focus on three factors:

1. **Specificity**: Which selector is more specific?
2. **Inheritance**: Is the value inherited from a parent or explicitly declared on the element?
3. **Rule order**: If competing declarations are otherwise equal, which one appears last?

In the full CSS cascade, other factors-including the origin and importance of a declaration-are considered before specificity.

## Specificity

**Specificity** is the priority assigned to a selector based on the types of selectors it contains.

When multiple applicable declarations conflict over the same property, the more specific declaration generally wins, provided earlier cascade factors are equal.

### Specificity Hierarchy

For the basic selectors covered so far, the hierarchy is:

1. **ID selectors** - `#main-title`
2. **Class selectors** - `.highlight`
3. **Type selectors** - `p, h1, div`

### Example: ID vs. Class Selector

```css
#main-title {
	color: red;
}

.title {
	color: blue;
}
```

```html
<h1 id="main-title" class="title">Hello World!</h1>
```

The text is red because an ID selector has higher specificity than a class selector.

**Important**: Specificity is compared separately for each CSS property. A winning declaration for `color` does not automatically cancel other declarations for `background-color`, `font-size`, or other properties.

## Comparing Multiple Selectors

A selector can contain several IDs, classes, or type selectors. To compare specificity accurately, count each category separately.

A useful notation is:

| **Selector component** | **Specificity contribution** |
| --- | --- |
| ID selector | `1-0-0` |
| Class, attribute, or pseudo-class selector | `0-1-0` |
| Type or pseudo-element selector | `0-0-1` |
| Universal selector (`*`) | `0-0-0` |
| Combinators, such as spaces and `>` | `0-0-0` |

Compare the three numbers from left to right. A difference in the first category decides the result before the second and third category is considered.

### Example: Multiple Classes

```css
.subsection {
	color: blue;
}

.main .list {
	color: red;
}
```

Suppose an element has the `list` class and is inside an element with the `main` class.

- `.subsection` has specificity `0-1-0`.
- `.main .list` has specificity `0-2-0`.

The second rule wins when both match the same element because it contains two class selectors.

### Example: One ID vs. Multiple Classes

```css
#subsection {
	color: blue;
}

.main .list {
	color: red;
}
```

- `#subsection` has specificity `1-0-0`.
- `.main .list` has specificity `0-2-0`.

The ID selector wins because the ID category takes priority over the class category.

### Example: Chaining Selectors

```css
.class.second-class {
	font-size: 12px;
}

.class .second-class {
	font-size: 24px;
}
```

Both selectors have specificity `0-2-0`

- `.class.second-class` selects one element that has both classes.
- `.class .second-class` selects an element with `second-class` nested inside an element with `class`.

The selectors describe different relationships, but the spaces and combinators do not add specificity. If both rules match the same element and all other cascade factors are equal, the second rule wins because it comes later.

### Important Notes

- Count the number of selectors in each specificity category rather than adding all selectors into one total.
- An ID selector outweighs any number of class selectors under the standard specificity comparison.
- The universal selector (`*`) contributes no specificity.
- Combinators-including spaces, `>`, `+`, and `~`- do not add specificity.
- Specificity matters only when applicable declarations conflict over the same property.

## Inheritance

**Inheritance** allows certain CSS property values applied to a parent element to pass to its descendants automatically.

For example:

```html
<div class="parent">
	<p>This paragraph inherits its text color.</p>
</div>
```

```css
.parent {
	color: red;
}
```

The paragraph appears red because `color` is normally inherited from its parent.

### Common Inherited Properties

Typography-related properties are often inherited.

Examples include:

- `color`
- `font-family`
- `font-size`
- `font-style`
- `line-height`

Not every property is inherited. Many layout and box-related properties, such as `margin`, `padding`, `border`, and `background-color`, are not inherited by default.

Check the documentation for a property when you are unsure whether it inherits.

### Directly Targeted Elements vs. Inherited Values

A declaration that directly targets an element takes precedence over a value that the element would otherwise inherit.

```html
<div id="parent">
	<p class="child">Hello World!</p>
</div>
```

```css
#parent {
	color: red;
}

.child {
	color: blue;
}
```

The paragraph is blue.

Although `#parent` uses a more specific ID selector, its red color is inherited by the paragraph. The `.child` rule directly specifies the paragraph’s color, so the paragraph uses blue.

**Key takeaway**: An inherited value is not a competing declaration directly applied to the child. A directly specified value wins over the inherited value regardless of the parent’s selector specificity.

## Rule Order

When two declarations have the same cascade precedence and specificity, **the declaration that comes later wins**.

This is also known as the source-order rule.

### Example

```css
.alert {
	color: red;
}

.warning {
	color: yellow;
}
```

```html
<div class="alert warning">Warning!</div>
```

Both selectors have equal specificity: `0-1-0`.

Since `.warning` is defined later, the text is yellow.

If the order is reversed:

```css
.warning {
	color: yellow;
}

.alert {
	color: red;
}
```

The text becomes red because `.alert` is now the later rule.

### Rule Order Across Stylesheets

Source order can also matter when styles come from different stylesheets.

For example:

```html
<head>
	<link rel="stylesheet" href="base.css">
	<link rel="stylesheet" href="overrides.css">
</head>
```

When applicable declarations have the same cascade precedence and specificity, a conflicting declaration in `overrides.css` can win because it is loaded later.

This assumes no other cascade factor changes the outcome.

### When Does Rule Order Matter?

Rule order is considered after higher-priority factors have been resolved. A later rule does not automatically defeat a more specific rule.

```css
#main-title {
	color: red;
}

.title {
	color: blue;
}
```

Even though `.title` could be declared later, the ID selector normally wins for this conflict because it has higher specificity.

## Browser Default Styles

Browsers provide default styles, also called **user-agent styles**, even when you have not written any CSS.

For example, browsers commonly display:

- Headings in bold, with different default sizes.
- Paragraphs with vertical margins.
- Links with distinctive colors and underlines.
- Buttons with default borders and backgrounds.

These styles are supplied by the browser’s stylesheet.

You can override ordinary browser defaults by providing applicable author CSS.

```css
h1 {
	font-size: 24px;
	color: darkblue;
}

p {
	margin: 0;
}
```

Understanding browser defaults helps explain why elements have certain appearances even when your own stylesheet does not explicitly define those styles.

## Understanding the Full Cascade

The three main concepts for this lesson-specificity, inheritance, and source order-are important, but the complete CSS cascade includes additional steps.

A simplified overview of the modern cascade is:

1. **Relevance**: Determine which rules apply to the element and current conditions.
2. **Origin and importance**: Compare the source of the styles and whether declarations use `!important`. Cascade layers are considered as part of this stage.
3. **Specificity**: Compare the selectors of declarations that remain in competition.
4. **Scoping proximity**: When applicable, compare how close scoped rules are to their scope roots.
5. **Source order**: If the competing declarations are still tied, the later declaration wins.

For beginner exercises, you can usually focus on specificity, inheritance, and source order unless the example includes inline styles, `!important`, or other advanced cascade features.

### Inline Styles and `!important`

Inline styles are written directly in an HTML element:

```html
<p style="color: red;">Hello World!</p>
```

A normal inline style generally takes precedence over normal selector-based author styles, even a highly specific ID selector.

The `!important` flag raises a declaration’s priority within the cascade:

```css
p {
	color: blue !important;
}
```

However, `!important` is not simply another specificity value. The cascade considers importance before comparing selector specificity.

Avoid relying on `!important` to solve routine conflicts. First check which selectors match, compare their specificity, and inspect the rule order.

## A Practical Debugging Checklist

When a CSS style does not appear as expected:

1. **Check the selector**: Does it match the intended element?
2. **Check the property**: Are multiple rules setting the same property to different values?
3. **Compare cascade precedence**: Are there inline styles, `!important` declarations, or other factors that affect priority?
4. **Compare specificity**: Which competing selector has the higher specificity?
5. **Check inheritance**: Is the element receiving a value from a parent, or does it have a directly specified value?
6. **Check source order**: If the rules are otherwise tied, which declaration appears last?
7. **Inspect browser defaults**: Is the appearance caused by the browser’s own stylesheet?

Browser developer tools can help by showing the CSS rules applied to an element and indicating which declarations are overridden.