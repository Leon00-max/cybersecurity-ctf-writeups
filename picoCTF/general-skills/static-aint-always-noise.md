# picoCTF · Static ain't always noise

**Event:** picoCTF 2021 · **Category:** General Skills
**Tools:** `file`, `chmod`, `ltdis.sh`, `strings`, `grep`
**Skills:** static analysis, binary inspection, string extraction

## Challenge
> Can you look at the data in this binary? The bash script might help!

Files provided: `static` (binary) and `ltdis.sh` (script).

## Steps

**1. Recon**
```bash
ls -la
file static
# static: ELF 64-bit LSB pie executable, x86-64, dynamically linked, not stripped
cat ltdis.sh
```

`ltdis.sh` runs two common static-analysis tools:
```bash
objdump -D "$1" > "$1.ltdis.x86_64.txt"   # disassembly
strings "$1"    > "$1.ltdis.strings.txt"  # printable strings
```

**2. Run it and search the strings output**
```bash
chmod +x ltdis.sh
./ltdis.sh static
grep picoCTF static.ltdis.strings.txt
```

## Takeaway
The flag was sitting in plain text inside the binary. That's the binary-world version of leaving secrets in HTML comments or JS bundles: if it ships with the file, anyone can read it. See [Natas 1](../../overthewire/natas/README.md) for the web equivalent.
