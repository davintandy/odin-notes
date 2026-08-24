# Clean Code

## Naming Standards & Grammatical Semantics

The primary purpose of clean naming conventions is to maximize code readability and minimize cognitive load across an engineering team. Consistent naming patterns provide immediate structural and semantic context.

### Case Conventions

- `camelCase`: The universal standard for JavaScript variables, object properties, and function names. Combine multiple words by keeping the first word entirely lowercase and capitalizing the first letter of subsequent words (e.g., `generateUserGreeting`).
- `UPPER_SNAKE_CASE`: Reserved exclusively for **true compile-time constants** whose values are structurally or mathematically immutable (e.g., `const ONE_HOUR = 3600000;`).  This signals to external scope readers that the value must never be reassigned.

### Grammatical Rule Matrix

| **Code Construct** | **Grammatical Part** | **Structural Rule** | **Examples** |
| --- | --- | --- | --- |
| **Variables** | Noun or Adjective phrase | Must represent a distinct state, primitive value, or object entity. Avoid verbs | `numberOfThings`, `myName`, `isActive` |
| **Functions** | Verb phrase | Must represent an explicit action, execution routine, or transformation path | `getCount()`, `calculateBMI()`, `fetchData()` |

### Vocabulary Consistency

Establish a singular, uniform verb vocabulary across an entire codebase. Mixing operational synonyms implies that separate, distinct architectural workflows are occurring under the hood when they are not.

```jsx
// Inconsistent naming (creates false assumptions about underlying mechanics)
function getUserScore();
function fetchPlayerName();
function retrievePlayerTag();

// Consistent naming (unified architectural pattern)
function getPlayerScore();
function getPlayerName();
function getPlayerTag();
```

## Formatting, Syntax & Decoupling Constraints

### Line Length & Continuity Breakage

Code blocks are significantly easier to scan horizontally when lines remain within an **80-character boundary**. When manually breaking long statement expressions across lines, place the newline break immediately following an operator or comma.

```jsx
// Unreadable long line execution
let reallyReallyLongName = something + somethingElse + anotherThing + howManyTacos + oneMoreReallyLongThing;

// Standard continuity format (stacked operators)
let reallyReallyLongLine =
	something +
	sometingElse +
	anotherThing +
	howManyTacos +
	oneMoreReallyLongThing;
```

### Semicolon Deployment

While the JavaScript engine utilizes Automatic Semicolon Insertion (ASI) to parse omissions, certain edge cases (e.g., lines starting with backticks, immediately invoked functional expressions, or array destructing brackets) cause parsing errors and silent runtime bugs. Explicitly terminating statements with semicolons ensures predictable engine execution.

### Separation of Concerns (Language Decoupling)

Never indiscriminately mix programming paradigms within a single file. Avoid inline CSS style attributes or scattering arbitrary `<script>` tags inside HTML markup bodies. Maintain strict design boundaries by isolating asset spaces:

1. **HTML (`.html`):** Limited strictly to the structural DOM layout skeleton.
2. **CSS (`.css`):** Isolated design rules and visual layouts housed inside external production stylesheets.
3. **JavaScript (`.js`):** Core logical routines, data handling, and state control isolated inside dedicated application scripts.

### Import Optimization

Consolidate separate asset stylesheets into unified production payloads where possible. Minimizing separate asset dependencies optimizes client-side performance by drastically reducing overhead HTTP round-trips.

## Structural Cleanliness & Scope Layouts

### Exposing Semantic Layouts

When building structural DOM frameworks, ensure every major structural container carries an explicit, distinct ID or class attribute reflecting its layout destination. This creates self-documenting markup that is predictable for styling and scripting.

```html
<div id="main-container">
	<header id="global-header">
		<div id="brand-logo">...</div>
		<nav id="main-navigation">...</nav>
	</header>
	
	<main id="content-body">
		<section id="left-sidebar">...</section>
		<article id="primary-article">...</article>
	</main>
</div>
```

### Refactoring Large Functions

As functions expand, algorithmic complexity scales rapidly, increasing the likelihood of bugs. Methods exceeding critical scannability thresholds must be broken down into micro-functions that execute isolated, modular routines.

**The Single Responsibility Rule:** A function should do exactly one thing, do it cleanly, and handle it completely. If a distinct process within a function repeats elsewhere, extract it into an autonomous utility function.

## The Strategic Architecture of Code Comments

### Code Explains “How”; Comments Explain “Why”

The high-priority goal of clean code is to make the logic entirely self-documenting. Comments should never copy or explicitly restate what a line of code does mechanically. Use comments exclusively as narrative asides to explain the reasons or business logic constraints behind an unconventional implementation choice.

```jsx
// Redundand pseudocode commenting (restates execution mechanics)
function extractText(s) {
	// Return the string starting after the "[" and ending at "]"
	return s.substring(s.indexOf("[") + 1, s.indexOf("]");
}

// Self-documenting layout (code reads clearly without commentary)
function extractTextWithinBrackets(text) {
	const bracketTextStart = text.indexOf("[") + 1;
	const bracketTextEnd = text.indexOf("]");
	return text.substring(bracketTextStart, bracketTextEnd);
}
```

### Case Study: Refactoring over Commenting

Using comments to explain cryptic, unreadable code is an anti-pattern. If code requires documentation to be understood, the code should be refactored into descriptive, functional semantic elements.

### Cryptic Implementation with Crutch Commenting

```jsx
// Square root of n with Newton-Raphson approximation
let r = n / 2;
while(Math.abs(r - n / r) > t) {
	r = 0.5 * (r + n / r);
}
console.log("r = " + r);
```

### Clean Refactored Architecture (Zero Comments Required)

```jsx
function getSquareRootApproximation(number, tolerance) {
	let guess = number / 2;
	while (Math.abs(guess - number / guess) > tolerance) {
		guess = 0.5 * (guess + number / guess);
	}
	return guess;
}

const result = getSquareRootApproximation(val, targetTolerance);
console.log(`Approximation: ${result}`);
```

### The Git Source Control Boundary

Never convert the top of source files into manual revision changelogs or leave dead, commented-out blocks of code in production files. This introduces unnecessary noise and maintainability problems.

```jsx
// Toxic code bloat anti-pattern (pollutes production files)
/**
 * 2024-01-10: Removed unnecessary code causing confusion (RM)
 * 2025-03-05: Simplified the loop execution logic (JP)
 */
theActiveFunction();
// oldUselessFunction();
// legacyBuggyLogic();
```

- **Revision History:** Trust your source control versioning system. Git cleanly tracks author metadata, cryptographic file updates, and structural differentials across time. Review changes using `git log`.
- **Dead Code:** If a block of code is no longer actively executing in production architecture, **delete it completely**. If it is ever needed again, it can be effortlessly recovered via previous Git commits.