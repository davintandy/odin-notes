# Command Line Basics

## What is the Command Line?

- **CLI (Command-Line Interface)**: An interface for interacting with a computer by typing commands.
- **Terminal**: The application or window where you enter commands.
- **Shell**: The program that interprets your commands and executes them. This lesson uses Bash.
- **GUI (Graphical User Interface)**: An interface that uses windows, buttons, menus, and a mouse.

### Why Learn the Command Line?

- Navigate and manage files and directories quickly.
- Install and run developer tools.
- Automate repetitive tasks.
- Use tools such as Git and other development utilities.
- Perform tasks that would be tedious through a graphical interface.

### Running Commands

A terminal displays a **prompt** when it is ready for input.

```bash
$ whoami
```

This command displays your username.

- Type the command after the prompt, **not the $ symbol itself**.
- Press `Enter` to execute a command.
- Some commands display output; others finish silently when successful.
- Passwords entered into the terminal may not appear on screen. This is normal.

## Basic Command Syntax

A typical command follows this structure:

```bash
command [options] [arguments]
```

- **Command**: The action to perform.
- **Option**: Modifies how the command behaves.
- **Argument**: Specifies what the command should operate on.

For example:

```bash
ls -F /
```

- `ls` lists directory contents.
- `-F` adds indicators to identify file types.
- `/` specifies the root directory.

Options may use a single dash (`-F`) or two dashes (`--help`). Capitalization matters, and spaces separate the parts of a command.

## Navigating Files and Directories

A **file** stores information, while a **directory** (folder) contains files and other directories.

### Essential Commands

| **Command** | **Purpose** |
| --- | --- |
| `pwd` | Print the current working directory |
| `ls` | List files and directories in the current directory |
| `ls -F` | List contents with file-type indicators |
| `ls -a` | Show hidden files and directories |
| `ls -l` | Display detailed file information |
| `ls -lh` | Display detailed information with human-readable sizes |
| `cd directory` | Move into a directory |
| `cd ..` | Move up one directory level |
| `cd ~` | Move to your home directory |
| `cd` | Also return to your home directory |
| `cd -` | Return to the previous working directory |
| `clear` | Clear the terminal display |

Use `pwd` whenever you are unsure where you are.

### Special Path Symbols

| **Symbol** | **Meaning** | **Example** |
| --- | --- | --- |
| `/` | Root directory; also separates path components | `/home/user/projects` |
| `~` | Current user’s home directory | `~/Documents` |
| `.` | Current directory | `./index.html` |
| `..` | Parent directory | `../images` |
| `-` | Previous directory when used with `cd` | `cd -` |

A filename beginning with `.` is usually hidden in Unix-like environments. For example, `.bashrc` and `.gitignore`.

### Absolute vs. Relative Paths

**Absolute path**: Starts at the root directory and identifies a location independently of your current directory.

```bash
cd /home/user/projects
```

**Relative path**: Identifies a location from your current working directory.

```bash
cd projects
cd ../images
```

Suppose your current directory is `/home/user/projects`:

- `cd ..` moves to `/home/user`.
- `cd ./images` enters the `images` directory inside `projects`.
- `cd ~/Downloads` navigates to your `Downloads` directory, regardless of your current location.

> Remember: relative paths depend on where you are currently working; absolute paths do not.
> 

## Creating Files and Directories

| **Command** | **Purpose** |
| --- | --- |
| `mkdir folder` | Create a directory |
| `mkdir -p path/to/folder` | Create nested directories, including missing parent directories |
| `touch file.txt` | Create an empty file if it does not exist |
| `nano file.txt` | Open or create a plain-text file using Nano |
| `code file.txt` | Open a file in Visual Studio Code, if the code command is configured |
| `code .` | Open the current directory as a VS Code project |

### Examples

Create a directory and enter it:

```bash
mkdir my-project
cd my-project
```

Create a basic website structure:

```bash
mkdir images
touch index.html style.css
```

The result is

```
my-project/
├── images/
├── index.html
└── style.css
```

Open the project in VS Code:

```bash
code .
```

Use `touch` when you need an empty file. It does not open an editor or add content to the file.

## Moving, Renaming, and Copying

### Move or Rename: `mv`

The `mv` command moves a file or directory. It can also rename one.

Renames `old.txt` to `new.txt:`

```bash
mv old.txt new.txt
```

Moves `index.html` into the existing `website` directory:

```bash
mv index.html website/
```

Moves `logo.png` into the current directory:

```bash
mv images/logo.png .
```

### Copy: `cp`

The `cp` command creates a copy while keeping the original.

Copies a file and gives the copy a new name:

```bash
cp index.html index-backup.html
```

Copies a file into an existing directory:

```bash
cp index.html website/
```

To copy a directory and its contents, use `-r` (recursive):

```bash
cp -r my-project my-project-backup
```

**Important**: For `mv` and `cp`, the destination can represent either a new filename or an existing directory. Check the destination carefully to avoid overwriting or misplacing files.

## Deleting Files and Directories

| **Command** | **Purpose** |
| --- | --- |
| `rm file.txt` | Delete a file |
| `rm -i file.txt` | Ask for confirmation before deleting a file |
| `rm -r folder` | Delete a directory and its contents recursively |
| `rmdir folder` | Delete an empty directory |

> **Warning: `rm` can permanently delete files**. Unlike deleting files through many graphical file managers, terminal deletion generally does not send files to the Trash. Be especially careful with `rm -r`, and verify your current directory with `pwd` before running destructive commands.
> 

## Working with Multiple Files

You can pass multiple filenames to commands such as `cp` and `mv`.

```bash
cp file1.txt file2.txt backup/
```

This copies both files into the existing `backup` directory.

### Wildcards

Wildcards represent patterns in filenames, allowing you to work with multiple matching files.

| **Wildcard** | **Meaning** | **Example** |
| --- | --- | --- |
| `*` | Zero or more characters | `*.txt` matches filenames ending in `.txt` |
| `?` | Exactly one character | `file?.txt` matches `file1.txt` and `fileA.txt` |

Wildcards can match more files than expected, so inspect the pattern before using it with a command that deletes or modifies files.

## Useful Shortcuts and Getting Help

### Tab Completion

Press `Tab` to complete a partially typed command or filename.

For example, type:

```bash
cd Doc
```

Then press `Tab` to complete `Documents` if it is the only matching directory. If multiple matches exist, the shell may show the available options.

This reduces typing and helps prevent spelling mistakes.

### Command History

- Press `↑` to recall previous commands.
- Press `↓` to move forward through command history.
- On many terminals, `Ctrl + L` clears the display.

### Getting Help

Displays usage information and available options on systems that support it.

```bash
ls --help
```

Opens the manual page for `ls` on systems that provide it.

```bash
man ls
```

Displays help for the Bash built-in command `cd`.

```bash
help cd
```

Press `q` to exit a manual page.

### Copying and Pasting

In many Linux terminals, including common terminal configurations:

- Copy: `Ctrl + Shift + C`
- Paste: `Ctrl + Shift + V`

Shortcuts can differ by operating system and terminal application.