# JavaScript Developer Tools

Chrome DevTools is a powerful built-in suite for debugging JavaScript, optimizing page performance, and mutating the DOM and CSS in real-time.

## Global Workflows & The Console REPL

### Opening DevTools

- **Menu:** `Chrome Menu` > `More Tools` > `Developer Tools`
- **Mouse:** Right-click anywhere on a webpage > **Inspect**
- **Keyboard:** `F12` or `Ctrl` + `Shift` + `I`

Press `Esc` inside any panel to toggle the **Console Drawer** at the bottom of the screen to run quick scripts or look up elements instantly.

### Element Targeting

- **Target Mode:** Click the **Inspect Element Arrow** (`Ctrl + Shift + C`) at the top-left of DevTools, then click any viewport element.
- **Console Reveal:** Run a query in the Console (e.g., `document.querySelector('p')`), right-click the returned node, and select **Reveal in Elements panel**.
- **Show Rulers:** Open the Command Menu (`Ctrl + Shift + P`), type `Show rulers on hover`, and press `Enter`. This displays a pixel grid in the viewport when hovering elements in the DOM tree.

### The Interactive Console (Logging & REPL)

The Console serves as both a diagnostic log and a live **REPL** (Read-Eval-Print Loop):

- **Execution Context:** The Console has full access to the page’s `window` object and execution context, allowing you to manipulate live data, call in-scope functions, or test independent JavaScript snippets.
- **Diagnostic Logging:** Use `console.log()` statements to audit execution order and inspect variable states at specific execution moments without freezing the browser thread.

## DOM Tree Navigation & Live Editing

The DOM Tree inside the **Elements** panel handles all live structural manipulation.

### Keyboard Navigation

With a DOM node selected:

- `Left Arrow`: Collapses the current node or jumps up to its parent.
- `Right Arrow`: Expands a collapsed node.
- `Ctrl + F`: Opens the search pane at the bottom of the DOM Tree to query by string, CSS selector, or XPath.

### Live Content Mutators

- **Quick-Edit:** Double-click any text string, attribute name, or element tag (e.g., changing `<div>` to `<section>`) to modify it instantly. Press `Enter` to save.
- **Edit as HTML:** Right-click a node > **Edit as HTML** to open an editor pane with syntax highlighting and autocomplete. Press `Ctrl + Enter` to apply.
- **Structure Tweaks:**
    - **Reorder:** Click and drag any node up or down within the tree hierarchy.
    - **Duplicate:** Right-click a node > **Duplicate element** (Shortcut: `Shift + Alt + Down`).
    - **Hide:** Select a node and press `H` (or right-click > **Hide element**). This toggles `visibility: hidden` and applies a `__web-inspector-hide-shortcut__` indicator.
    - **Delete:** Select a node and press `Delete`. Press `Ctrl + Z` to instantly undo.
- **Scroll into View:** Right-click an out-of-bounds node in the tree and select **Scroll into view** to snap the viewport straight to that element.
- **Capture Screenshot:** Right-click any specific node and select **Capture node screenshot** to download an isolated graphic render of that element.

## CSS Mastery: Styles vs. Computed Panels

### The Styles Tab

Lists all CSS rules matching the selected node, including overridden styles (which appear crossed out).

- **Source Links:** Click the file links next to any rule to view the raw source declaration inside the **Sources** tab.
- **Metadata Tooltips:** Hover over a CSS selector to view its calculated **Selector Specificity Weight.**
    - Hover over a `--custom-property` variable to view its evaluated value.
    - Hover over a standard property name to view an inline MDN reference card.

### The Computed Tab

Strips away cascade rules and lists only the single, final computed style property actively rendering on the screen.

- Check **Show All** to include hidden inherited browser user-agent defaults.
- Check **Group** to sort active properties into clean, collapsible categories (Layout, Text, Background, etc.).
- Properties are displayed in strict alphabetical order for fast filtering.

## Dynamic CSS Manipulation & Graphic Editors

### Value Stepping Shortcuts

When editing a numeric CSS value (e.g., `font-size: 14px`), use these keyboard shortcuts to increment or decrement values:

- `Alt + Up / Down` > Change by 0.1
- `Up / Down` > Change by 1
- `Shift + Up / Down` > Change by 10
- `Ctrl + Shift + PageUp / PageDown` > Change by 100

### Managing Element Rules & Classes

- **Add Rules:** Click **New Style Rule (`+`)** to craft a fresh selector block, or long-press it to target a specific stylesheet file.
- **Toggle Declarations:** Hover over an active rule and check or clear the checkbox next to individual declarations to toggle them on or off. Disabled parameters are struck through.
- **`.cls` (Class Manager):** Opens an interactive text input to append new classes to the active element, providing toggle checkboxes to quickly swap them on or off.

### Built-In CSS Graphic Editors

Look for these preview icons next to property definitions inside the **Styles** tab to open visual adjustment widgets:

- **Box Model Diagram:** Click the **Show sidebar** button in the Styles tab action bar to reveal the interactive Box Model diagram. Hovering over layers highlights padding, margins, and borders in the live viewport. Double-click any edge boundary to alter its dimensions directly.
- **Angle Clock:** Click the circle icon next to a `transform: rotate()` or gradient rule to alter angles with an interactive clock dial.
- **Shadow Editor:** Click the shadow box icon next to `text-shadow` or `box-shadow` properties to visually tweak X/Y offsets, blur, spread, and inset configurations.
- **Easing Editor:** Click the purple wave icon next to animation or transition timing functions to adjust Cubic Bezier acceleration curves manually, execute preset templates, or track transitions via this mapping table:

| **Timing Keyword** | **Preset Style** | **Cubic Bezier Definition** |
| --- | --- | --- |
| `ease-in-out` | Fast Out, Slow In | `cubic-bezier(0.4, 0, 0.2, 1)` |
| `ease-in-out` | In Out, Cubic | `cubic-bezier(0.65, 0.05, 0.36, 1)` |
| `ease-in` | In, Quadratic | `cubic-bezier(0.55, 0.09, 0.68, 0.53)` |
| `ease-out` | Out, Back | `cubic-bezier(0.18, 0.89, 0.32, 1.28)` |

## The Breakpoint Matrix

The **Sources** panel features multiple dedicated breakpoint types to automatically halt execution for distinct debugging scenarios.

### Line-of-Code Breakpoints

- **UI Breakpoint:** Open a script file in the **Sources** panel and click any line number column on the left. A blue icon indicates execution will freeze before that line runs.
- **Hardcoded Breakpoint:** Write `debugger;` explicitly inside your code. Execution automatically halts on this statement if DevTools is open.

```jsx
console.log('a');
debugger; // DevTools pauses on this line
console.log('b');
```

### Advanced Code Breakpoints

- **Conditional Breakpoints:** Right-click a line number column > **Add conditional breakpoint…** Provide a truthy expression. Execution will only freeze if your condition resolves to true (ideal for deep arrays or loops).
- **Logpoints:** Right-click a line number column > **Add logpoint…** Type an evaluation string (e.g., `"Value: " + obj.id`). This logs data directly to the Console without halting execution or polluting your codebase with permanent logs. (Indicated by a pink icon).
- **Never Pause Here:** Right-click a line number > **Never pause here**. This injects a conditional breakpoint with a `false` condition to mute noisy exceptions or debugger statements on that specific line.
- **Function Breakpoints:** Execute `debug(functionName)` within your Console drawer. The browser automatically pauses execution on the first internal line of that targeted function whenever it is called.

```jsx
function sum(a, b) {
	let result = a + b; // Pauses right here if debug(sum) is active
	return result;
}
debug(sum); // Pass the function reference object
```

The target function must be in active scope. If it is wrapped in an IIFE or closure, set a standard breakpoint inside that scope first, then execute `debug()` inside the console while execution is paused.

### Structural & Event Breakpoints

- **DOM Change Breakpoints:** Right-click any node in the DOM tree > **Break on** and choose your criteria:
    - **Subtree modifications:** Pauses when child elements are appended, removed, or have text content edited.
    - **Attribute modifications:** Pauses if an attribute key or value changes on the targeted node.
    - **Node removal:** Pauses if the element is purged from the DOM.
- **XHR/Fetch Breakpoints:** Found in the right side pane of the Sources panel. Click **Add breakpoint** (`+`) and input a URL string identifier. DevTools will freeze execution the instant an HTTP network request containing that string calls `.send()`.
- **Event Listener Breakpoints:** Expand the event pane on the right side of the Sources panel. Check categorical boxes (e.g., `Mouse > click`, `Animation`) to pause script execution on the exact line of an event handler execution block.

### Error & Security Breakpoints

- **Exception Breakpoints:** Check **Pause on uncaught exceptions** or **Pause on caught exceptions** inside the Sources panel sidebar. DevTools automatically breaks on synchronous or asynchronous promise rejections.
- **Trusted Type Breakpoints:** Located under **CSP Violation Breakpoints**. Check Sink Violations or Policy Violations to trap malicious data pathways before they hit execution sinks (like `eval()` or `.innerHTML`).

## Tracing Code Execution & State Inspection

### Tracing Controls Cheat Sheet

When paused on any breakpoint, use the controls at the top of the right panel to step through execution:

| **Action** | **Shortcut** | **Description** |
| --- | --- | --- |
| **Resume** | `F8` | Resumes execution until the next breakpoint is hit |
| **Step** | `F9` | Runs the next line of code (steps into nested function internals) |
| **Step Over** | `F10` | Runs the next line of code (skips over evaluation function internals) |
| **Step Into** | `F11` | Steps inside asynchronous or scheduled blocks (e.g., `setTimeout`) |
| **Step Out** | `Shift + F11` | Executes the rest of the current function and pauses at its exit line |

### Inspecting State

- **Scope Pane:** Displays variables segmented by Local, Closure, and Global environments. Evaluated properties are also superimposed inline directly next to your code inside the editor view.
- **Watch Pane:** Click `+` to add arbitrary code variables or expressions. DevTools re-evaluates these tracking metrics dynamically as you step through breakpoints.
- **Call Stack Pane:** Displays the history path of functions leading up to the current breakpoint block. Click any stack item to look back at the historical execution context.
- **Managing Breakpoint Lists:** The **Breakpoints** pane aggregates your configurations by file name. Toggle checkboxes to quickly enable/disable entries, or right-click the file grouping to select deep-clean commands like Remove all breakpoints in file.

## Referencing DOM Nodes inside the Console

DevTools exposes several direct variable tokens to pass nodes from your layout straight into JavaScript code:

- **The `$0` Token:** Whichever node is actively highlighted inside your DOM tree is automatically bound to the global variable `$0`. Open your Console drawer and run operations like `$0.getBoundingClientRect()` or `$0.classList`.
- **Store as Global Variable:** Right-click a node inside your DOM tree > **Store as global variable**. DevTools creates a sequential global reference (e.g., `temp1`, `temp2`) accessible anywhere in the Console context.
- **Copy JS Path:** Right-click a node > **Copy** > **Copy JS Path**. This saves an explicit, native `document.querySelector("...")` selector query to your clipboard, built for use in testing suites or validation scripts.

## Advanced Layout Emulations & Media Testing

- **Emulate a Focused Page:** Open the Styles pane, click the `:hov` tab, and check **Emulate a focused page**. This locks volatile components (like focus dropdowns, date-pickers, or popovers) open on your display screen even when you click away into DevTools.
- **Force Pseudo-Classes:** Toggle checkboxes under the `:hov` section to lock the active node layout into explicit mock behaviors like `:hover`, `:active`, or `:focus`.
- **Theme Preference Emulations:** Click the **Toggle common rendering emulations** shortcut inside the Styles action bar to simulate `prefers-color-scheme: dark` or evaluate an automatic dark-mode rendering script instantly.
- **Print Layout Emulation:** Open the Command Menu (`Ctrl + Shift + P`), search for `Show Rendering`, and set **Emulate CSS Media** to `print` to evaluate print sheets.
- **CSS Coverage Tab:** Open the Command Menu, launch `Show Coverage`, and click reload. DevTools analyzes assets line by line, providing a color-coded bar chart highlighting exactly how much CSS/JS is actively used (green) versus unused (red).

## Exporting and Copying CSS Assets

Right-click any property definition inside the **Styles** tab to extract formatting options using the reference grid:

| **Context Menu Action** | **Syntax Example Output** | **Ideal Implementation** |
| --- | --- | --- |
| **Copy declaration** | `background-color: red;`  | Standard style sheets |
| **Copy property** | `background-color`  | Isolating specific properties |
| **Copy value** | `red`  | Copying custom variables or metrics |
| **Copy rule** | `h1 { background-color: red; }`  | Copying a complete selector block |
| **Copy declaration as JS** | `backgroundColor: 'red'`  | JavaScript style definitions |
| **Copy all declarations** | `background-color: red; margin: 10px;`  | Transferring block contents |
| **Copy all declarations as JS** | `backgroundColor: 'red', margin: '10px'` | React inline layouts / Emotion configs |
| **Copy all CSS changes** | Compiles modified adjustments | Exporting live modifications |