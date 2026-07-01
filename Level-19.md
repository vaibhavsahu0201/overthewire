# Bandit Level 19 → Level 20

#Objective

Use the provided SetUID binary to read the password for `bandit20`.

#Challenge

Directly reading `/etc/bandit_pass/bandit20` was not permitted with the current user's privileges.

#Solution

Verify the execution context:

```bash
./bandit20-do whoami
```

Read the password using the SetUID binary:

```bash
./bandit20-do cat /etc/bandit_pass/bandit20
```

#Commands Used

1. `ls -l`
2. `./bandit20-do`
3. `./bandit20-do whoami`
4. `./bandit20-do cat /etc/bandit_pass/bandit20`

#Key Learning

- The `s` permission bit indicates a SetUID executable.
- A SetUID program runs with the permissions of its owner, not the user executing it.
- `whoami` is a simple way to verify the effective user of a SetUID program.
- Execute an unfamiliar binary without arguments first to understand its expected usage before supplying commands.
