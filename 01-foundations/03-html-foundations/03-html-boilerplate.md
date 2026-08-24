# HTML Boilerplate

## The Setup

1. Create a folder named `html-boilerplate`.
2. Inside, create a file named `index.html`.

Web servers are programmed to look for `index.html` as the “home” or default page. If you name it anything else, the server might not know where to start, leading to errors.

---

## The Boilerplate Breakdown

Every HTML5 document requires a specific structure to function correctly.

### 1. The Declaration

`<!DOCTYPE html>` - Tells the browser: “Hey, this is a modern HTML5 document.” (Older versions had much messier declarations!)

### 2. The Root Element

`<html lang="en">` - The container for everything else.

- The `lang="en"` attribute tells screen readers and search engines that the primary language is English, ensuring correct pronunciation and indexing.

### 3. The `<head>` (Behind the Scenes)

Contains metadata **about** the page. Nothing here is visible on the actual webpage.

- `<meta charset="UTF-8">`: Ensures special characters and symbols display correctly.
- `<title>`: Sets the name shown on the browser tab.

### 4. The `<body>` (The Visible Stage)

Everything you want the user to see (text, images, buttons) goes here.

---

## The Full Template

Copy this into your `index.html`:

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8">
		<title>My First Webpage</title>
	</head>
	<body>
		<h1>Hello World!</h1>
	</body>
</html>
```

---

## How to View Your work

Once you’ve saved your file, use one of these three methods to see it in action:

1. **Drag & Drop:** Drag the file from your folder into a browser tab.
2. **Double-Click:** Find the file in your system and open it (it will use your default browser).
3. **Terminal:** Navigate to the folder and type `google-chrome index.html`.

---

## The VS Code Pro Shortcut

VS Code has a built-in tool called `Emmet:`

1. Open a blank `.html` file.
2. Type `!` and press **Enter**.
3. VS Code will instantly generate the entire boilerplate for you.

You’ll see a line about `viewport`. This is used for **Responsive Design** (making your site look good on phones). You can safely ignore it for now!