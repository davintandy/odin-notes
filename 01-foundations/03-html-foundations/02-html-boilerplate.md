# HTML Boilerplate

## What is HTML Boilerplate?

**HTML boilerplate** is the standard starting structure of an HTML document. It contains the essential elements that help browsers interpret and display a webpage correctly.

Every new HTML page should begin with a proper document structure before you add its content.

## Creating an HTML File

1. Create a project folder named `html-boilerplate`.
2. Create a file inside it named `index.html`.

The `.html` extension identifies the file as an HTML document.

### Why `index.html`?

`index.html` is the conventional filename for a website’s homepage. Web servers commonly look for this file as the default entry point when someone visits a directory on a website.

## The Basic HTML Boilerplate

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8">
		<meta name="viewport" content="width=device-width, initial-scale=1.0">
		<title>My First Webpage</title>
	</head>
	
	<body>
		<h1>Hello World!</h1>
	</body>
</html>
```

### Breakdown of the Boilerplate

### `<!DOCTYPE html>`

Declares that the document uses modern HTML.

- Must appear at the beginning of the document.
- Tells the browser to render the page using modern HTML standards rather than legacy quirks mode.

### `<html lang="en">`

The `<html>` element is the **root element** of the document. All other HTML elements belong inside it.

- `lang="en"` is an attribute specifying that the document’s primary language is English.
- Helps screen readers and other assistive technologies interpret the language and pronunciation correctly.
- Change `"en"` to the appropriate language code when necessary.

### `<head>`

Contains metadata and information used by the browser about the document.

It commonly includes the character encoding, page title, viewport settings, and references to stylesheets or other resources.

The `<head>` content is generally not displayed as the page’s main visible content.

### `<meta charset="UTF-8"?>`

Specifies the document’s character encoding.

- UTF-8 supports a wide range of characters and symbols.
- Helps prefent text from displaying incorrectly because of character-encoding issues.

### `<meta name="viewport" content="width=device-width, initial-scale=1.0">`

- `width=device-width` sets the viewport width to the device’s width.
- `initial-scale=1.0` sets the initial zoom level to 100%.

This is especially important for responsive webpages viewed on mobile devices.

### `<title>My First Webpage</title>`

Defines the document’s title, usually displayed in the browser tab.

```html
<title>My Portfolio</title>
```

The title is different from a visible heading such as `<h1>`. It identifies the webpage in the browser rather than displaying the page’s main content.

### `<body>`

Contains the content displayed to users, such as:

- Headings and paragraphs.
- Images and links.
- Lists and other page elements.

For example:

```html
<body>
	<h1>Hellow World!</h1>
	<p>This is my first webpage.</p>
</body>
```

## Understanding the Document Structure

The HTML document follows a hierarchical structure:

```
HTML Document
├── <!DOCTYPE html>
└── <html>
    ├── <head>
    │   ├── <meta charset="UTF-8">
    │   ├── <meta name="viewport">
    │   └── <title>
    └── <body>
        ├── <h1>
        └── <p>
```

The `<head>` and `<body>` elements are children of `<html>`, while elements such as `<title>` and `<h1>` belong in their respected sections.

## Viewing an HTML File in the Browser

HTML files can be opened directly in a web browser without deploying them to a server.

### Method 1: Open the File Directly

1. Save `index.html`.
2. Locate the file using File Explorer.
3. Double-click it to open it in your default browser.

### Method 2: Open It Through the Browser

1. Open your browser.
2. Press `Ctrl + O`.
3. Locate and select `index.html`.

### Testing Changes

1. Edit the HTML file in your code editor.
2. Save the file.
3. Return to the browser.
4. Refresh the page to see the latest changes.

If the `<body>` is empty, the browser may display a blank page even though the HTML document is valid.

## Generating Boilerplate in VS Code

Visual Studio Code can automatically generate the standard HTML boilerplate using Emmet.

1. Create or open a file with the `.html` extension.
2. Ensure VS Code recognizes the file as HTML.
3. Type `!` on an empty line.
4. Select the Emmet abbreviation suggestion, usually by pressing `Enter`.
5. Save the generated HTML.

VS Code typically generates the document structure, including the `DOCTYPE`, `<html>`, `<head>`, `<body>`, character encoding, viewport settings, and a default title.

You can then replace the default title and add your own content.

> **Tip**: You do not need to memorize every line immediately. Learn what each part does so that you can recognize and modify the boilerplate when needed.
> 

## Validating HTML

An HTML validator checks your markup for errors and potential problems.

The W3C Markup Validation Service can help identify issues such as:

- Missing or incorrectly nested tags.
- Invalid attributes.
- Incorrect HTML syntax.
- Other markup errors that may be difficult to notice manually.

Validation is useful when learning because it helps you recognize mistakes and write more reliable HTML.