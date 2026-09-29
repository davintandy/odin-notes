# CSS Units

CSS properties accept specific **value types** (e.g., `<color>`, `<length>`, `<percentage>`). Understanding how these types and units behave ensures consistent layouts, responsive design, and accessible typography.

## Value Types & Identifiers

CSS values define allowable data formats for properties.

- **Identifiers (Keywords):** Predefined, unquoted words (e.g., `display: flex;`, `color: red;`).
- **Strings:** Quoted text values, used mainly in pseudo-elements (e.g., `content: "Note:";`).
- **Unitless Numbers:** Raw numbers without units (e.g., `opacity: 0.6;`, `line-height: 1.5;`).

### Numeric Data Types

| **Data Type** | **Description** | **Examples** |
| --- | --- | --- |
| `<integer>` | Whole numbers (positive or negative) | `1`, `1024`, `-55` |
| `<number>` | Decimal or floating-point numbers | `0.255`, `1.5`, `-1.2` |
| `<dimension>` | A `<number>` with a unit attached | `10px`, `45deg`, `200ms` |
| `<percentage>` | A fraction relative to a parent/container value | `50%`, `100%` |

## Length Units (`<length>`)

Lengths are `<dimension>` types used for properties like `width`, `height`, `margin`, `padding`, and `font-size`.

### Absolute Units

Fixed physical sizes across screen contexts. Primarily used for print stylesheets, with `px` being the primary baseline unit for digital displays.

| **Unit** | **Name** | **Definition / Equivalent** |
| --- | --- | --- |
| `px` | Pixels | Standard web unit (1px = 1/96th inch). Visual angle unit; doesn’t always equal 1 physical hardware pixel |
| `in` | Inches | `1in` = `2.54cm` = `96px` |
| `cm` | Centimeters | `1cm` = `37.8px` |
| `mm` | Millimeters | `1mm` = `0.1cm` |
| `pt` | Points | `1pt` = `1/72in` |
| `pc` | Picas | `1pc` = `12pt` = `1/6in` |
| `Q` | Quarter-mm | `1Q` = `1/40cm` |

### Relative Units

Scale dynamically based on parent element size, root font size, or viewport dimensions.

| **Unit** | **Relative To** | **Common Use Cases** |
| --- | --- | --- |
| `rem` | **Root** element (`<html>`) font size | Global typography, structural spacing |
| `em` | **Current/Parent** element font size | Local component scaling (e.g., padding inside a button) |
| `vw` | **1% of Viewport Width** | Fluid typography, full-width containers |
| `vh` | **1% of Viewport Height** | Full-screen hero sections, modal dialogs |
| `vmin` | **1% of Viewport’s smaller dimension** | Responsive sizing across orientations |
| `vmax` | **1% of Viewport’s larger dimension** | Sizing relative to the larger screen axis |
| `%` | **Parent element’s** property value | Responsive column widths, fluid containers |

## Deep Dive: `px` vs `em` vs `rem`

Understanding unit behavior, compounding, and accessibility implications:

### Unit Breakdown

- **`px` (Pixels):** Fixed baseline (`1/96th inch`). While modern browser zoom scales `px` content effectively, `px` **ignores** user-customized default browser font size settings.
- **`em` (Element Relative):** Relative to parent font size. Excellent for self-contained components where padding/margin should scale alongside text, but risky for nested typography due to compounding.
- **`rem` (Root Relative):** Relative to the `<html>` root font size (default `16px`). Predictable, non-compounding, and respects user accessibility preferences.

### The `em` Compounding Effect

```css
html {
	font-size: 16px;
}

/* Compounding with em: Nested elements multiply exponentially */
ul li {
	font-size: 1.3em;
}
/* Level 1: 20.8px | Level 2: 27px | LEvel 3: 35.1px */

/* Predictable with rem: All nested levels remain identical */
ul li {
	font-size: 1.3rem;
}
/* Every level remains exactly 20.8px */
```

### Best Practices & Accessibility

> **Accessibility Rule:** Prefer `rem` **for typography** so text scales smoothly when users customize their browser base font settings.
> 
- **Typography:** Default to `rem` across all body and heading styles to maintain accessibility.
- **Spacing (`margin`, `padding`):** Use `rem` or `px` based on layout needs. `em` is best reserved for spacing that must scale proportionally with element text size.
- **Flexible Layouts:** Design containers to be flexible enough to handle text wrapping or overflow when users zoom or enlarge font sizes. Avoid rigid container heights on text wrappers.

## Viewport Units & Layout Patterns

Viewport units scale relative to the browser window size and are accepted anywhere lengths are valid (margins, typography, width, padding, etc.).

### Fluid & Responsive Typography

Direct viewport scaling (`font-size: 5vw`) scales too aggressively across screen sizes. Mixing steady units (`px`/`rem`) with viewport units via `calc()` or `clamp()` creates smooth, controlled font growth:

```css
body {
	/* Font grows 1px per 100px of viewport width */
	font-size: calc(16px + 1vw);
	/* Line-height scales relative to font size and viewport */
	line-height: calc(1.1em + 0.5vw);
}

h1 {
	/* Fluid typography with upper and lower constraints */
	font-size: clamp(2rem, 1.2rem + 3vw, 4rem);
}
```

### Full-Height Layouts & Sticky Footers

Constrain applications or expand footers to the edge of the screen:

```css
/* App UI layout */
body {
	height: 100vh;
	overflow: hidden; /* Prevent body scroll; scroll inner sections instead */
}

/* Sticky footer pattern */
footer-wrapper {
	min-height: 100vh;
	display: flex;
	flex-direction: column;
}
```

### Breaking Out of Containers

Expand an element full-bleed to match the screen edges even when inside a constrained container:

```css
.full-bleed {
	width: 100vw;
	margin-left: calc(50% - 50vw);
	margin-right: calc(50% - 50vw);
}
```

### Fluid Aspect Ratios

Calculate dynamic heights based on viewport width (useful for full-width media):

```css
.hero-video {
	width: 180vw;
	height: calc(100vw * (9 / 16)); /* 16:9 aspect ratio */
	max-width: 1200px;
	max-height: calc(1200px * (9 / 16));
}
```

## Color Values (`<color>`)

Modern CSS supports multiple color spaces across the 24-bit RGB gamut (~16.7M colors).

| **Format** | **Syntax Example** | **Key Features** |
| --- | --- | --- |
| **Hexadecimal** | `#02798b` / `#ff00ff66` | `#RGB` shorthand supported (`#f0f`). Last 2 digits set alpha transparency |
| **RGB** | `rgb(2 121 139 / 0.5)` | Channel values (0-255 or 0%-100%). Optional `/ alpha` channel |
| **HSL** | `hsl(188 97% 28% / 0.5)` | Hue (0-360°), Saturation (0-100%), Lightness (0-100%) |
| **HWB** | `hwb(188 10% 20%)` | Hue (0-360°), Whiteness (0-100%), Blackness (0-100%) |
| Keywords | `blueviolet`, `transparent` | Predefined color names; best for quick prototyping |

### Alpha Transparency vs. `opacity`

- **Alpha Channel (`rgb(... / 0.5)` or `hsl(...)`):** Makes **only the background or color** transparent; text and child elements remain fully opaque.
- **`opacity` Property:** Applies transparency to the **entire element including all nested children**.

## Positions, Images, & CSS Functions

### Images(`<image>`)

Supports external image URLs and CSS gradients:

```css
.card {
	background-image: url("banner.png");
	background-image: linear-gradient(90deg, rgb(119 0 255 / 40%), rgb(0 212 255 / 25%));
}
```

### Position (`<position>`)

Defines spatial coordinates using keywords (`top`, `right`, `bottom`, `left`, `center`) or unit offsets:

```css
.hero {
	background-position: right 60px center;
}
```

### CSS Math Functions

Perform dynamic calculations directly inside CSS rules:

- **`calc()`:** Performs calculations across mixed units (`width: calc(100% - 32px);`).
- **`min()` & `max()`:** Constrains values to minimum or maximum thresholds (`width: min(100%, 600px);`).
- **`clamp()`:** Restricts values within a range: `clamp(MIN, VAL, MAX)` (`font-size: clamp(1rem, 2.5vw, 2rem);`).