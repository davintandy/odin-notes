# Commit Messages

## What Is a Commit Message?

A **commit message** describes the changes recorded in a Git commit. It helps you and other developers understand what changed and why the change was made.

A Git commit acts as a snapshot of your project at a particular point in its history.

### Why Are Good Commit Messages Important?

- **Understand project history**: Identify what changed without inspecting every file immediately.
- **Debug problems**: Find commits that may have introduced a bug.
- **Maintain projects**: Understand decisions when returning to a project after a long time.
- **Collaborate effectively**: Help other developers review and understand your work.
- **Present your skills**: A clear Git history demonstrates good development habits when others review your GitHub projects.

A vague message such as `fixed a bug` provides little context. A more specific message, such as `Fix broken navigation link`, communicates the change clearly.

## Anatomy of a Commit Message

A commit message can contain two parts:

- **Subject**: A short summary of the change.
- **Body**: Additional context explaining what changed and why.

### Example

```
Add missing link and alt text to company logo

Screen readers need alternative text to communicate
the logo's meaning to users with visual impariments.
```

The subject summarizes the change, while the body explains its purpose.

### Subject vs. Body

| **Component** | **Purpose** | **Guidelines** |
| --- | --- | --- |
| Subject | Summarizes the change | Short, specific, and action-oriented |
| Body | Explains the context behind the change | Describe the problem, reasoning, and relevant consequences |

A body is optional. For a simple change, a subject alone may be sufficient. For a change that requires explanation, include a body separated from the subject by a blank line.

## The Seven Rules of a Great Commit Message

### Rule 1: Separate the Subject and Body with a Blank Line

Always place a blank line between the subject and body when both are present.

```
Fix broken navigation link

The About link pointed to a nonexistent file.
Update the destination to use the correct path.
```

The separation helps Git tools distinguish the summary from the detailed explanation.

### Rule 2: Keep the Subject Short

A practical rule is to aim for 50 characters and avoid exceeding 72.

Bad:

```
I finally fixed the problem with the navigation link
that I have been trying to fix for a while
```

Better:

```
Fix broken navigatoin link
```

A concise subject is easier to scan in Git history.

### Rule 3: Capitalize the Subject

Begin the subject with a capital letter.

```
Add HTML boilerplate notes
```

Instead of:

```
add HTML boilerplate notes
```

Consistency makes the commit history easier to read.

### Rule 4: Do Not End the Subject with a Period

Avoid unnecessary punctuation at the end of the subject.

```
Update Git notes
```

Instead of:

```
Update Git notes.
```

The subject is a summary rather than a complete prose paragraph.

### Rule 5: Use the Imperative Mood

Write the subject as a command or instruction, describing what the commit will accomplish.

Good examples:

```
Add links and images notes
Fix relative image paths
Update HTML examples
Remove duplicated explanations
```

Avoid past-tense or ongoing-action descriptions:

```
Added links and images notes
Fixed relative image paths
Updateing HTML examples
```

One helpful test is to complete this sentence:

> If applied, this commit will …
> 

For example:

- If applied, this commit will **add links and images notes**.
- If applied, this commit will **fix relative image paths**.

If the subject fits naturally into that sentence, it generally follows the imperative convention.

### Rule 6: Wrap the Body at Approximately 72 Characters

When writing a longer body, keep each line around 72 characters or fewer.

This improves readability in terminals and other Git tools, particularly when text is displayed with indentation.

Example:

```
Improve image accessibility

Add descriptive alt text to meaningful images so that
screen readers can communicate their content to users.
```

Do not confuse this with subject-length recommendation. The subject should be concise; the body can be longer but should remain readable.

### Rule 7: Explain What and Why, Rather Than How

The code diff already shows many details about **how** the change was implemented. The commit message should provide context that may not be obvious from the code alone.

For example:

```
Add descriptive alt text to images

Screen readers need text alternatives to communicate
meaningful image content to users who cannot see it.
```

The subject describes what changed. The body explains why the change matters.

A useful body can explain:

- The problem that existed before the change.
- Why the change was necessary.
- The reasoning behind the chosen solution.
- Important side effects or consequences.

Not every commit needs a body. Include one when it adds meaningful context.

## When Should You Commit?

A good practice is to **commit whenever you complete a meaningful, logical change**.

Examples of suitable commits include:

- Completing a small feature.
- Fixing a bug.
- Correcting a typo.
- Improving documentation.
- Refactoring code for readability.
- Completing a coherent section of learning notes.

### Make Small, Focused Commits

Each commit should ideally represent one logical change. This makes the history easier to understand and helps isolate problems later.

For example, rather than grouping unrelated changes into one commit:

```
Update HTML notes, fix CSS, and rename project files
```

Separate them into focused commits:

```
Update HTML links and images notes
Fix navigation styling
Rename project files
```

These are easier to inspect, review, and undo independently.

### Why Commit Early and Often?

Frequent commits create checkpoints throughout your progress.

If a later change breaks something, you can inspect previous commits to identify when the problem appeared or restore an earlier state.

However, committing frequently does not mean committing every keystroke. Commit when a change forms a useful checkpoint.

## Writing Multi-Line Commit Messages

For simple commits, the `-m` option is convenient:

```bash
git commit -m "Add commit messages notes"
```

For a message with a subject and body, use `git commit` without `-m`:

```bash
git commit
```

Git opens the configured commit-message editor. Enter the subject, leave a blank line, and then write the body.

Example:

```
Improve command line notes

Add examples for file navigatoin and directory management
to make the commands easier to review during practice.
```

Save and close the editor to complete the commit. The exact steps depend on which editor is configured for Git.

### Writing a Body with `-m`

You can also provide the subject and body with two `-m` options:

```
git commit \
	-m "Improve command line notes" \
	-m "Add practical examples for file navigatoin and directory management."
```

The second `-m` creates the body, separated from the subject by a blank line.

## Common Commit Message Mistakes

| **Weak message** | **Problem** | **Better message** |
| --- | --- | --- |
| `update` | Too vague | `Update HTML boilerplate notes` |
| `fixed bug` | Does not identify the problem | `Fix broken image path` |
| `changes` | Does not describe the change | `Add examples of ordered lists` |
| `Added Git notes.` | Past tense and trailing period | `Add Git notes` |
| `fix links` | Starts lowercase | `Fix broken links` |
| `Add notes` | May be too broad without context | `Add working with text notes` |

The goal is not to make every message elaborate. It is to make each message specific enough to understand later.