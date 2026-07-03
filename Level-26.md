# Bandit Level 26 → Level 27

## Objective

Escape the restricted environment started by **bandit26's login shell** and obtain the password for **bandit27**.

---

## Concepts Learned

* Restricted shells
* Process replacement using `exec`
* The `more` pager
* `vi` editor
* Shell escaping from interactive programs

---

## Understanding the Flow

From the previous level:

```text
bandit26 Login Shell
        │
        ▼
/usr/bin/showtext
        │
        ▼
exec more ~/text.txt
```

When logging in as **bandit26**, a Bash shell is **not** started.

Instead, `showtext` replaces itself with:

```text
more ~/text.txt
```

If `more` exits, the SSH session also ends.

---

## Process Flow

```text
SSH Login
    │
    ▼
Authentication
    │
    ▼
/usr/bin/showtext
    │
    ▼
more
    │
    ▼
vi
    │
    ▼
bash
```

---

## Key Idea

The `more` program supports interactive features.

Useful shortcuts discovered from its manual:

```text
v
```

Opens the current file in **vi**.

---

```text
!command
```

Executes a command in a subshell (when supported).

---

Once inside **vi**, it is possible to spawn a shell and continue as **bandit26**.

---

## Common Mistakes

### ❌ Reducing the font size

Using:

```text
Ctrl + -
```

only changes the **font size**.

It does **not** change the terminal dimensions.

---

### ✅ Correct approach

Physically resize the terminal window so it has fewer rows.

This forces `more` to pause instead of exiting immediately.

---

### ❌ Assuming the issue was SSH

Authentication was successful.

The real challenge was understanding what happened **after** SSH authentication, when the login shell (`showtext`) started `more`.

---

## Key Takeaways

* Login shells are simply programs configured for a user.
* `exec` replaces the current process instead of creating a new one.
* Interactive programs such as `more` and `vi` may provide shell escape mechanisms.
* Understanding the execution flow is often more important than trying random commands.
