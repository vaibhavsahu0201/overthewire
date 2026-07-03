# Bandit Level 25 → Level 26

## Objective

Log in as **bandit26**.

The challenge states that **bandit26's login shell is not `/bin/bash`**. The goal is to identify the login shell, understand how it works, and find a way to escape it.

---

## Concepts Learned

* Login shells
* `/etc/passwd`
* Restricted environments
* The `more` pager
* Reading shell scripts before executing them

---

## Investigation Process

### 1. Find the login shell

Every Linux user has a login shell defined in `/etc/passwd`.

```bash
grep bandit26 /etc/passwd
```

Example output:

```text
bandit26:x:11026:11026:bandit level 26:/home/bandit26:/usr/bin/showtext
```

The last field is the user's **login shell**.

---

### 2. Read the login shell script

```bash
cat /usr/bin/showtext
```

Output:

```bash
#!/bin/sh

export TERM=linux

exec more ~/text.txt
```

---

## Script Breakdown

```bash
export TERM=linux
```

Sets the terminal type.

---

```bash
exec more ~/text.txt
```

* Starts the `more` pager.
* `exec` replaces the current shell with `more`.
* When `more` exits, the SSH session also ends.

---

## Important Discovery

Reading the manual revealed that `more` supports:

* `v` → Opens the current file in **vi**.
* `!command` → Executes a command in a subshell (when available).

These features are the basis of the intended escape.

---

## Common Mistakes

### ❌ Looking in the home directory for the login shell

The login shell is **not** stored inside the user's home directory.

It is configured in:

```text
/etc/passwd
```

---

### ❌ Treating `/etc/passwd` output as a file path

Example:

```text
/home/bandit26:/usr/bin/showtext
```

This is **not** a directory.

It represents:

```text
Home Directory : Login Shell
```

---

### ❌ Investigating unrelated files

Files such as:

* `bandit27-do`
* `text.txt`

were not the starting point of the challenge.

The key clue was the user's configured login shell.

---

## Key Takeaways

* A login shell can be **any executable**, not just `/bin/bash`.
* `/etc/passwd` is the first place to check when investigating user login behavior.
* Always read shell scripts before executing them.
* Programs such as `more` may provide ways to escape a restricted environment.
