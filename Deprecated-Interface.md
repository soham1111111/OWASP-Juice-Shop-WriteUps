# OWASP Juice Shop – Deprecated Interface

## Category :

**Vulnerable Components**

### Challenge Name

**Deprecated Interface**

### Difficulty

**2 Star**

## Objective

- Use a deprecated B2B interface that was not properly shut down.

## Description

- This challenge is solved by using the old XML-based complaint upload feature that is still enabled inside the application.

## Vulnerable Page

```http
http://192.168.1.122:3000/#/complain
````

## Step-by-Step Solution

### Step 1: Open Complaint Page

- Navigate to:

```text
#/complain
```

### Step 2: Create XML File

- Example:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<complaint>
  <name>Test User</name>
  <email>test@test.com</email>
  <message>Test Complaint</message>
</complaint>
```

Save as:

```text
complaint.xml
```

### Step 3: Upload XML File

- Use the upload option in Complaint Box.

### Step 4: Submit

- After successful upload, challenge gets solved.

![[Pasted image 20260421162625.png]]

## Why It Works

- A deprecated XML complaint interface was not removed and is still functional.

## Vulnerability Type

### Vulnerable Components / Legacy Interface Exposure

## Impact

- Hidden legacy features accessible
    
- Increased attack surface
    
- Possible XML parser risks
    
- Old insecure functionality exposed

## Severity

**Medium**

## Prevention

- Remove unused legacy routes
    
- Disable deprecated upload handlers
    
- Audit old components
    
- Restrict obsolete interfaces

## Key Lesson

Old forgotten features often become security weaknesses.

## Conclusion

This challenge demonstrates the risk of leaving deprecated systems enabled after upgrades.
