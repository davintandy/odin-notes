# Understanding Errors

## High-Level Classifications: Errors vs. Warnings

Not every issue in the console carries the same weight. Understanding the distinction between categories and operational states prevents wasted debugging cycles.

### Operational Severity

| **Type** | **Severity** | **Execution Impact** | **Visual Indicator** | **Core Characteristic** |
| --- | --- | --- | --- | --- |
| **Error** | Critical | **Halts** execution entirely | Red | The engine cannot proceed with the current call stack |
| **Warning** | Informational | **Continues** execution | Yellow | Highlights potential bugs, optimizations, or deprecations without crashing |

### The Three Execution Classifications

- **Syntax Errors:** Grammatical violations of the JavaScript language rules. Discovered during the parsing phase **before** the code executes. The program will typically fail to launch entirely.
- **Runtime Errors:** Safe syntactical code that encounters an impossible operation during execution (e.g., trying to invoke a variable that resolves to `undefined`).
- **Logic Errors:** Syntactically perfect code that runs completely without throwing an error, but produces incorrect calculations or behavior. These are the hardest to detect because the engine offers no console feedback.

## Anatomy of a Native Error Object

In JavaScript, an error is a built-in object consisting of a structural metadata payload. When an invalid operation occurs, the engine **throws** this object instance.

### Core Error Metadata

```
Uncaught ReferenceError: b is not defined
	at script.js:2:13
```

- **Error Name / Type:** `ReferenceError` - Identifies the structural category of the error.
- **Error Message:** `b is not defined` - Human-readable description explaining why the failure occurred.
- **File Identity:** `script.js` - The target script containing the problematic logic.
- **Line & Column Numbers:** `2:13` - The exact location of the error (Line 2, Character/Column 13). Clicking this link in browser developer tools jumps directly to the source code layout.

### The Execution Stack Trace

A stack trace provides a chronological roadmap of function invocations leading up to the unhandled exception. It reads from **top to bottom** (Last-In, First-Out sequence).

```jsx
function add() {
	return c; // 'c' is unallocated state
}

function print() {
	add();
}

print();
```

When this snippet runs, it generates the following trace stack:

```
Uncaught ReferenceError: c is not defined
	at add (script.js:2:10)
	at print (script.js:6:3)
	at script.js:9:1
```

### Tracing the Execution Lifecycle:

1. The error occurs inside scope `add()` at line 2.
2. `add()` was originally called inside scope `print()` at line 6.
3. `print()` was originally invoked in the global execution context at line 9.

## Native JavaScript Error Types

While there are many built-in error instances, these three represent the vast majority of web development exceptions.

### `SyntaxError`

Thrown when code breaks the syntactic structural rules of the language.

```jsx
// Missing invocation parentheses
function helloWorld() {
	console.log "Hello World!";
}
// Uncaught SyntaxError: Unexpected string
```

### `ReferenceError`

Thrown when attempting to access a variable that has not been declared or initialized within the current scope boundaries.

```jsx
const a = "Hello World";
console.log(b);
// Uncaught ReferenceError: b is not defined
```

### `TypeError`

Thrown when an operation or method is performed on an incompatible data type, or when modifying an immutable value.

```jsx
const str1 = "Hello";
const str2 = "World!";

// .push() is an exclusive Array prototype method, invalid on a String type
const message = str1.push(str2);
// Uncaught TypeError: str1.push is not a function
```

**Debugging Rule:** When debugging a `TypeError`, always look directly to the left of the method or property. Verify that the runtime data type matches your expected architectural assumptions.

## Professional Debugging Workflow

### Essential Console Utilities

Move beyond basic `console.log()` outputs to extract cleaner contextual data from the engine.

- `console.table()`: Renders arrays of objects or complex structured objects into a clean, sortable tabular matrix. Highly readable for data arrays.
- `console.trace()`: Explicitly dumps a snapshot of the current call stack trace at that exact moment in execution without needing to throw a formal error.

### Systematic Action Framework

1. **Adopt a Diagnostic Mindset:** View error messages as precise technical readouts. They explicitly declare what failed and where the breakdown occurred.
2. **Isolate with Breakpoints:** Open browser Developer Tools (`Sources` tab) and utilize the interactive debugger. Set line breakpoints to pause execution states, inspect variable allocations live, and step through routines manually.
3. **Isolate Code Search:** If you hit an impasse, leverage search engines or documentation. Avoid searching for your entire master logic implementation; isolate your queries to exact error signatures or targeted sub-problems (e.g., `TypeError: cannot read properties of undefined"`).