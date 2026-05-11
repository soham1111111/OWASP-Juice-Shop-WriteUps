# OWASP Juice Shop – Zero Stars Challenge

## Category: Improper Input Validation | Challenge Name: Zero Stars | Difficulty: Unknown

### Objective

- Submit a devastating **0-star feedback** to the store.

### Challenge Description

- The feedback form normally expects ratings within the visible UI range (commonly 1–5 stars).  
- This challenge is solved by bypassing client-side controls and submitting a rating of `0`.

## Normal UI Behavior

- The feedback page usually allows selecting:

```text id="u2m8ra"
1 Star
2 Stars
3 Stars
4 Stars
5 Stars
````

But **0** is not available in the interface.


## Solution Concept

- Modify the feedback request before it reaches the server and set:

```text
"rating": 0
```

## Working Request Example

```json
{
  "captchaId": 6,
  "captcha": "50",
  "comment": "Worst experience ever.",
  "rating": 0
}
```

## Step-by-Step Solution

### Method 1: Intercept Proxy

1. Open Feedback page
    
2. Fill form normally
    
3. Submit feedback
    
4. Intercept request
    
5. Change:

```text
"rating": 3
```

to:

```text
"rating": 0
```

![[Pasted image 20260418172952.png]]

6. Forward request

>Challenge gets solved.

### Method 2: Manual API Request

- Send POST request to:

```text
/api/Feedbacks/
```

- With JSON body containing:

```text
"rating": 0
```


## Why It Works

- The UI restricts rating values, but backend validation may not enforce the same minimum.

Possible logic:

```text
Accept any numeric rating
```

Instead of:

```text
Only allow 1–5
```

## Vulnerability Type

### Improper Input Validation

- Client-side restrictions exist, but server-side validation is weak or missing.

## Impact

### Risks

- Invalid data stored in database
    
- Broken analytics/reporting
    
- Business logic abuse
    
- Reputation manipulation
    
- Inconsistent application state

## Severity

**Low**

## OWASP Mapping

- A04: Insecure Design
    
- A05: Security Misconfiguration
    
- Improper Input Validation

## Root Cause

- Trusting frontend validation
    
- Missing numeric range checks
    
- Backend accepts unexpected values

## Prevention

- Validate ratings server-side
    
- Enforce integer range (1–5)
    
- Reject malformed/negative/zero values
    
- Keep frontend/backend rules aligned

## Secure Validation Example

```text
Allowed values: 1,2,3,4,5
Blocked values: 0,-1,99
```

## Key Lesson

Anything hidden or disabled in the UI can still be modified in requests unless the server validates it.

## Conclusion

This challenge shows how client-side controls alone cannot protect application logic or data integrity.




