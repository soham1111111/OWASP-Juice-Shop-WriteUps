# OWASP Juice Shop – DOM XSS via Search Box

## Challenge Name

- **DOM XSS**  
- Perform a DOM XSS attack with:

```html id="u5c1ez"
<iframe src="javascript:alert(`xss`)">
````

**Difficulty:** 1 Star

## Objective

- Exploit a **DOM-Based Cross-Site Scripting (XSS)** vulnerability by injecting the provided payload into a client-side input field.

## Vulnerable Input Location

```text
Search Box
```

>The search field reflects user-controlled input into the page DOM without proper sanitization.

## Payload Used

```html
<iframe src="javascript:alert(`xss`)">
```

## Step-by-Step Exploitation

### Step 1: Open OWASP Juice Shop

- Navigate to the application homepage.

### Step 2: Locate Search Box

- Use the top search bar.

### Step 3: Inject Payload

- Paste: into the search box.

```html
<iframe src="javascript:alert(`xss`)">
```

![[Pasted image 20260416165115.png]]


### Step 4: Execute

- Press **Enter**

### Result

A JavaScript alert box appears:

```text
xss
```

Challenge gets marked as solved.

![[Pasted image 20260416165141.png]]

![[Pasted image 20260416165128.png]]

## Why It Works

- The application processes the search term inside browser-side JavaScript and inserts it into the page DOM unsafely.

- Instead of treating input as text, it renders attacker-controlled HTML.

- This causes the injected `<iframe>` element to execute JavaScript.

## Vulnerability Type

### DOM-Based XSS

- Occurs when:
	- Input is handled entirely in browser JavaScript
	- Data is written to DOM insecurely
	- No server-side reflection required

## Impact

### Security Risks

- Session hijacking
    
- Token theft
    
- Fake login prompts
    
- DOM manipulation
    
- Redirect users to malicious pages
    
- Run actions as victim user

## Severity

**High**
>(Depends on session/token protections)


## OWASP Mapping

- A03:2021 – Injection
    
- Cross-Site Scripting (XSS)

## Root Cause

- Unsafe JavaScript methods such as:

```javascript
innerHTML
document.write()
insertAdjacentHTML()
```

>with unsanitized user input.


## Prevention

- Use `textContent` instead of `innerHTML`
    
- Sanitize user input
    
- Encode output properly
    
- Implement CSP headers
    
- Use secure frontend frameworks correctly
    
- Avoid `javascript:` URLs


## Key Lesson

- Even if the server is secure, frontend JavaScript alone can introduce XSS.

- DOM-based vulnerabilities happen fully in the browser.

## Conclusion

This challenge demonstrates how a simple search field can become an execution point when user input is inserted into the DOM unsafely.









