# picoCTF · keygenme-py

**Category:** Reverse Engineering

## Goal
Understand how a Python program validates a license key, and work out the key it expects.

## Initial inspection
Provided file: `keygenme-trial.py`. I searched the source for the important names:

```bash
grep -n "username_trial\|key_part\|check_key\|sha256" keygenme-trial.py
```

## What I found
I identified the validation function and traced how SHA-256 is used to derive part of the expected key from a known username. Then I reproduced the calculation.

**SHA-256 was not cracked.** The program exposed the username and the exact hash indexes it used to build the key. The weakness was exposed client-side validation logic, not the hash.

## How I'd fix it
Don't put secret key-generation logic on the client. Use server-side validation, or digitally signed licenses: the app verifies a signature with a public key while the private signing key stays on a protected server.

## What I learned
Reverse engineering is often about finding the part of a program that makes a **security decision** and tracing the data behind it. Strong cryptography can still sit inside an insecure design if the surrounding logic exposes everything needed to reproduce a trusted value.
