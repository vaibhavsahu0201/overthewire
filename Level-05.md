# Bandit Level 5 → Level 6

#Objective

Find the file that is:
- Human-readable
- 1033 bytes
- Not executable

#Challenge

Search through multiple directories using specific conditions.

#Solution

```bash
find . -type f -size 1033c ! -executable
cat <filename>
```

#Commands Used

1. `find`
2. `cat`

#Key Learning

* `find` can search files based on size, type, and permissions.
* `!` negates a search condition.
