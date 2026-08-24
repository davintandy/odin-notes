# Data Types and Conditionals

## Strings: Text in JavaScript

A string is a sequence of text. While you can use single (`’`) or double (`”`) quotes, **Template Literals** (backticks  `` ` ``) are the modern standard.

### Why Template Literals are Superior

- **Expression Embedding:** Inject variables directly using `${}`.
- **Multi-line Support:** No need for `\n` characters to break lines.

```jsx
const name = "Chris";
const score = 9;
const output = `Hello ${name}. Score: ${(score/10)*100}%`;
```

### Core String Methods

All string methods return a new string; they never modify the original.

| **Category** | **Methods** | **Purpose** |
| --- | --- | --- |
| **Extraction** | `.at(i)`, `.slice(start, end)`  | Get specific characters or parts. (`.at(-1)` gets the last character) |
| **Case** | `.toUpperCase()`, `.toLowerCase()`  | Standardize casing |
| **Whitespace** | `.trim()`, `.trimStart()`, `.trimEnd()` | Remove leading/trailing spaces |
| **Padding** | `.padStart(len, char)`, `.padEnd()`  | Add filler characters (e.g., `padStart(4, "0")`) |
| **Replace** | `.replace(old, new)`, `.replaceAll()`  | Update content (supports Regex for complex patterns) |

## Control Flow: Conditionals

### Truthy & Falsy Values

Before using conditionals, you must know how JS evaluates non-boolean data.

- **Falsy:** `0`, `""` (empty string), `null`, `undefined`, `NaN`, `false`.
- **Truthy:** Literally everything else (including `"0"`, `"false"`, and empty arrays).

### The `if...else` Statement

Executes code based on whether a condition is truthy or falsy.

```jsx
if (temperature < 86) {
	console.log("Nice weather!");
} else if (temperature >= 86) {
	console.log("Too hot!");
} else {
	console.log("Tepmerature unknown.");
}
```

### The `switch` Statement

A `switch` statement replaces multiple `else if` checks by matching an expression against various `case` clauses.

**Core Rules:**

- **Strict Equality:** The switch statement uses strict equality (`===`). A string `"3"` will not match a number `3`.
- **The `break` Keyword:** Once a match is found, JS executes all code downwards until it hits a `break`. If you omit `break`, it will execute the next case sequentially even if the condition doesn’t match (called “fall-through”).
- **Grouping Cases:** You can use intentional fall-through to group cases that share the same output.

```jsx
let a = 3;

switch (a) {
	case 4:
		console.log("Exactly right!");
		break;
	
	// Grouping cases using fall-through
	case 3:
	case 5:
		console.log("Wrong! You were off by one.");
		break;
	
	default:
		console.log("I don't know such values.");
		// No break needed on the final block
}
```

### The Ternary Operator (`?`)

A one-line shorthand for simple `if...else` assignments.

**Syntax:** `condition ? runIfTrue : runIfFalse`

```jsx
let age = 20;
let accessAllowed = (age > 18) ? true : false;
// Or simply: let accessAllowed = (age > 18);
```

**Note:** You can chain multiple ternaries together, but it severely hurts readability. Use `if...else` or `switch` for complex logic.

## Logical Operators & Short-Circuiting

Unlike Python’s `and`/`or` which return booleans in some contexts, JavaScript’s logical operators evaluate expressions from left to right and return the **actual value** of the operand that stops the evaluation.

### `||` (OR): Finds the first TRUTHY value

Returns the first truthy value it encounters. If all are falsy, it returns the last value.

- `alert(1 || 0);` returns `1`
- `alert(null || 0 || "Anonymous");` returns `"Anonymous"`

**Common Use Case (Setting Defaults):**

```jsx
let currentUser = null;
let defaultUser = "Guest";
let displayUser = currentUser || defaultUser; // Sets displayUser to "Guest"
```

### `&&` (AND): Finds the first FALSY value

Returns the first falsy value it encounters. If all are truthy, it returns the last value.

- `alert(1 && 0):` returns `0`
- `alert(1 && 5 && 10);` returns `10`

**Common Use Case (Short-circuit execution):**

```jsx
let isLoggedIn = true;
isLoggedIn && showDashboard(); // showDashboard() only runs if isLoggedIn is true
```

### `!` (NOT): Inverts Boolean

Converts the operand to a boolean, then inverts it.

- `!true` → `false`
- `!0` → `true`

**Common Use Case (Double NOT for Type Coercion):**

You can use `!!` to quickly force any value into a strict boolean, exactly like using `Boolean(value)`.

- `!!"non-empty string"` → `true`
- `!!null` → `false`