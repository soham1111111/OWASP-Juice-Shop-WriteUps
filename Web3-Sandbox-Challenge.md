# OWASP Juice Shop – Web3 Sandbox Challenge

## Category: Broken Access Control | Challenge Name: Web3 Sandbox | Difficulty: 1 Star

### Objective

- Find an accidentally deployed code sandbox intended for writing smart contracts on the fly.

### Challenge Description

- A hidden route exists inside the frontend application but is not exposed through normal navigation.  
- Users can access it directly if they discover the internal path.

## Hidden Route

```http
http://192.168.1.122:3000/#/web3-sandbox
```

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

3. Open bundled file:

```text
main.js
```

4. Search with:

```text
Ctrl + F
```

>Keywords:

```text
web3-sandbox
```

## Step-by-Step Solution

### Step 1: Open Developer Tools

- Press:

```text
F12
```

### Step 2: Search Routes

- Inside `main.js`, search for:

```text
web3-sandbox
```

![[Pasted image 20260418170033.png]]

### Step 3: Find Hidden Path

- Route discovered:

```text
web3-sandbox
```

### Step 4: Open Direct URL

- Visit:

```text
http://192.168.1.122:3000/#/web3-sandbox
```

![[Pasted image 20260418165936.png]]

>Challenge gets solved.

## Why It Works

- The route exists in the frontend router configuration but is hidden from menus/navigation.

- Anyone who knows the path can access it directly.

## Vulnerability Type

### Broken Access Control / Forced Browsing

- Sensitive or internal functionality is deployed without proper access restrictions.

## Impact

### Risks

- Unauthorized feature access
    
- Exposure of internal tools
    
- Test/dev environments publicly reachable
    
- Potential code execution surfaces
    
- Information disclosure

## Severity

**Medium**
>(Higher if sandbox has execution/backend privileges)

## OWASP Mapping

- A01: Broken Access Control
    
- A05: Security Misconfiguration

## Root Cause

- Hidden route relied on obscurity
    
- No server-side authorization check
    
- Internal tool deployed to production

## Prevention

- Remove unused internal routes
    
- Protect sensitive pages with auth checks
    
- Disable dev/test tools in production
    
- Perform route audits before release
    
- Enforce backend authorization

## Key Lesson

- Hidden pages are not secure pages.  
- If code is shipped to users, routes can often be discovered.

## Conclusion

- This challenge demonstrates that relying on secrecy of frontend routes instead of access control can expose internal functionality.









