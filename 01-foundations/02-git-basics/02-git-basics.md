# Git Basics

## Pre-Flight Configuration

Before you start, tell Git to use **VS Code** for commit messages (so you don’t get trapped in the VIM editor).

```bash
$ git config --global core.editor "code --wait"
```

---

## Setting Up the Remote Repo

1. **On GitHub:** Create a new repository named `git_test`. Check **”Add a README file.”**
2. **Copy SSH:** Click the green **Code** button, select **SSH**, and copy the link.
3. **On Local Machine:** Create a place for your projects:

```bash
$ mkdir ~/repos
$ cd ~/repos
$ git clone git@github.com:USER-NAME/git_test.git
$ cd git_test
```

Run `git remote -v` to see your connection. By convention, your GitHub link is named `origin` (though you could technically name it `dancing-banana`).

---

## The Daily Workflow

Git is a two-step saving process: **Stage** then **Commit**.

### Step A: The First File

1. **Create:** `touch hello_world.txt`
2. **Check:** `git status` (File will be red/untracked)
3. **Stage:** `git add hello_world.txt` (File turns green)
4. **Commit:** `git commit -m "Add hello_world.txt"`

### Step B: Modifying Existing Files

1. **Open & Edit:** Use `code .` to open the folder. Add text to `README.md` and `hello_world.txt`.
2. **Stage All:** Instead of typing every filename, use the dot:

```bash
$ git add .
```

3. **Commit:** `git commit -m "Update README and hello_world"`

---

## Shipping to GitHub

Your local machine now has “snapshots” that GitHub doesn’t have yet.

```bash
$ git push origin main
```

**Warning:** Avoid editing files directly on the GitHub website. It creates a “history gap” that can be a headache to fix later. Always edit locally, commit, and push.

---

## Viewing History

If you want to see your trail of breadcrumbs:

```bash
$ git log
```

Press **q** to exit the log view.

---

## Best Practices

- **Atomic Commits:** Only include changes related to **one** task. This makes it easy to revert a specific feature if it breaks without losing unrelated work.
- **Descriptive Messages:** “Fixed typo” is better than “Update.” “Add login logic” is better than “Changes.”

---

## Git Cheatsheet

| **Command** | **Action** |
| --- | --- |
| `git clone <url>` | Copies a remote repo to your machine. |
| `git status` | Shows which files are modified/staged. |
| `git add .` | Stages **all** changes for the next commit. |
| `git commit -m "..."` | Saves the staged snapshot with a message. |
| `git push origin main` | Uploads your local commits to GitHub. |
| `git log` | Displays the commit history. |