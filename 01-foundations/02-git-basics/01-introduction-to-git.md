# Introduction to Git

**Version Control** is your project’s “time machine.” It records changes over time so you can recall specific versions, compare updates, and see exactly who changed what.

---

## The Core Philosophy: Snapshots

Unlike older systems that store a list of changes (deltas), Git thinks in **Snapshots**.

- **The “Picture”:** Every time you commit, Git takes a miniature “picture” of your entire filesystem.
- **Efficiency:** If a file hasn’t changed, Git just links to the previous version rather than duplicating it.
- **Integrity:** Every snapshot is identified by a **SHA-1 hash** (a 40-character ID). This makes it impossible to lose data or corrupt files without Git noticing.

---

## The Three States

To use Git, you must understand where your files “live” at any given moment:

| **State** | **Meaning** | **Location** |
| --- | --- | --- |
| **Modified** | Changes exist but aren’t saved to the DB yet. | **Working Tree** |
| **Staged** | You’ve marked a file to go into the next snapshot. | **Staging Area (Index)** |
| **Committed** | The data is safely stored in your local database. | **Git Directory (.git)** |

### The Local Workflow

1. **Modify:** Edit your files.
2. **Stage:** Use `git add` to move changes to the Staging Area.
3. **Commit:** Use `git commit` to move staged changes into a permanent snapshot.

---

## Git + GitHub: The Dynamic Duo

It is vital to distinguish the **tool** from the **platform:**

- **Git (The Engine):** The software on your **local machine** that manages the snapshots and history.
- **GitHub (The Hub):** A **cloud-based hosting service** for your Git repositories.

**Why use GitHub?** It allows you to showcase your portfolio, manage changes through “Pull Requests,” and collaborate without overwriting your teammates’ work.

---

## Collaboration & Syncing

Most developers work locally and then “sync” with a **Remote Repository** on GitHub.

### The Branching Strategy

Instead of editing the “Main” copy directly, you create a **Branch**. This is a safe, independent workspace where you can experiment. Once your code is perfect, you **Merge** it back into the main project.

### The Syncing Cycle

- **Pull:** Fetch the latest changes from your team on GitHub to your local computer.
- **Push:** Send your local committed snapshots up to GitHub for others to see.

---

## History & Origin

- **Created by:** Linus Torvalds (2005) for the Linux Kernel
- **The Catalyst:** After losing access to a proprietary tool (BitKeeper), the community needed a **distributed** system that was fast, secure, and handled large projects efficiently.
- **The Advantage:** Because Git is **Distributed**, every collaborator has a **full mirror** of the repository. If the server dies, any local copy can restore it.