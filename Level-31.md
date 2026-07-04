# Bandit Level 31 → Level 32

## Objective

Push a file to the remote Git repository.

Requirements given in `README.md`:

* File name: `key.txt`
* Content: `May I come in?`
* Branch: `master`

---

# Step 1 — Read the Instructions

Read the repository instructions.

```bash
cat README.md
```

Output:

```text
This time your task is to push a file to the remote repository.

Details:
    File name: key.txt
    Content: 'May I come in?'
    Branch: master
```

---

# Step 2 — Create the Required File

Create the file.

```bash
nano key.txt
```

Add the following content:

```text
May I come in?
```

Verify the contents.

```bash
cat key.txt
```

---

# Step 3 — Check Git Status

```bash
git status
```

Unexpected output:

```text
On branch master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean
```

### Observation

Although `key.txt` exists, Git does not detect it.

This indicates that Git is ignoring the file.

---

# Step 4 — Investigate Hidden Files

List all files, including hidden ones.

```bash
ls -la
```

Notice:

```text
.gitignore
```

Read it.

```bash
cat .gitignore
```

Output:

```text
*.txt
```

---

# Understanding `.gitignore`

`.gitignore` tells Git which files should **not** be tracked.

Pattern:

```text
*.txt
```

means:

* `*` → Match any filename.
* `.txt` → Match every file ending with `.txt`.

Examples:

```text
notes.txt
key.txt
password.txt
hello.txt
```

Since `key.txt` matches this pattern, Git ignores it.

---

# Step 5 — Force Git to Track the File

Normally,

```bash
git add key.txt
```

would fail because the file is ignored.

Force Git to stage the file.

```bash
git add -f key.txt
```

### Meaning of `-f`

`-f` stands for **Force**.

It tells Git:

> "Add this file even if it matches a rule in `.gitignore`."

---

# Step 6 — Verify the Staging Area

```bash
git status
```

Output:

```text
Changes to be committed:

new file: key.txt
```

The file has now been added to the **staging area**.

---

# Step 7 — Configure Git Identity

While committing, Git displays:

```text
Author identity unknown
```

Every Git commit stores:

* Author name
* Author email
* Commit message
* Timestamp

Configure the repository.

```bash
git config user.name "cybersec"
git config user.email "cybersec@example.com"
```

Verify:

```bash
git config --list
```

---

# Step 8 — Commit the Changes

Create a commit.

```bash
git commit -m "Add key.txt"
```

Git creates a snapshot of the staged changes.

---

# Step 9 — Push the Commit

Push the local commit to the remote repository.

```bash
git push origin master
```

The server validates the submission and prints:

```text
Well done!
Here is the password for the next level:
```

After validation, Git reports:

```text
remote rejected
(pre-receive hook declined)
```

---

# Why Was the Push Rejected?

The rejection is **intentional**.

The Bandit server uses a **pre-receive hook**.

Workflow:

```text
Working Directory
        │
        ▼
git add
        │
        ▼
Staging Area
        │
        ▼
git commit
        │
        ▼
Local Repository
        │
        ▼
git push
        │
        ▼
Remote Repository
        │
        ▼
Pre-receive Hook
        │
        ├── Checks key.txt
        ├── Validates contents
        ├── Prints the next password
        └── Rejects the push
```

The push is rejected so the shared repository remains unchanged for future players.

---

# Git Concepts Learned

## `.gitignore`

A configuration file that tells Git which files should not be tracked.

Example:

```text
*.txt
```

Ignore every `.txt` file.

---

## `git add`

Stages changes before committing.

```bash
git add file
```

---

## `git add -f`

Forces Git to stage an ignored file.

```bash
git add -f key.txt
```

---

## Staging Area

Git does **not** commit directly from the working directory.

Workflow:

```text
Working Directory
        │
        ▼
git add
        │
        ▼
Staging Area
        │
        ▼
git commit
        │
        ▼
Local Repository
```

The staging area lets you decide exactly which changes will be included in the next commit.

---

## `git commit`

Creates a snapshot of the staged files.

```bash
git commit -m "message"
```

Each commit contains:

* File changes
* Author
* Email
* Commit message
* Timestamp

---

## `git config`

Configures Git settings.

Repository only:

```bash
git config user.name "cybersec"
git config user.email "cybersec@example.com"
```

Global:

```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```

---

## `git push`

Uploads local commits to a remote repository.

```bash
git push origin master
```

Syntax:

```text
git push <remote> <branch>
```

Example:

* Remote → `origin`
* Branch → `master`

---

## Git Hook

A Git hook is a script that automatically runs when a Git event occurs.

Examples:

* Before commit
* After commit
* Before push
* After push

---

## Pre-receive Hook

Runs on the **remote server** before a push is accepted.

In this level it:

* Validates the submitted file.
* Prints the next password.
* Rejects the push intentionally.

---

# Commands Used

```bash
cat README.md
nano key.txt
cat key.txt
ls -la
cat .gitignore
git status
git add -f key.txt
git config user.name "cybersec"
git config user.email "cybersec@example.com"
git commit -m "Add key.txt"
git push origin master
```

---

# Key Takeaways

* `.gitignore` tells Git which files to ignore.
* Ignored files do not appear in `git status`.
* `git add -f` overrides `.gitignore` for a specific file.
* Git workflow:
  **Working Directory → Staging Area → Commit → Push**.
* Every commit requires an author name and email.
* `git push` sends **commits**, not individual files.
* A remote **pre-receive hook** can validate and reject a push before it is accepted.
