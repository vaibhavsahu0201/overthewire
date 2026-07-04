# Bandit Level 32 → Level 33

## Objective

Escape from a restricted shell (`uppershell`) and obtain the password for **bandit33**.

---

# Step 1 — Login

SSH into the Bandit server.

```bash
ssh bandit32@bandit.labs.overthewire.org -p 2220
```

After logging in, the prompt changes to:

```text
>>
```

This is **not** a normal Bash shell.

It is a restricted shell called **uppershell**.

---

# Step 2 — Observe the Restriction

Try common Linux commands.

```bash
pwd
```

Output:

```text
sh: 1: PWD: Permission denied
```

Another example:

```bash
ls
```

Output:

```text
sh: 1: LS: Permission denied
```

### Observation

Every command entered is automatically converted to uppercase.

Example:

```text
pwd  →  PWD
ls   →  LS
cat  →  CAT
```

Since Linux is case-sensitive, commands such as `PWD`, `LS`, and `CAT` do not exist.

---

# Step 3 — Investigate the Shell

Instead of typing normal commands, use shell parameter expansion.

```bash
$0
```

Output:

```text
$
```

The prompt changes from

```text
>>
```

to

```text
$
```

This indicates that the restricted shell has been escaped and a normal shell is now available.

---

# Step 4 — Verify the Current User

```bash
whoami
```

Output:

```text
bandit33
```

You are now operating as the **bandit33** user.

---

# Step 5 — Read the Password

```bash
cat /etc/bandit_pass/bandit33
```

This displays the password for the next level.

---

# Understanding the Challenge

## What is `uppershell`?

`uppershell` is a restricted shell.

Instead of executing commands directly, it first converts all user input to uppercase.

Example:

```text
ls
```

becomes

```text
LS
```

Because Linux commands are case-sensitive, execution fails.

---

## Why did `$0` work?

`$0` is a **special shell parameter**.

It stores the name of the currently running shell or script.

Unlike ordinary commands, shell parameter expansion is handled by the shell itself.

Using `$0` bypasses the uppercase restriction and causes the shell to execute itself in a way that escapes the restricted environment.

---

## Why could `bandit33` read the password?

Every Bandit password file is protected by Linux file permissions.

Example:

```text
-r-------- 1 bandit33 bandit33 ...
```

Meaning:

* Owner (`bandit33`) → Read permission
* Group → No permission
* Others → No permission

When logged in as `bandit33`, the Linux kernel recognizes that the current user owns the file and allows it to be read.

---

# Commands Used

```bash
pwd
ls
$0
whoami
cat /etc/bandit_pass/bandit33
```

---

# Concepts Learned

## Restricted Shell

A restricted shell limits what a user can execute by filtering or modifying input.

Examples include:

* Blocking commands
* Restricting directories
* Converting user input
* Disabling shell features

---

## Shell Parameter Expansion

The shell replaces special parameters before executing commands.

Example:

```bash
$0
```

represents the current shell or script.

Common special parameters include:

| Parameter | Meaning                          |
| --------- | -------------------------------- |
| `$0`      | Current shell or script          |
| `$?`      | Exit status of previous command  |
| `$$`      | Current process ID               |
| `$#`      | Number of command-line arguments |
| `$@`      | All command-line arguments       |

---

## Linux Case Sensitivity

Linux treats uppercase and lowercase characters as different.

Examples:

```text
ls   ✔
LS   ✘

cat  ✔
CAT  ✘

pwd  ✔
PWD  ✘
```

---

# Key Takeaways

* Always identify how a restricted shell modifies input before attempting to bypass it.
* Linux commands are case-sensitive.
* Shell parameter expansion is processed differently from ordinary command names.
* Escaping a restricted shell often relies on understanding shell parsing rather than trying random commands.
* Linux file permissions determine who can read a file based on ownership and permission bits.
