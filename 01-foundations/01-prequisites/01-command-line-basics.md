# Command Line Basics

The **Command Line Interface (CLI)** is a text-based conversation with your computer. While a GUI (Graphical User Interface) uses icons, the CLI uses a specific vocabulary to automate tasks with precision.

---

## Essential Shortcuts

| **Action** | **Shortcut** |
| --- | --- |
| **Open Terminal** | `Ctrl + Alt + T` |
| **Copy / Paste** | `Ctrl + Shift + C` / `Ctrl + Shift + V` |
| **Auto-complete** | `Tab`  (press twice to see all options) |
| **The Prompt (`$`)** | Indicates the terminal is ready for your command. |

---

## Navigating the Filesystem

The system is an “upside-down tree.” The very top is **Root (`/`)**.

- `pwd` (Print Working Directory): “Where am I right now?”
- `ls` (List): “What is in this folder?”
    - `ls -F`: Adds markers (`/` for folders, `*` for executables).
    - `ls -a`: Shows hidden files (those starting with `.`).
- `cd` (Change Directory): “Take me to…”
    - `cd ..`: Move up to the **parent** folder.
    - `cd ~`: Jump to your **Home** folder.
    - `cd -`: Jump to the **previous** folder you were in.

---

## File & Directory Management

### Creation & Editing

- `mkdir -p path/to/folder`: Creates a directory (and any missing parent folders).
- `nano file.txt`: A simple text editor.
    - `Ctrl + O` to Save | `Enter` to confirm | `Ctrl + X` to Exit.

### Moving, Copying, and Deleting

- `mv`: Move or **Rename** a file (`mv old.txt new.txt`).
- `cp`: Copy a file. Use `cp -r` to copy entire directories.
- `rm`: Remove a file.
    - **Warning:** There is no “Trash Bin” here. Once it’s gone, it’s gone.
    - Use `rm -i` for a safety confirmation prompt.

---

## Wildcards (Power Selection)

Wildcards are symbols that represent other characters, allowing you to handle multiple files at once.

- `*`: Matches **zero or more** characters.
    - `*.txt` matches all text files.
- `?`: Matches **exactly one** character.
    - `??.txt` matches `me.txt` but not `home.txt`.

---

## Anatomy & Help

The syntax is always: `command -options arguments`

- **Short options** (`-h`) are for speed.
- **Long options** (`—help`) are for clarity in scripts.

When stuck:

- `man <command>`: Opens the manual (e.g., `man ls`).
    - Use `Arrows` to scroll, `/` to search, and `q` to quit.

---

## Best Practices for Naming

To avoid “breaking” your commands, follow these rules:

1. **No Spaces:** Use `under_scores` or `hypens-instead`.
2. **Avoid leading dashes:** Names like `-file.txt` confuse the CLI for an option.
3. **Stick to Lowercase:** Prevents confusion between `Thesis` and `thesis`.
4. **Extensions matter (mostly):** `.png` doesn’t make a file an image, but it helps the OS know which program to use.