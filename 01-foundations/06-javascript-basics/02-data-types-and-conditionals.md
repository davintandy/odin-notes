# Data Types and Conditionals

## JavaScript Data Types

JavaScript has **eight data types**, divided into two categories:

- **Primitive types**: Represent individual values.
- **Object type**: Represents collections of properties and more complex data structures.

### The Eight Data Types

| **Data Type** | **Description** | **Example** |
| --- | --- | --- |
| String | Represents text | `"Hello"` |
| Number | Represents integer and floating-point numbers | `25, 3, 14` |
| BigInt | Represents integers larger than the safe `Number` range | `123n` |
| Boolean | Represents logical values | `true`, `false` |
| Undefined | Represents a variable that has been declared but not assigned a value | `undefined` |
| Null | Represents an intentional absence of a value | `null` |
| Symbol | Represents a unique identifier | `Symbol("id")` |
| Object | Represents collections of properties and complex data | `{ name: "John" }` |

### Primitive vs. Reference Types

**Primitive types** store individual values and are immutable.

The seven primitive types are:

- String
- Number
- BigInt
- Boolean
- Undefined
- Null
- Symbol

**Objects** can contain multiple values and are accessed through references.

Examples of objects include:

```jsx
// Object
const person = {
	name: "John",
	age: 25
};

// Array
const colors = ["red", "blue", "green"];

// Date
const today = new Date();
```

Arrays and dates are specialized types of objects.

### Checking Data Types with `typeof`

The `typeof` operator returns a string indicating the type of a value.

```jsx
console.log(typeof "Hello"); // "string"
console.log(typeof 25); // "number"
console.log(typeof 3.14); // "number"
console.log(typeof 123n); // "bigint"
console.log(typeof true); // "boolean"
console.log(typeof undefined); // "undefined"
console.log(typeof Symbol()); // "symbol"
console.log(typeof {}); // "object"
```

There are two important exceptions:

```jsx
console.log(typeof null); // "object"
console.log(typeof []); // "object"
```

- `typeof null` returning `"object"` is a historical JavaScript behavior.
- Arrays are objects, so `typeof` does not distinguish arrays from ordinary objects.

Use `Array.isArray()` to check whether a value is an array:

```jsx
console.log(Array.isArray([1, 2, 3])); // true
console.log(Array.isArray({})); // false
```

## Strings

A **string** is a sequence of characters used to represent text.

Strings can contain letters, numbers, spaces, punctuation, and special characters.

```jsx
const firstName = "John";
const message = "Hello, World!";
const numberText = "12345";
```

Even though `"12345"` contains digits, it is still a string rather than a number.

### Three Ways to Create Strings

JavaScript supports single quotes, double quotes, and backticks.

```jsx
const single = 'Hello World';
const double = "Hello World";
const backtick = `Hello World`;
```

| **Syntax** | **Name** | **Purpose** |
| --- | --- | --- |
| `' '` | Single quotes | Creates a regular string |
| `" "` | Double quotes | Creates a regular string |
| `` ` `` | Backticks | Creates a template literal |

Single and double quotes behave the same way. Choose one style and use it consistently.

Backticks provide additional functionality, including variable interpolation and multiline strings.

### Escaping Characters

Sometimes you need to include quotation marks or special characters inside a string.

Use a backslash (`\`) to escape characters.

```jsx
const message = 'It\'s a beautiful day!';

console.log(message);
```

Common escape sequences:

| **Escape sequence** | **Meaning** |
| --- | --- |
| `\'` | Single quotation mark |
| `\"` | Double quotation mark |
| `\\` | Backslash |
| `\n` | New line |
| `\t` | Tab |

Example:

```jsx
const message = "Hello!\nWelcome to JavaScript.";

console.log(message);
```

Output:

```
Hello!
Welcome to JavaScript.
```

### Template Literals

Template literals use backticks and allow variables or expressions to be embedded using `${}`.

```jsx
const firstName = "John";
const age = 25;

const message = `My name is ${firstName} and I am ${age} years old.`;

console.log(message);
```

Output:

```
My name is John and I am 25 years old.
```

You can also perform calculations inside `${}`:

```jsx
const price = 100;
const quantity = 3;

console.log(`Total: ${price * quantity}`);
```

Output:

```
Total: 300
```

Template literals can span multiple lines:

```jsx
const message = `Hello!
Welcome to my website.
Enjoy your visit.`;
```

**Best practice**: Prefer template literals when combining text with variables or expressions.

## String Properties and Methods

A **method** is a function associated with an object or data type that performs a particular operation.

Strings have built-in properties and methods that make it easier to inspect, search, and manipulate text.

### String Length

The `.length` property returns the number of UTF-16 code units in a string.

```jsx
const text = "Hello World";

console.log(text.length); // 11
```

Remember that `.length` is a property, not a method, so it does not use parentheses.

### Changing Letter Case

| **Method** | **Purpose** |
| --- | --- |
| `toUpperCase()` | Converts letters to uppercase |
| `toLowerCase()` | Converts letters to lowercase |

```jsx
const text = "Hello World";

console.log(text.toUpperCase()); // HELLO WORLD
console.log(text.toLowerCase()); // hello world
```

### Removing Whitespace

| **Method** | **Purpose** |
| --- | --- |
| `trim()` | Removes whitespace from both ends |
| `trimStart()` | Removes whitespace from the beginning |
| `trimEnd()` | Removes whitespace from the end |

```jsx
const text = "   Hello World!   ";

console.log(text.trim()); // "Hello World!"
console.log(text.trimStart()); // "Hello World!   "
console.log(text.trimEnd()); // "   Hello World!"
```

These methods are particularly useful when cleaning up user input.

### Extracting Parts of a String

| **Method** | **Purpose** |
| --- | --- |
| `slice(start, end)` | Extracts part of a string |
| `substring(start, end)` | Extracts part of a string using start and end positions |
| `at(index)` | Returns the character at a specified position |
| `charAt(index)` | Returns the character at a specified position |

Example:

```jsx
const text = "JavaScript";

console.log(text.slice(0, 4)); // Java
console.log(text.substring(4, 10)); // Script
console.log(text.at(0)); // J
console.log(text.charAt(4)); // S
```

Important differences:

- String positions start at index `0`.
- The ending position in `slice()` and `substring()` is excluded.
- `slice()` supports negative positions, counting from the end.
- `substring()` treats negative positions as `0`.

```jsx
const text = "JavaScript";

console.log(text.slice(-6)); // Script
```

### Finding Text Within a String

| **Method** | **Purpose** |
| --- | --- |
| `includes(searchValue)` | Checks whether a string contains specified text |
| `indexOf(searchValue)` | Returns the first position where text occurs |
| `lastIndexOf(searchValue)` | Returns the last position where text occurs |
| `startsWith(searchValue)` | Checks whether a string beings with specified text |
| `endsWith(searchValue)` | Checks whether a string ends with specified text |

Example:

```jsx
const text = "Learning JavaScript";

console.log(text.includes("JavaScript")); // true
console.log(text.indexOf("JavaScript")); // 9
console.log(text.startsWith("Learning")); // true
console.log(text.endsWith("Script")); // true
```

If `indexOf()` cannot find the specified text, it returns `-1`.

### Replacing Text

| **Method** | **Purpose** |
| --- | --- |
| `replace()` | Replaces the first matching occurrence when given a string search value |
| `replaceAll()` | Replaces all matching occurrences when given a string search value |

```jsx
const text = "I like cats. Cats are cute.";

console.log(text.replace("cats", "dogs")); // I like dogs. Cats are cute.

console.log(text.replaceAll("cats", "dogs")); // I like dogs. Cats are cute.
```

String matching is case-sensitive.

### Splitting a String

The `split()` method divides a string into an array based on a specified separator.

```jsx
const fruits = "Apple,Banana,Orange";

const result = fruits.split(",");

console.log(result); // ["Apple", "Banana", "Orange"]
```

You can also split a string by spaces:

```jsx
const sentence = "Learning JavaScript is fun";

const words = sentence.split(" ");

console.log(words); // ["Learning", "JavaScript", "is", "fun"]
```

### Joining Strings

The `concat()` method joins strings together.

```jsx
const firstName = "John";
const lastName = "Doe";

const fullName = firstName.concat(" ", lastName);

console.log(fullName); // John Doe
```

The `+` operator and template literals are generally more convenient for concatenation.

### Other Useful String Methods

| **Method** | **Purpose** |
| --- | --- |
| `repeat(count)` | Repeats a string a specified number of times |
| `padStart(length, text)` | Adds characters to the beginning until the target length is reached |
| `padEnd(length, text)` | Adds characters to the end until the target length is reached |

Example:

```jsx
const number = "5";

console.log(number.padStart(3, "0")); // "005"
console.log(number.padEnd(3, "0")); // "500"
console.log("Hello ".repeat(3)); // "Hello Hello Hello"
```

### Important: Strings Are Immutable

Strings cannot be changed directly. String Methods return a new string rather than modifying the original.

```jsx
let message = "hello";

message.toUpperCase();

console.log(message); // hello
```

To keep the modified result, assign it to a variable:

```jsx
message = message.toUpperCase();

console.log(message); // HELLO
```

**Best practice**: Use string methods to transform and inspect text rather than trying to modify individual characters directly.

## Comparison Operators

Comparison operators compare two values and return a Boolean result: `true` or `false`.

### Common Comparison Operators

| **Operator** | **Meaning** | **Example** | **Result** |
| --- | --- | --- | --- |
| `===` | Strict equality | `5 === 5` | `true` |
| `!==` | Strict inequality | `5 !== "5"` | `true` |
| `==` | Loose equality | `5 == "5"` | `true` |
| `!=` | Loose inequality | `5 != "3"` | `true` |
| `>` | Greater than | `10 > 5` | `true` |
| `<` | Less than | `5 < 10` | `true` |
| `>=` | Greater than or equal to | `10 >= 10` | `true` |
| `<=` | Less than or equal to | `5 <= 10` | `true` |

### Strict Equality (`===`)

Strict equality checks whether two values are equal without performing type conversion.

```jsx
console.log(5 === 5); // true
console.log(5 === "5"); // false
console.log(true === 1); // false
```

### Loose Equality (`==`)

Loose equality allows JavaScript to convert values before comparing them.

```jsx
console.log(5 == "5"); // true
console.log(0 == false); // true
```

This automatic type conversion can produce unexpected results.

### Best Practice

Prefer `===` and `!==` in most situations because they avoid unexpected type coercion.

### Comparing Strings

JavaScript compares strings lexicographically, examining characters from left to right.

```jsx
console.log("A" < "B"); // true
console.log("apple" > "ban"); // false
console.log("2" > "12"); // true
```

String comparison is based on character code values, not ordinary human dictionary rules.

### Comparing Different Data Types

When using relational operators such as `>`, `<`, `>=`, and `<=`, JavaScript may convert different types into numbers before comparing them.

```jsx
console.log("10" > 5); // true
console.log("2" > "12"); // true
```

The second example compares two strings character by character rather than converting them into numbers.

### Special Cases: `null` and `undefined`

These values have some unusual comparison behavior.

```jsx
console.log(null == undefined); // true
console.log(null === undefined); // false

console.log(null == 0); // false
console.log(null >= 0); // true
console.log(null > 0); // false
```

Avoid comparing potentially `null` or `undefined` values using relational operators without checking them first.

### Important: `NaN`

`NaN` represents an invalid numeric result.

```jsx
console.log(NaN === NaN); // false
console.log(NaN > 5); // false
```

Use `Number.isNaN()` to check whether a value is `NaN`.

```jsx
console.log(Number.isNaN(NaN)); // true
```

## Conditional Statements

**Conditionals** allow a program to make decisions and execute different blocks of code depending on whether a condition is satisfied.

For example, a program can check whether a user is old enough to access a particular service.

### The `if` Statement

The `if` statement executes a block of code when its condition evaluates to `true`.

```jsx
const age = 20;

if (age >= 18) {
	console.log("You are an adult.");
}
```

If `age >= 18` evaluates to `true`, the code inside the block executes.

If the condition is `false`, the block is skipped.

### The `if...else` Statement

Use `else` when you want to provide an alternative action.

```jsx
const age = 16;

if (age >= 18) {
	console.log("Access granted.");
} else {
	console.log("Access denied.");
}
```

Only one of the two branches executes.

### The `else if` Statement

Use `else if` when multiple conditions need to be checked.

```jsx
const score = 85;

if (score >= 90) {
	console.log("Grade A");
} else if (score >= 80) {
	console.log("Grade B");
} else if (score >= 70) {
	console.log("Grade C");
} else {
	console.log("Needs improvement");
}
```

JavaScript checks conditions from top to bottom and executes the first matching brand.

Once a brand executes, the remaining branches are skipped.

### Best Practices

- Use curly braces `{}` around conditional blocks, even when they contain only one statement.
- Write conditions clearly and avoid unnecessarily complicated expressions.
- Order multiple conditions carefully.
- Use `else` for a default outcome when appropriate.

## Truthy and Falsy Values

JavaScript allows values of different data types to be evaluated in conditional statements.

Every value can be converted into a Boolean value.

- **Truthy**: Values that behave like `true` in a Boolean context.
- **Falsy**: Values that behave like `false` in a Boolean context.

### Falsy Values

JavaScript has eight commonly recognized falsy values:

| **Value** | **Example** |
| --- | --- |
| `false` | `if (false)` |
| `0` | `if (0)` |
| `-0` | `if (-0)` |
| `0n` | `if (0n)` |
| Empty string | `if ("")` |
| `null` | `if (null)` |
| `undefined` | `if (undefined)` |
| `NaN` | `if (NaN)` |

All other ordinary value are truthy.

### Examples of Truthy Values

```jsx
if ("Hello") {
	console.log("This runs");
}

if (42) {
	console.log("This also runs");
}

if ([]) {
	console.log("Empty arrays are truthy");
}

if ({}) {
	console.log("Empty objects are truthy");
}
```

Even empty arrays and empty objects are truthy.

### Boolean Conversion

Use `Boolean()` to convert a value explicitly into a Boolean.

```jsx
console.log(Boolean(1)); // true
console.log(Boolean(0)); // false
console.log(Boolean("Hello")); // true
console.log(Boolean("")); // false
```

You can also use double NOT (`!!`) for the same conversion:

```jsx
console.log(!!"Hello"); // true
console.log(!!0); // false
```

### Why Truthy and Falsy Values Matter

You can use a value directly as an `if` condition.

```jsx
const username = "";

if (username) {
	console.log(`Welcome, ${username}!`);
} else {
	console.log("Please enter a username.");
}
```

Since an empty string is falsy, the `else` branch executes.

**Important**: Truthiness checks whether a value is empty or falsy, not whether it is valid for a particular application. For example, `0` is falsy but may be a perfectly valid age, score, or quantity.

## Logical Operators

Logical operators combine or modify conditions.

JavaScript has three fundamental logical operators:

- OR (`||`)
- AND (`&&`)
- NOT (`!`)

### OR (`||`)

The OR operator returns a truthy result when at least one condition is truthy.

```jsx
const age = 17;
const hasPermission = true;

if (age >= 18 || hasPermission) {
	console.log("Access granted.");
}
```

In this example, access is granted because `hasPermission` is `true`, even though the age requirement is not met.

Truth table:

| **`A`** | **`B`** | **`A \|\| B`** |
| --- | --- | --- |
| `true` | `true` | `true` |
| `true` | `false` | `true` |
| `false` | `true` | `true` |
| `false` | `false` | `false` |

### AND (`&&`)

The AND operator requires all conditions to be truthy.

```jsx
const age = 20;
const hasPermission = true;

if (age >= 18 && hasPermission) {
	console.log("Access granted.");
}
```

Both conditions must be satisfied.

Truth table:

| **`A`** | **`B`** | **`A && B`** |
| --- | --- | --- |
| `true` | `true` | `true` |
| `true` | `false` | `false` |
| `false` | `true` | `false` |
| `false` | `false` | `false` |

### NOT (`!`)

The NOT operator reverses a Boolean value.

```jsx
const isLoggedIn = false;

if (!isLoggedIn) {
	console.log("Please log in.");
}
```

Since `isLoggedIn` is `false`, `!isLoggedIn` evaluates to `true`.

Truth table:

| **`A`** | **`!A`** |
| --- | --- |
| `true` | `false` |
| `false` | `true` |

### Logical Operators with Non-Boolean Values

Unlike comparison operators, `&&` and `||` do not necessarily return Boolean values. They return one of their operands based on truthiness.

**OR (`||`)**: Returns the first truthy operand, or the last operand if none are truthy.

```jsx
console.log("" || "Default"); // "Default"
console.log("Hello" || "World"); // "Hello"
console.log(0 || 10); // 10
```

**AND (`&&`)**: Returns the first falsy operand, or the last operand if all are truthy.

```jsx
console.log("Hello" && "World"); // "World"
console.log(0 && "World"); // 0
```

This behavior is called short-circuit evaluation.

### Short-Circuit Evaluation

JavaScript stops evaluating an expression when the result is already determined.

For OR:

```jsx
const username = "John";

const result = username || "Anonymous";
```

Since `username` is truthy, JavaScript does not need to evaluate the second operand.

For AND:

```jsx
const isLoggedIn = false;

isLoggedIn && console.log("Welcome!");
```

Since the first operand is falsy, the second expression is not executed.

### Operator Precedence

The AND operator (`&&`) has higher precedence than OR (`||`).

```jsx
console.log(true || false && false); // true
```

This is evaluated as:

```jsx
console.log(true || (false && false));
```

Use parentheses when combining conditions to make the intended logic easier to read.

## Nesting Conditionals

**Nesting** means placing one conditional statement inside another.

This is useful when a decision depends on multiple levels of conditions.

### Example

```jsx
const age = 20;
const hasLicense = true;

if (age >= 18) {
	if (hasLicense) {
		console.log("You can drive.");
	} else {
		console.log("You need a driving license.");
	}
} else {
	console.log("You are too young to drive.");
}
```

The program checks the age first.

Only when the age requirement is satisfied does it check the license.

### Nested vs. Combined Conditions

The same logic can sometimes be written using logical operators.

```jsx
const age = 20;
const hasLicense = true;

if (age >= 18 && hasLicense) {
	console.log("You can drive.");
} else {
	console.log("You cannot drive.");
}
```

Use nesting when the inner decision is meaningful only after the outer condition succeeds. Use logical operators when a straightforward combined condition is easier to understand.

Avoid excessive nesting because deeply nested code can become difficult to read and maintain.

## The Ternary Operator (`? :`)

The **ternary operator** is a shorter way to express a conditional that chooses between two expressions.

### Syntax

```jsx
condition ? expressionIfTrue : expressionIfFalse;
```

Example:

```jsx
const age = 20;

const message = age >= 18
	? "Adult"
	: "Minor";

console.log(message); // Adult
```

This is equivalent to:

```jsx
const age = 20;
let message;

if (age >= 18) {
	message = "Adult";
} else {
	message = "Minor";
}
```

### When to Use It

Ternary operators are useful when:

- Choosing between two values.
- Assigning a result based on a simple condition.
- Writing short condition expressions.

Avoid deeply nested ternary expressions because they can be difficult to read.

Use ordinary `if...else` statements when logic involves multiple steps or complex operations.

## The `switch` Statement

A `switch` statement provides an alternative to multiple `if...else` if conditions when comparing one expressions against several possible values.

### Syntax

```jsx
switch (expression) {
	case value1:
		// Code to execute
		break;
	
	case value2:
		// Code to execute
		break;
	
	default:
		// Code if no case matches
}
```

### Example

```jsx
const day = 3;

switch (day) {
	case 1:
		console.log("Monday");
		break;
	
	case 2:
		console.log("Tuesday");
		break;
	
	case 3:
		console.log("Wednesday");
		break;
	
	default:
		console.log("Unknown day");
}
```

Output:

```
Wednesday
```

### Understanding the Components

| **Component** | **Purpose** |
| --- | --- |
| `switch` | Evaluates the expression |
| `case` | Defines a value to compare against |
| `break` | Exits the switch statement |
| `default` | Executes when no case matches |

### Why Is `break` Important?

Without `break`, JavaScript continues executing the following cases after finding a match. This behavior is called **fall-through**.

Example:

```jsx
const number = 2;

switch (number) {
	case 1:
		console.log("One");
	
	case 2:
		console.log("Two");
	
	case 3:
		console.log("Three");
}
```

Output:

```
Two
Three
```

The execution continues from `case 2` because there is no `break`.

Normally, add `break` after each case unless you intentionally want fall-through.

### Grouping Cases

You can intentionally group multiple cases when they should execute the same code.

```jsx
const day = "Saturday";

switch (day) {
	case "Saturday":
	case "Sunday":
		console.log("Weekend");
		break;
	
	default:
		console.log("Weekday");
}
```

Both Saturday and Sunday produce the same result.

### Important: Switch Uses Strict Equality

`switch` compares its expression with each case using strict equality (`===`).

```jsx
const number = "2";

switch (number) {
	case 2:
		console.log("Number two");
		break;
	
	case "2":
		console.log("String two");
		break;
}
```

Output:

```
String two
```

The number `2` and string `"2"` are different values because their data types differ.

### When to Use `switch` vs. `if...else`

| `switch` | `if...else` |
| --- | --- |
| Compares one expression against several specific values | Evaluates different conditions |
| Useful for menu choices and fixed categories | Useful for ranges and complex conditions |
| Uses strict equality for matching cases | Supports any valid Boolean condition |
| Requires attention to break and fall-through | Uses the first matching conditional branch |

For example, use `switch` for selecting a day of the week and `if...else` for checking whether a score falls within a particular range.

## Choosing the Right Conditional

Different conditional structures are useful for different situations.

| **Situation** | **Recommended approach** |
| --- | --- |
| Execute code when one condition is true | `if` |
| Choose between two outcomes | `if...else` |
| Evaluate several conditions or ranges | `if...else if` |
| Choose between two simple values | Ternary operator |
| Compare one value against several fixed options | `switch` |
| Combine multiple conditions | Logical operators |
| Evaluate a decision within another decision | Nested conditionals |