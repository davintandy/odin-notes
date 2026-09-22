# Default Styles

## The Core Problem: User-Agent Stylesheets

Browsers ship with built-in **User-Agent Stylesheets** to ensure unstyled HTML is readable out of the box. However, these present four primary challenges for modern web development:

1. **Cross-Browser Inconsistencies:** Slight rendering differences across browser engines (Chromium, Gecko, WebKit).
2. **Problematic Defaults:** Default behaviors like `box-sizing: content-box`, cramped `line-heights` (~`1.15`), and auto-zooming text on mobile rotation (`-webkit-text-size-adjust`).
3. **Semantic vs. Visual Conflicts:** Using tags like `<h1>` or `<ul>` for document structure forces developers to constantly strip unwanted default margins and font sizes.
4. **Layout Breaking Media:** Unstyled `<img>` tags display at native dimensions, overflowing narrow parent containers.

## Baseline Strategies Compared

| **Strategy** | **Core Mechanism** | **Key Examples** | **Primary Advantage** | **Trade-Off** |
| --- | --- | --- | --- | --- |
| **Normalize** | Fixes cross-browser bugs while preserving native defaults | `Normalize.css` | Retain browser typographic hierarchy | Retains default margins; requires heavy overrides for custom UIs |
| **Traditional Reset** | Wipes margins, padding, font weights, and list styles across all elements | Meyer Reset, `undohtml.css` | Creates a completely blank slate | Destroys element legibility if custom CSS fails to load |
| **Modern Hybrid** | Fixes engine bugs + applies modern zero-margin & `border-box` baselines | `moder-normalize`, Tailwind `Preflight`, Josh Comeau Reset | Combines bug remediation with zero-margin layouts | Opinionated; requires explicitly setting up typography scale |

## Production-Ready Modern Reset

This single snippet combines modern normalization, zero-margin predictability, accessible typography, and cutting-edge CSS features.

```css
@import "modern-normalize";

/* 1. Global Box=Sizing Model */
*, *::before, *::after {
	box-sizing: border-box;
}

/* 2. Zero Margins Across All UI Elements (Preserving Dialog Centering) */
*:not(dialog) {
  margin: 0;
}

/* 3. Base Typography & Text Rendering */
body {
	line-height: 1.5;
	-webkit-font-smooting: antialiased;
}

/* 4. Decouple Heading Semantics from Visual Sizing */
h1, h2, h3, h4, h5, h6 {
  font-size: inherit;
  font-weight: inherit;
}

/* 5. Inherit Fonts for Form Controls */
input, button, textarea, select {
	font: inherit;
}

/* 6. Block-Level Responsive Media */
img, picture, video, canvas, svg {
	display: block;
}

/* 7. Prevent Text Overflows & Improve Line Wrapping */
p, h1, h2, h3, h4, h5, h6 {
	overflow-wrap: break-word;
}

p {
	text-wrap: pretty;
}

h1, h2, h3, h4, h5, h6 {
	text-wrap: balance;
}

/* 8. Preserve Accessible List Announcements in Safari */
ol[role="list"], ul[role="list"] {
  list-style: none;
  padding-inline: 0;
}

/* 9. Enable Intrinsic Keyword Animation (0px -> auto) */
@media (prefers-reduced-motion: no-preference) {
	html {
		interpolate-size: allow-keywords;
	}
}

/* 10. Root Stacking Context Isolation for Frameworks */
#root, #__next {
	isolation: isolate;
}
```

## Technical Rule Breakdown & Rationale

### Box Model & Spacing

- `box-sizing: border-box`: Includes `padding` and `border` inside the element’s specified `width`/`height`. Prevents `width: 100%` elements with padding from overflowing parents.
- `*:not(dialog) { margin: 0; }`: Eliminates unwanted default margins across all elements while keeping the native browser centering (`margin: auto`) intact for `<dialog>`.

### Typography & Line Wrapping

- `line-height: 1.5`: Overrides browser defaults (`~1.15`) to meet WCAG accessibility guidelines and reduce reading fatigue.
- `-webkit-font-smoothing: antialiased`: Disables legacy subpixel antialiasing on macOS, preventing heavy, blurry font rendering on modern high-DPI displays.
- `overflow-wrap: break-word`: Forces long strings (like URLs or technical terms) to break across lines instead of overflowing containers horizontally.
- `text-wrap: balance` & `pretty`:
    - `balance` (Headings): Equalizes line lengths across multi-line titles.
    - `pretty` (Paragraphs): Prevents single-word “orphans” on the final line of text.

### Form Controls

- `font: inherit`: Form controls (`<input>`, `<button>`, `<textarea>`) do not inherit font properties by default and use browser-default monospace or small 13px sizes. Inheriting document typography fixes awkward auto-zoom behaviors on mobile browsers (which trigger on font sizes smaller than 16px).

### Responsive Media

- `display: block; max-width: 100%`: Eliminates the default inline descender gap beneath images (line-height spacing) and prevents oversized media from overflowing their parent wrappers.

### Accessibility Fixes

- `ol[role="list"], ul[role="list"]`: Stripping `list-style` without specifying `role="list"` causes VoiceOver on Safari to stop announcing elements as lists. Matching on `role="list"` explicitly preserves screen reader list announcements.

### Modern Features & Framework Extras

- `interpolate-size: allow-keywords`: Enables native CSS transitions between pixel values and keyword sizes (e.g., `height: 0` to `height: auto`) without needing JavaScript height measurements.
- `isolation: isolate`: Creates a clean stacking context on the root React/Next.js element, preventing modals or dropdown z-index values from leaking into background layers.

## Advanced Techniques

### Restoring Browser Defaults for CMS / Rich Text Content

When rendering user-generated or CMS HTML (e.g., Markdown blog posts, Terms of Service pages) inside a zero-margin reset environment, use the `revert` keyword inside a wrapper class:

```css
/* Restores native heading scale, list bullets, and margins inside .prose */
.prose :where(h1, h2, h3, h4, h5, ul, ol, p) {
	all: revert;
}
```

### Automated Trimming with Browserslist

By configuring a `.browserlistrc` file, modern build tools (like Lightning CSS or PostCSS) dynamically analyze target environment and automatically strip out obsolete browser hacks or legacy resets from your final CSS bundle.