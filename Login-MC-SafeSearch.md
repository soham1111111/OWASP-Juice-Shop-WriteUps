# Login MC SafeSearch

**Log in with MC SafeSearch's original user credentials without applying SQL Injection or any other bypass.**

## Solution

After watching the in-app video, certain lyrics provide a clue about the password.

Video Repo :- https://www.youtube.com/watch?v=v59CX2DiX0Y

It mentions:

- Password is **Mr. Noodles**
    
- Some vowels were replaced with **0 (zero)**

>So the letter **o** becomes **0**

![[Pasted image 20260421174024.png]]

## Password Attempts

```text
Mr. N00dles
Mr. Noodles
N00dles
```

## Correct Credentials

![[Pasted image 20260421170419.png]]

```text
Email: mc.safesearch@juice-sh.op
Password: Mr. N00dles
```

## Login Request

```http
POST /rest/user/login HTTP/1.1
Host: 192.168.1.122:3000
Content-Type: application/json

{
  "email": "mc.safesearch@juice-sh.op",
  "password": "Mr. N00dles"
}
```

## Expected Response

```http
HTTP/1.1 200 OK
```

## Result

Successful login completes the challenge.






