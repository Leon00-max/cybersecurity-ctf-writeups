# C: stdio buffering and unsafe functions

## Standard I/O buffering
C's standard I/O may **buffer** output instead of sending it to the terminal immediately. `fflush(stdout)` forces pending output to be written. This matters for interactive programs where a prompt must appear *before* the program waits for input.

The deeper lesson: C programs talk through streams (`stdin`, `stdout`, `stderr`) that can connect to terminals, files, pipes or other programs. Understanding that helps in systems programming, automation, networking and security tooling.

```text
USER / SCRIPT
     │
     ▼
   stdin
     │
     ▼
 C PROGRAM
     ├── stdout ──→ normal output
     └── stderr ──→ errors
```

Buffering is not a vulnerability by itself. But knowing a program's I/O sequence helps you analyse its behaviour and build reliable test tooling.

> **Developer mindset:** don't only ask whether input/output works. Ask what happens with malformed, oversized, missing, piped or unexpected input.

## Unsafe functions and safer habits

| Unsafe | Better | Caveat |
|---|---|---|
| `gets()` | `fgets(buf, size, stdin)` | `gets()` was removed from the C standard. Never use it. |
| `strcpy()` | `snprintf()`, `strlcpy()` (if available) | `strncpy()` is **not** a safe drop-in: it may not NUL-terminate. |
| `sprintf()` | `snprintf()` | Always check the return value for truncation. |
| `strcat()` | `snprintf()` / `strlcat()` | `strncat()`'s size argument is the space left, not the buffer size. |
| `scanf("%s", buf)` | `scanf("%99s", buf)` or `fgets` | Width must be buffer size minus 1. |

Rule of thumb: always state the maximum length, and check what happens at the boundary.
