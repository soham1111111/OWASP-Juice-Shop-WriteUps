# OWASP Juice Shop – NFT Takeover Challenge

## Category: Broken Access Control / Sensitive Data Exposure | Challenge Name: NFT Takeover | Difficulty: 2 Star

### Objective

- Take over the wallet containing the official **Soul Bound Token (NFT)**.
    
- Discover an exposed wallet seed phrase and use it to derive the private key.

## Challenge Description

- This challenge demonstrates how exposing cryptocurrency recovery phrases or wallet secrets in public comments can lead to complete wallet compromise.

## Target URLs

```site
http://192.168.2.199:3000/#/about
```

```site
http://192.168.2.199:3000/#/juicy-nft
```

## Step-by-Step Solution

### Step 1: Open About Us Page

- Navigate to:

```text
#/about
```

![[Pasted image 20260428171425.png]]

>Inspect the page source / comments.

### Step 2: Find Hidden Comment

- Inside the HTML comments you will find:

```text
Please send me the juicy chatbot NFT in my wallet at /juicy-nft
```

- Along with a **12-word wallet seed phrase**:

```text
purpose betray marriage blame crunch monitor spin slide donate sport lift clutch
```

### Step 3: Open NFT Route

- Visit:

```text
#/juicy-nft
```

### Step 4: Derive Ethereum Private Key

- Use a BIP39 wallet derivation tool:

```site
https://iancoleman.io/bip39/#english
```

- Enter mnemonic:

```text
purpose betray marriage blame crunch monitor spin slide donate sport lift clutch
```

- Select Coin :

```text
ETH
```

- Generated private key:

```text
0x5bcc3e9d38baa06e7bfaab80ae5957bbe8ef059e640311d7d6d465e6bc948e3e
```

### Step 5: Submit Private Key

- Paste the derived private key into the input box on:

```text
#/juicy-nft
```

![[Pasted image 20260428171149.png]]

### Step 6: Challenge Solved

- Wallet access granted
    
- NFT takeover completed
    
- Challenge marked as solved

## Why It Works

- Recovery seed phrase was publicly exposed in comments.
    
- Anyone with the mnemonic can derive private keys and control wallet assets.

## Vulnerability Type

### Sensitive Data Exposure / Secret Leakage

- Exposed seed phrase
    
- Client-side secret disclosure
    
- Credential leakage

## Impact

### Security Risks

- Full wallet compromise
    
- NFT theft
    
- Token theft
    
- Permanent asset loss
    
- Reputation damage

## Severity

**Critical**

## OWASP Mapping

- A02: Cryptographic Failures
    
- A01: Broken Access Control
    
- A05: Security Misconfiguration

## Root Cause

- Secret phrase stored in client-visible comments
    
- No secret management practices
    
- Sensitive data embedded in frontend code

## Prevention

- Never expose seed phrases anywhere client-side
    
- Use secure vault storage
    
- Remove debug comments before production
    
- Rotate compromised wallets immediately
    
- Use multisig for valuable assets

## Key Lesson

- A leaked seed phrase equals total ownership loss.

## Conclusion

This challenge shows that blockchain assets are only as secure as their key management. Exposing a mnemonic phrase publicly gives attackers complete wallet control instantly.



