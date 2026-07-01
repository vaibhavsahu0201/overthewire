# Bandit Level 8 → Level 9

#Objective

Find the only line that appears exactly once.

#Challenge

Duplicate lines must be removed before identifying the unique one.

#Solution

```bash
sort data.txt | uniq -u
```

#Commands Used

1. `sort`
2. `uniq`

#Key Learning

* `uniq` only works correctly on sorted input.
* `uniq -u` prints lines that occur only once.
