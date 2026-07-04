# Bandit Level 29 → Level 30

## Objective

A Git repository contains the password for **Bandit30**, but it is not visible in the current branch. Investigate the repository and explore other branches.

---

## Concepts Learned

* Local branches
* Remote branches
* Tracking branches
* `HEAD`
* `git switch`
* Detached HEAD

---

# Step 1 — Read the Current File

View the README.

```bash
cat README.md
```

Output:

```text
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: <no passwords in production!>
```

The password is not present.

---

# Step 2 — Check Commit History

Display previous commits.

```bash
git log
```

Example:

```text
commit b607fba...
    fix username

commit 84c16f8...
    initial commit of README.md
```

Observation:

Unlike the previous level, there is no commit mentioning a password leak.

---

# Step 3 — Inspect the Latest Commit

View what changed.

```bash
git show
```

Output:

```diff
- username: bandit29
+ username: bandit30
```

Only the username changed.

The password never existed in the commit history.

---

# Step 4 — Check Local Branches

List local branches.

```bash
git branch
```

Output:

```text
* master
```

Only one local branch exists.

---

# Step 5 — Check All Branches

Display local and remote branches.

```bash
git branch -a
```

Output:

```text
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/dev
  remotes/origin/master
  remotes/origin/sploits-dev
```

Observation:

The repository contains additional remote branches.

This suggests the password may exist outside the `master` branch.

---

# Step 6 — Understanding the Output

```text
master
```

Local branch.

---

```text
origin/master
```

Remote-tracking reference for the master branch.

---

```text
origin/dev
```

Remote development branch.

---

```text
origin/sploits-dev
```

Another remote development branch.

---

# Step 7 — Attempt to Switch Directly

```bash
git switch origin/dev
```

Output:

```text
fatal: a branch is expected, got remote branch 'origin/dev'
```

Reason:

`origin/dev` is **not** a local branch.

It is only a reference to the remote repository.

---

# Step 8 — Detached HEAD

Temporarily inspect the remote branch.

```bash
git switch --detach origin/dev
```

Output:

```text
HEAD is now at 0bf8160 add data needed for development
```

Meaning:

Git moved to the commit pointed to by `origin/dev` without creating a local branch.

This state is called **Detached HEAD**.

---

# Command Explanations

## `git branch`

Displays only local branches.

```bash
git branch
```

---

## `git branch -a`

Displays every branch.

```bash
git branch -a
```

* Local branches
* Remote-tracking branches

---

## `git log`

Displays commit history.

```bash
git log
```

---

## `git show`

Displays information about a commit.

```bash
git show
```

---

## `git switch`

Moves from one branch to another.

```bash
git switch <branch>
```

---

## `git switch --detach`

Temporarily moves to a commit without being on a branch.

```bash
git switch --detach origin/dev
```

Useful for investigating another branch without creating a local one.

---

# Common Mistakes

❌ Thinking `master` is a file.

```bash
cat master
```

`master` is a branch, not a file.

---

❌ Trying to execute a branch.

```bash
./master
```

Branches are not executable files.

---

❌ Restoring a branch.

```bash
git restore master
```

`git restore` works with files, not branches.

---

❌ Assuming `git branch` shows every branch.

```bash
git branch
```

Only local branches are displayed.

Use:

```bash
git branch -a
```

to view both local and remote branches.

---

# Key Takeaways

* `git branch` lists local branches.
* `git branch -a` lists local and remote branches.
* A branch is a pointer to a commit, not a file.
* `origin` is the default name of the remote repository.
* `origin/dev` is a remote-tracking branch.
* `git switch --detach` allows inspection of a commit or remote branch without creating a local branch.

