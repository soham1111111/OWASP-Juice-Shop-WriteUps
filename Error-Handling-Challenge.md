# OWASP Juice Shop – Error Handling Challenge

## Category: Security Misconfiguration | Challenge Name: Error Handling | Difficulty: 1 Star

### Objective

- Trigger an application error that is not handled gracefully or consistently.

### Challenge Description

- This challenge demonstrates how poor exception handling can expose raw errors, unstable responses, or inconsistent behavior to users.

## Example URLs to Trigger Errors

```site
http://192.168.1.122:3000/#/thispagedoesnotexist
http://192.168.1.122:3000/rest/products/999999
http://192.168.1.122:3000/rest/user/whoami
http://192.168.1.122:3000/ftp/unknownfile.txt
````

>Try invalid pages, missing resources, or unexpected endpoints.

## How the Challenge Was Solved

- Open one of the invalid URLs above or send a malformed request.  
- When the application returns an ugly / inconsistent / raw error response, the challenge gets solved.

## Why It Works

- Secure applications should return clean, consistent error messages.
- In this case, the application exposed poor handling such as:
	- Raw stack traces
	- Technical messages
	- Unformatted server errors
	- Inconsistent responses

## Vulnerability Type

### Security Misconfiguration / Improper Error Handling

- When applications fail to sanitize or standardize error responses.

## Impact

### Security Risks

- Reveals backend technologies
    
- Exposes file paths
    
- Leaks SQL / code errors
    
- Helps attacker reconnaissance
    
- Easier vulnerability chaining

## Severity

**Low to Medium**
>(High if sensitive internals are exposed)

## OWASP Mapping

- A05: Security Misconfiguration
- Information Disclosure

## Prevention

- Use generic user-facing errors
    
- Log detailed errors server-side only
    
- Disable debug mode in production
    
- Standardize API responses
    
- Centralized exception handling

## Key Lesson

- Even simple error messages can help attackers understand how an application works.

## Conclusion

- This challenge highlights that secure coding includes handling failure states cleanly—not just successful requests.