# SVG

SVG (Scalable Vector Graphics) is an XML-based image mathematical formulas, rather than a fixed pixel grid, to draw shapes, paths, and text at any scale without losing quality.

### Vector vs. Raster Comparison

| **Feature** | **Vector Graphics (SVG)** | **Raster Graphics (JPEG, PNG, WebP)** |
| --- | --- | --- |
| **Data Format** | Mathematical points, lines, and curves | Fixed grid of colored pixels |
| **Scalability** | Infinite resolution (no quality loss) | Pixelates and blurs when zoomed in |
| **File Size** | Based on visual shape complexity | Based on pixel dimension/resolution |
| **Styling & Scripting** | Modifiable via CSS & JavaScript | Requires an external image editor |
| **Best For** | Icons, logos, UI charts, simple graphics | Photography, complex high-detail art |

> **Limitation:** SVGs become extremely inefficient and result in large file sizes for photorealistic artwork, as every detail requires explicit XML nodes.
> 

## Embedding Strategies: Linked vs. Inline

| **Feature** | **Linked** | **Inline** |
| --- | --- | --- |
| **Syntax** | `<img src="file.svg">` or `background-image: url()` | Direct `<svg>...</svg>` in HTML |
| **Caching** | Standard asset caching | Part of the HTML payload |
| **Styling & Interactivity** | Cannot access or style internal SVG nodes | Full CSS/JS control (hover effects, animations) |
| **Best Practice** | Static icons, decorative background images | Interactive icons, dynamic UI components, charts |

## Responsive Scaling & the `viewBox` Attribute

By default, SVG elements use absolute coordinates. The `viewBox` attribute establishes an **internal coordinate system**, allowing the graphic to scale fluidly without cropping.

```html
<svg width="100%" height="auto" viewBox="min-x min-y width height">
	<circle cx="150" cy="110" r="60" fill="hotpink" />
</svg>
```

- `min-x`, `min-y`: Shifts the visible origin point (pan/scroll position).
- `width`, `height`: Defines the internal resolution and visible area bounds (zoom level).

## Basic Geometry Primitives

SVG elements use **geometry attributes** to define their coordinates and dimensions.

| **Primitive** | **Key Attributes** | **Description** |
| --- | --- | --- |
| `<line>` | `x1`, `y1`, `x2`, `y2` | Draws a straight line between two points |
| `<rect>` | `x`, `y`, `width`, `height`, `rx`, `ry` | Draws rectangles. `rx` / `ry` round the corners |
| `<circle>` | `cx`, `cy`, `r` | Positioned by center coordinates (`cx`, `cy`) and radius (`r`) |
| `<ellipse>` | `cx`, `cy`, `rx`, `ry` | Similar to a circle, but allows distinct x/y radii |
| `<polygon>` | `points="x1,y1 x2,y2 ..."` | Draws closed multi-sided shapes connecting designated points |
| `<path>` | `d="..."` | The most versatile shape element, using path commands (e.g., `M`, `L`, `C`) |

> **Degenerate Shapes:** If a 2D shape like `<rect>` or `<circle>` has a width, height, or radius of `0`, it is considered “degenerate” and will note render at all.
> 

## Styling with Presentational Attributes & CSS

SVG appearance properties can be written as XML attributes or manipulated directly via CSS.

```html
<button class="icon-btn">
	<svg viewBox="0 0 100 100">
		<circle cx="50" cy="50" r="30" class="animated-circle" />
	</svg>
</button>
```

```css
/* Presentational attributes function as CSS properties */
.animated-circle {
	fill: oklch(0.9 0.3 164);
	stroke: hsl(210deg 15% 30%);
	stroke-width: 5px;
	stroke-linecap: round;
	transition: r 300ms ease, fill 300ms ease;
}

.icon-btn:hover .animated-circle {
	r: 40;
	fill: hotpink;
}
```

### Core Stroke Properties

- `stroke`: Sets the outline color (defaults to `transparent`).
- `stroke-width`: Defines outline thickness in user units/pixels.
- `stroke-dasharray`: Defines dash/gap lengths for dashed lines (e.g., `stroke-dasharray="10 5"`).
- `stroke-linecap`: Controls line endings (`butt`, `round`, `square`).