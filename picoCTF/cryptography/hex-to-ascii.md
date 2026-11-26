# picoCTF · Hex to ASCII

**Category:** General Skills / Cryptography fundamentals
**Tools:** CyberChef, Python, `xxd`, an ASCII table

## Objective
Convert a string of hexadecimal values (the `0x` prefix) into readable ASCII.

## The part where I got stuck
I knew `0x` meant hex and that ASCII maps numbers to characters. I did the first few by hand (`0x70` = p, `0x69` = i, `0x63` = c, `0x6f` = o, so "pico") and refused to do 50 more.

My failed attempts, in order:
- `bytes.fromhex()` on the raw string: failed on `0x` and spaces.
- `replace(' ', '')`: still failed because of `0x`.
- Both replaces: worked, but I lost the string in a fresh terminal.
- `binascii.unhexlify()`: same formatting problems.
- `xxd -r -p`: expects plain hex, so `0x` gave garbage.
- CyberChef "From Hex": failed because I pasted `0x` and spaces.

**Lesson:** the tool was never broken. My *input format* was. When a decoder fails, check the input before blaming the tool.

## Working methods
```bash
# Python (hex string without 0x or spaces)
python3 -c "print(bytes.fromhex('<hex-string>').decode('utf-8'))"

# xxd (spaces are fine, 0x prefixes are not)
echo "70 69 63 6f ..." | xxd -r -p
```

## Real-world use
- **Malware analysis:** attackers hide URLs, IPs and commands as hex or Base64 to dodge simple AV scans.
- **Web security / traffic analysis:** URLs, cookies and packet captures use hex encoding (e.g. `%20` for a space).
