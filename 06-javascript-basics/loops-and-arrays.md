# Loops and Arrays

## Loops & Control Flow

Loops repeat execution blocks until a specified condition becomes falsy. Each pass through a loop is an **iteration**.

## Core Constructs

```jsx
// 1. while: Evaluates condition BEFORE each iteration
let i = 3;
while (i) console.log(i--); // 0 is falsy -> terminates at 0

// 2. do...while: Evaluates condition AFTER each iteratoin (Runs AT LEAST once)
let j = 0;
do {
	console.log(j++);
} while (j < 3);

// 3. Standard for loop
for (let k = 0; k < 3; k++) {
	console.log(k);
}
```

### Standard `for` Loop Lifecycle

| **Component** | **Execution Phase** | **Role** |
| --- | --- | --- |
| `begin` (`let i = 0`) | Pre-loop entry | Runs once before the loop starts |
| `condition` (`i < 3`) | Pre-iteration | Evaluated before each pass; exits if falsy |
| `step` (`i++`) | Post-iteration | Runs immediately after the loop body |

### Directives & Labeled Statements

- `break`: Immediately exits the loop structure completely.
- `continue`: Skips the rest of the current iteration and jumps to the next step.
- **Labeled Statements**: Allow breaking/continuing through nested parent loops.

sampai sini

```jsx
// Skipping even numbers
for (let i = 0; i < 10; i++) {
	if (i % 2 === 0) continue;
	console.log(i); // 1, 3, 5, 7, 9
}

// Breaking outer loop from inner loop
outerLoop: for (let i = 0; i < 3; i++) {
	for (let j = 0; j < 3; j++) {
		let input = prompt(`Value at (${i},${j})`, "");
		if (!input) break outerLoop; // Exits BOTH loops
	}
}
```

## Array Architecture & Engine Internals

JavaScript arrays are ordered, integer-indexed collections backed by dynamic engine optimizations (e.g., V8).

### Deque Operations & Time Complexity

Arrays function as **deques** (double-ended queues). Modifying the **tail** (end) is significantly faster than modifying the **head** (start) because starting elements require index re-indexing.

| **Method** | **Array Side** | **Action** | **Time Complexity** | **Engine Impact** |
| --- | --- | --- | --- | --- |
| `push(...items)` | Tail (End) | Append | $\mathcal{O}(1)$ | Fast. Modifies tail slot & `.length` |
| `pop()` | Tail (End) | Remove last | $\mathcal{O}(1)$ | Fast. Deletes tail slot & decrements `.length()` |
| `unshift(...items)` | Head (Start) | Prepend | $\mathcal{O}(n)$ | Slow. Must shift every element right |
| `shift()` | Head (Start) | Remove first | $\mathcal{O}(n)$ | Slow. Mush shift every element left |

### Memory Allocation & Iteration Choice

- **Contiguous Memory:** V8 optimizes dense, sequentially indexed arrays as continuous memory buffers.
- **Sparse Degradation:** Creating gaps (`arr[99999] = “x”`) or adding non-numeric properties (`arr.age = 25`) forces the engine to downgrade storage to a slow hashtable lookup.
- **Iteration Selection:** Use `for...of` for array values. **Avoid** `for...in` on arrays - it iterates over all enumerable string keys (including prototype properties) and can run 10x-100x slower.

## Iteration & Functional Methods

### Imperative vs. Functional Transformation

Considering summing the tripled values of only the **even** numbers in an array:

```jsx
const numbers = [1, 2, 3, 4, 5, 6];

// Imperative Approach (Traditional Loop)
function sumTripledEvensLoop(arr) {
	let sum = 0;
	for (let i = 0; i < arr.length; i++) {
		if (arr[i] % 2 === 0) {
			sum += arr[i] * 3;
		}
	}
	return sum;
}

// Functional Approach (Chaining map, filter, reduce)
const sumTripledEvens = (arr) =>
	arr
		.filter((num) => num % 2 === 0) // 1. Keep evens: [2, 4, 6]
		.map((num) => num * 3) // 2. Triple them: [6, 12, 18]
		.reduce((total, curr) => total + curr, 0); // 3. Sum total: 36
```

### Functional Core Trio

1. `.map(cb)`: Transforms each item and returns a **new array** of the exact same length.
2. `.filter(cb)`: Evaluates each item with a predicate (`true`/`false`) and returns a **new array** with matching elements.
3. `.reduce(cb, initialValue)`: Accumulates array values down to a single output value (number, object, array, etc.).

### Standard Callback Signature & `thisArg`

Iterative methods (`map`, `filter`, `forEach`, `find`, etc.) pass 3 arguments to callbacks: `(element, index, array)`. They also accept an optional `thisArg`:

```jsx
let army = {
	minAge: 18,
	canJoin(user) { return user.age >= this.minAge; }
};

let users = [{ age: 16 }, { age: 20 }];
// Pass "army" as thisArg to preserve context inside callback
let recruits = users.filter(army.canJoin, army); // [{ age: 20 }]
```

### Mutating vs. Modern Immutable Alternatives

| **Operation** | **Mutating Method (in-place)** | **Modern Non-Mutating Alternative (Returns Copy)** |
| --- | --- | --- |
| **Reverse** | `arr.reverse()` | `arr.toReversed()` |
| **Sort** | `arr.sort(compareFn)` | `arr.toSorted(compareFn)` |
| **Splice** | `arr.splice(start, count, ...items)` | `arr.toSpliced(start, count, ...items)` |
| **Set Index** | `arr[i] = val` | `arr.with(i, val)`  |

**Sorting Gotcha:** Default `.sort()` sorts alphabetically (`”15” < “2”`). Always supply a comparator for numbers: `arr.sort((a, b) => a - b`).

## Array Edge Cases & “Gotchas”

### `.length` Truncation

Setting `.length` to a smaller value permanently deletes elements. Setting it to `0` clears the array instantly.

```jsx
let nums = [1, 2, 3, 4, 5];
nums.length = 2; // [1, 2] - elements 3, 4, 5 are destroyed!
```

### Single-Argument `new Array()`

```jsx
let a = new Array(3); // Creates sparse array with 3 empty slots: [empty x 3]
let b = new Array("3"); // Creates array with 1 string element: ["3"]
```

### Sparse Slot Handling

- **Skipped by:** `forEach()`, `map()`, `filter()`, `every()`, `some()`.
- **Visited as `undefined` by:** `find()`, `findIndex()`, `includes()`, `Array.from()`.

### Coercion & Equality Reference

```jsx
console.log([] == []); // false (Different memory references)
console.log([] + 1); // "" + 1 -> "1"
console.log([1, 2] + 1); // "1,2" + 1 -> "1,21"
```

### CRUD Operations & Negative Indexing (`.at()`)

```jsx
const list = ["B", "C"];

// Create / Append
list.push("D"); // Tail -> ["B", "C", "D"]
list.unshift("A"); // Head -> ["A", "B", "C", "D"]

// Read & Negative Indexing
list.at(-1); // "D" (Last item)
list.includes("C"); // true

// Update & Replace
list.splice(1, 2, "X", "Y"); // Replaces 2 items at index 1 -> ["A", "X", "Y", "D"]

// Delete
const last = list.pop(); // Remove & returns "D"
const first = list.shift(); // Remove & returns "A"
```

### Copying Strategies

```jsx
const original = [{ a: 1 }, { b: 2 }];

// Shallow Copy (Top-level duplicated, nested objects share reference)
const shallow = [...original];

// Deep Copy (Fully duplicates nested structures)
const deep = structuredClone(original); // Modern Native API
```

### Generic Methods on Array-Likes

Objects with integer indexes and a `.length` property can borrow array methods:

```jsx
const arrayLike = { 0: "Alpha", 1: "Beta", length: 2 };
const result = Array.prototype.join.call(arrayLike, " + "); // "Alpha + Beta"
```

## Test-Driven Development (TDD)

**Test-Driven Development (TDD)** is the practice of writing automated unit tests before writing the implementation code.

1. **Red:** Write a failing test for the desired functionality.
2. **Green:** Write the minimal code necessary to make the test pass.
3. **Refactor:** Clean and optimize the code while keeping tests green.

**Why it matters:** Eliminates manual runtime testing (e.g., manually checking complex state outputs) and prevents regression bugs when refactoring functions.