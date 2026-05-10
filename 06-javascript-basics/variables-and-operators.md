# Variables and Operators

## The Core of JavaScript

JavaScript (JS) is the **dynamic layer** of the web. It provides the “muscles” that allow a page to move, react, and process data.

### The “Layer Cake” Analogy

- **HTML (Markup):** The skeleton.
- **CSS (Style):** The skin and clothes.
- **JavaScript (Behavior):** The muscles and nervous system.

---

## Environment & Execution

### Execution Context

JS runs in an **Execution Environment** (like a browser tab). For security, each tab is a “bucket” that cannot see into other tabs.

### Script Loading Strategies

| **Method** | **Syntax** | **Strategy** |
| --- | --- | --- |
| **Internal** | `<script>...</script>` | Place at the bottom of `<body>` so HTML loads first |
| **External** | `<script src="app.js" defer>`  | Use `defer` in the `<head>` to download while HTML parses |
| **Module** | `<script type="module">` | Modern standard; handles loading and scope automatically |

---

## Variables: Named Storage

Think of a variable as a **box** with a unique label. In JS, we have three ways to declare those boxes:

| **Keyword** | **Reassignable?** | **Note** |
| --- | --- | --- |
| `const` | **No** | Your default choice. Prevents accidental changes |
| `let` | **Yes** | Use for values that must change (counters, toggles) |
| `var` | **Yes** | Legacy. **Avoid** in modern code due to scope quirks |

### Naming Rules & Conventions

- **The Rules:** Must contain only letters, digits, `$`, or `_`. Cannot start with a digit.
- **camelCase:** The standard for JS (`userProfileData`).
- **UPPER_CASE:** Reserved for “hard-coded” constants (e.g., `const SECONDS_IN_HOR = 3600;`).
- **Clarity: A variable should describe the data it holds (`userName` > `u`).**

---

## Numbers & Arithmetic

JavaScript primarily uses the `Number` type for both integers and decimals.

### Definitions

- **Operand:** What operators are applied to (in `5 * 2`, the operands are `5` and `2`).
- **Unary Operator:** Applied to one operand (e.g., `-x` for negation).
- **Binary Operator:** Applied to two operands (e.g., `x + y`).

### Standard Operations

- `+`, `-`, `*`, `/`: Basic math.
- `**`: Exponentiation ($a^b$). `4 ** (1/2)` returns the square root.
- `%`: Remainder (Modulo). Returns the integer remainder of a division.

### The String “Plus” Gotcha

The binary `+` is the **only** operator that supports string concatenation. If any operand is a string, the result is a string.

```jsx
alert(2 + 2 + '1'); // "41" (4 + '1')
alert('1' + 2 + 2); // "122" ('12' + 2)
alert(6 - '2'); // 4 (Subtraction forces numeric conversion)
```

### Quick Conversions

- **Unary Plus(`+`):** A shorthand for `Number()`. It converts non-numbers into numbers.
    - `+true` becomes `1`.
    - `+""` becomes `0`.

---

## Operator Precedence

If an expression has multiple operators, JS uses a **Precedence Table** to decide the order.

1. **Parentheses** `( )` (Highest priority)
2. **Unary** `+`, `-`, `++`, `--`
3. **Exponentiation** `**`
4. **Multiplication/Division** `*`, `/`
5. **Addition/Subtraction** `+`, `-`
6. **Assignment** `=` (Lowest priority)

---

## Assignment & Incrementing

### Assignment is an Operator

Because `=` is an operator, it returns the value being assigned. This allows for **Chained Assignments**:

```jsx
a = b = c = 2 + 2; // All become 4
```

### Modify-in-Place

Use shorthands to update a variable based on its current value:

`n += 5;` (same as `n = n + 5`)

`n *= 2;` (same as `n = n * 2`)

### Increment (`++`) & Decrement (`--`)

These only work on variables.

- **Prefix (`++n`):** Increments, then returns the **new** value.
- **Postfix (`n++`):** Returns the **old** value, then increments.

```jsx
let counter = 1;
alert(++counter); // 2
alert(counter++); // 2 (but counter is now 3)
```

---

## Comparison Operators

These return a **Boolean** (`true` or `false`).

| **Operator** | **Name** | **Purpose** |
| --- | --- | --- |
| `===` | Strict Equality | Checks if value **and** type (use this!) |
| `!==` | Strict Inequality | Checks if they are not identical |
| `==` | Loose Equality | Tries to “guess” type similarity (avoid this) |
| `>`, `<` | Greater/Less than | Standard numeric comparison |

---

## Advanced & Rare Operators

### Bitwise Operators

Treat numbers as 32-bit binary digits. Rarely used in web dev, but common in cryptography:

`&` (AND), `|` (OR), `^` (XOR), `~` (NOT), `<<`, `>>`

### The Comma Operator (`,`)

Allows multiple expressions to be evaluated, but **only the last result** is returned.

```jsx
let a = (1 + 2, 3 + 4); // a = 7
```

Used primarily in complex `for` loops to perform multiple actions in one line.