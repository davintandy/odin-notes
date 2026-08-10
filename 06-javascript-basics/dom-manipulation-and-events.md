# DOM Manipulation and Events

## Prerequisites: Functions & Callbacks

A **callback** is simply a function passed as an argument into another function to be executed later.

### Function Syntaxes Compared

```jsx
// 1. Function Declaration (Named)
function playMusic(track) {
	return `Playing: ${track}`;
}

// 2. Function Expression (Anonymous function assigned to variable)
const playMusic = function(track) {
	return `Playing; ${track}`;
};

// 3. Arrow Function (Concise syntax)
const playMusic = (track) => `Playing: ${track}`;
```

### Arrow Function Rules

- **Single parameter:** Parentheses `()` are optional (`track => ...`).
- **No parameters:** Parentheses `()` are **required** (`() => “Playing music”`).
- **Single-line body:** Brackets `{}` and `return` keyword can be omitted for implicit returns.

## How Callbacks Work Under the Hood

### Array Iterator (`forEach`, `map`)

```jsx
// Custom implementation of Array.prototype.forEach
function myForEach(array, callback) {
	for (let i = 0; i < array.length; i++) {
		callback(array[i], i); // Invokes the callback for each item
	}
}

// Usage with an inline arrow function
myForEach(["do", "re", "mi"], (item) => console.log(item));

// Usage with a named function reference
function logItem(item) {
	console.log(item);
}
myForEach(["do", "re", "mi"], logItem); // Pass reference, DO NOT invoke with ()
```

### Asynchronous Event Listeners

```jsx
const btn = document.querySelector("#myBtn");

// The browser executes the callback function when the "click" event occurs. passing the Event object automatically as its argument.
btn.addEventListener("click", (event) => {
	console.log("Clicked target:", event.target);
});
```

## DOM Architecture & Script Timing

The **Document Object Model (DOM)** is a tree representation of an HTML document where every element is a programmable JS object node.

```
       HTML
        │
      Body
    ┌───┴───┐
   h1      div#container
           ┌───┴──────────────┐
     div.display        div.controls
    (first child)      (sibling)
```

### Script Execution Timing

Executing DOM selection scripts before HTML elements are loaded into memory returns `null`.

```html
<!-- RECOMMENDED: Parses asynchronously and executes ONLY after HTML parsing completes -->
<head>
	<script src="app.js" defer></script>
</head>
<!-- ALTERNATIVE: Place scripts at the very bottom of the <body> -->
```

## Selecting & Navigating Nodes

| **Method** | **Returns** | **Description** |
| --- | --- | --- |
| `document.querySelector(selector)` | `Element` | `null` | Returns the **first** matching node |
| `document.querySelectorAll(selector)` | `NodeList` | Returns **all** matching nodes |

```jsx
// CSS Selector Variations
const display = document.querySelector(".display");
const displayInContainer = document.querySelector("#container > .display");

// Relationship Navigation
const controls = document.querySelector(".controls");
const prevSibling = controls.previousElementSibling; // <div class="display"></div>
const parent = controls.parentElement; // <div id="container></div>
```

> 
> 
> 
> ### `NodeList` vs. `Array` Gotcha
> 
> `querySelectorAll` returns a static `NodeList`. While it supports `.forEach()`, it lacks array methods like `.map()`, `.filter()`, or `.reduce()`.
> 
> ```jsx
> const nodeArray = Array.from(document.querySelectorAll("div"));
> // OR using spread syntax
> const nodeArray = [...document.querySelectorAll("div")];
> ```
> 

## DOM CRUD & Element Manipulation

### Element Creation & Placement

```jsx
// 1. Create in memory
const newDiv = document.createElement("div");

// 2. Append or Insert
const container = document.querySelector("#container");
const controls = document.querySelector(".controls");

container.appendChild(newDiv); // Appends as LAST child
container.insertBefore(newDiv, controls); // Inserts before reference node

// 3. Remove
container.removeChild(newDiv); // Removes & returns reference node
```

### Attributes, Classes, & Styles

```jsx
const div = document.createElement("div");

// Attributes
div.setAttribute("id", "main-card"); // Set attribute
div.getAttribute("id"); // Read attribute ("main-card")
div.removeAttribute("id"); // Removes attribute

// Classes
div.classList.add("card", "active"); // Add class(es)
div.classList.remove("active"); // Remove class
div.classList.toggle("hidden"); // Toggle class (returns boolean)

// Styles
div.style.color = "blue";
div.style.backgroundColor = "black"; // camelCase required for inline styles
```

### Content Updates: `textContent` vs `innerHTML`

```jsx
// PREFERRED: Safe, fast, escapes HTML strings
div.textContent = "<span>Hello World!</span>";
// Output string: <span>Hello World!</span>

// CAUTION: Parses string as HTML (Potential XSS vulnerability)
div.innerHTML = "<span>Hello World!</span>";
// Output element: Hello World!
```

## Event Registration & Flow Control

An **Event** is a browser signal indicating a user or system action (click, keypress, submit).

### Registration Patterns

| **Pattern** | **Example Syntax** | **Assessment** |
| --- | --- | --- |
| **Inline HTML** | `<button onclick="alert('Hi')">` | Clutters markup; limits to 1 handler |
| **DOM Property** | `btn.onclick = () => alert('Hi');`  | Clean JS; **overwrites** existing handlers |
| **Event Listener** | `btn.addEventListener("click", fn)`  | **Best Practice**. Supports multiple listeners |

```jsx
const btn = document.querySelector("#btn");

// Binding via Event Listener
btn.addEventListener("click", () => alert("Clicked!");

// Reusable Named Handlers
function handleClick(event) {
	console.log(`Clicked element ID: ${event.target.id}`);
}
btn.addEventListener("click", handleClick);

// Binding Listeners across a Node Group
const buttons = document.querySelectorAll("button");
buttons.forEach((button) => {
	button.addEventListener("click", (e) => alert(`Clicked: ${e.target.id}`));
});
```

### DOM Level 2 Event Flow

Nested DOM events propagate through **3 distinct phases**:

```
[Phase 1: Capturing]           [Phase 2: Target]          [Phase 3: Bubbling]
document ──┐                                                      ┌──► document
  html     │                                                      │     html
   body    ▼                                                      │      body
    div  ──────► [ <button id="btn"> ] (Target Reached) ──────────┘       div
```

1. **Capturing Phase (1):** Event moves downward from `document` through parents to the target node.
2. **Target Phase (2):** Event hits the actual target node (`e.target`).
3. **Bubbling Phase (3):** Event propagates back upward through parent nodes to `document`.

### The Event Object (`e`)

| **Member** | **Type** | **Purpose** |
| --- | --- | --- |
| `e.target` | `Element` | The exact node where the event originated |
| `e.currentTarget`  | `Element` | The element handling the current listener |
| `e.type` | `string` | Event name (e.g., `"click"`, `"keydown"`) |
| `e.eventPhase` | `number` | `1` (Capture), `2` (Target), `3` (Bubble) |
| `e.preventDefault()` | `method` | Cancels default browser behavior (e.g., link redirects, form reloads) |
| `e.stopPropagation()` | `method` | Halts event movement through subsequent DOM propagation phases |

```jsx
// Prevent Default
document.querySelector("a").addEventListener("click", (e) => {
	e.preventDefault(); // Prevents link navigation
});

// Stop Propagation
document.querySelector("#btn").addEventListener("click", (e) => {
	e.stopPropagation(); // Stops event from bubbling to parent containers
});
```

## Deep Dive: Mouse Events

### Types & Behavior

| **Event** | **Triggers When…** | **Note** |
| --- | --- | --- |
| `mousedown` | Mouse button is pressed down | Part of click sequence |
| `mouseup` | Mouse button is released | Part of click sequence |
| `click` | `mousedown` + `mouseup` complete on same element | Standard click action |
| `dblclick` | Double click detected | Fires after two `click` sequences |
| `mousemove` | Mouse moves across an element | Fires repeatedly (can impact performance) |
| `mouseenter` | Mouse enters element | Does **NOT** bubble |
| `mouseleave` | Mouse leaves element | Does **NOT** bubble |
| `mouseover` | Mouse enters element or any child | **Bubbles** upward |
| `mouseout` | Mouse leaves element or any child | **Bubbles** upward |
| `wheel` | Mouse wheel or touchpad is scrolled | Returns delta values via `e.deltaY`  |

```
Click Sequence: mousedown -> mouseup -> click
Double Click Sequence: mousedown -> mouseup -> click -> mousedown -> mouseup -> click -> dblclick
```

> 
> 
> 
> **Performance Tip:** Unbind or throttle `mousemove` handlers when active tracking is complete to avoid layout trashing.
> 
> ```jsx
> element.onmousemove = handleMove;
> element.onmousemove = null; // Unbind when done
> ```
> 

### Mouse Buttons & Coordinates

```jsx
// Detecting Mouse Buttons (e.button)
// 0: Left, 1: Middle/Wheel, 2: Right, 3: Back, 4: Forward
btn.addEventListener("mousedown", (e) => {
	console.log(`Button pressed: ${e.button}`);
});

// Position Coordinates
// e.clientX / e.clientY -> Relative to browser viewport
// e.screenX / e.screenY -> Relative to physical monitor screen
```

## Deep Dive: Keyboard Events

Keyboard events fire primarily on focusable elements (`<input>`, `<textarea>`, or elements with `tabindex`).

### Keyboard Event Types & Firing Sequence

- **Character Keys (`a`, `5`, `Enter`):** `keydown` → `keypress` (deprecated) → DOM updates → `keyup`
- **Non-Character Keys (`Shift`, `Escape`):** `keydown` → `keyup`

> **Timing Rule:** `keydown` fires **before** the input value updates in the DOM. `keyup` fires **after** the DOM value has updated.
> 

### Key Identification (`e.key` vs `e.code`)

```jsx
const textBox = document.getElementById("message");

textBox.addEventListener("keydown", (e) => {
	// e.key: Printed character value (e.g., "z" or "Z" based on Shift/Caps)
	console.log(`Character Value (key): ${e.key}`);
	// e.code: Physical key location on keyboard (e.g., "KeyZ", "ShiftLeft")
	console.log(`Physical Key (code): ${e.code}`);
});
```

## Deep Dive: Event Delegation

**Event Delegation** leverages **event bubbling** to manage events efficiently by attaching a single event listener to a parent container rather than multiple listeners to individual child elements.

```html
<ul id="menu">
	<li><a id="home">Home</a></li>
	<li><a id="dashboard">Dashboard</a></li>
	<li><a id="report">Report</a></li>
</ul>
```

### Optimized Delegation Approach

Instead of attaching 3 separate listeners, attach **one** listener to `#menu`:

```jsx
const menu = document.querySelector("#menu");

menu.addEventListener("click", (e) => {
	const target = e.target; // The exact element clicked
	
	switch (target.id) {
		case "home":
			console.log("Home menu item clicked");
			break;
		case "dashboard":
			console.log("Dashboard menu item clicked");
			break;
		case "report":
			console.log("Report menu item clicked");
			break;
	}
});
```

### Why Use Delegation?

- **Reduced Memory:** Fewer function objects in memory.
- **Dynamic Elements:** Automatically handles elements added to the DOM after page load.

## Synthetic & Custom Events

### Programmatic Events (`dispatchEvent`)

```jsx
const btn = document.querySelector(".btn");

btn.addEventListener("click", (e) => {
	console.log(`Was event user generated? ${e.isTrusted}`);
});

// Programmatically simulate a click
const clickEvent = new MouseEvent("click", {
	bubbles: true,
	cancelable: true,
	clientX: 150,
	clientY: 150
});

btn.dispatchEvent(clickEvent); // e.isTrusted will be FALSE
```

### Custom Events (`CustomEvent`)

`CustomEvent` allows you to create event-driven communication between application modules, using the `detail` property to pass custom data payloads.

```jsx
// Function that performs an action and dispatches a custom event
function highlight(elem) {
	const bgColor = "yellow";
	elem.style.backgroundColor = bgColor;
	
	// Create CustomEvent with detail payload
	const markEvent = new CustomEvent("mark", {
		bubbles: true,
		detail: { backgroundColor: bgColor }
	});
	
	elem.dispatchEvent(markEvent);
}

// Attach listener for the custom "mark" event
const noteDiv = document.querySelector(".note");

noteDiv.addEventListener("mark", (e) => {
	e.target.style.border = "1px solid red";
	console.log("Custom payload received:", e.detail.backgroundColor);
});

// Trigger action
highlight(noteDiv);
```