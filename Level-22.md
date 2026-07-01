# Bandit Level 22 → Level 23

#Objective

Retrieve the password for `bandit23` by analyzing a cron job that automatically executes a shell script.

#Challenge

The cron job did not store the password in a fixed filename. Instead, it generated the output filename dynamically using an MD5 hash based on the user executing the script.

#Solution

Inspect the cron configuration:

```bash
cat /etc/cron.d/cronjob_bandit23
```

Read the script executed by cron:

```bash
cat /usr/bin/cronjob_bandit23.sh
```

The script generated the output filename using:

```bash
echo "I am user bandit23" | md5sum
```

Use the generated hash as the filename and read the password from `/tmp`:

```bash
cat /tmp/<generated_md5_hash>
```

#Commands Used

1. `cat /etc/cron.d/cronjob_bandit23`
2. `cat /usr/bin/cronjob_bandit23.sh`
3. `echo "I am user bandit23" | md5sum`
4. `cat /tmp/<generated_md5_hash>`

#Key Learning

- A cron job executes with the permissions of the user specified in its configuration.
- `whoami` returns the user currently executing the script, not the script owner or the logged-in user.
- `md5sum` generates a deterministic hash; the same input always produces the same output.
- Understanding how a script derives filenames is often enough to locate sensitive data without modifying or executing it with elevated privileges.
- Always analyze the logic of automated scripts instead of assuming fixed output locations.
