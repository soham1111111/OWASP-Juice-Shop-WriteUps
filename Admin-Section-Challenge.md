# OWASP Juice Shop – Admin Section Challenge

## Category: Broken Access Control | Challenge Name: Admin Section | Difficulty: Sources

### Objective

- Access the hidden administration section of the store.

### Challenge Description

- The frontend application contains an internal route for administration functionality.  
- By reviewing shipped client-side code, the route can be discovered and accessed directly.

## Hidden Admin Route

```text id="u3m7ra"
http://192.168.1.122:3000/#/administration
````

## Discovery Method

### Inspect Frontend Source Code

1. Open browser Developer Tools:

```text
F12
```

2. Go to:

```text
Sources
```

3. Search across files:

```text
Ctrl + Shift + F
```

>Keyword:

```text
administration
```

4. Route reference appears inside:

```text
main.js
```

![[Pasted image 20260418190702.png]]

## Step-by-Step Solution

### Step 1: Open DevTools

- Press:

```text
F12
```

### Step 2: Search for Admin Route

- Use global search:

```text
administration
```

### Step 3: Find Hidden Path

- Discovered route:

```text
#/administration
```

### Step 4: Open Direct URL

- Visit:

```text
http://192.168.1.122:3000/#/administration
```

>Challenge gets solved when admin page is reached.


## Why It Works

- The admin route exists in frontend routing code and can be accessed directly if no proper authorization blocks it.

- Security relied on hiding navigation links rather than enforcing access control.

## Vulnerability Type

### Broken Access Control / Forced Browsing

- Sensitive functionality exposed through predictable or discoverable routes.

## Impact

### Risks

- Unauthorized admin panel access
    
- Data exposure
    
- Privileged operations
    
- User management abuse
    
- Configuration tampering

## Severity

**High**

>(Critical if full admin actions are enabled)

## OWASP Mapping

- A01: Broken Access Control
    
- A05: Security Misconfiguration

## Root Cause

- Hidden route treated as protection
    
- Missing server-side authorization
    
- Internal pages shipped to all users

## Prevention

- Enforce role-based access checks server-side
    
- Do not rely on hidden links
    
- Remove unused admin routes from production builds
    
- Validate permissions on every sensitive request
    
- Separate admin interfaces where possible

## Key Lesson

If a page exists publicly, obscurity alone is not security.

## Conclusion

This challenge demonstrates how easily hidden administrative functionality can be discovered when access control is not properly enforced.










