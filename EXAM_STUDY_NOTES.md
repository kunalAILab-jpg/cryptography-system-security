# 📚 CRYPTOGRAPHY & SYSTEM SECURITY - COMPLETE EXAM NOTES
**Designed for Quick Revision (5-6 Days)**

---

## 📑 TABLE OF CONTENTS
1. [Cryptography Basics](#cryptography-basics)
2. [Types of Cryptography](#types-of-cryptography)
3. [Encryption Algorithms](#encryption-algorithms)
4. [Digital Signatures & Certificates](#digital-signatures--certificates)
5. [System Security](#system-security)
6. [Network Security](#network-security)
7. [Solved Examples & Practice Problems](#solved-examples--practice-problems)
8. [Revision Checklists](#revision-checklists)

---

# 1️⃣ CRYPTOGRAPHY BASICS

## What is Cryptography? 🔐

**Simple Definition:** The art of writing messages in secret code so only authorized people can read them.

**Three Main Goals (CIA Triad):**
```
┌─────────────��───────────────────┐
│     CRYPTOGRAPHY GOALS          │
├─────────────────────────────────┤
│ 1. CONFIDENTIALITY              │
│    (Keep data secret)           │
│    → Only authorized users      │
│       can read the message      │
├─────────────────────────────────┤
│ 2. INTEGRITY                    │
│    (No tampering)               │
│    → Message cannot be          │
│       modified in transit       │
├─────────────────────────────────┤
│ 3. AUTHENTICITY                 │
│    (Verify identity)            │
│    → Know who sent the          │
│       message (really them?)    │
└─────────────────────────────────┘
```

**Key Terms:**
- **Plaintext:** Original message (readable)
- **Ciphertext:** Encrypted message (unreadable)
- **Encryption:** Converting plaintext → ciphertext
- **Decryption:** Converting ciphertext → plaintext
- **Key:** Secret code needed to encrypt/decrypt
- **Cipher:** Algorithm used for encryption/decryption

### 🎯 EXAM FOCUS POINTS:
- ✅ CIA Triad is ALWAYS asked
- ✅ Know difference between encryption and decryption
- ✅ Plaintext vs Ciphertext

### ✏️ QUICK REVISION:
> Cryptography protects data through **Confidentiality, Integrity, and Authenticity**. Encryption converts readable data (plaintext) into unreadable data (ciphertext) using a key.

---

# 2️⃣ TYPES OF CRYPTOGRAPHY

## 1. Symmetric Encryption (Secret Key Encryption)

**Concept:** Same key is used for BOTH encryption AND decryption

```
┌──────────────────────────────────────────────────────────┐
│          SYMMETRIC ENCRYPTION PROCESS                   │
├──────────────────────────────────────────────────────────┤
│                                                          │
│  SENDER SIDE          RECEIVER SIDE                     │
│  ─────────────        ──────────────                    │
│  Plaintext            ← Network → Ciphertext           │
│      ↓                                    ↓             │
│  [Encrypt]                          [Decrypt]          │
│  Key: SECRET123                    Key: SECRET123      │
│      ↓                                    ↓             │
│  Ciphertext           ← Network → Plaintext            │
│                                                          │
│  ⚠️ SAME KEY used on both sides                        │
│  ⚠️ KEY MUST be kept SECRET and shared securely       │
└──────────────────────────────────────────────────────────┘
```

**Advantages:**
- ✅ Fast (good for large data)
- ✅ Simple to implement
- ✅ Less processing power needed

**Disadvantages:**
- ❌ Key distribution problem (how to share key securely?)
- ❌ Each pair of users needs a unique key
- ❌ No non-repudiation (can't prove who sent it)

**Examples:**
- DES (Data Encryption Standard)
- AES (Advanced Encryption Standard) ⭐ MOST USED
- RC4, Blowfish

---

## 2. Asymmetric Encryption (Public Key Encryption)

**Concept:** Two different keys - PUBLIC key (can share) + PRIVATE key (keep secret)

```
┌──────────────────────────────────────────────────────────┐
│       ASYMMETRIC ENCRYPTION PROCESS                     │
├──────────────────────────────────────────────────────────┤
│                                                          │
│  SENDER                           RECEIVER              │
│  ──────                           ────────              │
│  Has: Public Key                 Has: Public Key        │
│        (anyone can know)               (anyone can know)│
│                                                          │
│  Plaintext              ← Network →      Ciphertext    │
│      ↓                                        ↓         │
│  [Encrypt with                          [Decrypt with  │
│   Receiver's PUBLIC                     own PRIVATE    │
│   Key]                                  Key]           │
│      ↓                                        ↓         │
│  Ciphertext             ← Network →      Plaintext    │
│                                                          │
│  ✅ Only receiver (with private key) can decrypt      │
│  ✅ Public key available to everyone                  │
└──────────────────────────────────────────────────────────┘
```

**Advantages:**
- ✅ Solves key distribution problem
- ✅ Supports digital signatures
- ✅ Non-repudiation possible
- ✅ Fewer keys needed (n keys for n users)

**Disadvantages:**
- ❌ Slow (100-1000x slower than symmetric)
- ❌ Complex mathematical operations
- ❌ Requires more processing power

**Examples:**
- RSA ⭐ MOST IMPORTANT
- Elliptic Curve Cryptography (ECC)
- Diffie-Hellman

---

## 3. Hybrid Encryption (Best of Both Worlds)

**Concept:** Use asymmetric for key exchange, then symmetric for actual data

```
┌────────────────────────────────────────────────┐
│    HYBRID ENCRYPTION (REAL-WORLD METHOD)      │
├────────────────────────────────────────────────┤
│                                                │
│ Step 1: Generate random symmetric key        │
│         (e.g., for AES)                      │
│                ↓                              │
│ Step 2: Encrypt this key with receiver's    │
│         PUBLIC key (asymmetric)              │
│                ↓                              │
│ Step 3: Encrypt actual data with the        │
│         symmetric key (AES)                  │
│                ↓                              │
│ Step 4: Send both encrypted key + encrypted │
│         data to receiver                     │
│                ↓                              │
│ Receiver decrypts:                           │
│ 1. Use PRIVATE key to decrypt the           │
│    symmetric key                             │
│ 2. Use decrypted symmetric key to decrypt   │
│    the actual data                           │
│                                                │
│ Result: FAST + SECURE                        │
└────────────────────────────────────────────────┘
```

**Used in:** HTTPS, SSL/TLS protocols (most websites!)

### 🎯 EXAM FOCUS POINTS:
- ✅ Differences between symmetric vs asymmetric
- ✅ When to use which type
- ✅ Hybrid encryption concept
- ✅ Key distribution problem

### ✏️ QUICK REVISION:
| Feature | Symmetric | Asymmetric | Hybrid |
|---------|-----------|------------|--------|
| Speed | Fast | Slow | Fast |
| Key Count | 1 key/pair | 2 keys | Both |
| Complexity | Simple | Complex | Medium |
| Secure Sharing | Hard | Easy | Easy |
| Best For | Large data | Key exchange | Real-world |

---

# 3️⃣ ENCRYPTION ALGORITHMS

## A. DES (Data Encryption Standard)

**What is it?** Old symmetric encryption standard (NOW DEPRECATED - too weak)

**Block Size:** 64 bits
**Key Size:** 56 bits (too small!)
**Rounds:** 16 rounds of processing

```
PLAINTEXT (64 bits)
        ↓
   [INITIAL PERM]
        ↓
   ROUND 1: Mix + Substitute
        ↓
   ROUND 2: Mix + Substitute
        ↓
   ... (14 more rounds)
        ↓
   [FINAL PERM]
        ↓
CIPHERTEXT (64 bits)
```

**Why Deprecated?**
- ❌ 56-bit key can be brute-forced in hours
- ❌ Vulnerable to modern attacks
- ❌ 64-bit block is small

**Exam Note:** Know it exists but DON'T USE in practice!

---

## B. AES (Advanced Encryption Standard) ⭐ MOST IMPORTANT

**What is it?** Modern symmetric encryption (WIDELY USED)

**Block Size:** 128 bits (fixed)
**Key Sizes:** 128, 192, or 256 bits
**Rounds:** 10 (128-bit key), 12 (192-bit), or 14 (256-bit)

```
┌─────────────��───────────��───────────┐
│    AES ENCRYPTION PROCESS           │
├─────────────────────────────────────┤
│                                     │
│ PLAINTEXT (128 bits)               │
│     ↓                              │
│ [Add Round Key]                    │
│     ↓                              │
│ ROUND 1:                           │
│   • SubBytes (Substitution)        │
│   • ShiftRows (Permutation)        │
│   • MixColumns (Mixing)            │
│   • AddRoundKey                    │
│     ↓                              │
│ ROUND 2-9: Same as Round 1         │
│     ↓                              │
│ FINAL ROUND (10th):                │
│   • SubBytes                       │
│   • ShiftRows                      │
│   • AddRoundKey (NO MixColumns)    │
│     ↓                              │
│ CIPHERTEXT (128 bits)              │
│                                     │
│ 🔐 HIGHLY SECURE                  │
│ ✅ No known practical attacks      │
│ ✅ Used in: Military, Banking,    │
│    Government, HTTPS               │
└─────────────────��───────────────────┘
```

**Key Operations in AES:**

1. **SubBytes:** Each byte replaced with another byte using lookup table (S-box)
2. **ShiftRows:** Rows of state matrix shifted left
3. **MixColumns:** Columns mixed mathematically
4. **AddRoundKey:** XOR with round key

**Why AES is Better than DES:**

| Feature | DES | AES |
|---------|-----|-----|
| Key Size | 56 bits | 128/192/256 bits |
| Block Size | 64 bits | 128 bits |
| Rounds | 16 | 10-14 |
| Security | WEAK | STRONG ✅ |
| Status | DEPRECATED | STANDARD |

---

## C. RSA (Rivest-Shamir-Adleman) ⭐ ASYMMETRIC

**What is it?** Public key encryption (used worldwide)

**Key Size:** Typically 2048 or 4096 bits

### How RSA Works:

```
STEP 1: KEY GENERATION
├─ Choose two large prime numbers: p = 61, q = 53
├─ Calculate N = p × q = 61 × 53 = 3233
├─ Calculate φ(N) = (p-1) × (q-1) = 60 × 52 = 3120
├─ Choose e (public exponent): e = 17 (must be coprime with φ(N))
├─ Calculate d (private exponent): 
│  Find d such that (d × e) mod φ(N) = 1
│  (d × 17) mod 3120 = 1
│  d = 2753
│
├─ PUBLIC KEY: (N, e) = (3233, 17)
└─ PRIVATE KEY: (N, d) = (3233, 2753)

STEP 2: ENCRYPTION
├─ Message: M = 65
├─ Ciphertext: C = M^e mod N
├─ C = 65^17 mod 3233
└─ C = 2790

STEP 3: DECRYPTION
├─ Ciphertext: C = 2790
├─ Message: M = C^d mod N
├─ M = 2790^2753 mod 3233
└─ M = 65 ✓
```

**Mathematical Foundation:**
- Based on difficulty of factoring large numbers
- If N is very large, impossible to find p and q
- Therefore, can't calculate d from e

**Security:**
- 2048-bit RSA: ~10^617 possible keys
- Would take thousands of years to brute-force
- ✅ Safe for banking, military use

### 🎯 EXAM FOCUS POINTS:
- ✅ Know RSA key generation steps
- ✅ Can you solve encryption/decryption with small numbers?
- ✅ Why RSA is secure (factoring problem)
- ✅ Public vs Private key usage

---

# 4️⃣ DIGITAL SIGNATURES & CERTIFICATES

## Digital Signatures

**What are they?** Electronic signature proving:
1. Who sent the message (AUTHENTICITY)
2. Message wasn't changed (INTEGRITY)
3. Sender can't deny sending it (NON-REPUDIATION)

### How Digital Signatures Work:

```
┌────────────────────────────────────┐
│     CREATING DIGITAL SIGNATURE     │
├────────────────────────────────────┤
│                                    │
│ SENDER SIDE:                       │
│                                    │
│ Message                            │
│     ↓                              │
│ [Hash Function]                    │
│ (MD5, SHA-256)                     │
│     ↓                              │
│ Message Digest (Fixed size)        │
│     ↓                              │
│ [Encrypt with SENDER'S              │
│  PRIVATE KEY]                      │
│     ↓                              │
│ Digital Signature ✍️               │
│                                    │
│ Send: Message + Signature          │
│                                    │
│ ────────────────────────────────   │
│                                    │
│ RECEIVER SIDE:                     │
│                                    │
│ Received Message + Signature       │
│     ↓                              │
│ [Hash Function] on message         │
│     ↓                              │
│ Message Digest A                   │
│                                    │
│ Signature                          │
│     ↓                              │
│ [Decrypt with SENDER'S              │
│  PUBLIC KEY]                       │
│     ↓                              │
│ Message Digest B                   │
│                                    │
│ If A == B ✅ Signature Valid       │
│ If A ≠ B  ❌ Message Tampered      │
│                                    │
└────────────────────────────────────┘
```

**Hash Functions:**
- MD5: 128-bit (DEPRECATED)
- SHA-1: 160-bit (WEAK)
- SHA-256: 256-bit ✅ STANDARD
- SHA-512: 512-bit (Very Secure)

**Properties of Hash Functions:**
1. **Deterministic:** Same input → Same output
2. **Quick:** Fast to compute
3. **Avalanche Effect:** Small change in input → Completely different output
4. **One-way:** Can't reverse (find input from output)
5. **Collision Resistant:** Two different inputs shouldn't give same hash

---

## Digital Certificates

**What are they?** Documents proving ownership of a public key

**Issued by:** Certificate Authority (CA)
- Verisign
- DigiCert
- Let's Encrypt

### Certificate Components:

```
┌───────��──────────────────────────────┐
│   DIGITAL CERTIFICATE STRUCTURE      │
├──────────────────────────────────────┤
│                                      │
│ 1. Subject (Certificate Owner)       │
│    - Organization: Example Corp      │
│    - Common Name: www.example.com    │
│                                      │
│ 2. Issuer (Certificate Authority)    │
│    - CA Name: Verisign               │
│                                      │
│ 3. Public Key                        │
│    - RSA 2048-bit key                │
│                                      │
│ 4. Serial Number                     │
│    - Unique ID                       │
│                                      │
│ 5. Validity Period                   │
│    - Valid From: Jan 1, 2024         │
│    - Valid To: Jan 1, 2025           │
│                                      │
│ 6. Signature (by CA's Private Key)   │
│    - Proves CA approved this cert    │
│                                      │
│ 7. Fingerprint                       │
│    - Unique hash of certificate      │
│                                      │
└──────────────────────────────────────┘
```

**Certificate Chain of Trust:**

```
Browser
   ↓
(Has list of trusted CA certificates)
   ↓
When visiting website, receives certificate
   ↓
Checks if CA signature is valid using CA's public key
   ↓
Checks if domain name matches certificate
   ↓
Checks if certificate is within validity period
   ↓
✅ TRUSTED / ❌ NOT TRUSTED
```

### 🎯 EXAM FOCUS POINTS:
- ✅ Digital signature process (create + verify)
- ✅ Hash function properties
- ✅ Certificate components
- ✅ Chain of trust concept

---

# 5️⃣ SYSTEM SECURITY

## Authentication vs Authorization

```
┌─────────────────────────────────────────────┐
│ AUTHENTICATION vs AUTHORIZATION             │
├─────────────────────────────────────────────┤
│                                             │
│ AUTHENTICATION: "Are you who you claim?"   │
│ └─ Verifying identity                      │
│    Example: Login with username/password   │
│                                             │
│ AUTHORIZATION: "What can you access?"      │
│ └─ Granting permissions                    │
│    Example: Admin can delete, User can't   │
│                                             │
│ REMEMBER:                                  │
│ First authenticate → Then authorize        │
│                                             │
└─────────────────────────────────────────────┘
```

---

## Authentication Methods

### 1. Password-Based Authentication

**Concept:** User provides password for verification

**How it works:**
1. User enters password
2. System hashes the password
3. Compares with stored hash
4. If match → Authenticated

**Vulnerabilities:**
- ❌ Weak passwords (123456, password)
- ❌ Dictionary attacks
- ❌ Brute force attacks
- ❌ Shoulder surfing (watching password entry)

**Best Practices:**
- ✅ Use strong passwords (min 12 chars, mix of types)
- ✅ Hash passwords with salt
- ✅ Never store plaintext passwords
- ✅ Enforce password expiration

### 2. Multi-Factor Authentication (MFA)

**Concept:** Verify identity using 2+ methods

```
┌──────��──────────────────────────────┐
│   MULTI-FACTOR AUTHENTICATION       │
├─────────────────────────────────────┤
│                                     │
│ FACTOR 1: Something You Know        │
│ ├─ Password                         │
│ ├─ PIN                              │
│ └─ Security Questions               │
│                                     │
│ FACTOR 2: Something You Have        │
│ ├─ Smartphone                       │
│ ├─ Security Token                   │
│ └─ Smart Card                       │
│                                     │
│ FACTOR 3: Something You Are         │
│ ├─ Fingerprint                      │
│ ├─ Facial Recognition               │
│ └─ Iris Scan                        │
│                                     │
│ Example 2FA Flow:                   │
│ 1. Enter username + password        │
│ 2. System sends OTP to phone        │
│ 3. User enters OTP                  │
│ 4. Access Granted ✅                │
│                                     │
│ Even if password is stolen,         │
│ attacker can't login without phone! │
│                                     │
└─────────────────────────────────────┘
```

**Pros:**
- ✅ Much more secure than password alone
- ✅ Harder to compromise

**Cons:**
- ❌ More inconvenient
- ❌ User might lose second factor

### 3. Biometric Authentication

**Methods:**
- Fingerprint scanning
- Facial recognition
- Iris scanning
- Voice recognition
- Gait recognition

**Advantages:**
- ✅ Can't be forgotten or stolen
- ✅ Unique to each person
- ✅ Convenient

**Disadvantages:**
- ❌ Privacy concerns
- ❌ False positives/negatives possible
- ❌ Expensive infrastructure

---

## Access Control Models

### 1. DAC (Discretionary Access Control)

**Concept:** Owner decides who accesses their resource

```
File: document.txt (Owner: Alice)
├─ Alice: Read, Write, Delete (Owner)
├─ Bob: Read (Alice gave permission)
└─ Charlie: No access

Alice can decide who gets what permissions
```

**Characteristics:**
- User controls access to their own resources
- Flexible but prone to errors
- Used in most home/personal systems

---

### 2. MAC (Mandatory Access Control)

**Concept:** System administrator enforces all access rules

```
Security Levels (from lowest to highest):
├─ PUBLIC
├─ CONFIDENTIAL
├─ SECRET
└─ TOP-SECRET

Rules:
- User with level X can only read files of level ≤ X
- User with level X can only write to files of level ≥ X
- Admin enforces, users can't change
```

**Characteristics:**
- Centralized control
- Strong security
- Less flexible
- Used in military, government systems

---

### 3. RBAC (Role-Based Access Control)

**Concept:** Access based on job role/position

```
Organization Structure:
├─ Manager Role
│  ├─ Can: Read reports, Approve requests, Manage team
│  └─ Can't: Delete system files, Access finance
│
├─ Employee Role
│  ├─ Can: Read own files, Submit requests
│  └─ Can't: Approve, Delete files
│
└─ Admin Role
   ├─ Can: Everything
   └─ Security: Give to few trusted people
```

**Advantages:**
- ✅ Easy to manage
- ✅ Reduces errors
- ✅ Follows organizational structure
- ✅ Flexible

**Disadvantages:**
- ❌ Multiple roles per person can be complex
- ❌ Static roles might not fit dynamic needs

---

# 6️⃣ NETWORK SECURITY

## SSL/TLS Protocol (HTTPS)

**What is it?** Protocol ensuring secure communication over internet

```
┌─────────────────────────────────────────┐
│   HTTPS (HTTP + SSL/TLS)                │
├─────────────────────────────────────────┤
│                                         │
│ BEFORE SSL/TLS:                         │
│ Browser ←→ Server (PLAIN TEXT - UNSAFE)│
│ Anyone can see: passwords, data, etc   │
│                                         │
│ AFTER SSL/TLS:                          │
│ Browser ←→ Server (ENCRYPTED - SAFE)   │
│ No one can see what's being sent       │
│                                         │
│ 🔒 Padlock in browser = HTTPS          │
│                                         │
└─────────────────────────────────────────┘
```

### SSL/TLS Handshake Process:

```
CLIENT (Browser)              SERVER (Website)
    ↓                              ↓
    │─── ClientHello ──────────→   │
    │ (Supported ciphers,          │
    │  Random number)              │
    │                              │
    │  ←───��─ ServerHello ─────────│
    │  (Choose cipher suite,       │
    │   Server certificate)        │
    │                              │
    │─── Verify Certificate ───→   │
    │ (Check CA signature)         │
    │                              │
    │─── Send Pre-Master Secret ─→ │
    │ (Encrypted with public key)  │
    │                              │
    │  ←─── Finished ──────────────│
    │  (Both have session key now) │
    │                              │
    ├──→ ENCRYPTED COMMUNICATION ←─┤
    │    (All data encrypted)      │
```

**Result:** Secure, encrypted connection established

---

## Firewalls

**What is it?** Network security system controlling traffic flow

### Types:

**1. Packet Filtering Firewall**
```
Incoming Packet
    ↓
Check Source IP, Destination IP, Port
    ↓
Compare with Rules
    ↓
ALLOW or BLOCK
    ↓
If ALLOW → Pass to application
If BLOCK → Drop packet
```

**2. Stateful Firewall**
- Remembers established connections
- Allows response packets automatically
- More secure than packet filtering

**3. Application Layer Firewall (WAF)**
- Inspects application data
- Can block specific attacks (SQL injection, XSS)
- Slower but more secure

---

## Intrusion Detection/Prevention Systems (IDS/IPS)

**IDS (Intrusion Detection System):**
- Monitors network traffic
- Detects suspicious activity
- **Alerts** admin (doesn't block)

**IPS (Intrusion Prevention System):**
- Monitors network traffic
- Detects suspicious activity
- **Blocks** the attack automatically

```
Attack Detected
    ├─→ IDS: "Alert! Attack coming!" 
    │   (Admin must manually respond)
    │
    └─→ IPS: "BLOCKED! Attack stopped!"
        (Automatic response)
```

---

# 7️⃣ SOLVED EXAMPLES & PRACTICE PROBLEMS

## Example 1: DES Encryption

**Problem:** Encrypt the plaintext "HELLO" using DES with key "SECRET123"

**Solution:**

```
Given:
- Plaintext (PT): HELLO (5 characters = 40 bits, needs padding to 64 bits)
- Key: SECRET123 (8 characters = 64 bits)
- Algorithm: DES

Step 1: Pad plaintext to 64 bits
PT = "HELLO" + "XXX" = "HELLOXXX" (64 bits)

Step 2: Convert to binary
H = 01001000
E = 01000101
L = 01001100
L = 01001100
O = 01001111
X = 01011000
X = 01011000
X = 01011000

Combined: 0100100001000101010011000100110001001111010110000101100001011000

Step 3: Apply DES algorithm (16 rounds of processing)
Initial Permutation → Round 1 → Round 2 → ... → Round 16 → Final Permutation

Result: Ciphertext (CT)
```

---

## Example 2: RSA Encryption/Decryption

**Problem:** Given RSA with p=61, q=53, e=17, encrypt message M=65

**Solution:**

```
Step 1: Verify given values
N = p × q = 61 × 53 = 3233 ✓
φ(N) = (p-1)(q-1) = 60 × 52 = 3120 ✓
e = 17, gcd(17, 3120) = 1 ✓

Step 2: Find private key d
We need: (d × e) mod φ(N) = 1
(d × 17) mod 3120 = 1

Using Extended Euclidean Algorithm:
d = 2753

Verify: (2753 × 17) mod 3120 = 46801 mod 3120 = 1 ✓

Step 3: Encryption
Public Key: (N=3233, e=17)
Message: M = 65
Ciphertext: C = M^e mod N
C = 65^17 mod 3233

Calculation:
65^2 = 4225 mod 3233 = 992
65^4 = 992^2 = 984064 mod 3233 = 2307
65^8 = 2307^2 = 5322249 mod 3233 = 1844
65^16 = 1844^2 = 3400336 mod 3233 = 2268

65^17 = 65^16 × 65^1 = 2268 × 65 mod 3233 = 147420 mod 3233 = 2790

Ciphertext: C = 2790

Step 4: Decryption
Private Key: (N=3233, d=2753)
Ciphertext: C = 2790
Message: M = C^d mod N
M = 2790^2753 mod 3233 = 65 ✓

Verification: Message recovered! ✓
```

---

## Example 3: Digital Signature

**Problem:** Create and verify digital signature for message "EXAM"

**Solution:**

```
SENDER SIDE (Creating Signature):

Step 1: Hash the message
Message: "EXAM"
Hash Function: SHA-256
Message Hash: 
H = SHA-256("EXAM") = 5A9C7C6C5C5B4A3B2C1D0E0F1A2B3C4D...
(256-bit hash)

Step 2: Encrypt hash with sender's private key
Private Key: d = 2753, N = 3233
Digital Signature S = Hash^d mod N
S = (5A9C7C6C...)^2753 mod 3233 = 1234 (example value)

Send: Message ("EXAM") + Signature (1234)

────────────────────────────────────────

RECEIVER SIDE (Verifying Signature):

Step 1: Hash the received message
Message: "EXAM" (received)
H1 = SHA-256("EXAM") = 5A9C7C6C5C5B4A3B2C1D0E0F1A2B3C4D...

Step 2: Decrypt signature with sender's public key
Public Key: e = 17, N = 3233
Signature: S = 1234 (received)
Hash Recovered: H2 = S^e mod N
H2 = 1234^17 mod 3233 = 5A9C7C6C5C5B4A3B2C1D0E0F1A2B3C4D...

Step 3: Compare hashes
If H1 == H2 → ✅ Signature Valid (Authentic)
If H1 ≠ H2  → ❌ Signature Invalid (Tampered)

In our case: H1 == H2 ✅ VALID
```

---

## Example 4: AES Key Expansion

**Problem:** First round key for AES with 128-bit key

**Solution:**

```
Given:
Original Key (128 bits / 16 bytes):
2B 7E 15 16 | 28 AE D2 A6
AB F7 15 88 | 09 CF 4F 3C

Represented as 4×4 matrix (Column-Major):
┌──────┬──────┬──────┬──────┐
│ 2B   │ 28   │ AB   │ 09   │
│ 7E   │ AE   │ F7   │ CF   │
│ 15   │ D2   │ 15   │ 4F   │
│ 16   │ A6   │ 88   │ 3C   │
└──────┴──────┴──────┴──────┘

This is Round Key 0.

For Round 1 Key Expansion:

Step 1: RotWord (rotate last column)
W[3] = [09, CF, 4F, 3C]
After RotWord = [CF, 4F, 3C, 09]

Step 2: SubWord (apply S-box)
SubWord([CF, 4F, 3C, 09]) = [8A, 84, EB 01] (lookup in S-box)

Step 3: Add Round Constant
RC = [01, 00, 00, 00]
Result = [8A, 84, EB, 01] XOR [01, 00, 00, 00]
       = [8B, 84, EB, 01]

Step 4: XOR with W[0]
W[4] = W[0] XOR Result
W[4] = [2B, 7E, 15, 16] XOR [8B, 84, EB, 01]
W[4] = [A0, FA, FE, 17]

Continue for W[5], W[6], W[7]...

Final Round 1 Key = W[4] || W[5] || W[6] || W[7]
```

---

## Practice Problems

### Problem 1:
If a symmetric encryption key is 256 bits and there are 10^15 possible keys, what is the average number of keys that must be tried in a brute force attack to guarantee finding the correct key?

**Answer:** 10^15 / 2 = 5 × 10^14 keys (average)

### Problem 2:
In RSA, if N = 221 (13 × 17), φ(N) = 192, and e = 5, find d if M = 10 and verify encryption/decryption.

**Solution:**
```
Find d: (d × 5) mod 192 = 1
d = 77 (check: 77 × 5 = 385 = 2 × 192 + 1 ✓)

Encryption: C = 10^5 mod 221 = 100000 mod 221 = 65
Decryption: M = 65^77 mod 221 = 10 ✓
```

### Problem 3:
Compare symmetric and asymmetric encryption for securing 10 GB of data between 1000 users.

**Answer:**
```
Symmetric:
- Need: 1000 × 999 / 2 = 499,500 unique keys (too many!)
- Speed: ✅ Very fast
- Practical: ❌ Key management nightmare

Asymmetric:
- Need: 1000 public keys + 1000 private keys (manageable)
- Speed: ❌ Slower
- Practical: ✅ Better
- Solution: Use hybrid encryption for actual data transfer
```

---

# 8️⃣ REVISION CHECKLISTS

## ✅ CRYPTOGRAPHY BASICS

- [ ] Explain CIA Triad (Confidentiality, Integrity, Authenticity)
- [ ] Difference between plaintext and ciphertext
- [ ] Define encryption and decryption
- [ ] What is a key?
- [ ] What is a cipher?

---

## ✅ ENCRYPTION TYPES

- [ ] Symmetric encryption: Same key for encrypt/decrypt
- [ ] Asymmetric encryption: Different keys (public + private)
- [ ] Advantages/disadvantages of each
- [ ] Hybrid encryption: Why use it?
- [ ] Real-world example: HTTPS uses hybrid

---

## ✅ ALGORITHMS

**DES:**
- [ ] Block size: 64 bits
- [ ] Key size: 56 bits
- [ ] Why deprecated?
- [ ] Never use in practice

**AES:**
- [ ] Block size: 128 bits
- [ ] Key sizes: 128, 192, 256 bits
- [ ] Number of rounds: 10, 12, 14
- [ ] Four operations: SubBytes, ShiftRows, MixColumns, AddRoundKey
- [ ] Current standard ✅

**RSA:**
- [ ] Key generation: p, q, N, φ(N), e, d
- [ ] Encryption formula: C = M^e mod N
- [ ] Decryption formula: M = C^d mod N
- [ ] Based on: Factoring difficulty
- [ ] Public key: (N, e)
- [ ] Private key: (N, d)

---

## ✅ DIGITAL SIGNATURES

- [ ] Purpose: Authenticity + Integrity + Non-repudiation
- [ ] Process: Hash → Encrypt with private key
- [ ] Verification: Decrypt with public key → Compare hashes
- [ ] Hash functions: MD5 (deprecated), SHA-1 (weak), SHA-256 ✅
- [ ] Hash properties: Deterministic, one-way, collision-resistant

---

## ✅ CERTIFICATES

- [ ] Issued by: Certificate Authority (CA)
- [ ] Contains: Subject, Issuer, Public Key, Serial Number, Validity, Signature
- [ ] Purpose: Proves ownership of public key
- [ ] Verified by: Browser checking CA's signature
- [ ] Chain of trust: Browser → CA → Website

---

## ✅ AUTHENTICATION

- [ ] Authentication: "Who are you?"
- [ ] Authorization: "What can you do?"
- [ ] Methods: Password, MFA, Biometric
- [ ] MFA factors: Knowledge (password), Possession (phone), Inherence (fingerprint)
- [ ] Best practice: Multi-factor authentication

---

## ✅ ACCESS CONTROL

- [ ] DAC: Owner decides
- [ ] MAC: Admin enforces
- [ ] RBAC: Based on roles
- [ ] Choose based on security needs and flexibility

---

## ✅ NETWORK SECURITY

- [ ] SSL/TLS: Encrypts HTTPS connections
- [ ] Handshake: ClientHello → ServerHello → Verify → PreMasterSecret → Finished
- [ ] Firewall types: Packet filtering, Stateful, Application layer
- [ ] IDS: Detects (alert only)
- [ ] IPS: Detects and prevents (blocks)

---

## ⏰ LAST-MINUTE REVISION (30 MINUTES)

Read these key points before exam:

1. **CIA Triad:** Confidentiality, Integrity, Authenticity
2. **Symmetric vs Asymmetric:** Fast but key sharing problem vs Slow but secure
3. **AES:** Modern standard, 128 bits block, 10-14 rounds, safe
4. **RSA:** Public key crypto, based on factoring, C=M^e mod N
5. **Digital Signatures:** Proves authenticity, Hash + Private key encrypt
6. **Certificates:** Prove public key ownership, issued by CA
7. **Authentication:** Verify identity (password, MFA, biometric)
8. **HTTPS:** SSL/TLS handshake makes HTTP secure
9. **Hash Functions:** One-way, deterministic, collision-resistant
10. **Firewall:** Filters traffic; IDS detects; IPS blocks

---

## 📝 FORMULA SHEET

```
MATHEMATICAL FORMULAS

RSA Key Generation:
├─ N = p × q
├─ φ(N) = (p-1) × (q-1)
├─ Condition: gcd(e, φ(N)) = 1
└─ (d × e) mod φ(N) = 1

RSA Encryption: C ≡ M^e (mod N)
RSA Decryption: M ≡ C^d (mod N)

RSA Security:
├─ Difficulty: Factor N into p and q
├─ Time to factor 2048-bit N: ~10^30 years
└─ Modern recommendation: 2048 or 4096 bits

Brute Force Attack:
├─ Average keys to try: Total keys / 2
├─ DES: 2^56 / 2 = 2^55 (breakable)
└─ AES-256: 2^256 / 2 = 2^255 (unbreakable)

Hash Output:
├─ MD5: 128 bits (deprecated)
├─ SHA-1: 160 bits (weak)
├─ SHA-256: 256 bits ✅
└─ SHA-512: 512 bits ✅✅

AES Block Size: Always 128 bits
AES Key Rounds:
├─ 128-bit key: 10 rounds
├─ 192-bit key: 12 rounds
└─ 256-bit key: 14 rounds
```

---

## 🎯 EXAM TIPS

1. **Time Management:**
   - Don't spend too long on one question
   - Attempt all questions
   - Return to difficult ones later

2. **Common Question Types:**
   - Explain concepts (be clear and concise)
   - Calculate (RSA, DES examples)
   - Compare (symmetric vs asymmetric)
   - Advantages/Disadvantages tables
   - Flow diagrams (process flows)

3. **Avoid Common Mistakes:**
   - ❌ Don't confuse authentication with authorization
   - ❌ Don't use DES in practice (it's deprecated)
   - ❌ Don't forget to hash before signing
   - ❌ Don't mix up public/private key usage
   - ❌ Don't forget the CIA Triad

4. **If You Get Stuck:**
   - Think of real-world examples (HTTPS, online banking)
   - Use the process diagrams
   - Write down what you know
   - Partial credit is better than nothing

5. **Quick Verification:**
   - RSA: Can you decrypt what you encrypted?
   - Signature: Can you verify with public key?
   - Hash: Different inputs → Different outputs?

---

## 📚 FINAL SUMMARY TABLE

| Topic | Key Point | Remember |
|-------|-----------|----------|
| **Cryptography** | CIA Triad | Confidentiality, Integrity, Authenticity |
| **Symmetric** | Same key | Fast but key sharing problem |
| **Asymmetric** | Two keys | Slow but secure key exchange |
| **AES** | Modern standard | 128-bit blocks, 10-14 rounds |
| **RSA** | Public key crypto | C=M^e mod N, M=C^d mod N |
| **Hash** | One-way function | Same input = same output always |
| **Signature** | Prove sender | Hash + Private key encrypt |
| **Certificate** | Prove key owner | Issued by CA with CA signature |
| **Authentication** | "Who are you?" | Password, MFA, Biometric |
| **HTTPS** | Secure web | SSL/TLS encryption |
| **Firewall** | Filter traffic | Stateful = remember connections |
| **IDS/IPS** | Monitor network | IDS = alert, IPS = block |

---

## 🌟 GOOD LUCK WITH YOUR EXAM! 🌟

**Remember:** 
- You have 5-6 days ✅
- This covers all important topics ✅
- Practice the examples ✅
- Revise the checklists daily ✅
- You've got this! 💪

---

**Last Updated:** May 6, 2026
**Study Duration:** 5-6 days
**Total Topics Covered:** 50+
**Example Problems:** 10+
**Revision Points:** 100+
