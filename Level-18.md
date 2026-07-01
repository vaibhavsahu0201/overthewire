# Bandit Level 18 → Level 19

#Objective

Retrieve the password stored in the `readme` file despite being logged out immediately after SSH login.

#Challenge

The login shell was intentionally configured to terminate the session, preventing access to an interactive terminal.

#Solution

Instead of opening an interactive shell, execute a command directly during the SSH connection.

```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220 "cat readme"
```

#Commands Used

1. `ssh bandit18@bandit.labs.overthewire.org -p 2220`
2. `ssh bandit18@bandit.labs.overthewire.org -p 2220 "cat readme"`

#Key Learning

- SSH can execute a command remotely without starting an interactive shell.
- Authentication and shell initialization are separate stages of an SSH session.
- If the shell exits immediately, remote command execution can still be used.
- Always read the level description carefully—it often contains both the obstacle and the location of the target file.
