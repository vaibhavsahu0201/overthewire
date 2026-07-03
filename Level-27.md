# Bandit Level 27 → Level 28

## Objective

Clone a remote Git repository and find the password for **Bandit28**.

Unlike previous levels, this challenge is performed from your **local machine**, not on the OverTheWire server.

---

## Concepts Learned

* Git repositories
* Cloning a repository
* SSH URLs
* Custom SSH ports
* Working with a local Git repository

---

## Understanding the Challenge

The repository is hosted at:

```text
ssh://bandit27-git@bandit.labs.overthewire.org/home/bandit27-git/repo
```

The challenge also specifies:

* Protocol: **SSH**
* Port: **2220**
* Username: **bandit27-git**
* Password: **Same as Bandit27**

---

## Clone the Repository

Clone the repository from your **local machine**:

```bash
git clone ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo
```

---

## Explore the Repository

After cloning:

```bash
cd repo
```

List files:

```bash
ls
```

Read the available files:

```bash
cat README
```

or

```bash
cat README.md
```

The password is stored directly inside the repository.

---

## Common Mistakes

### ❌ Cloning from the Bandit server

The challenge explicitly says:

> **From your local machine (not the OverTheWire machine!)**

Git must be executed on your own system.

---

### ❌ Forgetting the SSH port

Without specifying:

```text
:2220
```

Git uses the default SSH port:

```text
22
```

which results in authentication errors because OverTheWire Git repositories are served on **2220**.

---

### ❌ Confusing Git username with Bandit username

The repository owner is:

```text
bandit27-git
```

Use:

* **Username:** `bandit27-git`
* **Password:** Your current **Bandit27 password**

---

## Key Takeaways

* `git clone` downloads a complete copy of a remote repository.
* SSH uses port **22** by default unless another port is specified.
* After cloning, all work is performed on the **local copy** of the repository.
* Always read the challenge carefully—small details like **"from your local machine"** and **"port 2220"** are essential.
