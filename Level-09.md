# Bandit Level 9 → Level 10

#Objective

Find the password hidden among human-readable strings.

#Challenge

The file contains mostly binary data.

#Solution

```bash
strings data.txt | grep "=="
```

#Commands Used

1. `strings`
2. `grep`

#Key Learning

* `strings` extracts printable text from binary files.
* Piping the output to `grep` helps narrow the search.
