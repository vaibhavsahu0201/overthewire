   # Bandit Level 3 → Level 4

#Objective

Find the hidden file inside the `inhere` directory.

#Challenge

Hidden files are not displayed with a normal `ls`.

#Solution

```bash
cd inhere
ls -la
cat ...Hiding-From-You
```

#Commands Used

1. `cd`
2. `ls`
3. `cat`

#Key Learning

* Hidden files begin with a `.`.
* Use `ls -a` to display hidden files.
