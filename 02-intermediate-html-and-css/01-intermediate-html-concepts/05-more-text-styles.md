# More Text Styles

## Font Delivery & Custom Web Fonts

When declaring `font-family`, browser evaluate the declaration list sequentially from left to right until finding an available font on the device or online. Always terminate font stacks with a generic fallback (`sans-serif` or `serif`).

### System Font Stack

Native operating system fonts load instantly without network requests, providing a familiar UI experience.

```css
body {
  font-family: system-ui, "Segoe UI", Roboto, Helvetica, Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
}
```

### Font Delivery Methods

| **Delivery Method** | **Implementation** | **Pros & Cons** |
| --- | --- | --- |
| **Online Font Libraries** (e.g., Google Fonts, Font Bunny) | Loaded via HTML `<link>` or CSS `@import` | **Pros:** Quick setup<br>**Cons:** Privacy considerations (e.g., GDPR compliance); reliant or external uptime |
| **Self-Hosted Fonts** | Downloaded and served via `@font-face` | **Pros:** Highly reliable, fully privacy-compliant, eliminates third-party origins<br>**Cons:** Requires manual file management and server setup (CDN + HTTP/2 recommended) |

### Custom Fonts (`@font-face`) & Formats

Define custom font files at the top of your stylesheet before referencing them on elements:

```css
@font-face {
	font-family: "Roboto";
	src:
		url("fonts/roboto-regular.woff2") format("woff2"),
		url("fonts/roboto-regular.woff") format("woff");
	font-weight: normal;
	font-style: normal;
	font-display: swap;
}

body {
	font-family: "Roboto", sans-serif;
}
```

- `font-family`: Custom alias defined to reference the font across your CSS.
- `src`: File path (`url`) and format (`format`). List **WOFF2 first**-browsers download the first format they support and ignore subsequent declarations.
- `font-weight`/`font-style`: Declares weight and style variants under a single family alias.
- `font-display`: Defines rendering behavior while the font file is downloading.

### Web Font File Formats

- **WOFF2:** Use Brotli compression (30% smaller than WOFF). Widely supported and recommended as the primary format.
- **WOFF:** Modern container format, used as a secondary fallback.
- **EOT,TTF,SVG:** Legacy formats required only for legacy browsers (e.g., Internet Explorer 9).

### Variable Fonts

Variable Fonts contain all weight and style variations inside a single responsive file using configurable axes (e.g., weight, slant).

- **Performance Trade-Off:** A single variable font file is larger than a single standard font file, but smaller than downloading multiple separate weight files (e.g., Light, Regular, Bold, Extra Bold).
- **Native System Variable Fonts:** Using `font-family: system-ui` leverages local OS variable font capabilities with zero download overhead.

## Text Styling & Formatting

### CSS Text Properties

| **Property** | **Purpose** | **Best Practices** |
| --- | --- | --- |
| `font-style` | Applies `italic`, `normal`, or `oblique` | Purely visual styling. Use HTML `<em>` only when semantic emphasis is required |
| `letter-spacing` | Adjusts character spacing in words | Use sparingly, primarily on headings, to preserve legibility |
| `line-height` | Controls vertical spacing between lines | Use unitless values (e.g., `1.5`) to keep line height proportional to font size |
| `text-transform` | Enforces casing (`uppercase`, `lowercase`, `capitalize`) | Keeps text causing rules consistent in CSS without altering raw HTML text |
| `text-shadow` | Adds horizontal/vertical shadows and blur around characters | Use sparingly on display text or headings |

## Practical Code Snippets

### Visual Styling vs. Semantic Emphasis (`font-style` vs `<em>`)

```css
/* CSS font-style for purely visual italics */
h1 {
	font-style: italic;
}
```

```html
<!-- HTML <em> for semantic emphasis -->
<p>I <em>never</em> said he stole your money.</p>
```

### Truncating Text with an Ellipsis

To display `...` when text overflows a container, combine `white-space`, `overflow`, and `text-overflow`:

```css
.overflowing {
	white-space: nowrap;
	overflow: hidden;
	text-overflow: ellipsis;
}
```

## Responsive Typography & Layout

Text on the web is responsive by default, wrapping to fit the viewport edge. Good typography requires controlling text size, line length, and line height for comfortable reading.

### Fluid Text Scaling (`calc` & `clamp`)

Static breakpoint adjustments using `@media` queries can cause jumpy text resizes. Fluid typography uses viewport units (`vw`) alongside relative unites (`rem`, `ch`) so font size scales smoothly with browser width.

### Viewport-Based Scaling

To keep text resizable via user browser settings, combine `vw` with relative units inside `calc()`:

```css
html {
	font-size: calc(0.75rem + 1.5vw);
}
```

### Clamping Fluid Text Range

To prevent font sizes from becoming unreadably small on narrow screens or overly large on wide displays, use `clamp(minimum, preferred, maximum)`:

```css
html {
	/* Minimum 1rem, Preferred 0.75rem + 1.5vw, Maximum 2rem */
	font-size: clamp(1rem, 0.75rem + 1.5vw, 2rem);
}
```

### Line Length (`max-inline-size` & `ch`)

- **Optimal Standard:** 45 to 75 characters per line (66 characters is considered ideal for single-column text).
- **Multi-Column Standard:** 40 to 50 characters per line.
- **Implementation:** Restrict container width using `max-inline-size` with relative `ch` units (where `1ch` equals the width of the `0` glyph) rather than fixed pixel dimensions.

```css
article {
	max-inline-size: 66ch; /* Wraps lines at approximately 66 characters */
}
```

### Line Height Rules

- **Proportional Line Height:** Always use unitless values so line height scales dynamically with `font-size`.
- **Length Adjustment:** Shorter line lengths can accommodate larger `line-height` values, whereas longer text lines require tighter `line-height` values to help the reader’s eye transition between lines.

```css
article {
	max-inline-size: 66ch;
	line-height: 1.65;
}

blockquote {
	max-inline-size: 45ch;
	line-height: 2;
}
```

## Font Loading & Optimization

### Discovery Mechanics & Critical CSS

A `@font-face` rule does **not** trigger a file download on its own. Browser download font files only when styled elements referencing the font exist in the DOM.

To accelerate font discovery, inline `@font-face` declarations and critical CSS inside a `<style>` block in the document `<head>`:

```html
<head>
	<style>
		@font-face {
			font-family: "Open Sans";
			src: url("/fonts/OpenSans-Regular-webfont.woff2") format("woff2");
		}
		body {
			font-family: "Open Sans", sans-serif;
		}
	</style>
</head>
```

Note: Avoid inlining font binary data directly into CSS, as large data URLs delay main HTML document parsing.

### Preconnecting Third-Party Origins

When referencing external fonts hosts, place `preconnect` hints in the `<head>`.  Font files require a separate CORS-enabled connection (`crossorigin`).

```html
<head>
	<link rel="preconnect" href="https://fonts.googleapis.com">
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
</head>
```

### Preloading Font Files

Use `<link rel="preload">` to force early fetching of ciritical font files defined in external stylesheets:

```html
<link href="/fonts/roboto-regular.woff2" rel="placehold" as="font" type="font/woff2" crossorigin>
```

Caution: Preloading competes with other critical page resources and bypasses `unicode-range` optimizations. Limit preloads to essential WOFF2 files.

### Font Subsetting & Size Reduction

Subsetting strips unused glyphs from font files to reduce download payload size.

- **Glyph Distribution:** Latin fonts range from 100 to 1,000 glyphs; CJK fonts often exceed 10,000 glyphs.
- **`unicode-range` Descriptor:** Restricts font file downloads to pages containing characters within a declared range.

```css
@font-face {
	font-family: "Open Sans";
	src: url("/fonts/OpenSans-Regular-webfont.woff2") format("woff2");
	unicode-range: U+0025-00FF; /* Downloads only if matching characters appear in HTML */
}
```

Subsetting CLI Tools: `subfont`, `glyphhanger` (always verify license permissions before modifying binaries).

## Deep Dive / Best Practices: Rendering & `font-display`

### Browser Default Blocking Behavior

When custom web fonts are downloading, default browser rendering behavior differs across engines:

- **Chromium & Firefox:** Hides text for up to **3 seconds** (Block Period).
- **Safari:** Hides text **indefinitely**.

### `font-display` Execution Matrix

The `font-display` descriptor configures text rendering behavior across two operational windows:

1. **Block Period:** Text renders invisibly using a fallback font while waiting for the web font.
2. **Swap Period:** Follows the block period; if the web font arrives, it replaces the fallback font.

```css
@font-face {
	font-family: "Roboto";
	src: url("/fonts/roboto.woff2") format("woff2");
	font-display: swap;
}
```

| **Value** | **Block Period** | **Swap Period** | **Performance & Rendering Behavior** |
| --- | --- | --- | --- |
| `optional` | 100ms | None | **Best for Performance**. Ultra-short wait; guarantees zero font-swap layout shifts (CLS). Late-arriving fonts are cached for future views |
| `swap` | 0ms | Infinite | **Best for Immediate Visibility**. Text renders instantly using a fallback font, swapping once loaded. May cause layout shifts |
| `fallback` | 100ms | 3 seconds | **Balanced**. Brief delay to allow font loading; if missed, renders fallback text and limits swap window |
| `block` | 2-3s | Infinite | **Visual Consistency Focus**. Hides text until loaded. Prevents text swapping, but delays readability |

### Layout Stability & Special Cases

- **Reducing Layout Shifts (CLS):** Late-arriving web fonts can shift page layouts when swapping. Use `size-adjust` within fallback `@font-face` definitions to match fallback font dimensions with the web font.
- **Icon Fonts vs. SVGs:** `font-display: swap` on icon fonts can display incorrect glyphs or trigger severe layout shifts. Replace icon fonts with **SVGs** for superior accessibility, predictability, and rendering performance.