# Commit Messages

## The Anatomy of a Great Commit

Effective commits consist of two parts: a **Subject** (the “what”) and a **Body** (the “why”).

### The “Seven Rules” Checklist

1. **Separate subject from body** with a blank line.
2. **Limit the subject line** to 50 characters (72 is the hard max).
3. **Capitalize** the subject line.
4. **Do not end the subject** with a period.
5. **Use the imperative mood** in the subject (e.g., “Fix bug,” not “Fixed bug”).
6. **Wrap the body** at 72 characters manually.
7. **Explain “what” and “why”** instead of “how.” (The code shows the “how”).

---

## Mastering the Imperative Mood

Git uses the imperative mood for its own internal messages (e.g., `Merge branch...`). You should too.

**The Golden Test:** A subject line should always complete this sentence:

“If applied, this commit will **[your subject line here]**”

---

## Bad vs. Good Commits

| **Type** | **Message** | **Why?** |
| --- | --- | --- |
| **Bad** | `fix a bug` | Vague. Doesn’t explain which bug or why it happened. |
| **Bad** | `more fixes for stuff` | “Stuff” isn’t a technical term. Hard to track. |
| **Good** | `Add alt text to logo` | **Subject:** Concise and imperative. **Body:** Explains accessibility benefits for screen readers. |

---

## Practical Workflow

### Writing Multi-line Messages

To write a proper subject and body, avoid the `-m` flag.

1. Type `git commit` in your terminal.
2. VS Code will open a new tab.
3. Write your subject on **Line 1**.
4. Leave **Line 2 blank**.
5. Write your body on **Line 3**.
6. **Save and close** the tab to finish.

### When to Commit?

Aim for **Atomic Commits:** one single, meaningful change per commit.

- Fix a type? **Commit**.
- Get a function working? **Commit**.
- Fix a bug? **Commit**.

---

A diff tells you **what** changed, but only the commit message tells you **why**. If you have to explain the code in the commit message, the code might be too complex. Focus on the reasoning behind the change.