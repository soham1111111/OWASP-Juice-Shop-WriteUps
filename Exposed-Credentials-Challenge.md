# OWASP Juice Shop – Exposed Credentials Challenge

## Category: Sensitive Data Exposure | Challenge Name: Exposed Credentials | Difficulty: Unknown

### Objective
- Find hardcoded but still valid test account credentials exposed on the client side and use them to log in.

### Challenge Description
- A developer accidentally left unused testing credentials inside frontend JavaScript files shipped to users.

- Because client-side code is public, anyone can inspect it.

## Exposed Credentials Found

```javascript id="u4n8ra"
testingUsername = "testing@juice-sh.op";
testingPassword = "IamUsedForTesting";
````

## Where Found

- Inside frontend bundle:

```text
main.js
```

## Step-by-Step Solution

### Step 1: Open Application

- Go to OWASP Juice Shop in browser.

### Step 2: Open Developer Tools

- Press:

```text
F12
```

>or Right Click → Inspect

### Step 3: Search Source Files

- Open:

```text
Sources
```

- Search using:

```text
credentials
password
login
@juice-sh.op
```

### Step 4: Locate Hardcoded Values

- Found:

```text
testing@juice-sh.op
IamUsedForTesting
```

![[Pasted image 20260418185528.png]]

### Step 5: Login

Use these credentials on the login page.

Challenge gets solved after successful authentication.

## Alternate Locations

Sometimes secrets are exposed in:

```text
main.js
bundle.js
comments
/assets/
/ftp/
```

## Why It Works

- Frontend JavaScript is downloadable by every user.

- Anything embedded in shipped JS can be extracted easily.

## Vulnerability Type

### Sensitive Data Exposure / Hardcoded Secrets

- Credentials stored in public client-side code.

## Impact

### Risks

- Unauthorized account access
    
- Privilege escalation
    
- Test accounts abused in production
    
- Credential reuse attacks
    
- Information disclosure

## Severity

**High**
>(Critical if privileged account)

## OWASP Mapping

- A02: Cryptographic Failures / Sensitive Data Exposure
    
- A05: Security Misconfiguration
    
- Secrets Management Failures

## Root Cause

- Credentials hardcoded in frontend code
    
- Test accounts left enabled
    
- Poor secret management practices

## Prevention

- Never store secrets client-side
    
- Remove test credentials before release
    
- Use environment-based secret storage
    
- Disable unused accounts
    
- Scan builds for secrets before deployment

## Key Lesson

If users can download it, they can read it.

## Conclusion

This challenge shows why client-side applications must never contain credentials or sensitive secrets.












