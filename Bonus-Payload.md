# OWASP Juice Shop – Bonus Payload (DOM XSS)

## Challenge Name

**Bonus Payload**  
- Use the provided payload in the DOM XSS challenge.

**Difficulty:** 1 Star

## Objective

- Inject a valid HTML payload into the vulnerable search field to trigger client-side HTML rendering and solve the bonus challenge.

## Payload Used

```html id="g7k2lv"
<iframe width="100%" height="166" scrolling="no" frameborder="no" allow="autoplay" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/771984076&color=%23ff5500&auto_play=true&hide_related=false&show_comments=true&show_user=true&show_reposts=false&show_teaser=true"></iframe>
````

## Vulnerable Input Location

```text
Search Box
```

## Step-by-Step Exploitation

### Step 1: Open OWASP Juice Shop

- Navigate to the application.

### Step 2: Locate Search Field

- Use the top search bar.

### Step 3: Inject Payload

Paste the full iframe payload into the search box.

![[Pasted image 20260416165755.png]]

### Step 4: Execute

Press **Enter**

## Result

- Challenge gets completed
    
- Embedded SoundCloud player loads
    
- Audio starts automatically

![[Pasted image 20260416165814.png]]

## Why It Works

- The application inserts search input into the DOM without proper sanitization.

- Because raw HTML is accepted, attacker-controlled `<iframe>` tags are rendered directly in the page.

- This allows third-party content embedding.

## Vulnerability Type

### DOM-Based XSS / HTML Injection

- This challenge demonstrates that unsafe DOM rendering can allow:
	- HTML injection
	- Embedded media
	- Malicious iframes
	- Script execution (depending on filters/browser)

## Impact

### Security Risks

- Malicious iframe embedding
    
- Phishing pages inside app UI
    
- Clickjacking overlays
    
- User tracking via third-party content
    
- Forced redirects
    
- XSS escalation depending on payload support

## Severity

**Medium to High**
>(Depends on browser protections and session context)


## OWASP Mapping

- A03:2021 – Injection
    
- XSS / HTML Injection

## Root Cause

- Unsafe rendering methods such as:

```javascript
innerHTML
insertAdjacentHTML()
dangerouslySetInnerHTML
```

>with unsanitized user input.

## Prevention

- Render user input as text only
    
- Sanitize HTML inputs
    
- Restrict iframe tags
    
- Use Content Security Policy (CSP)
    
- Block untrusted external embeds
    
- Validate search parameters

## Key Lesson

- Even when JavaScript execution is filtered, HTML injection alone can still be dangerous.

- Embedding attacker-controlled iframes can compromise trust and user safety.

## Conclusion

This challenge shows that DOM XSS is not limited to alert boxes—real attackers often use stealthier payloads like media embeds, fake forms, or hidden iframes.








