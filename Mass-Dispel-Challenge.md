# OWASP Juice Shop – Mass Dispel Challenge

## Category: Miscellaneous | Challenge Name: Mass Dispel | Difficulty: 1 Star

### Objective

- Close multiple **"Challenge solved"** notifications at once using a hidden UI shortcut.

### Challenge Description

- This challenge demonstrates hidden client-side functionality triggered through keyboard modifier keys during UI interaction.


## Step-by-Step Solution

### Step 1: Solve Multiple Challenges

- Generate several popup notifications such as:

```text id="r2v8ka"
Challenge solved!
Challenge solved!
Challenge solved!
````

>These appear as snackbar / toast notifications.

### Step 2: Hold Shift Key

Press and hold:

```text
Shift
```

### Step 3: Click Close (X)

- While holding Shift, click the close icon on one notification.

### Result

- All active notifications close simultaneously.

>Challenge gets marked as solved.

## How It Works

- The frontend checks whether the click event contains:

```javascript
event.shiftKey === true
```

- Example logic:

```javascript
if (event.shiftKey) {
   closeAllNotifications()
} else {
   closeSingleNotification()
}
```

>Normal click closes one popup.  
>Shift + Click closes all popups.

## Internal UI Logic

### Notification Queue Example

```text
Notification 1
Notification 2
Notification 3
```

- Shift-click triggers bulk dismissal:

```javascript
notifications = []
```

## Browser Event Perspective

- The click event contains:

```text
altKey: false
ctrlKey: false
shiftKey: true
metaKey: false
```

## Security Concept

### Hidden Client-Side Functionality

This challenge teaches testers to inspect:

- Keyboard shortcuts
    
- Modifier keys
    
- UI behaviors
    
- Frontend event handling
    
- Unlisted features

## Real World Relevance

- Applications often contain hidden actions like:

```text
Shift + Delete
Ctrl + Click
Shift + Multi-select
Alt + Shortcut
```

>These may expose unintended behavior.

## Severity

**Informational**

## OWASP Mapping

- Client-Side Security Testing
    
- UI Logic Enumeration
    
- Security Through Obscurity Concept

## Prevention / Best Practice

- Document hidden shortcuts
    
- Review client-side event logic
    
- Avoid sensitive actions without confirmation
    
- Test all modifier-key flows

## Key Lesson

Security testing includes UI behavior—not just URLs and APIs.

## Conclusion

This challenge shows that even harmless-looking interface elements can contain hidden functionality discoverable through keyboard-assisted interaction.