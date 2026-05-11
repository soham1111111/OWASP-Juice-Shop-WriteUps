# OWASP Juice Shop – Five-Star Feedback

## Category :

**Broken Access Control**

### Challenge Name

**Five-Star Feedback**

### Difficulty

**2 Star**

## Objective

- Get rid of all **5-star customer feedback**.

## Description

- This challenge demonstrates missing authorization controls on administrative functionality.  
- A user can access privileged review-management features and remove positive customer feedback.

## Requirement

- Usually solved after discovering the admin area.

```http
#/administration
````

## Vulnerable Area

```text
Administration Panel
```

>Contains user data, complaints, and feedback management controls.

## Step-by-Step Solution

### Step 1: Gain Access to Admin Section

- Open:

```text
http://192.168.1.122:3000/#/administration
```

>(Using previously solved admin access challenge)


### Step 2: Locate Customer Feedback Section

- Find the list of reviews / feedback entries.

### Step 3: Delete All 5-Star Reviews

- Remove every review with:

```text
★★★★★
Rating = 5
```

>Use delete/trash actions in the panel.

![[Pasted image 20260421164902.png]]

### Step 4: Challenge Solved

- After all five-star feedback is removed, the challenge completes.

## Why It Works

- Administrative review deletion functionality is exposed through insufficient access controls.

## Vulnerability Type

### Broken Access Control

- Users can perform privileged moderation actions they should not have.

## Impact

- Reputation manipulation
    
- Review tampering
    
- Unauthorized content moderation
    
- Loss of data integrity
    
- Abuse of admin functions

## Severity

**High**

## Root Cause

- Missing role-based access control
    
- Weak route protection
    
- Trusting client-side checks only
    
- Exposed admin endpoints

## Prevention

- Enforce server-side RBAC
    
- Restrict admin routes
    
- Verify privileges on every action
    
- Audit destructive operations
    
- Maintain action logs

## OWASP Mapping

- A01: Broken Access Control

## Key Lesson

If moderation tools are exposed, attackers can manipulate trust signals like ratings and reviews.

## Conclusion

This challenge shows how weak authorization can allow unauthorized deletion of valuable customer feedback.















