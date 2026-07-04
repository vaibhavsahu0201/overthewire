# Bandit Level 31 → Level 32

## Objective

Push a file to the remote Git repository.

Requirements given in `README.md`:

* File name: `key.txt`
* Content: `May I come in?`
* Branch: `master`

---

# Step 1 — Read the Instructions

View the README.

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

Contents:

```text
May I come in?
```

Verify:

```bash
cat key.txt
```

---

# Step 3 — Check Git Status

```bash
git status
```

Unexpected Output:

```text
nothing to commit, working tree clean
```

### Observation

Although `key.txt` exists, Git does not detect it.

This indicates that Git is ignoring the file.

---

# Step 4 — Investigate Hidden Files

Display all files.

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

`*.txt`

means

```text
*
```

matches any filename.

Therefore Git ignores every file ending with

```text
.txt
```

Examples:

```text
notes.txt
key.txt
password.txt
hello.txt
```

Since `key.txt` matches the rule, Git ignores it.

---

# Step 5 — Force Git to Track the File

Normally:

```bash
git add key.txt
```

fails because the file is ignored.

Force Git to stage it.

```bash
git add -f key.txt
```

### Meaning of `-f`

`-f`

stands for

**Force**

It tells Git:

> Add this file even though it matches a `.gitignore` rule.

---

# Step 6 — Verify the Staged File

```bash
git status
```

Output:

```text
Changes to be committed:

new file: key.txt
```

The file is now staged.

---

# Step 7 — Commit the Changes

Initially Git displayed:

```text
Author identity unknown
```

Git requires every commit to contain:

* Author name
* Author email
* Commit message
* Timestamp

Configure the repository.

```bash
git config user.name "cybersec"
git config user.email "cybersec@example.com"
```

Create the commit.

```bash
git commit -m "Add key.txt"
```

---

# Step 8 — Push to the Remote Repository

```bash
git push origin master
```

The server validates the submission.

Output:

```text
Well done!
Here is the password for the next level:
```

After validation Git displays:

```text
remote rejected
(pre-receive hook declined)
```

---

# Why Was the Push Rejected?

The rejection is **intentional**.

The remote repository contains a **pre-receive hook**.

Workflow:

```text
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
        ├── Prints next password
        └── Rejects the push
```

The repository never actually changes.

This allows thousands of Bandit players to solve the same challenge without modifying the original repository.

---

# Git Concepts Learned

## `.gitignore`

A file that tells Git which files should not be tracked.

Example:

```text
*.txt
```

Ignore every file ending with `.txt`.

---

## `git add`

Stages files before committing.

```bash
git add file
```

---

## `git add -f`

Force Git to stage an ignored file.

```bash
git add -f key.txt
```

---

## Staging Area

Git does **not** commit files directly.

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
```

The staging area lets you choose exactly which changes will be included in the next commit.

---

## `git commit`

Creates a snapshot of the staged changes.

```bash
git commit -m "message"
```

Each commit stores:

* Changed files
* Author
* Email
* Timestamp
* Commit message

---

## `git config`

Configures Git settings.

Repository only:

```bash
git config user.name "cybersec"
git config user.email "cybersec@example.com"
```

Global configuration:

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

```text
Remote : origin
Branch : master
```

---

## Git Hook

A Git hook is a script that runs automatically when specific Git events occur.

Examples:

* Before commit
* After commit
* Before push
* After push

---

## Pre-receive Hook

Runs on the **remote server** before accepting a push.

Bandit uses a pre-receive hook to:

* Validate the submitted file
* Print the next password
* Reject the push intentionally

This keeps the repository unchanged for future players.

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

* `.gitignore` controls which files Git ignores.
* Ignored files are hidden from `git status`.
* `git add -f` overrides `.gitignore` for a specific file.
* Changes follow the workflow:
  **Working Directory → Staging Area → Commit → Push**.
* Every commit requires author information.
* `git push` sends commits, **not individual files**.
* A pre-receive hook can validate or reject pushes on the remote server before they are accepted.
