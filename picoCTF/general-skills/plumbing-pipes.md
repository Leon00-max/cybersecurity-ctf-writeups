# picoCTF · Plumbing

**Category:** General Skills

## Objective
Handle process data *outside of a file* by sending the output of a live network stream straight into a text-search tool.

## Clues in the description
- "Sometimes you need to handle process data outside of a file."
- "What's a pipe? No not that kind of pipe... This kind"

That was a direct hint to use the Linux pipe operator `|`.

## Why a pipe
Running `nc` alone dumps a huge wall of dummy text. I could save it first (`nc host port > output.txt`), but the challenge asked to avoid files. A pipe feeds the first command's output directly into the next one in memory.

## Why `grep`
The hint gave the flag format `picoCTF{...}`. `grep` reads every line coming through the pipe, ignores the junk, and prints only the line that matches.

## Command
```bash
nc <challenge-host> <port> | grep "picoCTF{"
# flag: picoCTF{REDACTED}
```

## Real-world use
- **Blue team (SOC):** filter live server logs for specific IPs or malware signatures without filling the disk.
- **Red team:** pipe scanner output into filters to isolate vulnerable targets quickly.
