# OWASP Juice Shop – Meta Geo Stalking Challenge

## Category: Sensitive Data Exposure | Challenge Name: Meta Geo Stalking | Difficulty: 3 Star

### Objective

- Determine the answer to **John's security question** by analyzing metadata from an uploaded image on the Photo Wall.
    
- Use the discovered answer in the **Forgot Password** mechanism to reset his account password.

## Challenge Description

- This challenge demonstrates how image metadata (EXIF/GPS) can unintentionally leak sensitive personal information.
    
- Publicly uploaded photos may contain hidden location data that attackers can use for account recovery attacks.

## Target Areas

```site
Photo Wall
```

```site
Forgot Password
```

```site
John's Account
john@juice-sh.op
```

## Step-by-Step Solution

### Step 1: Open Photo Wall

- Navigate to the **Photo Wall** section.
    
- Locate John's hiking photo.

Caption contains:

```text
I love going hiking here... (© j0hNny)
```

> This suggests the image belongs to John.


### Step 2: Download the Image

- Open/download the hiking image locally.

### Step 3: Extract Metadata

- Use EXIF analysis tool:

```bash
exiftool favorite-hiking-place.png
```

- You will find GPS coordinates:

```text
36°57'31.38" N
84°20'53.58" W
```

### Step 4: Search Coordinates on Map

- Paste the coordinates into:

```text
Google Maps
OpenStreetMap
```

- Resolved location:

```text
Daniel Boone National Forest
Kentucky, USA
```

### Step 5: Use Forgot Password

- Go to password reset page for:

```text
john@juice-sh.op
```

- Enter the discovered security answer:

```text
Daniel Boone National Forest
```

>Use a new password.

### Step 6: Submit Reset Request

- Example request:

```http
POST /rest/user/reset-password HTTP/1.1
Host: 192.168.1.122:3000
Content-Type: application/json

{
  "email":"john@juice-sh.op",
  "answer":"Daniel Boone National Forest",
  "new":"12345678",
  "repeat":"12345678"
}
```

### Step 7: Challenge Solved

- Password reset succeeds.
    
- Challenge gets marked as completed.

## Why It Works

- Uploaded image contained GPS EXIF metadata.
    
- Metadata exposed John's favorite hiking place.
    
- Same location was used as security question answer.

## Vulnerability Type

### Sensitive Data Exposure / Metadata Leakage

- Hidden metadata in media files reveals private information.

## Impact

### Security Risks

- Account takeover through password reset
    
- Personal location disclosure
    
- Privacy violations
    
- OSINT-assisted attacks
    
- Social engineering support

## Severity

**Medium**

> (High if tied to real identities or sensitive accounts)

## OWASP Mapping

- A02: Cryptographic Failures (data exposure context)
    
- A01: Broken Access Control (weak recovery flow)
    
- A07: Identification and Authentication Failures

## Root Cause

- Images uploaded with metadata intact
    
- Security questions based on guessable personal facts
    
- Publicly accessible user content
    
- Weak account recovery design

## Prevention

- Strip EXIF metadata from uploaded images
    
- Avoid security questions based on public facts
    
- Use MFA for password reset
    
- Add anomaly detection for reset attempts
    
- Educate users on metadata privacy

## Key Lesson

- Hidden metadata can expose more than visible content.
    
- Public photos may reveal private answers.

## Conclusion

This challenge shows how a harmless-looking image upload can leak enough information for account recovery abuse through metadata analysis.