# OWASP Juice Shop – Confidential Document Challenge

## Category: Sensitive Data Exposure | Challenge Name: Confidential Document | Difficulty: 1 Star

### Objective

- Access a confidential internal document exposed through a publicly accessible FTP directory.

### Challenge Description
- The challenge demonstrates how sensitive internal files can be leaked due to insecure file hosting and directory exposure.

## Target URLs

```site
http://192.168.1.122:3000/ftp/legal.md
```

```site
http://192.168.1.122:3000/ftp/
```

```site
http://192.168.1.122:3000/ftp/acquisitions.md
````

## Step-by-Step Solution

### Step 1: Open Navigation Menu

- Click the top-left hamburger icon.

### Step 2: Open About Us

- Navigate to:

```text
About Us
```

### Step 3: Inspect Terms of Service Link

Hover over the **Terms of Service** hyperlink.

![[Pasted image 20260416172759.png]]

At the bottom of the browser, the linked path reveals:

```text
/ftp/legal.md
```

![[Pasted image 20260416172428.png]]

>This indicates a browsable `/ftp/` directory exists.

### Step 4: Browse FTP Directory

- Open:

```text
http://192.168.1.122:3000/ftp/
```

![[Pasted image 20260416172351.png]]

### Step 5: Access Confidential File

Open:

```text
http://192.168.1.122:3000/ftp/acquisitions.md
```

>This file contains confidential business information.

### Step 6: Return to Home Page

- After viewing the file, return to the main application page.

- Challenge gets marked as solved.



## Why It Works

- The server exposes internal markdown files inside a publicly accessible directory.

- No authentication or access restrictions are applied.

## Vulnerability Type

### Sensitive Data Exposure / Insecure Direct Object Access

- Internal documents are directly reachable via URL paths.

## Impact

### Security Risks

- Internal strategy leaks
    
- Acquisition/financial data exposure
    
- Reputation damage
    
- Competitor intelligence gathering
    
- Compliance violations
    
- Easier attacker reconnaissance

## Severity

**Medium**
>(High if real confidential data is exposed)

## OWASP Mapping

- A01: Broken Access Control
    
- A05: Security Misconfiguration
    
- A02: Cryptographic Failures (contextual)

## Root Cause

- Public file directory enabled
    
- Missing authorization checks
    
- Sensitive files stored in web root
    
- Predictable URLs

## Prevention

- Remove sensitive files from public directories
    
- Restrict file access with authentication
    
- Disable directory listing
    
- Separate internal/public storage
    
- Apply least privilege permissions
    
- Regular file exposure audits

## Key Lesson

- If a file is reachable by URL, assume attackers can find it.

- Hidden links are not protection.

## Conclusion

This challenge shows how simple directory exposure can leak confidential documents without any hacking tools—only observation and URL browsing.






