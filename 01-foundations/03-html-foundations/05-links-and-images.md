# Links and Images

## HTML Links

Links connect webpages and other resources, allowing users to navigate between pages or websites.

HTML uses the `<a>` (anchor) element to create hyperlinks.

### Basic Syntax

```html
<a href="https://www.theodinproject.com/">The Odin Project</a>
```

- `<a>` defines the anchor element.
- `href` specifies the destination URL or file path.
- The text between the tags is the clickable link text.

Without an `href` attribute, an anchor element does not function as a normal hyperlink.

### HTML Attributes

**Attributes** provide additional information about an HTML element. They are written inside the opening tag and generally follow this syntax:

```html
attribute="value"
```

For example:

```html
<a href="https://www.example.com">Visit Example</a>
```

Here, `href` is the attribute name, and the URL is its value.

## Opening Links in a New Tab

By default, links usually open in the current browser tab. Use the `target` attribute to change this behavior.

```html
<a href="https://www.theodinproject.com/"	target="_blank"	rel="noopener noreferrer">
	The Odin Project
</a>
```

### Important Attributes

| **Attribute** | **Purpose** |
| --- | --- |
| `href` | Specifies the destination |
| `target="_self"` | Opens the destination in the current tab; this is the default |
| `target="_blank"` | Opens the destination in a new tab or window, depending on browser settings |
| `rel="noopener"` | Prevents the opened page from accessing the original page through `window.opener` |
| `rel="noreferrer"` | Prevents referrer information from being sent and also implies `noopener` behavior in modern browsers |

**Best practice**: When intentionally opening an external link in a new tab, `target="_blank"` with `rel="noopener noreferrer"` is a common safe pattern.

## Absolute and Relative Links

There are two essential ways to reference a resource: absolute URLs and relative file paths.

### Absolute URLs

An absolute URL specifies the complete web address, including the scheme and domain.

```html
<a href="https://developer.mozilla.org/en-US/docs/Web/HTML">HTML Documentation</a>
```

An absolute URL typically contains:

- **Scheme**: `https://`
- **Domain**: `developer.mozilla.org`
- **Path**: `/en-US/docs/Web/HTML`

Use absolute URLs primarily when linking to external websites or resources.

### Relative Paths

A relative path specifies a resource based on the location of the current HTML file.

Suppose your project has this sturcutre.

```
my-website/
├── index.html
├── pages/
│   └── about.html
└── images/
    └── logo.png
```

From `index.html`, you can link to the other files using:

```html
<a href="./pages/about.html">About</a>
<img src="./images/logo.png" alt="Website logo">
```

The paths are relative to the location of `index.html`.

### Special Path Symbols

| **Symbol** | **Meaning** | **Example** |
| --- | --- | --- |
| `./` | Current directory | `./pages/about.html` |
| `../` | Parent directory | `../images/logo.png` |
| `/` at the start of a URL path | Root of the website | `/images/logo.png` |

A non-relative path such as `/images/logo.png` starts from the website’s root, not the current HTML file’s directory. Its behavior can differ when a site is hosted under a subdirectory.

### Accessing a Parent Directory

Consider `pages/about.html` from the project structure above. To display the logo, you must move up one directory level before entering `images/`.

```html
<img src="../images/logo.png" alt="Website logo">
```

Path breakdown:

1. `..` moves from `pages/` to `my-website/`.
2. `images/` enters the images directory.
3. `logo.png` identifies the image file.

To move up two directory levels, use `../../`.

> **Key rule**: Relative paths are resolved from the location of the current HTML file, not automatically from the project’s root directory.
> 

## Adding Images to a Webpage

HTML uses the `<img>` element to embed an image.

Unlike most HTML elements, `<img>` is a **void element**. It does not wrap content and does not require a closing tag.

### Basic Syntax

```html
<img src="./images/dog.jpg" alt="A dog sitting on the grass">
```

- `src` specifies the image’s location.
- `alt` provides alternative text describing the image.

The `src` attribute accepts both absolute URLs and relative file paths.

### Using an External Image

```html
<img src="https://example.com/images/dog.jpg" alt="A dog sitting on the grass">
```

The image is loaded from the external URL, so it depends on that resource remaining available and accessible.

### Using a Local Image

A common approach is to keep images in a dedicated directory.

```
my-website/
├── index.html
└── images/
    ├── dog.jpg
    └── logo.png
```

From `index.html`:

```html
<img src="./images/dog.jpg" alt="A dog sitting on the grass">
```

Organizing images separately keeps projects easier to maintain as they grow.

## The `alt` Attribute

The `alt` attribute supplies a text alternative for an image.

```html
<img src="./images/dog.jpg" alt="A brown dog running in a park">
```

### Why Is `alt` Important?

- **Accessibility**: Screen readers can announce the description to users who cannot see the image.
- **Fallback**: The browser can display the alternative text when an image cannot be loaded.
- **Context**: It communicates the relevant information conveyed by an image.

### Best Practices

- Describe the image’s relevant content or purpose.
- Keep descriptions useful and concise.
- Do not use filenames as the only description.
- Avoid repeating nearby text unnecessarily.
- For purely decorative images, use `alt=""` so assistive technologies can skip them.

Example:

```html
<!-- Meaningful image -->
<img src="./images/logo.png" alt="My Website">

<!-- Decorative image -->
<img src="./images/divider.png" alt="">
```

Choose alternative text based on the image’s role in the page, not merely its appearance.

## Image Dimensions

The `<img>` element supports `width` and `height` attributes.

```html
<img
	src="./images/dog.jpg"
	alt="A dog sitting on the grass"
	width="600"
	height="400"
>
```

The values represent dimensions in pixels. Do not include a `px` unit in these HTML attributes.

### Why Specify Dimensions?

- Helps the browser reserve space before an image loads.
- Reduces unexpected layout shifts as content appears.
- Communicates the image’s intrinsic dimensions.

Use the image’s actual intrinsic width and height when providing both attributes to preserve its proportions.

### HTML Attributes vs. CSS

HTML dimension attributes provide intrinsic sizing information, while CSS controls how images are displayed and resized.

```html
<img
	src="./images/dog.jpg"
	alt="A dog sitting on the grass"
	width="1200"
	height="800"
>
```

```css
img {
	max-width: 100%;
	height: auto;
}
```

This CSS allows the image to shrink to fit its container without exceeding the container’s width or distorting its proportions.

**Best practice**: Include appropriate `width` and `height` attributes and use CSS for responsive sizing and visual layout.

## Common Image Formats

Different image formats are suited to different purposes.

| **Format** | **Characteristics** | **Common uses** |
| --- | --- | --- |
| JPEG / JPG | Lossy compression; does not support transparency | Photographs and images with many colors |
| PNG | Lossless compression; supports transparency | Logos, screenshots, diagrams, and graphics with transparent backgrounds |
| GIF | Supports simple animation and limited transparency; limited color palette | Simple animations |
| SVG | Vector-based; scales without pixelation | Icons, logos, illustrations, and diagrams |

### Choosing the Right Format

- Use **JPEG** for photographs where efficient file size matters.
- Use **PNG** for graphics requiring lossless quality or transparency.
- Use **GIF** when a simple animated image is appropriate.
- Use **SVG** for scalable vector graphics, especially icons and logos.

No single format is best for every situation. Consider visual quality, file size, transparency, animation, and browser support.

## File and Folder Organization

A clear file structure makes it easier to maintain links and images across a website.

Example:

```
odin-links-and-images/
├── index.html
├── pages/
│   └── about.html
└── images/
    ├── dog.jpg
    └── logo.png
```

The homepage can reference files in other directories:

```html
<a href="./pages/about.html">About</a>
<img src="./images/dog.jpg" alt="A dog sitting on the grass">
```

The about page can reference the same image using a different relative path:

```html
<img src="../images/dog.jpg" alt="A dog sitting on the grass">
```

Notice that the correct path depends on where the current HTML file is located.

### File-Naming Best Practices

- Use descriptive filenames, such as `company-logo.png`.
- Prefer lowercase names for consistency.
- Use hyphens instead of spaces, such as `about-us.html`
- Match filenames and file extensions exactly, especially when deploying to case-sensitive systems.
- Keep related files in organized directories.

Avoiding spaces in filenames also makes URLs easier to read and manage.

## Image Licensing and Attribution.

Images found online are not automatically free to use.

Before using an image in a project:

1. Check the license and whether it permits your intended use.
2. Review any requirements for attribution, modification, or redistribution.
3. Credit the creator when required by the license.
4. Keep attribution details in your project’s README or another appropriate location when necessary.

For portfolio and public projects, prefer images you created yourself or images with licenses that explicitly allow your intended use.

## Common Mistakes

| **Mistake** | **Why it causes problems** | **How to fix it** |
| --- | --- | --- |
| Forgetting `href` | The anchor does not have a destination | Add the correct `href` attribute |
| Using the wrong relative path | The browser cannot locate the file | Calculate the path from the current HTML file |
| Forgetting `alt` | Accessibility suffers and no text alternative is provided | Write appropriate alternative text |
| Using `../` incorrectly | The path may point to the wrong directory | Check the folder hierarchy |
| Using the wrong filename or extension | The resource may not load | Match the actual filename and capitalization |
| Omitting image dimensions | The page may shift while images load | Specify appropriate `width` and `height` attributes |
| Using an image without checking its license | The use may violate the creator’s terms | Check usage rights and attribution requirements |