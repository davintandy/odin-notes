# Problem Solving

## The 4-Step Engineering Problem-Solving Framework

Many developers fall into a reactive “guess-and-check” cycle: write code immediately, testing, failing, and shifting lines blindly. This is highly inefficient. Professional software engineering requires a proactive, systematic framework.

### 1. Understand the Problem

Before writing a single line of code, you must define the destination. If you cannot explain the problem in plain, non-technical English, you do not understand it.

- **Action:** Write the problem down, reword it, and visualize the constraints.
- **Success Metric:** You can clearly explain the requirements, edge cases, and constraints to a non-technical peer.

### 2. Plan & Blueprint

Analyze data architecture and logic flows before typing syntax. Use scratchpads or code comments to map out your execution sequence.

- **Interface Requirements:** Identify if the program requires a user interface, what it looks like, and its functional boundaries.
- **Inputs & Outputs:** Define exactly where the data originates, its type, and the precise expected output format.
- **Core Algorithm:** Map out the structural logic required to safely transform those inputs into the desired outputs.

### 3. Divide & Conquer (Decomposition)

Do not attempt to solve a complex architectural problem all at once. Decomposition is your primary tool for managing programmatic complexity.

**The Decomposition Rule:** Break the master problem down into isolated, manageable sub-problems. Identify the simplest, most independent sub-problem. Solve it completely, verify its output, and iteratively connect it to the next sub-problem.

### 4. Reassess & Debug

When an implementation encounters a wall or fails a test case, pivot from frustration to systematic diagnostic execution:

- **Trace:** Step through execution paths line-by-line to pinpoint exactly where the runtime state diverges from your mental model.
- **Reassess:** Step back. If an approach is overly convoluted, do not hesitate to delete the flawed attempt and restart with a clean slate and fresh eyes.
- **Targeted Research:** Never search for solutions to the master problem. Only research technical solutions for specific, isolated sub-problems (e.g., “How to convert string to integer in JavaScript”).

## Pseudocode Specifications

### Core Definition

Pseudocode is a syntax-free technique used to map out the distinct, sequential steps of an algorithm in natural language. It eliminates to focus entirely on structural logic design, algorithmic validity, and early error detection.

### The 6 Core Control Flow Constructs

| **Construct** | **Algorithmic Paradigm** | **Purpose** |
| --- | --- | --- |
| **SEQUENCE** | Linear | Represents sequential tasks executed one after another |
| **WHILE** | Conditional Loop | A loop that evaluates a condition at the **beginning** |
| **REPEAT-UNTIL** | Conditional Loop | A loop that evaluates a condition at the **bottom** (runs at least once) |
| **FOR** | Iterative Loop | A counting loop utilized when the bounds of iteration are predetermined |
| **IF-THEN-ELSE** | Conditional Branch | A structural fork that routes execution paths based on a boolean state |
| **CASE** | General Branch | A multi-way branch that generalizes complex `IF-THEN-ELSE` chains |

Advanced operations may introduce the **CALL** keyword to invoke functions/classes, or **EXCEPTION/WHEN** blocks for robust error handling.

### Universal Writing Rules

1. **Capitalize Core Keywords:** Always capitalize your main control constructs (`IF`, `THEN`, `ELSE`, `WHILE`, `FOR`, `END`).
2. **Single Statement Per Line:** Maintain exactly one clear, distinct logical action per line.
3. **Indentation Hierarchy:** Use consistent indentation to clearly demonstrate nested blocks and logical scope.
4. **Explicit Block Closures:** Always close multi-line control structures with matching termination keywords (`ENDIF`, `ENDWHILE`, `ENDFOR`).
5. **Language Independence:** Keep statements agnostic of specific programming language quirks.
6. **Domain Naming:** Use the terminology of the problem domain rather than implementation mechanics (e.g., use “Append last name to first name” instead of `name = first + last`).

### Practical Pseudocode Blueprint (Quiz Evaluation System)

```
IF employee answers score is greater than or equal to 8
	PRINT "Congratulations on passing the quiz!"
	CALL NavigateToCertificatePage
ELSE
	PRINT "Let's try again!"
	CALL ResetQuizInterface
ENDIF
```

### Strategic Benefits of Pseudocode

- **Cross-Functional Communication:** Bridges technical execution with non-technical stakeholders (managers, business analysts, data scientists).
- **Simplified Coding Construction:** Reduces the actual writing of code to a straightforward line-by-line syntax translation.
- **Early Architecture Verification:** Serves as a vital middle ground between abstract design flowcharts and concrete development.
- **Documentation Seed:** Translates directly into clear inline commentary and function docstrings.

## Practical Application: Solving FizzBuzz

### 1. Problem Clarification & Requirements

**Raw Requirement:** Write a program that takes a user’s input and prints the numbers from one to the number the user entered. However, for multiples of three print `Fizz` instead of the number, and for the multiples of five print `Buzz`. For numbers which are multiples of both three and five print `FizzBuzz`.

**Refined Requirements:** Accept a single integer input from a user prompt. Loop through all whole numbers from 1 up to and includingthat input.

- If a number is cleanly divisible by 3, output `Fizz`.
- If a number is cleanly divisible by 5, output `Buzz`.
- If a number is cleanly divisible by both 3 and 5, output `FizzBuzz`.
- Otherwise, print the number.

### 2. Planning & Design Matrix

| **Component** | **Target Architecture** |
| --- | --- |
| **Interface** | Browser Developer Console |
| **Input Data** | A user-defined string captured via a popup window and explicitly cast to an integer |
| **Output Data** | Streamed sequential string values or raw integers printed directly to the console log |

### 3. Algorithmic Architecture (Pseudocode)

```
When a user inputs a value:
PARSE input string to integer "limit"
FOR counter variable "i" from 1 up to and including "limit"
	IF "i" is divisible by 3 AND "i" is divisible by 5 THEN
		PRINT "FizzBuzz"
	ELSE IF "i" is divisible by 3 THEN
		PRINT "Fizz"
	ELSE
		PRINT "i"
	ENDIF
ENDFOR
```

### 4. Step-by-Step Implementation Flow

### Step 1: Capture and Cast Input

Use `prompt()` to capture the input data, immediately parsing it to `parseInt()` to safely cast the raw string data into a clean mathematical integer.

```jsx
let answer = parseInt(prompt("Please enter the number you would like to FizzBuzz up to: "));
```

### Step 2: Construct the Loop Iterator

Implement a standard `for` loop starting at `1` and continuing through each increment until it reaches the upper bound defined by the user.

```jsx
let answer = parseInt(prompt("Please enter the number you would like to FizzBuzz up to: "));

for (let i = 1; i <= answer; i++) {
	console.log(i);
}
```

### Step 3: Integrate the Modulus Check for Multiples of 3

Apply the **modulus operator (`%`)** to check remainders. If a number divided by 3 yields a remainder of 0 (`i % 3 === 0`), it is a multiple of 3.

```jsx
let answer = parseInt(prompt("Please enter the number you would like to FizzBuzz up to: "));

for (let i = 1; i <= answer; i++) {
	if (i % 3 === 0) {
		console.log("Fizz");
	} else {
		console.log(i);
	}
}
```

### Step 4: Expand the Chain for Multiples of 5

Introduce an `else if` branch to intercept and process variations matching multiples of 5.

```jsx
let answer = parseInt(prompt("Please enter the number you would like to FizzBuzz up to: "));

for (let i = 1; i <= answer; i++) {
	if (i % 3 === 0) {
		console.log("Fizz");
	} else if (i % 5 === 0) {
		console.log("Buzz");
	} else {
		console.log(i);
	}
}
```

### Step 5: Master Implementation (Preventing Short-Circuit Traps)

The evaluation for mutual multiples (`i % 3 === 0 && i % 5 === 0`) **must** take absolute priority at the top of the conditional hierarchy. If placed lower in the chain, numbers like 15 will hit the `i % 3 === 0` condition first, print a false-positive `Fizz`, and short-circuit the rest of the block completely.

```jsx
let answer = parseInt(prompt("Please enter the number you would like to FizzBuzz up to: "));

for (let i = 1; i <= answer; i++) {
	if (i % 3 === 0 && i % 5 === 0) {
		console.log("FizzBuzz");
	} else if (i % 3 === 0) {
		console.log("Fizz");
	} else if (i % 5 === 0) {
		console.log("Buzz");
	} else {
		console.log(i);
	}
}
```