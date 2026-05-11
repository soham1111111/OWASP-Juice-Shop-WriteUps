# OWASP Juice Shop – Weird Crypto Challenge

## Category: Cryptographic Issues | Challenge Name: Weird Crypto | Difficulty: 2 Star

### Objective

- Inform the shop about an insecure cryptographic algorithm or library that should not be used.

## Challenge Description

- This challenge demonstrates insecure cryptographic practices.
    
- The application expects users to report usage of weak hashing algorithms.

## Step-by-Step Solution

### Step 1: Open Complaint / Feedback Section

- Navigate to:

```text
Customer Feedback
```

>or

```text
Complaints
```

### Step 2: Submit Crypto Warning

- Enter a message mentioning insecure hashing.

- Example:

```text
Do not use MD5 for password hashing.
```

### Step 3: Submit Feedback

- Complete captcha if required
    
- Submit the form

### Step 4: Challenge Solved

- After successful submission, the challenge gets marked as completed.

![[Pasted image 20260507233043.png]]

## Why It Works

- MD5 is an outdated and insecure hashing algorithm.
    
- Juice Shop detects references to insecure crypto algorithms/libraries.

## Vulnerability Type

### Cryptographic Issues

- Weak password hashing
    
- Insecure cryptographic implementation

## Impact

### Security Risks

- Fast brute-force attacks
    
- Rainbow table attacks
    
- Credential cracking
    
- Weak password storage

## Severity

**High**

## OWASP Mapping

- A02: Cryptographic Failures

## Root Cause

- Use of deprecated hashing algorithms
    
- Missing modern password hashing protections

## Secure Alternatives

- Use modern password hashing algorithms such as:

```text
bcrypt
Argon2
scrypt
PBKDF2
```

## Prevention

- Never use MD5/SHA1 for password hashing
    
- Use adaptive hashing algorithms
    
- Add salts to password hashes
    
- Enforce strong password policies

## Key Lesson

- Fast hashes are dangerous for password storage.

## Conclusion

This challenge highlights why outdated cryptographic algorithms like MD5 should never be used for password hashing in modern applications.


