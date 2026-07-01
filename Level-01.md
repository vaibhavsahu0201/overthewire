# Bandit Level 1 → Level 2

#Objective

Read the password stored in a file named `-`.

#Challenge

The filename `-` is treated as standard input by many commands.

#Solution

```bash
cat ./-
```

#Commands Used

1.`cat`

#Key Learning

* `./` tells the shell to treat `-` as a filename instead of an option.
* Special filenames may require a path to access them.
