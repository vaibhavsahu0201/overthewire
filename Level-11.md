# Bandit Level 11 → Level 12

#Objective

Decode the password stored in `data.txt`, where all letters are rotated by 13 positions (ROT13).

#Challenge

At first, I thought `tr` worked like other commands and tried using options like `-d`, `-s`, and `-t` without understanding that it requires two character sets for translation.

#Solution

```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

#Commands Used

1. `cat`
2. `tr`

#Key Learning

* `tr` translates characters from one set to another.
* The first set contains the original characters, and the second set contains their replacements.
* ROT13 shifts every alphabet character by 13 positions.
* Numbers and special characters remain unchanged.
