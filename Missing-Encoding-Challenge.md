# OWASP Juice Shop – Missing Encoding Challenge

## Category: Improper Input Validation | Challenge Name: Missing Encoding | Difficulty: Shenanigans

### Objective

- Retrieve the photo of **Bjoern's cat** in **"melee combat-mode"** by correcting a broken image URL.

### Challenge Description

- The image filename contains special characters (`#`) that were not properly URL-encoded.  
>Because of this, the browser misinterprets the filename and the cat image does not load.

## Broken Image URL

```text id="g3m8ra"
http://192.168.1.122:3000/assets/public/images/uploads/%E1%93%9A%E1%98%8F%E1%97%A2-#zatschi-#whoneedsfourlegs-1572600969477.jpg
````

## Why It Fails

- In a URL:

```text
# = Fragment Identifier
```

- The browser treats everything after `#` as client-side fragment data and does **not** send it as part of the file path.

>So the server receives an incomplete request.

## Correct Fix

- Replace every:

```text
# → %23
```

## Working URL

```text
http://192.168.1.122:3000/assets/public/images/uploads/%E1%93%9A%E1%98%8F%E1%97%A2-%23zatschi-%23whoneedsfourlegs-1572600969477.jpg
```

## Step-by-Step Solution

### Method 1: Direct Open (Fastest)

1. Open a new browser tab
    
2. Paste the corrected URL
    
3. Press Enter

>Challenge gets solved when the cat photo loads.

### Method 2: Photo Wall Method

1. Open:

```text
Photo Wall
```

2. Broken cat image appears
    
3. Right-click image
    
4. Choose:

```text
Open image in new tab
```
or

```text
Copy image address
```

5. Replace `#` with `%23`
    
6. Reopen URL


### Method 3: Inspect Element

1. Right-click broken image
    
2. Select **Inspect**
    
3. Find:

```html
<img src="assets/public/images/uploads/...">
```

![[Pasted image 20260417165239.png]]

4. Copy `src`
    
5. Replace `#` with `%23`
    
6. Open fixed URL

### Method 4: Network Edit & Resend

1. Press `F12`
    
2. Open **Network**
    
3. Refresh page
    
4. Locate broken image request
    
5. Right-click → **Edit and Resend**
    
6. Replace:
    

```text
# → %23
```

7. Send request

## Why Network Request Looks Incomplete

- Browser converts:

```text
file.jpg#abc
```
into:

```text
Requested file: file.jpg
Fragment: abc
```

>So server never receives the full filename.

## Vulnerability Type

### Missing Output Encoding / Improper Input Validation

- Special characters in filenames were stored without safe URL encoding.

## Impact

- Broken media rendering
    
- File retrieval failures
    
- Parsing inconsistencies
    
- Potential path/filter bypasses
    
- Poor user experience

## Severity

**Low**

## OWASP Mapping

- A04: Insecure Design
    
- A05: Security Misconfiguration
    
- Improper Input Validation

## Root Cause

- Unsafe filename generation
    
- Reserved URL characters allowed in filenames
    
- Missing percent-encoding

## Prevention

- Sanitize filenames during upload
    
- Replace unsafe characters automatically
    
- Use random file IDs instead of user names
    
- Encode URLs before rendering
    
- Validate allowed characters

## Key Lesson

A file may exist correctly on disk but still fail in browsers if URL encoding is ignored.

## Conclusion

This challenge teaches how browser URL parsing rules can break file access and why `%23` matters when `#` appears in filenames.








