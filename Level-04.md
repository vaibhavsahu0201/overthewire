# Bandit Level 4 → Level 5

#Objective

Find the only human-readable file inside the `inhere` directory.

#Challenge

Several files exist, but only one contains readable text.

#Solution

```bash
file ./*
cat ./-file07
```

#Commands Used

1. `file`
2. `cat`

#Key Learning

* `file` identifies a file's type by inspecting its contents.
* File extensions are not always reliable in Linux.
