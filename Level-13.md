# Bandit Level 13 → Level 14

#Objective

Use the provided private SSH key to log in as `bandit14` and retrieve the next password.

#Challenge

I initially tried using the SSH key without specifying a destination and later encountered permission issues when using the key on my local machine. I learned that SSH private keys require restricted permissions before they can be used.

#Solution

```bash
chmod 600 sshkey.private

ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
```

After logging in:

```bash
cat /etc/bandit_pass/bandit14
```

#Commands Used

1. `chmod`
2. `ssh`
3. `cat`

#Key Learning

* A private key is another authentication method besides passwords.
* `chmod 600` protects the private key so only the owner can read and write it.
* SSH refuses to use private keys with overly permissive permissions.
* The `-i` option specifies the identity file (private key) for authentication.
