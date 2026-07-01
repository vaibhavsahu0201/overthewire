# Bandit Level 10 → Level 11

#Objective

Decode the Base64 encoded password.

#Challenge

The password is encoded rather than stored as plain text.

#Solution

```bash
base64 -d data.txt
```

#Commands Used

1. `base64`

#Key Learning

* Base64 is an encoding format, not encryption.
* Use `-d` to decode Base64 encoded data.
