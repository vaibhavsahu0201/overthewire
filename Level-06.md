# Bandit Level 6 → Level 7

#Objective

Find the file owned by:
- User: `bandit7`
- Group: `bandit6`
- Size: 33 bytes

#Challenge

Searching the entire filesystem produces many permission errors.

#Solution

```bash
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
cat /var/lib/dpkg/info/bandit7.password
```

#Commands Used

1. `find`
2. `cat`

#Key Learning

* `2>/dev/null` hides error messages by redirecting stderr.
* Even if many permission errors appear, valid results are still shown.
