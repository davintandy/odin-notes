# Inspecting HTML and CSS

## Accessing the Toolkit

### Keyboard Shortcuts

| **Target** | **Shortcut** | **Mnemonic** |
| --- | --- | --- |
| **Elements (CSS/DOM)** | `Ctrl + Shift + C` | **C** for **CSS** |
| **Console (JS)** | `Ctrl + Shift + J` | **J** for **JavaScript** |
| **Last Panel** | `Ctrl + Shift + I` / `F12` | **I** for **Inspector** |

### UI Access

- **Right-click:** Select **”Inspect”** on any element to jump directly to its code.
- **Auto-Open:** Run Chrome from your terminal with `--auto-open-devtools-for-tabs` to have it always ready for every new tab.

---

## Navigating the Elements Panel (The DOM)

The **Elements Panel** is a live view of the **DOM (Document Object Model)**.

- **Select Tool:** Click the icon in the top-left (`Ctrl + Shift + C`) to hover over the page and highlight nodes.
- **Search (`Ctrl + F`):** Find nodes using plain text, CSS selectors (e.g., `.container`), or XPath.
- **Scroll into View:** Right-click a node in the tree and select **Scroll into view** to find where it is on a long page.
- **Rulers:** Enable **”Show rulers on hover”** in Settings to see exact pixel dimensions in the viewport.

---

## Editing the DOM & Styles

The inspector is non-destructive. Refreshing the page wipes your changes, so it’s perfect for safe experimentation.

### Live DOM Editing

- **Content/Attributes:** Double-click any text, attribute, or tag type (e.g., change `<h1>` to `<h2>`) to edit it instantly.
- **Edit as HTML:** Right-click and choose **Edit as HTML** for full syntax highlighting.
- **Reorder & Duplicate:** Drag-and-drop nodes to move them. Use `Shift + Alt + Down Arrow` to duplicate a selected element.
- **Visibility:** Press `H` to hide a node, or `Delete` to remove it.

### The Styles Tab (CSS Control)

- **Add Declarations:** Click inside any selector to add a new property.
- **Toggle Classes (`.cls`):** Click the `.cls` button to manually add/remove classes and toggle them with checkboxes.
- **Force State (`:hov`):** Click the `:hov` button to force states like `:hover`.
- **Strikethrough Text:** This indicates the rule is being **overwritten** by the Cascade (specificity or rule order).

---

## DevTools Power-Use Features

### Referencing Nodes in the Console

- **`$0` Reference:** Type `$0` in the console to talk to the node currently selected in the Elements panel.
- **Global Variables:** Right-click a node > **Store as global variable** to reference it later as `temp1`, `temp2`, etc.
- **Copy JS Path:** Right-click > **Copy** > **Copy JS Path** to get the exact code needed for an automated test or script.
- **Capture Screenshot:** Right-click a node and select **Capture node screenshot** for a perfect, isolated image of that element.

### Advanced Panels Reference

| **Panel** | **Primary Use Case** |
| --- | --- |
| **Device Mode** | Simulates mobile screens and tablets. |
| **Console** | View logged messages and run/debug JavaScript. |
| **Sources** | Debug JS, save snippets, and map local files. |
| **Network** | View page load speed and API requests. |
| **Performance** | Diagnose slow animations or laggy scrolling. |
| **Application** | Inspect local storage, cookies, and cached data. |