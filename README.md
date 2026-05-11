# OWASP Juice Shop Solutions

## Overview

This repository contains solutions, walkthroughs, setup instructions, screenshots, tools used, and security learning
notes for the OWASP Juice Shop project.

## Purpose

Educational repository for web security learning, API security practice, OWASP Top 10 understanding, penetration
testing, and ethical hacking labs.

## Official Resources


OWASP Juice Shop Official Site: https://owasp.org/www-project-juice-shop/
GitHub Repository: https://github.com/juice-shop/juice-shop

## Lab Setup - Docker


```shell
docker pull bkimminich/juice-shop
```

```shell
docker run -d -p 3000:3000 bkimminich/juice-shop
```

## Lab Setup - Source Installation


```shell
git clone https://github.com/juice-shop/juice-shop.git
```


```shell
cd juice-shop
```


```shell
npm install
```


```shell
npm start
```

## Challenge Categories


- SQL Injection

- Cross-Site Scripting (XSS)

- Broken Authentication

- IDOR

- Sensitive Data Exposure

- API Security Issues

- Security Misconfiguration

- File Upload Vulnerabilities

## Tools Used

- Burp Suite

- OWASP ZAP

- Postman

- Gobuster

- SQLMap

- Docker

- VS Code

## Disclaimer


- This repository is intended strictly for educational and ethical security testing purposes only.

## License

This project is licensed under the MIT License.

## Author

Soham

