# Function Basics

Functions are the core “building blocks” of JavaScript applications. They allow code to be grouped, isolated, structured, and executed multiple times without repetition.

## Core Anatomy & Execution Mechanics

A function encapsulates statements into an executable block. It can be a custom routine or a native browser API feature.

```jsx
// Function Declaration
function showMessage(parameter1, parameter2) {
	// Function Body (code to execute)
	console.log(parameter1 + " " + parameter2);
}

// Function Call (Invocation)
showMessage("Hello", "World");
```

### Functions vs. Methods

- **Function:** A standalone block of globally or locally scoped code called directly by its name (e.g., `draw()`).
- **Method:** A function stored inside an object property, invoked via dot notation (e.g., `console.log()` or `myText.replace()`).

### Inline Return Substitution

When a function resolves to a value, that return value is cleanly substituted directly at the exact location where the function was invoked before the rest of the execution line evaluates.

```jsx
function random(number) {
	return Math.floor(Math.random() * number);
}

// When the engine evaluates this line:
ctx.arc(random(100), random(200), random(50), 0, 2 * Math.PI);
// The engine executes the random() routines first, substituting their return values inline:
// ctx.arc(54, 122, 35, 0, 2 * Math.PI);
```

## Function Declarations vs. Function Expressions

There are two primary structural paradigms for creating traditional functions in JavaScript:

```jsx
// Function Declaration (Standalone Statement)
function sum(a, b) {
	return a + b;
}

// Function Expression (Created inside an assignment statement)
const sumExpression = function(a, b) {
	return a + b;
}; // Semicolon is required here as it terminates an assignment statement
```

### Structural Differences Matrix

| **Feature** | **Function Declaration** | **Function Expression** |
| --- | --- | --- |
| **Parsing Time** | Created before the script executes during the initialization stage | Created only when the execution thread explicitly reaches the line |
| **Hoisting** | **Yes**. Can be safely invoked anywhere within its parent scope before its definition line | **No**. Cannot be called before its explicit initialization line |
| **Block Scope (Strict Mode)** | Strictly confined to the enclosing code block (`if`, `for`, etc.) | Confined to the block scope of its declared variable (`let`/`const`) |

### Conditional Block-Scoping Mechanics

Under strict mode, Function Declarations are bound to the block code area where they are written. To declare a function conditionally, you **must** use a Function Expression:

```jsx
// BROKEN: Function Declaration is trapped in block scopes
let age = 18;
if (age >= 18) {
	function welcome() { console.log("Greetings!"); }
} else {
	function welcome() { console.log("Hello!"); }
}
welcome(); // Error: welcome is not defined

// CORRECT: Assigning Function Expressions to an outer scope variable
let welcome;
if (age >= 18) {
	welcome = function() { console.log("Greetings!"); };
} else {
	welcome = function() { console.log("Hello!"); );
}
welcome(); // Works flawlessly
```

## Functions as First-Class Values & Callbacks

In JavaScript, **functions are values**. They do not merely represent static syntax; the represent an executable “action” value that can be copied, passed around, and manipulated like numbers or strings.

### Copying Functions

Because functions are values, you can pass their references to other variables without executing them (by omitting the execution parentheses `()`):

```jsx
function sayHi() {
	console.log("Hello");
}

let func = sayHi; // Copies the reference. No parentheses

func(); // Logs "Hello"
sayHi(); // Logs "Hello"
```

### Callback Functions

A **callback** is a function passed into another function as an argument, intended to be “called back” or executed later when a condition is met.

```jsx
// Declaring a function that accepts two callback routines
function ask(question, yesCallback, noCallback) {
	if (confirm(question)) yesCallback();
	else noCallback();
}

// Passing anonymous function expressions directly as arguments
ask(
	"Do you agree?",
	function() { alert("You agreed."); },
	function() { alert("You canceled execution."); }
);
```

## Anonymous & Arrow Functions

### Anonymous Functions

Functions omitted of an explicit text identifier name are **anonymous functions**. They are used heavily as inline arguments, structural event handlers, and callbacks.

```jsx
// Anonymous function passed into a DOM event listener
textBox.addEventListener("keydown", function (event) {
	console.log(`You pressed "${event.key}".`);
});
```

### Arrow Functions (`=>`)

Arrow functions provide a clean, highly concise shorthand alternative to standard anonymous function expressions.

```jsx
// Standard Arrow Function
textBox.addEventListener("keydown", (event) => {
	console.log(`You pressed "${event.key}".`);
});

// Single-Parameter Shorthand (Parentheses around parameters can be omitted)
textBox.addEventListener("keydown", event => {
	console.log(`You pressed "${event.key}".`);
});

// Single-Line Implicit Return (Omit both the curly braces and the 'return' keyword)
const originals = [1, 2, 3];
const doubled = originals.map(item => item * 2); // Instantly evaluates to [2, 4, 6]
```

**Multiline Arrow Functions:** If your arrow function requires multiple lines of logic or statements, you must wrap the body inside curly braces `{}`. Once curly braces are used, you **must explicitly include** the `return` keyword to pass back a value.

```jsx
const sum = (a, b) => {
	let result = a + b;
	return result; // Required because curly braces are present!
};
```

## Variable Parameters vs. Arguments

Data inputs dictate how custom operations dynamically handle contextual processing variations.

| **Term** | **Context** | **Definition** |
| --- | --- | --- |
| **Parameter** | Declaration-time | The **placeholder variables** listed inside the function’s parentheses |
| **Argument** | Call-time | The **actual values** mapped into the function when it is invoked |

### Pass-by-Value (Copying Mechanics)

When primitive data types (strings, numbers, booleans) are passed into a function, they are passed by value. The function receives an isolated local **copy**. Mutating that parameter inside the inner scope will never alter the original variable residing on the outside.

```jsx
function secureName(from) {
	from = "*" + from + "*"; // Modifies internal local parameter copy only
}

let from = "Ann";
secureName(from);
console.log(from); // Outputs: "Ann" (original outer variable remains unchanged)
```

### Fallbacks & Default Parameters

If an expected argument is omitted during invocation, its respective parameter defaults to `undefined`. You can intercept this behavior to specify fallbacks:

```jsx
// Modern Syntax Default (Evaluates expression ONLY if the argument is omitted/undefined)
function showMessage(from, text = "no text given") {
	console.log(from + ": " + text);
}

// Legacy Falsy Fallback (Warning: Incorrectly overwrites valid falsy values like "" or 0)
text = text || "empty";

// Nullish Coalescing Fallback (Safe: Overwrites ONLY null or undefined inputs)
function showCount(count) {
	console.log(count ?? "unknown"); // 0 and false remains completely valid inputs here
}
```

## Variable Scoping & Namespace Conflicts

Scope rules govern where variables can be accessed or mutated within your application codebase.

### Local vs. Outer/Global Scope

- **Local Scope:** Variables declared inside a function are strictly local to that function. They are locked within that block boundary and cannot be reached from any outer parent execution context.
- **Global Scope:** Variables declared outside of any function block exist in the top-level global scope. They can be read or modified by any internal processing routines down the script tree.

### Variable Shadowing

If a local variable is declared with an identical name as an outer variable, it **shadows** the outer variable. The current context prioritizes the local version, hiding the outer reference without modifying it.

```jsx
let userName = "John"; // Outer/Global variable

function showMessage() {
	let userName = "Bob"; // Local variable shadows outer variable
	console.log(message); // Logs "Bob"
}

showMessage();
console.log(userName); // Logs "John" (unchanged in outer scope)
```

### Global Scope Collisions

Loading independent, separate scripts assets that declare tracking components inside the global scope risks unexpected namespace collisions and errors.

```jsx
<script>
	// script_one.js defines: const appName = "Alpha";
	// script_two.js defines: const appName = "Omega";
	// Result Uncaught SyntaxError: Identifier 'appName' has already been declared
</script>
```

If legacy named functions are declared with matching signatures within the same global scope layer, the last declaration encountered simply overwrites all previous iterations.

**The Zoo Analogy:** Think of function scopes like zoo enclosures. Animals (local variables) live securely inside their own environments. If a tiger steps directly into a penguin enclosure, chaos ensues. The global scope acts like the zookeeper - possessing the master keys to access every environment uniformly, but it should be used sparingly to keep the ecosystem orderly.

### Block Scope (`let`/`const`) vs. Function Scope (`var`)

- **`let` and `const`:** Strictly block-scoped. Variables declared inside loops (`for`) or conditionals (`if`) remain trapped within those curly braces.
- **`var`:** Function-scoped. It completely ignores structural block limits (`if`/`for`), hoisting variables up into the parent function or global scope, which can cause subtle state bugs.

## Returns & Values Safeguards

The `return` directive halts function execution immediately and hands an evaluation value back to the calling parent block.

- **Early Exits:** A plain `return;` statement drops execution lines instantly and resolves to `undefined`. This acts as an elegant guard clause to prevent deep conditional nesting.
- **Implicit Evaluators:** Functions lacking an explicit `return` directive automatically emit `undefined` back to the tracking environment thread upon structural completion.

```jsx
function showMovie(age) {
	if (age < 18) return; // Guard clause stops evaluation immediately
	console.log("Showing you the movie...");
}
```

### **The Automatic Semicolon Insertion (ASI) Trap**

Never inject a newline break directly beneath the `return` keyword. JavaScript will automatically compile an implicit semicolon there, generating an unintended empty `undefined` exit block.

```jsx
// BOROKEN Syntax: Returns undefined
return
	(some + long + expressions);

// CORRECT Syntax: Keep the opening parentheses on the same line
return (
	some + long + expression
);
```

## The JavaScript Call Stack

The JavaScript engine uses a **Call Stack** to manage execution contexts based on the **Last-In-First-Out (LIFO)** principle. It tracks what function is currently running and what sub-functions are invoked from within it.

### Stack Lifecycle Lifecycle Actions

1. **Global Execution Context:** When a script starts, the engine creates a global context and pushes it to the bottom of the stack (often represented as `main()` or `global()`).
2. **Function Push:** Whenever a function is invoked, the engine generates a unique function execution context, pushes it to the top of the stack, and executes its body.
3. **Function Pop:** When a function hits a `return` or reaches the end of its block, its context is popped off the top of the stack, and execution resumes where it left off in the calling block.
4. **Halt:** The script terminates execution once the call stack becomes entirely empty.

### Execution Example Trace

```jsx
function add(a, b) {
	return a + b;
}

function average(a, b) {
	return add(a, b) / 2;
}

let x = average(10, 20);
```

### Stack Changes During Execution:

```
Step 1: [ global() ] -> Script starts
Step 2: [ average(), global() ] -> average(10, 20) is called
Step 3: [ add(), average(), global() ] -> add(a, b) is called inside average()
Step 4: [ average(), global() ] -> add() finishes execution and pops off
Step 5: [ global() ] -> average() finishes execution and pops off
```

### Stack Overflow

The call stack has a fixed total size capacity determined by the host runtime (browser environment or Node.js). If the volume of execution contexts exceeds this allocated memory threshold (most commonly caused by infinite, un-guarded recursive functions), a **Stack Overflow** error occurs, crashing the thread.

## Asynchronous JavaScript & The Event Loop

JavaScript is inherently a **single-threaded** language. It features exactly one call stack, meaning it can only perform one single operation at any given time.

- **Synchronous Flow:** By default, code evaluates line-by-line from top to bottom. If a line takes a long time to run, it blocks the entire execution stack.
- **Asynchronous Flow:** To prevent locking up user interfaces, JavaScript utilizes browser Web APIs and an **Event Loop** mechanism. This allows the engine to hand off heavy tasks (like network fetches or timers) to the browser background and continue processing other code blocks synchronously while waiting.

## Architectural & Clean Code Practices

### Semantic Naming Conventions

Functions represent **actions**. Always use concise, descriptive verb prefixes to communicate the operational target of a code block instantly:

| **Prefix** | **Functional Intent** | **Architectural Boundary Constraints** |
| --- | --- | --- |
| `"show..."` | Exposes visual UI or content data | Modifies display parameters or components directly |
| `"get..."` | Requests or extracts exact data values | Computes data and **returns** it cleanly with zero side-effects |
| `"calc..."` | Combines mathematical configurations | Runs mathematical formulations and returns numeric output |
| `"create..."` | Builds new data items or collections | Instantiates and outputs new object or array structures |
| `"check..."` | Validates conditional configurations | Evaluates logic states, returning a strict **boolean** |

### Single Responsibility Principle (”One Function, One Action”)

A function must perform exactly what its semantic prefix asserts - nothing more. For instance, a function named `getAge()` should purely calculate and return an age numerical value; it must never trigger an `alert()` dialog window or modify layout documents.

### Writing Self-Documenting Code

Abstract complex nested loops and conditions into clearly named helper functions. This design pattern removes messy comment blocks and ensures code is readable at a glance.

```jsx
// HARD TO PARSE: Nested loops with tricky label controls
function showPrimes(n) {
	nextPrime: for (let i = 2; i < n; i++) {
		for (let j = 2; j < i; j++) {
			if (i % j == 0) continue nextPrime;
		}
		console.log(i);
	}
}

// CLEAN & SELF-DOCUMENTING: Complex logic cleanly abstracted
function showPrimes(n) {
	for (let i = 2; i < n; i++) {
		if (!isPrime(i)) continue; // The operational intent here is crystal clear
		console.log(i);
	}
}

function isPrime(n) {
	for (let i = 2; i < n; i++) {
		if (n % i == 0) return false;
	}
	return true;
}
```