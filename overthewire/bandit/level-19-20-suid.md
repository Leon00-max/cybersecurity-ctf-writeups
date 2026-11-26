# Bandit 19 → 20: SUID binary

## 1. Where this level sits
This level starts the **privilege-escalation arc** of Bandit. Earlier levels cover permissions, encodings, networking basics and cron. From here the idea is: *a privileged program does something on your behalf, and you abuse that trust.*

The chain around it:

- 19 → 20: SUID binary that runs a command as another user
- 20 → 21: SUID binary that talks to a port you control (confused deputy)
- 21 → 22 / 22 → 23 / 23 → 24: cron-based levels

SUID (Set User ID) is one of the most important concepts in Linux privilege escalation.

## 2. Reading the challenge
> "To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary."

Three things stand out:

1. **"setuid binary"**: a SUID file runs with its *owner's* privileges, not the caller's.
2. **"Execute it without arguments"**: the binary documents itself. In real life: `--help`, `-h`, or `strings`.
3. **`/etc/bandit_pass`**: as `bandit19` I can't read `bandit20`'s file, but a SUID binary owned by `bandit20` can.

It reminds me of: the Linux permission model (owner, group, others, plus SUID/SGID/sticky), the confused deputy problem, and real SUID bugs such as PwnKit (`pkexec`), Baron Samedit (`sudo`) and Dirty Pipe (kernel-level).

## 3. What I tried

### Attempt 1: read the password directly
```bash
cat /etc/bandit_pass/bandit20
```
Result: `Permission denied`.

> 🚧 **Unfinished:** attempts 2–5 and the final solution reasoning are still to be written up.
