# Task 5: Password Auditing & Cryptography Basics

**Growfinix Cybersecurity Internship — Month 1**

## Goal
Explain the difference between encryption and hashing, and demonstrate why weak/unsalted hashes are trivially crackable while modern hashing (bcrypt/Argon2) resists dictionary attacks.

## Environment
- Kali Linux (VirtualBox VM)
- John the Ripper

## Concept
- **Encryption** is reversible — data can be decrypted back to its original form using a key. Used for protecting data in transit or storage where you need to retrieve the original value.
- **Hashing** is one-way — it cannot be reversed. Used for storing passwords, so even if a database leaks, raw passwords aren't directly recoverable.
- **Why bcrypt/Argon2 matter**: legacy hashes like MD5/SHA1 are extremely fast to compute, letting attackers try billions of guesses per second. bcrypt and Argon2 are deliberately slow and use unique salts per password, making large-scale dictionary/brute-force attacks impractical.

## Process
1. Created a sample list of common weak passwords
2. Generated MD5 hashes of each password
3. Ran a dictionary attack using John the Ripper with the rockyou.txt wordlist
4. Cracked all weak MD5 hashes within seconds
5. Compared against a bcrypt hash of the same password to demonstrate resistance to the same attack

## Commands Used
```bash
for pw in $(cat passwords.txt); do echo -n "$pw" | md5sum | awk '{print $1}'; done > hashes.txt
john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hashes.txt
john --show --format=raw-md5 hashes.txt
```

## Results
- All sample MD5 hashes cracked within seconds using a dictionary attack
- Demonstrates why storing passwords as raw MD5/SHA1 is unsafe for production systems

## Conclusion
Modern systems must use bcrypt or Argon2 with strong, unique salts per password to resist dictionary and rainbow table attacks. Fast, unsalted hash functions like MD5 offer effectively no protection against a targeted attacker with a good wordlist.

## Deliverables
- `hashes.txt` — sample generated hashes
- `screenshots/` — terminal output of cracking process

## Disclaimer
All passwords and hashes used were self-generated sample data for demonstration purposes — no real or leaked credentials were used.
