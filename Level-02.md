
# Bandit Level 2 → Level 3

#Objective

Read the password stored in a file with spaces in its name.

#Challenge

The shell treats spaces as separators between arguments.

#Solution

```bash
cat "spaces in this filename"
```

#Commands Used

1. `cat`

#Key Learning

* Use quotes (`" "`) or escape spaces (`\ `) when working with filenames containing spaces.
* The shell splits arguments unless they are quoted.
