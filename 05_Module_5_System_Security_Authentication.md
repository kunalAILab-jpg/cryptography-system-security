# 📚 MODULE 5: SYSTEM SECURITY & AUTHENTICATION

## 🎯 LEARNING OBJECTIVES

By the end of this module, you will understand:
- ✓ Authentication vs Authorization
- ✓ Password-based authentication
- ✓ Multi-Factor Authentication (MFA)
- ✓ Biometric authentication
- ✓ Password hashing and salting
- ✓ Access Control models (DAC, MAC, RBAC)
- ✓ Real-world security practices

**Time to Complete:** 50-65 minutes | **Difficulty:** ⭐⭐ Medium

---

## 📖 SECTION 1: AUTHENTICATION VS AUTHORIZATION

### 🔑 TWO DIFFERENT CONCEPTS!

**MOST CONFUSED TOPIC** - Understand this clearly!

```
┌────────────────────────────────────────────────┐
│  AUTHENTICATION vs AUTHORIZATION               │
├────────────────────────────────────────────────┤
│                                                │
│  AUTHENTICATION: "WHO ARE YOU?"                │
│  ├─ Verify identity                           │
│  ├─ Prove you are who you claim               │
│  ├─ Example: Login with username/password     │
│  ├─ Checks: Is this really John?              │
│  └─ Answer: YES/NO (binary)                   │
│                                                │
│  AUTHORIZATION: "WHAT CAN YOU DO?"            │
│  ├─ Grant/deny permissions                    │
│  ├─ Decide what user can access               │
│  ├─ Example: Can John delete files?           │
│  ├─ Checks: Does John have admin role?        │
│  └─ Answer: Allowed/Denied (based on role)   │
│                                                │
│  ═══════════════════════════════════════════  │
│                                                │
│  PROCESS ORDER:                                │
│  ├─ FIRST: Authenticate (who are you?)        │
│  ├─ THEN: Authorize (what can you do?)        │
│  └─ Without auth → auth fails → no access    │
│                                                │
└────────────────────────────────────────────────┘
```

### 🎯 Real-World Example: Airport Security

```
AUTHENTICATION:
├─ Show your passport
├─ Security checks: "Are you really John Smith?"
├─ Verifies using ID, fingerprints, questions
├─ Result: YES, you are John Smith ✓

AUTHORIZATION:
├─ Check your boarding pass
├─ Determines: Which flight can you board?
├─ "You're authorized for Flight 101 to NY"
├─ Not authorized for other flights
└─ Result: Access to Gate 5 only

Without Authentication:
├─ Can't board any flight ❌
├─ No one knows who you are

With Authentication but no Authorization:
├─ Verified as John Smith ✓
├─ But no boarding pass
├─ Can't board ❌
```

---

## 📖 SECTION 2: PASSWORD-BASED AUTHENTICATION

### 🔐 How Password Authentication Works

```
┌──────────────────────────────────────────────┐
│  PASSWORD AUTHENTICATION PROCESS             │
├──────────────────────────────────────────────┤
│                                              │
│  REGISTRATION PHASE:                         │
│  ├─ User creates account                     │
│  ├─ User enters password: "MySecure123"     │
│  ├─ System hashes password                   │
│  │  Hash = SHA256("MySecure123")            │
│  │       = "A3K2B091F7D18982..."           │
│  └─ Stores: (username, hash)                │
│     Does NOT store plaintext! ✓             │
│                                              │
│  LOGIN PHASE:                                │
│  ├─ User enters username: "john"            │
│  ├─ User enters password: "MySecure123"    │
│  ├─ System hashes input                      │
│  │  Input_Hash = SHA256("MySecure123")     │
│  │           = "A3K2B091F7D18982..."       │
│  ├─ System retrieves stored hash             │
│  │  Stored_Hash = "A3K2B091F7D18982..."    │
│  ├─ Compare:                                 │
│  │  If Input_Hash == Stored_Hash → ✅       │
│  │  If Input_Hash ≠ Stored_Hash → ❌        │
│  └─ Result: Login success/failure            │
│                                              │
└──────────────────────────────────────────────┘
```

### ⚠️ Password Attacks

#### 1️⃣ Brute Force Attack

```
Attacker:
├─ Tries every possible password
├─ "aaa", "aab", "aac", ...
├─ Eventually finds correct one

Prevention:
├─ Rate limiting (max 5 tries per 5 minutes)
├─ Account lockout (after 10 failed attempts)
├─ Longer passwords (exponentially more tries needed)
```

#### 2️⃣ Dictionary Attack

```
Attacker:
├─ Uses common passwords dictionary
├─ "password", "123456", "admin"
├─ Tests hundreds of thousands quickly

Why it works:
├─ Humans are predictable
├─ Most use weak, common passwords
├─ Faster than true brute force

Prevention:
├─ Enforce strong password requirements
├─ Ban common passwords
├─ "password123" → REJECTED
```

#### 3️⃣ Rainbow Table Attack

```
Attacker pre-computes:
├─ Hash of every possible password
├─ "a" → A3K2B091...
├─ "b" → B4L3C092...
├─ ... millions of hashes
└─ When steals database → quick lookup

Prevention:
├─ Use SALT (random string added to password)
├─ Hash(password + salt) instead of Hash(password)
├─ Each password has different salt
├─ Rainbow tables become useless!

Example:
├─ User "john" with password "secret"
├─ Salt: "R@nd0m123"
├─ Hash(secret + R@nd0m123) = A3K2B091...
├─ User "alice" with password "secret"
├─ Salt: "DiFf3r3nt456"
├─ Hash(secret + DiFf3r3nt456) = X@#9$K2L...
├─ Same password → different hashes! ✓
```

#### 4️⃣ Phishing Attack

```
Attacker creates:
├─ Fake website (looks like real site)
├─ User enters username/password
├─ Attacker captures credentials
├─ Now has real password

Prevention:
├─ Check URL carefully
├─ Look for HTTPS/🔒
├─ Be suspicious of emails
├─ Never click links in emails
├─ Type URL directly instead
```

### ✅ Password Best Practices

```
FOR USERS:

DO:
├─ ✅ Use 12+ character passwords
├─ ✅ Mix: uppercase, lowercase, numbers, symbols
├─ ✅ Use unique passwords for each site
├─ ✅ Use password manager (LastPass, 1Password)
├─ ✅ Enable MFA where possible
└─ ✅ Never share passwords

DON'T:
├─ ❌ Use common passwords (password, 123456)
├─ ❌ Use personal info (name, birthday, address)
├─ ❌ Use words from dictionary
├─ ❌ Reuse passwords across sites
├─ ❌ Share passwords with others
├─ ❌ Write password on sticky notes
└─ ❌ Click suspicious links

───────────────────────────────────────

FOR DEVELOPERS:

DO:
├─ ✅ Hash passwords with bcrypt/Argon2
├─ ✅ Use salt (unique per password)
├─ ✅ Use slow hash function (on purpose!)
├─ ✅ Force strong password requirements
├─ ✅ Implement rate limiting
├─ ✅ Lock accounts after failed attempts
└─ ✅ Encourage MFA

DON'T:
├─ ❌ Store passwords in plaintext
├─ ❌ Use simple hash (MD5, SHA-256 alone)
├─ ❌ Hash password without salt
├─ ❌ Use fast hash functions
├─ ❌ Allow weak passwords
└─ ❌ Reuse salt across users
```

---

## 📖 SECTION 3: MULTI-FACTOR AUTHENTICATION (MFA)

### 🔐 What is MFA?

**Definition:** Verify identity using 2 or more methods

**Why?** Even if password is stolen, attacker can't login!

### 🎯 Three Authentication Factors

```
┌──────────────────────────────────────────────────────┐
│    THREE AUTHENTICATION FACTORS                      │
├──────────────────────────────────────────────────────┤
│                                                      │
│  FACTOR 1: SOMETHING YOU KNOW                       │
│  (Knowledge)                                         │
│  ├─ Password                                        │
│  ├─ PIN (Personal Identification Number)            │
│  ├─ Security questions ("What's your pet name?")   │
│  ├─ Passphrase                                      │
│  └─ Example: "My password is SecurePass123"        │
│                                                      │
│  ───────────────────────────────────────────────    │
│                                                      │
│  FACTOR 2: SOMETHING YOU HAVE                       │
│  (Possession)                                        │
│  ├─ Smartphone                                      │
│  ├─ Security token/fob (generates codes)           │
│  ├─ Smart card                                      │
│  ├─ USB key                                         │
│  ├─ Email (receive code)                           │
│  └─ Example: "OTP sent to 555-0123"                │
│                                                      │
│  ───────────────────────────────────────────────    │
│                                                      │
│  FACTOR 3: SOMETHING YOU ARE                        │
│  (Inherence - Biometric)                            │
│  ├─ Fingerprint scanning                           │
│  ├─ Facial recognition (Face ID)                   │
│  ├─ Iris scanning                                  │
│  ├─ Voice recognition                             │
│  ├─ Gait recognition (walking pattern)             │
│  └─ Example: "Fingerprint verified"                │
│                                                      │
└──────────────────────────────────────────────────────┘
```

### 📱 MFA Methods & Examples

```
2-Factor Authentication (2FA):

Combination 1: Password + SMS
├─ User enters: username + password
├─ Server sends: OTP (One-Time Password) to phone
├─ User enters: OTP
├─ Server verifies: OTP code matches
├─ Result: Access granted ✓

Combination 2: Password + Email
├─ User enters: username + password
├─ Server sends: verification link to email
├─ User clicks: link in email
├─ Server verifies: email verified
├─ Result: Access granted ✓

Combination 3: Password + Authenticator App
├─ User enters: username + password
├─ User opens: Google Authenticator / Authy
├─ User enters: 6-digit code
├─ Server verifies: code matches (based on time)
├─ Result: Access granted ✓

Multi-Factor (3+ Factors):

Example: Password + Fingerprint + Email
├─ User enters: password
├─ User provides: fingerprint scan
├─ User receives: verification email
├─ All three verified → Access granted ✓
```

### 🎯 MFA Flow Diagram

```
┌─────────────────────────────────────────────────┐
│     TYPICAL 2FA (Password + OTP) FLOW            │
├─────────────────────────────────────────────────┤
│                                                 │
│  User visits: amazon.com                        │
│      ↓                                          │
│  Enter: username "john@email.com"               │
│  Enter: password "MySecure123"                  │
│      ↓                                          │
│  Server: Validates password ✓                   │
│      ↓                                          │
│  Server: Sends OTP to phone                     │
│      ↓                                          │
│  User receives SMS: "Your code is: 123456"      │
│      ↓                                          │
│  User enters: 123456                            │
│      ↓                                          │
│  Server: Validates OTP ✓                        │
│      ↓                                          │
│  ✅ LOGIN SUCCESSFUL!                           │
│                                                 │
│  ═════════════════════════════════════════      │
│                                                 │
│  Why is this secure?                            │
│  ├─ Even if password stolen:                    │
│  │  Attacker needs SMS code (can't access)      │
│  ├─ Even if SMS intercepted:                    │
│  │  Code expires in 5-10 minutes                │
│  ├─ Even if OTP guessed:                        │
│  │  Wrong code → Login fails                    │
│  └─ Two independent factors = Secure!           │
│                                                 │
└─────────────────────────────────────────────────┘
```

### ✅ Advantages of MFA

```
1. Dramatically increases security
   ├─ Password alone: Vulnerable to:
   │  ├─ Brute force
   │  ├─ Dictionary attack
   │  ├─ Phishing
   │  └─ Data breach
   └─ With MFA: Attacker needs multiple factors

2. Prevents common attacks
   ├─ Password stolen → Still can't login (need 2nd factor)
   ├─ Phishing attack → Need physical device
   └─ Insider threat → Limited by second factor

3. Industry standard
   ├─ Banks: Use card + PIN
   ├─ Google/Microsoft: SMS/Authenticator app
   ├─ Government: Often requires biometric
   └─ Enterprises: Nearly universal
```

### ❌ Disadvantages of MFA

```
1. More inconvenient
   ├─ Slower login process
   ├─ Extra steps every time
   └─ Can be annoying

2. Hardware dependency
   ├─ Lost phone → Can't login
   ├─ Email provider down → Can't verify
   └─ Backup codes needed

3. Cost
   ├─ SMS: Small cost per message
   ├─ Biometric scanners: Expensive hardware
   └─ Still worth it for security
```

---

## 📖 SECTION 4: BIOMETRIC AUTHENTICATION

### 🔐 What is Biometric Authentication?

**Definition:** Authentication using physical/behavioral characteristics

**Advantage:** Can't be forgotten or stolen (unlike passwords)

### 📊 Types of Biometrics

```
┌───────────────────────────────────┬────────────────────┐
│ BIOMETRIC TYPE                    │ EXAMPLES & NOTES   │
├───────────────────────────────────┼────────────────────┤
│ Fingerprint                       │ Most common        │
│ └─ Unique ridge patterns          │ Mobile phones      │
│                                   │ Government IDs     │
├───────────────────────────────────┼────────────────────┤
│ Facial Recognition                │ Face ID on iPhone  │
│ └─ Unique facial features         │ Airports           │
│                                   │ Surveillance       │
├───────────────────────────────────┼────────────────────┤
│ Iris Scanning                     │ High security      │
│ └─ Unique iris pattern            │ Government         │
│                                   │ Borders            │
├───────────────────────────────────┼────────────────────┤
│ Voice Recognition                 │ Phone verification │
│ └─ Unique voice characteristics   │ Voiceprint         │
├───────────────────────────────────┼────────────────────┤
│ Palm Print                        │ Rare/Specialized   │
│ └─ Unique palm vein patterns      │ Hospitals          │
├───────────────────────────────────┼────────────────────┤
│ Gait Recognition                  │ Experimental       │
│ └─ Unique walking pattern         │ Surveillance       │
└───────────────────────────────────┴────────────────────┘
```

### ✅ Advantages of Biometric

```
1. CANNOT BE FORGOTTEN
   └─ Unlike password (you can forget)

2. CANNOT BE SHARED
   └─ Unlike password (you might share)

3. CANNOT BE EASILY STOLEN
   └─ Attacker needs actual body part!

4. CONVENIENT
   └─ Just scan fingerprint/face, no typing

5. UNIQUE
   └─ 99.9%+ unique per person

6. FAST
   └─ Instant recognition
```

### ❌ Disadvantages of Biometric

```
1. PRIVACY CONCERNS
   ├─ Biometric data is very personal
   ├─ Surveillance implications
   └─ Who controls this data?

2. FALSE POSITIVES/NEGATIVES
   ├─ Might not recognize: Tired person, dirty finger
   ├─ Might accept wrong person: 0.1% error rate
   └─ Not 100% accurate

3. EXPENSIVE
   ├─ Fingerprint scanner: $50-500
   ├─ Iris scanner: $2000+
   ├─ Facial recognition: $1000+
   └─ Not feasible for small businesses

4. CANNOT BE CHANGED
   ├─ Password compromised → Change it
   ├─ Fingerprint compromised → Can't change!
   └─ Permanent vulnerability

5. CANNOT BE USED ALONE
   ├─ Usually requires password too
   └─ For added security
```

---

## 📖 SECTION 5: ACCESS CONTROL MODELS

### 🔐 What is Access Control?

**Definition:** System determining WHO can access WHAT resources

**Formula:**
```
Authentication (WHO) + Authorization (WHAT) = Access Control
```

### 1️⃣ DAC (Discretionary Access Control)

**Definition:** Owner of resource decides who accesses it

```
┌──────────────────────────────────┐
│  DAC: OWNER DECIDES              │
├──────────────────────────────────┤
│                                  │
│  File: document.txt              │
│  Owner: Alice                    │
│                                  │
│  Alice decides:                  │
│  ├─ Alice: Read, Write, Delete  │
│  ├─ Bob: Read only              │
│  ├─ Charlie: No access          │
│  └─ Diana: Read, Write          │
│                                  │
│  Alice can change permissions    │
│  whenever she wants!             │
│                                  │
└──────────────────���───────────────┘
```

**Characteristics:**
- Flexible (owner has full control)
- User-friendly
- Not very secure (mistakes possible)
- Used in: Personal computers, home networks

**Vulnerability:**
```
Problem: If Alice infected with malware
├─ Malware runs as Alice
├─ Malware can: Read, Write, Delete files
├─ Malware can: Infect other users' files
└─ No protection from trusted user being compromised!
```

---

### 2️⃣ MAC (Mandatory Access Control)

**Definition:** System administrator enforces ALL access rules

```
┌──────────────────────────────────────────┐
│  MAC: ADMIN ENFORCES                     │
├──────────────────────────────────────────┤
│                                          │
│  Security Levels (from low to high):     │
│  ├─ Level 1: PUBLIC (anyone)             │
│  ├─ Level 2: CONFIDENTIAL (org)          │
│  ├─ Level 3: SECRET (need-to-know)       │
│  └─ Level 4: TOP-SECRET (rare access)    │
│                                          │
│  Rules (Mandatory):                      │
│  ├─ User Level 2 can read Level 1-2     │
│  ├─ User Level 2 can write only to 2+   │
│  ├─ User Level 4 can read anything      │
│  ├─ User Level 4 can write only to 4    │
│  └─ Admin ENFORCES these rules          │
│     └─ User cannot override!            │
│                                          │
│  Example:                                │
│  ├─ Employee classified Level 2         │
│  ├─ Tries to read Level 4 document      │
│  ├─ System: "DENIED" (automatically)   │
│  └─ Employee cannot override!           │
│                                          │
└──────────────────────────────────────────┘
```

**Characteristics:**
- Strict (system enforces, no exceptions)
- Secure (strong protection)
- Inflexible (hard to change)
- Complex to implement
- Used in: Military, government, nuclear facilities

**Advantages:**
- No accidental security breaches
- Information cannot leak due to user mistake
- Designed for high-security environments

**Disadvantages:**
- Not practical for business (too restrictive)
- Difficult to use
- Hard to manage exceptions

---

### 3️⃣ RBAC (Role-Based Access Control)

**Definition:** Access based on user's job ROLE

```
┌────────────────────────────────────────────┐
│  RBAC: ROLE-BASED                          │
├────────────────────────────────────────────┤
│                                            │
│  Organization Structure:                   │
│                                            │
│  CEO ROLE:                                 │
│  ├─ Permissions: View all reports         │
│  ├─ Permissions: Approve spending >$100k  │
│  ├─ Permissions: Access financials        │
│  └─ Permissions: Manage staff              │
│                                            │
│  MANAGER ROLE:                             │
│  ├─ Permissions: View team's files        │
│  ├─ Permissions: Approve leave requests   │
│  ├─ Permissions: Approve spending <$5k   │
│  └─ Permissions: Create reports           │
│                                            │
│  EMPLOYEE ROLE:                            │
│  ├─ Permissions: View own files           │
│  ├─ Permissions: Submit leave request     │
│  ├─ Permissions: Create own documents     │
│  └─ Permissions: Access shared folder     │
│                                            │
│  INTERN ROLE:                              │
│  ├─ Permissions: View public folder       │
│  ├─ Permissions: Create in temp folder    │
│  └─ Permissions: No financial access      │
│                                            │
│  Assignment:                               │
│  ├─ Alice = CEO role → Gets CEO perms    │
│  ├─ Bob = Manager role → Gets Mgr perms  │
│  ├─ Charlie = Employee role → Gets Emp p.│
│  └─ Diana = Intern role → Gets Intern p. │
│                                            │
│  If Alice promoted to CEO:                │
│  └─ Simply assign CEO role                │
│     → All permissions change automatically
│                                            │
│  If Bob takes vacation:                   │
│  ├─ Assign another manager temporarily    │
│  └─ Remove assignment when back           │
│                                            │
└────────────────────────────────────────────┘
```

**Characteristics:**
- Practical for business
- Easy to manage (roles, not individual permissions)
- Flexible (add new roles, modify as needed)
- Scalable (1000s of users, dozens of roles)
- Secure (controlled permissions by role)
- Used in: Enterprise, business, government

**Advantages:**
- Easy to understand
- Follows organizational structure
- Easy to onboard/offboard employees
- Simple to audit compliance
- Reduces errors

**Disadvantages:**
- Less granular than MAC
- Role explosion (too many roles)
- Difficult to handle exceptions
- Role creep (permissions kept after promotion)

---

## 📊 ACCESS CONTROL COMPARISON

```
┌──────────────────────┬──────────┬──────────┬──────────┐
│ Feature              │ DAC      │ MAC      │ RBAC     │
├──────────────────────┼──────────┼──────────┼──────────┤
│ Who decides?         │ Owner    │ Admin    │ Admin    │
│ Flexibility          │ High     │ Low      │ Medium   │
│ Security             │ Low      │ Very High│ Good     │
│ Ease of use          │ Easy     │ Hard     │ Easy     │
│ Scalability          │ Poor     │ Poor     │ Good     │
│ Practical for biz?   │ No       │ No       │ YES ✓    │
│ Used where?          │ Personal │ Military │ Business │
└──────────────────────┴──────────┴──────────┴──────────┘
```

---

## 📋 REVISION CHECKLIST

- [ ] Authentication = WHO, Authorization = WHAT
- [ ] Order: Authenticate first, then authorize
- [ ] Know password attack types (brute force, rainbow table)
- [ ] Hash passwords with salt (not plaintext)
- [ ] MFA uses 2+ factors (knowledge, possession, inherence)
- [ ] Biometric can't be forgotten but has privacy concerns
- [ ] DAC: Owner decides (flexible, not secure)
- [ ] MAC: Admin enforces (secure, not practical)
- [ ] RBAC: Role-based (practical for business)
- [ ] Understand when to use each access model

---

## 📝 POSSIBLE EXAM QUESTIONS

### Theory

**Q1: Explain authentication and authorization with example.**

*Answer:*
- Authentication: Verify identity (login with password)
- Authorization: Grant permissions (can user delete files?)
- Example: Airport (Auth = check passport, Author = check boarding pass)

**Q2: Compare DAC, MAC, and RBAC.**

*Answer:*
- DAC: Owner decides, flexible, insecure
- MAC: Admin enforces, very secure, inflexible
- RBAC: Role-based, practical for business, scalable

**Q3: Why is biometric better than password?**

*Answer:*
- Can't be forgotten
- Can't be shared
- Hard to steal
- Convenient
- But: Privacy concerns, can't change if compromised

---

## 🌟 KEY TAKEAWAYS

| Topic | Remember |
|-------|----------|
| **Auth** | WHO, verify identity, first step |
| **Author** | WHAT, grant permissions, after auth |
| **Password** | Hash + salt, strong 12+ chars |
| **MFA** | 2+ factors, much more secure |
| **Biometric** | Unique, convenient, permanent |
| **DAC** | Owner decides, home/personal |
| **MAC** | Admin enforces, military/government |
| **RBAC** | Role-based, business/enterprise |

---

## ✅ MODULE 5 COMPLETE!

**All Modules Finished!** 🎉

**What to do now:**
1. Review all 5 modules
2. Solve all practice problems
3. Take mock exams
4. Revise weak areas
5. Get that A+! 📝

---

**Estimated Time Spent:** 50-65 minutes ⏱️
**Checklist Items:** 10 ✓
**Total Course Time:** ~4.5 hours (perfect for exam prep!)

*You've done it! You're completely ready for the exam!* 💪✨
