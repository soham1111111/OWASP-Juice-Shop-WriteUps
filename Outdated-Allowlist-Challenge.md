# OWASP Juice Shop – Outdated Allowlist Challenge

## Category: Unvalidated Redirects | Challenge Name: Outdated Allowlist | Difficulty: Code Analysis

### Objective

- Use an old redirect target that still exists in the application's allowlist and get redirected to a cryptocurrency address that is no longer promoted.

### Challenge Description

- The application contains redirect functionality that only allows certain destinations.  
- This challenge demonstrates how outdated allowlists can still contain deprecated external URLs.

## Discovery Method

### Inspect Frontend Source Code

- Open browser Developer Tools:

```text id="r2v6na"
F12 → Sources
````

- Search inside bundled JS:

```text
/redirect?to=
```

- Found around lines:

```text
11112 - 11117
```

## Source Code Found

```javascript
showDashQrCode() {
  this.dialog.open(qt, {
    data: {
      data: "dash:Xr556RzuwX6hg5EGpkybbv5RanJoZN17kW",
      url: "./redirect?to=https://explorer.dash.org/address/Xr556RzuwX6hg5EGpkybbv5RanJoZN17kW",
      address: "Xr556RzuwX6hg5EGpkybbv5RanJoZN17kW",
      title: "TITLE_DASH_ADDRESS"
    }
  })
}
```

![[Pasted image 20260417170957.png]]

## Redirect URL Used

```text
http://192.168.1.39:3000/redirect?to=https://explorer.dash.org/address/Xr556RzuwX6hg5EGpkybbv5RanJoZN17kW
```

## External Destination

```text
https://explorer.dash.org/address/Xr556RzuwX6hg5EGpkybbv5RanJoZN17kW
```

## Step-by-Step Solution

### Step 1: Open DevTools

- Press:

```text
F12
```

### Step 2: Search Redirect References

- Use:

```text
Ctrl + F
```

- Search:

```text
/redirect?to=
```

### Step 3: Find Old Crypto Redirect

- Locate deprecated Dash wallet redirect URL in source code.

### Step 4: Open Redirect Endpoint

- Visit:

```text
http://192.168.1.39:3000/redirect?to=https://explorer.dash.org/address/Xr556RzuwX6hg5EGpkybbv5RanJoZN17kW
```

>Challenge gets solved.

## Why It Works

- The redirect endpoint checks an allowlist of approved external URLs.

- An old Dash address remained approved even though it is no longer actively promoted.

## Vulnerability Type

### Unvalidated Redirect / Weak Allowlist Management

- Redirect controls exist, but stale entries remain trusted.

## Impact

### Risks

- Users redirected to outdated destinations
    
- Phishing opportunities if domains expire
    
- Trust abuse through old links
    
- Weak redirect governance

## Severity

**Medium**
>(High if destination becomes malicious)

## OWASP Mapping

- A01: Broken Access Control
    
- A05: Security Misconfiguration
    
- Unvalidated Redirects

## Root Cause

- Old allowlist entries not removed
    
- Hardcoded redirect URLs in frontend code
    
- Poor lifecycle management of trusted domains

## Prevention

- Regularly audit redirect allowlists
    
- Remove deprecated destinations
    
- Use signed redirect tokens
    
- Store allowlists server-side only
    
- Avoid exposing trusted targets in JS bundles

## Key Lesson

Even “safe redirect lists” become risky if nobody maintains them.

## Conclusion

This challenge shows that security controls can fail when outdated trusted entries remain active.









