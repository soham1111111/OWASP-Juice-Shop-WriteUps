# OWASP Juice Shop – Finding Hidden Score Board via Source Code Analysis

## Challenge Overview

- One of the beginner challenges in **OWASP Juice Shop** is discovering the hidden **Score Board** page by inspecting frontend source code.

## Target URL

```text
http://192.168.1.122:3000/#/score-board
````

## Objective

- Locate an unlinked/hidden route by reviewing client-side JavaScript files.

## Step-by-Step Process

### Step 1: Open Developer Tools

- Right-click anywhere on the page
    
- Select **Inspect**
    
- Browser Developer Tools will open

### Step 2: Open Sources Tab

 - Navigate to:

```text
Developer Tools → Sources → Page
```

- Inside the listed files, locate:

```text
main.js
```

>This is the bundled frontend JavaScript file.

### Step 3: Search Inside main.js

Open `main.js`, then press:

```text
Ctrl + F
```

Search for:

```text
score
```

>You may see multiple results. Review them one by one.

### Step 4: Discover Hidden Route

Eventually, one result reveals the route:

```text
/score-board
```

![[Pasted image 20260416164409.png]]

## Access Hidden Endpoint

- Open directly in browser:

```text
http://localhost:3000/#/score-board
```

- Or in your case:

```text
http://192.168.1.122:3000/#/score-board
```


![[Pasted image 20260416164435.png]]


## Security Concept Demonstrated

### Client-Side Information Disclosure

Sensitive routes or hidden pages stored in frontend JavaScript can be discovered easily.

Even if not shown in navigation menus, routes exposed in JS bundles remain accessible.

## Impact

### Risks

- Hidden admin/debug pages discovered
    
- Challenge paths exposed
    
- Internal routes leaked
    
- Easier recon for attackers
    
- Security by obscurity fails


## Severity

**Low to Medium**  
>(Depends on what hidden route exposes)


## OWASP Mapping

- A05: Security Misconfiguration
    
- A01: Broken Access Control (if route lacks auth)
    
- Information Disclosure

## Key Lesson

- If a route exists in frontend code, assume users can find it.

- Hiding links is **not** access control.

## Prevention

- Protect sensitive routes with backend authorization
    
- Avoid exposing unused/internal routes
    
- Remove debug pages in production
    
- Use role-based access control
    
- Perform frontend bundle review before release

## Conclusion

This task demonstrates how simple **source code inspection + keyword search** can reveal hidden functionality. It’s a classic example of why frontend secrecy alone is ineffective.
























