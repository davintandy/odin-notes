# Introduction to Git

## What Is Version Control?

**Version control** is a system that records changes to files over time, allowing you to revisit previous versions, compare changes, and recover earlier work.

A **Version Control System (VCS)** is particularly useful for software development, where code changes frequently and multiple developers may work on the same project.

### Why Use Version Control?

- **Track changes**: See how a project has evolved over time.
- **Restore previous versions**: Recover earlier versions of files or the whole project.
- **Identify problems**: Determine when a bug was introduced and which changes may have caused it.
- **Experiment safely**: Develop new features without permanently losing working code.
- **Collaborate**: Combine changes made by different developers.
- **Maintain a history**: Record what changed and who contributed to the project.

### Without vs. With Version Control

Without version control, you might create multiple copies manually:

```
my-project/
├── index.html
├── index-final.html
├── index-final-v2.html
└── index-final-revised.html
```

This approach becomes difficult to manage and makes it easy to lose track of the correct version.

With Git, you can maintain one working copy while recording a history of project snapshots.

```
my-project/
├── index.html
├── style.css
└── script.js
```

Git keeps the history, so you do not need to create a separate copy of the entire project for every change.

## Types of Version Control Systems

There are three general approaches to version control.

### Local Version Control

Stores version history on a single computer.

- Maintains a local database of file changes.
- Allows previous versions to be reconstructed.
- Works well for managing changes on one machine.
- **Limitation**: The history may be lost if the computer or its storage fails and no backup exists.

### Centralized Version Control (CVCS)

Stores the shared version history on a central server.

Examples: CVS, Subversion (SVN), and Perforce.

- Developers obtain files from a central repository.
- A central server makes administration and access control easier.
- Team members can coordinate their work through the same shared history.
- **Limitation**: The central server is a single point of failure for collaboration. If it becomes unavailable, shared operations may be interrupted.

### Distributed Version Control (DVCS)

Gives each developer a complete copy of the repository, including its history.

Examples: Git, Mercurial, and Darcs.

- Each clone contains the project’s version history.
- Many operations can be performed locally, even without an internet connection.
- A repository can be recovered from another complete clone if a server fails.
- Multiple remote repositories can support different collaboration workflows.

**Git is a distributed version control system (DVCS)**.

| **Feature** | **Local VCS** | **Centralized VCS** | **Distributed VCS** |
| --- | --- | --- | --- |
| Where history is stored | Local computer | Central server | Every complete clone |
| Collaboration | Limited | Through a central server | Through repositories and remotes |
| Work offline | Yes | Limited | Yes, for most local operations |
| Dependence on one server | No shared server | High | Lower |
| Example | RCS | SVN | Git |

## A Brief History of Git

Git was created in **2005** by Linus Torvalds and the Linux development community.

### Why Was Git Created?

1. The Linux kernel project had been using BitKeeper, a proprietary version control system.
2. In 2005, the relationship between the Linux community and BitKeeper’s developers broke down, and free access to the tool was revoked.
3. The Linux development community needed a replacement suitable for managing a large, collaborative software project.
4. Linus Torvalds and other contributors developed Git to meet those needs.

### Original Design Goals

Git was designed to provide:

- Speed and efficiency.
- A simple, robust design.
- Distributed version control.
- Strong support for non-linear development and many parallel branches.
- The ability to handle large projects efficiently.

These goals help explain why Git is widely used for modern software development.

## What Is Git?

**Git is a free, open-source, distributed version control system that tracks changes to files and records project history**.

Think of Git as a powerful save system for your project.

A normal text editor saves the current contents of a file. Git allows you to record meaningful checkpoints of your project’s state and revisit them later.

### Git vs. a Text Editor

| **Text editor** | **Git** |
| --- | --- |
| Saves edits to files | Records project versions through commits |
| Usually focuses on the current file | Tracks changes across a project |
| Does not inherently provide complete project version history | Maintains a history of committed states |
| Does not inherently support team version-control workflows | Supports branching, merging, and collaboration |

**Important**: Saving a file in your editor does not automatically create a Git commit. You must explicitly record the changes using Git.

## How Git Stores Information

Git’s approach to storing information is one of its most important characteristics.

### Snapshots, Not Just Differences

Many traditional version control systems represent history primarily as a series of changes between file versions.

Git instead thinks of project history as a series of **snapshots**.

A snapshot represents the state of the project at a particular point in time.

For example,

```
Snapshot 1: Initial website
    |
    v
Snapshot 2: Added navigation bar
    |
    v
Snapshot 3: Added responsive styling
    |
    v
Snapshot 4: Fixed mobile layout
```

Each snapshot is recorded through a commit.

To be efficient, Git reuses references to unchanged file contents rather than storing every unchanged file again in every snapshot.

### Advantages of Git’s Approach

- Makes it practical to revisit previous project states.
- Supports efficient comparison between versions.
- Enables powerful branching and merging workflows.
- Makes most common operations fast because they use local data.

### Git’s Data Integrity

Git uses cryptographic hash checksums to identify and verify stored content. This helps Git detect unintended changes to repository data and maintain the integrity of its history.

## Git Is Designed to Work Locally

Because Git stores the repository history on your computer, most common operations do not require an internet connection.

You can generally inspect history, compare changes, and create commits locally.

An internet connection is needed when you perform operations that communicate with an online remote repository, such as sharing your commits with GitHub or retrieving changes from it.

This makes Git useful even when working offline.

## Git vs. GitHub

Git and GitHub are related, but **they are not the same thing**.

### Git

Git is the version control tool.

- Tracks file changes and project history.
- Creates commits and manages branches.
- Supports comparing, restoring, and combining changes.
- Works on your local computer without requiring GitHub.

### GitHub

GitHub is an online platform built around Git.

- Hosts Git repositories remotely.
- Allows developers to share projects.
- Supports collaboration, code review, and project planning.
- Provides tools such as issues, pull requests, and automated software workflows.
- Allows developers to publish and showcase their work.

Other platforms, including GItLab and Bitbucket, also host Git repositories.

### Comparison

| **Git** | **GitHub** |
| --- | --- |
| Version control system | Online development and collaboration platform |
| Primarily a tool you run locally | A service accessed online, with additional tools |
| Tracks project history | Hosts repositories and provides collaboration features |
| Does not require a GitHub account | An account is useful for hosting and collaborating on repositories |

### How They Work Together

A typical workflow looks like this:

```
Your computer
    |
    | Git tracks changes and records commits
    v
Local Git repository
    |
    | Push commits to a remote repository
    v
GitHub repository
    |
    | Other developers can retrieve and review changes
    v
Collaboration and shared development
```

You can use Git without GitHub. However, GitHub makes it easier to share work, collaborate, and showcase projects online.

## Essential Git Terminology

| **Term** | **Meaning** |
| --- | --- |
| **Repository (repo)** | A project managed by Git, including its tracked history and metadata |
| **Commit** | A recorded checkpoint of the project’s state |
| **Working directory** | The files you currently view and edit |
| **Branch** | An independent line of development within a repository |
| **Clone** | A copy of a repository, normally including its history |
| **Remote repository** | A repository hosted elsewhere, such as on GitHub |
| **Push** | Send local commits to a remote repository |
| **Pull** | Retrieve and integrate changes from a remove repository |
| **Merge** | Combine changes from different development lines |
| **Pull request** | A GitHub collaboration feature for proposing changes and discussing or reviewing them before integration |

These concepts form the foundation for learning Git’s everyday workflow.

## Using Git Through the Command Line

Git can be used through either a command-line interface (CLI) or a graphical user interface (GUI).

### Command-Line Interface

You interact with Git by typing commands in a terminal.

Advantages:

- Provides access to Git’s full range of commands.
- Makes it easier to follow tutorials and documentation.
- Helps develop a deeper understanding of Git’s workflow.
- Uses the same general command-line approach across many development environments.

### Graphical User Interface

A GUI lets you interact with Git through visual elements such as buttons, menus, and change lists.

Examples include GitHub Desktop and graphical source-control tools in Visual Studio Code.

Advantages:

- Can make changes and repository history easier to visualize.
- Reduces the need to memorize commands.
- Provides a convenient way to inspect files and commits.

Both approaches are useful. Learning the command line provides a strong foundation because not every GUI exposes every Git feature.