# OWASP Juice Shop – Repetitive Registration Challenge

## Category: Improper Input Validation | Challenge Name: Repetitive Registration | Difficulty: Unknown

### Objective

- Follow the **DRY principle** ("Don't Repeat Yourself") while registering a user.

### Challenge Description

- During registration, the application asks users to enter the password twice:

- `password`
- `passwordRepeat`

>This challenge is solved by **not repeating** the password value.

## Hint Meaning

```text id="p4v8na"
DRY = Don't Repeat Yourself
````

>The challenge uses this as a wordplay hint.

## Normal Registration Request

```json
{
  "email": "test@test.com",
  "password": "Password123",
  "passwordRepeat": "Password123",
  "securityAnswer": "12"
}
```

>This is standard signup behavior.

## Challenge Solution Request

- Send registration request where:

```text
passwordRepeat = ""
```

>Example:

```json
{
  "email": "test1@test.com",
  "password": "Password123",
  "passwordRepeat": "",
  "securityAnswer": "12"
}
```

- Challenge gets solved if backend accepts it.

![[Pasted image 20260417174900.png]]

## Step-by-Step Solution

### Method 1: Browser + Intercept Proxy

1. Open Signup page
    
2. Fill registration form
    
3. Intercept request with proxy tool
    
4. Modify:
    

```text
passwordRepeat: ""
```

5. Forward request


### Method 2: Direct API Request

- Send POST request to:

```text
/api/Users/
```

>With empty repeat password field.

## Why It Works

- The frontend likely requires password confirmation, but backend validation may not properly enforce it.

- Possible logic:

```text
If password exists → create user
Ignore passwordRepeat validation
```

>So challenge rewards bypassing unnecessary repetition.

## Vulnerability Type

### Improper Input Validation

Client-side checks exist, but server-side validation is weak or inconsistent.

## Impact

### Risks

- Inconsistent validation rules
    
- Business logic flaws
    
- Client-side only security controls
    
- Unexpected account creation states

## Severity

**Low to Medium**

## OWASP Mapping

- A04: Insecure Design
    
- A05: Security Misconfiguration
    
- Improper Input Validation

## Root Cause

- Frontend validation trusted too much
    
- Backend does not strictly compare fields
    
- Business logic mismatch

## Prevention

- Validate all required fields server-side
    
- Ensure password == passwordRepeat
    
- Reject empty confirmation fields
    
- Keep frontend and backend rules aligned

## Key Lesson

Any validation performed only in the browser can often be bypassed.

## Conclusion

This challenge teaches that duplicate confirmation fields are meaningless unless the server validates them properly.








