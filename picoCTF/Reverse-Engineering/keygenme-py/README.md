# picoCTF - keygenme-py

## Category
Reverse Engineering

## Goal
Understand how the Python program validates a license key and reconstruct the expected key.

## Initial Inspection

The challenge provided:

`keygenme-trial.py`

I searched the source code for important variables and functions.

```bash
grep -n "username_trial\|key_part\|check_key\|sha256" keygenme-trial.py
“I analyzed a Python license-key validation routine. I identified the validation function, traced how SHA-256 was used to derive part of the expected key from a known username,
 reproduced the calculation, and demonstrated that the weakness was in exposed client-side validation logic rather than in SHA-256 itself"
How would you fix it
“I would avoid placing secret key-generation logic entirely on the client. For a licensing system,
 I could use server-side validation or digitally signed licenses. The application could verify a signature using a public key, while the private signing key remains on a protected server.”

Understanding how software transforms input and makes security decisions.

What I learned:
I learned that reverse engineering is often about finding the part of a program that makes a security decision and tracing the data used in that decision.
In this challenge, SHA-256 was not cracked. The program exposed a known username and the exact indexes it used from that username's SHA-256 hash to construct a license key. By reproducing that logic,
I could determine what the program expected. This demonstrates that strong cryptography can still be part of an insecure system if the surrounding validation design exposes everything needed to reproduce
a trusted value.
