# Bandit Level 12 → Level 13

#Objective

Recover the password from a hexadecimal dump that has been compressed multiple times using different formats.

#Challenge

This level wasn't about one command—it was about identifying each file type and extracting it step by step. I initially thought renaming a file changed its format, but learned that extensions only help tools recognize the expected file type.

#Solution

```bash
mkdir /tmp/<directory>
cp data.txt /tmp/<directory>

xxd -r data.txt > data.bin
file data.bin

mv data.bin data.gz
gzip -d data.gz

file data
mv data data.bz2
bzip2 -d data.bz2

file data
mv data data.tar
tar -xf data.tar

# Continue repeating:
# file -> rename -> extract
```

#Commands Used

1. `xxd`
2. `file`
3. `mv`
4. `gzip`
5. `bzip2`
6. `tar`

#Key Learning

* `xxd -r` converts a hexadecimal dump back into its original binary form.
* `file` should always be used before extracting a file.
* File extensions do not determine the actual file type.
* `gzip`, `bzip2`, and `tar` are different formats and require different extraction tools.
* Keep repeating `file` until the final readable file is reached.
