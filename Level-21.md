# Bandit Level 21 → Level 22

#Objective

Find how a scheduled cron job stores the password for `bandit22` and retrieve it.

#Challenge

A cron job was automatically executed every minute. Instead of containing the password, the cron configuration pointed to a script that performed the actual task.

#Solution

Inspect the cron configuration:

```bash
ls /etc/cron.d
cat /etc/cron.d/cronjob_bandit22
```

The cron job executed:

```bash
/usr/bin/cronjob_bandit22.sh
```

Read the script:

```bash
cat /usr/bin/cronjob_bandit22.sh
```

The script:

- Read `/etc/bandit_pass/bandit22`
- Wrote its contents to a file in `/tmp`
- Changed the file permissions to `644`

Finally, read the file created by the script to obtain the password.

#Commands Used

1. `ls /etc/cron.d`
2. `cat /etc/cron.d/cronjob_bandit22`
3. `cat /usr/bin/cronjob_bandit22.sh`
4. `cat /tmp/<generated_filename>`

#Key Learning

- Cron is a time-based job scheduler that executes commands automatically.
- Cron configuration usually points to a script rather than containing the actual logic.
- Always inspect the script executed by a cron job to understand its behavior.
- `chmod 644` makes a file readable by everyone while allowing only the owner to modify it.
- In privilege-related tasks, focus on where sensitive data is written rather than only where it is read.
