# OWASP Juice Shop – Exposed Metrics Challenge

## Category: Sensitive Data Exposure | Challenge Name: Exposed Metrics | Difficulty: 1 Star

### Objective

- Find the endpoint that exposes internal monitoring / usage data used by a popular metrics collection system.

### Challenge Description

- This challenge demonstrates how publicly exposed observability endpoints can leak valuable operational information.

## Discovery Method

### Using Directory Fuzzing

```bash id="f4x9qp"
ffuf -u http://192.168.1.122:3000/FUZZ -w wordlist.txt
````

### Useful Wordlist Entries

```text
metrics
health
admin
ftp
robots.txt
api
debug
status
```

- During enumeration, the following endpoint is discovered:

```text
http://192.168.1.122:3000/metrics
```

## Step-by-Step Solution

### Step 1: Open Metrics Endpoint

```text
http://192.168.1.122:3000/metrics
```

### Step 2: View Exposed Monitoring Data

- The page returns Prometheus-style metrics such as:

```text
process_cpu_seconds_total
process_resident_memory_bytes
nodejs_version_info
juiceshop_version_info
http_requests_count
juiceshop_users_registered_total
juiceshop_challenges_solved
```

## Sensitive Information Exposed

### Application Details

```text
OWASP Juice Shop Version: 18.0.0
Node.js Version: v22.22.0
```

### Infrastructure Data

- CPU usage
    
- Memory usage
    
- Heap stats
    
- File descriptors
    
- Event loop lag
    

### Business Data

- Orders placed
    
- Users registered
    
- Wallet balance
    
- Reviews / feedback count

### Security Data

- Solved challenge counts
    
- Error count (`5XX`)
    
- Internal challenge progress

## Why It Works

- The `/metrics` route is intended for **Prometheus** or internal monitoring systems.

>Because it is publicly accessible, anyone can scrape internal telemetry.

## Vulnerability Type

- Sensitive Data Exposure + Security Misconfiguration


## Impact

- Risks
	- Reveals tech stack versions
	- Shows system load and uptime
	- Helps exploit version-based CVEs
	- Leaks business statistics
	- Assists attacker timing
	- Exposes internal app behavior

## Severity

**Medium**
>(High when combined with other findings)

## OWASP Mapping

- A05: Security Misconfiguration
    
- A01: Broken Access Control
    
- Information Disclosure

## Root Cause

- Public metrics endpoint
    
- No authentication
    
- No IP allowlisting
    
- Production monitoring route exposed

## Prevention

- Restrict `/metrics` to internal network
    
- Add authentication
    
- Reverse proxy ACL rules
    
- Separate admin/ops services
    
- Hide version information
    
- Regular external attack surface reviews

## Key Lesson

- Monitoring data is extremely valuable to defenders—and attackers.

## Conclusion

This challenge shows how a simple fuzzing scan can uncover operational endpoints that leak system intelligence without requiring exploitation.
