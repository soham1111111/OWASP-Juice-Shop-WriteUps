# OWASP Juice Shop – Security Policy Challenge

## Category: Miscellaneous | Challenge Name: Security Policy | Difficulty: 2 Star

### Objective

- Locate the application's **security policy / contact information** before performing any testing.
    
- Follow proper **white-hat disclosure practices**.

## Challenge Description

- This challenge demonstrates a **best practice**, not a vulnerability.
    
- Ethical hackers should always check how to responsibly report vulnerabilities before testing.

## Target URLs

```site
http://10.159.195.81:3000/security.txt
```

```site
http://10.159.195.81:3000/.well-known/security.txt
```

## Step-by-Step Solution

### Step 1: Access security.txt

- Open:

```text
/.security.txt
```

>or

```text
/.well-known/security.txt
```

### Step 2: View File Contents

- You will see something like:

```text
Contact: mailto:donotreply@owasp-juice.shop
Encryption: https://keybase.io/bkimminich/pgp_keys.asc
Acknowledgements: /#/score-board
Preferred-languages: en, ar, az, ...
Hiring: /#/jobs
Csaf: http://localhost:3000/.well-known/csaf/provider-metadata.json
Expires: Thu, 06 May 2027
```

### Step 3: Challenge Solved

- Simply accessing this file completes the challenge.

## Why It Works

- The application follows the **security.txt standard**, which provides:
    
    - Contact details for vulnerability reporting
        
    - Encryption keys for secure communication
        
    - Additional security-related metadata

## Vulnerability Type

### None (Good Practice)

- This is **not a vulnerability**
    
- It promotes **responsible disclosure**

## Impact

### Positive Security Practice

- Helps researchers report issues properly
    
- Reduces risk of irresponsible disclosure
    
- Improves coordination between researchers and developers

## Severity

**Informational**

## OWASP Mapping

- A05: Security Misconfiguration _(contextual)_
    
- Security Best Practices / Responsible Disclosure

## Root Concept

- Organizations should clearly publish:
    
    - Security contact email
        
    - PGP keys
        
    - Disclosure policy

## Prevention / Recommendation

- Always include a `security.txt` file
    
- Place it in:
    
    - `/security.txt`
        
    - `/.well-known/security.txt`
        
- Keep contact details updated
    
- Provide encryption methods (PGP keys)

## Key Lesson

- Ethical hacking starts with **permission and proper reporting channels**.

## Conclusion

This challenge emphasizes that before exploiting anything, a security researcher should first identify how to responsibly communicate findings. The `security.txt` standard makes this process transparent and structured.