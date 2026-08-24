# Object Basics

## Object Fundamentals

JavaScript has eight data types: seven **primitives** (storing a single value) and **Objects** (storing keyed collections of complex data and functionality).

An object contains **members**, which are `key: value` pairs:

- **Properties:** Members that hold data (strings, numbers, arrays, objects).
- **Methods:** Members that hold functions allowing the object to perform actions.

### Declaration Syntax

```jsx
// Object Literal Syntax (Preferred)
const user = {
	name: "John", // Property
	age: 30, // Property (trailing comma allowed)
	
	// Method (ES6 Shorthand)
	sayHi() {
		console.log(`Hello, I'm ${this.name}!`);
	}
};

// Object Constructor Syntax
const user2 = new Object();
```

## Primitives vs. Objects: Value vs. Reference

The fundamental difference between primitive types and objects lies in how they are stored and copied in memory.

### Copying Primitives (Passed by Value)

Primitive values store independent copies of data. Modifying a copy leaves the original value unchanged.

```jsx
let data = 42;
let dataCopy = data; // Stores a copy of 42

dataCopy = 43;

console.log(data); // 42
console.log(dataCopy); // 43
```

### Copying Objects (Passed by Reference)

Object variables stores a **reference** (memory address) to the actual object. Mutating an object through one reference affects all variables referencing that same object.

```jsx
const obj = { data: 42 };
const objCopy = obj; // References the exact same object in memory

objCopy.data = 43;

console.log(obj.data); // 43
console.log(objCopy.data); // 43
```

### Reassignment vs. Mutation

Reassigning a variable to a brand-new object breaks the shared reference for that specific variable without modifying the original object.

```jsx
let animal = { species: "dog" };
let dog = animal;

// Reassigning "animal" to a new memory reference
animal = { species: "cat" };

console.log(animal); // { species: "cat" }
console.log(dog); // { species: "dog" }
```

## Accessing & Modifying Properties

### Dot Notation vs. Bracket Notation

| **Feature** | **Dot Notation (`obj.key`)** | **Bracket Notation (`obj[key]`)** |
| --- | --- | --- |
| **Readability** | Concise & preferred for standard keys | Verbose |
| **Multi-word Keys** | Not allowed (`obj.likes birds`) | Allowed (`obj[”likes birds”]`) |
| **Variables / Dynamic Keys** | Evaluated literally as `"key"`  | Evaluates variable expression |
| **Valid Identifiers** | Must follow JS variable naming rules | Accepts any string or symbol |

### Access & Mutation Examples

```jsx
const person = {
	name: {
		first: "Bob",
		last: "Smith",
	},
	age: 32,
};

// Nested Dot Notation Chaining
console.log(person.name.first); // "Bob"

// Bracket Notation with Variables
const propName = "age";
console.log(person[propName]); // 32

// Setting & Creating Members
person.age = 33; // Update existing
person["eyes"] = "hazel"; // Add new property via bracket
person.farewell = function() { ... }; // Add new method
delete person.eyes; // Delete property
```

## Dynamic & Advanced Property Features

### Computed Properties

Use square brackets inside an object literal to derive property keys dynamically at creation time:

```jsx
const keyName = "fruit";

const bag = {
	[keyName]: 5 // Property key becomes "fruit"
};

console.log(bag.fruit); // 5
```

### Property Value Shorthand

When property keys match existing variable names, omit the colon and explicit value:

```jsx
function makeUser(name, age) {
	return {
		name, // Same as name: name
		age, // Same as age: age
	};
}
```

### Property Naming Rules & Coercion

- **No Reserved Word:** Property names are not restricted by JS keywords (`for`, `let`, `return` are valid keys).
- **Type Coercion:** Non-string keys automatically convert to strings (e.g., number `0` becomes `"0"`).

```jsx
const obj = {
	for: 1,
	0: "test" // Auto-coerced to string "0"
};

console.log(obj["0"]); // "test"
console.log(obj[0]); // "test"
```

> 
> 
> 
> ### The `__proto__` Exception
> 
> The special key `__proto__` cannot be assigned a primitive value. Setting `obj.__proto__ = 5` will be ignored or fail to set a primitive.
> 

## The `this` Keyword

Inside an object method, `this` refers to the **current object executing the code**. This allows the same function logic to be reused across different objects.

```jsx
const person1 = {
	name: "Chris",
	introduceSelf() {
		console.log(`Hi! I'm ${this.name}.`);
	},
};

const person2 = {
	name: "Deepti",
	introduceSelf() {
		console.log(`Hi! I'm ${this.name}.`);
	},
};

person1.introduceSelf(); // "Hi! I'm Chris."
person2.introduceSelf(); // "Hi! I'm Deepti."
```

## Property Existence: The `in` Operator

Accessing a non-existent property returns `undefined` without throwing an error.

```jsx
const user = { name: "John" };

// Basic check
console.log(user.age === undefined); // true (Property does not exist)

// "in" Operator Syntax: "key" in object
console.log("name" in user); // true
console.log("age" in user); // false
```

### Why use `in` instead of checking `=== undefined`?

The `in` operator correctly handles cases where a key **exists** on the object but holds an explicit `undefined` value:

```jsx
const obj = { test: undefined };

console.log(obj.test === undefined); // true (Ambiguous: does it exist?)
console.log("test" in obj); // true (Accurate: property key exists)
```

## Object Iteration & Key Ordering

### The `for..in` Loop

Iterates through all enumerable property keys of an object:

```jsx
const user = {
	name: "John",
	age: 30,
	isAdmin: true,
};

for (let key in user) {
	console.log(key); // "name", "age", "isAdmin"
	console.log(user[key]); // "John", 30, true
}
```

### Property Ordering Rules

1. **Integer Keys:** Sorted in **ascending numeric order**.
2. **Other Keys:** Listed in **creation order**.

> 
> 
> 
> **Integer Property:** A string that can convert to and from an integer without changing (e.g., `"49"` is an integer key, but `"+49"` or `"1.2"` are non-integer keys).
> 

```jsx
// Numeric sorting automatic behavior
const phoneCodes = {
	"49": "Germany",
	"41": "Switzerland",
	"1": "USA"
};

for (let code in phoneCodes) {
	console.log(code); // 1, 41, 49 (Sorted automatically)
}

// Workaround: Add non-digit prefix to preserve creation order
let fixedCodes = {
	"+49": "Germany",
	"+41": "Switzerland",
	"+1": "USA"
};

for (let code in fixedCodes) {
	console.log(code); // "+49", "+41", "+1" (Preserves insertion order)
}
```