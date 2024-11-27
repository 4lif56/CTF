# Solution to My Friend John CTF Challenge
You did complete it right?

## Problem Analysis
The challenge involved cracking a password-protected zip file, `flag.zip`. The password was related to the organization name and a number.

### Tools Used:
- `zip2john` — to extract password hash from the zip file.
- `John the Ripper` — to crack the password using a wordlist.
- `crunch` — to generate a custom wordlist based on a given pattern.

## Steps:
1. **Extract the password hash from `My_Friend_John.zip`**:  
   First, use the `zip2john` tool to extract the password hash from the `My_Friend_John.zip` file. This will allow you to later crack the password using a tool like `John the Ripper`.
   ```bash
   zip2john My_Friend_John.zip > hash.txt
2. Crack the password using `John the Ripper` with a custom wordlist:
   ```bash
   hash.txt --wordlist=/usr/share/wordlists/rockyou.txt
3. Once received the password, open `My_Friend_John.zip` with the recovered password.
4. Repeat the first step with flag.txt (eg. flag_hash.txt):
   ```bash
   zip2john flag.zip > flag_hash.txt
4. Generate a Custom Wordlist Using crunch:
   Follow the pattern according to the hint (uccuitm<symbol><four digits>)
   ```bash
   crunch 12 12 -o custom_wordlist.txt -t uccuitm^%%%%


## Passwords:
1. 9112iloveyou
2. uccuitm@1111

### Flag:
The flag was: `UCC{CR4CK3D_W1TH_J0HN_W0ND3RFUL}`

