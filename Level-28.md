# Bandit Level 28 → Level 29

## Objective

Investigate the Git repository to recover the password for **Bandit29**.

The current `README.md` hides the password, but Git preserves the complete history of every committed change.

---

## Concepts Learned

* Git commit history
* Repository versions
* Viewing previous file contents
* Reading commit messages
* Git object inspection

---

## Initial Observation

Reading the current file:

```bash
cat README.md
```

Output:

```text
# Bandit Notes
Some notes for level29 of bandit.

## credentials

- username: bandit29
- password: xxxxxxxxxx
```

The password has been replaced with:

```text
xxxxxxxxxx
```

This suggests it may have existed in an earlier commit.

---

## View Commit History

Display all commits:

```bash
git log
```

Example:

```text
commit e2e1de5...
    fix info leak

commit 2678cfa...
    add missing data

commit 9530d52...
    initial commit of README.md
```

---

## Understanding the Commit Messages

The message:

```text
fix info leak
```

indicates that sensitive information was accidentally exposed and later removed.

This means the previous commit is likely to contain the original password.

---

## View an Older Version of a File

Git allows viewing a file exactly as it existed in a previous commit.

Example:

```bash
git show <commit>:README.md
```

Using the shortened commit hash:

```bash
git show 2678cfa:README.md
```

This displays `README.md` from that specific commit without changing your working directory.

---

## Common Mistakes

### ❌ Using `git commit`

```bash
git commit
```

`git commit` **creates** a new commit.

It does **not** display previous commits.

---

### ❌ Using repository URLs after cloning

Example:

```bash
git log ssh://...
```

Once the repository has been cloned, Git already knows which repository you are in.

Simply use:

```bash
git log
```

inside the cloned repository.

---

### ❌ Assuming the current file is the only version

Git stores the complete history of the repository.

Even if information is removed from the latest version, it may still exist in older commits.

---

## Key Takeaways

* Git stores every committed version of a project.
* Commit messages often reveal why changes were made.
* `git log` shows the repository's history.
* `git show <commit>:<file>` lets you inspect previous versions of a file without modifying the current working tree.
* Sensitive information committed to Git can often remain recoverable unless the repository history is rewritten.
