# Links and Images

To build a multi-page website, you need to connect files using **Anchor tags** (`<a>`) and display media using **Image tags** (`<img>`).

---

## Anchor Elements (`<a>`)

The `<a>` tag creates a hyperlink. On its own, it does nothing; it requires the `href` attribute to specify a destination.

```html
<a href="https://www.google.com">Visit Google</a>
```

### Link Types

| **Type** | **Description** | **Example `href`** |
| --- | --- | --- |
| **Absolute** | Full URL including scheme (`https://`). Used for external sites. | `https://developer.mozilla.org` |
| **Relative** | Path to a file within your project based on the current file’s location. | `about.html` or `pages/contact.html`  |
| **Root-Relative** | Path relative to the website’s root folder. Starts with a `/`. | `/images/logo.png` |

Root-relative links usually require a live web server to function correctly and won’t always work on local files.

### Opening in a New Tab

Use the `target` attribute to change how a link opens.

- `target="_blank"`: Opens the link in a new tab.
- `rel="noopener noreferrer"`: **Security Essential**. Prevents the new page from accessing your original tab (protecting against “tabnabbing” attacks).

---

## Understanding File Paths

File paths are the “directions” you give the browser to find a file.

- `./`: Look in the **current** folder.
- `foldername/`: Look inside a sub-folder.
- `../`: Go **up** one level to the parent folder.

### Naming Conventions

To avoid broken links and “ugly” URLs (like `%20` representing spaces):

- **No Spaces:** Use **hyphens** (`about-us.html`) instead of spaces.
- **Lowercase:** Always use lowercase for files and folders to ensure consistency across different servers.
- **Be Descriptive:** Your file names become the “slug” in the URL that users see.

---

## Image Elements (`<img>`)

The `<img>` tag is a **void elements** (no closing tag). It embeds an external resource into your page.

### **Essential Attributes**

- `src`: The path to the image file (Absolute or Relative).
- `alt`: **Mandatory for accessibility**. Describes the image for screen readers and displays if the image fails to load.
- `width` / `height`: Specified in pixels (do **not** include `px`). Providing these helps the browser reserve space so the page doesn’t “jump” while loading.

```html
<img src="./images/dog.jpg" alt="A golden retriever playing" width="400" height="300">
```

---

## Image Formats

Choosing the right format significantly impacts site speed and quality.

| **Format** | **Best For…** | **Supports Transparency?** |
| --- | --- | --- |
| **JPG** | Photos and complex gradients. Small file size. | No |
| **PNG** | Logos, icons, and technical diagrams. | Yes |
| **SVG** | Vector graphics. Scales to any size without losing quality. | Yes |
| **GIF** | Simple animations and very simple color palettes. | Yes (Limited) |

---

## Practice Project Structure

Maintain this structure in your `odin-links-and-images` folder to keep your paths organized:

- `index.html` (Main entry)
- `images/` (Folder for `dog.jpg`)
- `pages/` (Folder for `about.html`)