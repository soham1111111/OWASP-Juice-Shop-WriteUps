# OWASP Juice Shop – Allowlist Bypass Challenge

## Category: Unvalidated Redirects | Challenge Name: Allowlist Bypass | Difficulty: Prerequisite

### Objective

- Enforce a redirect to a page that should **not** be allowed by the redirect allowlist.

### Challenge Description

- The application restricts redirects using an allowlist, but the validation can be bypassed by embedding an allowed URL inside the query string while using a different real destination.

## Payload Used

```text id="u2m8ra"
http://192.168.1.122:3000/redirect?to=http://youtube.com?pd=https://explorer.dash.org/address/Xr556RzuwX6hg5EGpkybbv5RanJoZN17kW
```

## Step-by-Step Solution

### Step 1: Open Browser

- Visit:

```text
http://192.168.1.122:3000/redirect?to=http://youtube.com?pd=https://explorer.dash.org/address/Xr556RzuwX6hg5EGpkybbv5RanJoZN17kW
```

### Step 2: Press Enter

- The browser redirects to:

```text
http://youtube.com
```

>Challenge gets solved.

## Why It Works

- The redirect filter likely checks whether the destination string contains an approved domain such as:

```text
explorer.dash.org
```

>But instead of validating the actual hostname, it uses weak text matching.

- The trusted domain is hidden inside:

```text
?pd=https://explorer.dash.org/...
```

- So the check passes, while the true redirect target is:

```text
youtube.com
```

## Vulnerability Type

### Open Redirect / Weak Allowlist Validation

- Redirect controls are present but implemented incorrectly.

## Impact

### Risks

- Phishing attacks
    
- Brand trust abuse
    
- Token theft in auth flows
    
- Malicious traffic redirection
    
- Social engineering links

## Severity

**High**
>(Depends on application context)

## OWASP Mapping

- A01: Broken Access Control
    
- A05: Security Misconfiguration
    
- Unvalidated Redirects

## Root Cause

- String-based validation
    
- No hostname parsing
    
- Trusting raw user input
    
- Allowlist logic bypassable through parameters

## Prevention

- Parse URL before validation
    
- Compare exact hostname only
    
- Normalize scheme and host
    
- Reject nested redirect parameters
    
- Use signed redirect IDs/tokens

## Secure Validation Example

```text
Allowed: explorer.dash.org
Blocked: youtube.com
```

## Key Lesson

An allowlist is ineffective if it checks text fragments instead of the actual redirect destination.

## Conclusion

This challenge demonstrates how weak allowlist checks can be bypassed to redirect users to unauthorized websites.