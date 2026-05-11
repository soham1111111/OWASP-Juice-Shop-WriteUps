# OWASP Juice Shop – Visual Geo Stalking Challenge

## Category: Sensitive Data Exposure | Challenge Name: Visual Geo Stalking | Difficulty: 3 Star

### Objective

- Determine the answer to **Emma's security question** by visually analyzing a photo uploaded to the Photo Wall.
    
- Use the discovered information to reset her password through the **Forgot Password** feature.

## Challenge Description

- This challenge demonstrates how sensitive information can be exposed through visible details inside publicly shared images.
    
- Attackers can use visual clues for OSINT and account recovery attacks.

## Target Areas

```site
Photo Wall
```

```site
Forgot Password
```

```site
emma@juice-sh.op
```

## Step-by-Step Solution

### Step 1: Open Photo Wall

- Navigate to the Photo Wall section.

- Search for the image uploaded by:

```text
E=ma²
```

![[Pasted image 20260507231621.png]]

### Step 2: Open the Image

- Open the image in a new tab.
    
- Zoom into the building/windows shown in the photo.

### Step 3: Identify the Visual Clue

- On the far-left window of the middle floor, a company logo is visible.

- The logo text reads:

```text
ITsec
```

![[Pasted image 20260507230128.png]]
![[Pasted image 20260507230206.png]]

### Step 4: Open Forgot Password

- Go to the login page and click:

```text
Forgot your password?
```

### Step 5: Enter Account Details

- Use:

```text
Email: emma@juice-sh.op
```

- Security answer:

```text
ITsec
```

- Choose a new password.

![[Pasted image 20260507230407.png]]

### Step 6: Submit Reset Request

- Example request:

```http
POST /rest/user/reset-password HTTP/1.1
Host: 192.168.1.122:3000
Content-Type: application/json

{
  "email":"emma@juice-sh.op",
  "answer":"ITsec",
  "new":"test1234",
  "repeat":"test1234"
}
```

### Step 7: Challenge Solved

- Password reset succeeds.
    
- Challenge is marked as completed.

## Why It Works

- Sensitive information was visually exposed inside a publicly accessible image.
    
- The security question relied on publicly discoverable information.

## Vulnerability Type

### Sensitive Data Exposure / OSINT Leakage

- Information disclosure through images
    
- Weak account recovery mechanisms

## Impact

### Security Risks

- Account takeover
    
- Privacy exposure
    
- Social engineering support
    
- OSINT-assisted attacks

## Severity

**Medium**

## OWASP Mapping

- A01: Broken Access Control
    
- A07: Identification and Authentication Failures
    
- A02: Cryptographic Failures (contextual exposure)

## Root Cause

- Public image revealed sensitive organizational information
    
- Weak security question design
    
- Reliance on guessable/public facts

## Prevention

- Avoid security questions based on public information
    
- Use MFA for password recovery
    
- Review uploaded media for sensitive details
    
- Train users about OSINT risks

## Key Lesson

- Even background details in images can expose sensitive information.

## Conclusion

This challenge highlights how attackers can use visual clues from publicly shared images to answer security questions and compromise accounts through OSINT techniques.


