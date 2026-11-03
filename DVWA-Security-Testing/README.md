# DVWA — Web Application Security Testing

**Platform:** Damn Vulnerable Web Application (DVWA)  
**Environment:** Kali Linux, locally hosted DVWA  
**Security Levels:** Low and High

## Overview

This project documents practical web application security testing conducted using DVWA as part of my cybersecurity internship.

The objective was to understand common web application vulnerabilities, demonstrate their impact in an authorised lab environment and compare how different security configurations affect exploitation.

## Vulnerabilities Tested

| Vulnerability | Security Level | Outcome |
|---|---|---|
| SQL Injection | Low / High | Injection remained possible at High |
| Reflected XSS | Low / High | Original payload blocked at High |
| File Upload | Low / High | PHP upload rejected at High |
| Command Injection | Low / High | Original payload produced no output at High |
| CSRF | Low / High | Legitimate password change confirmed at High; cross-site protection not independently tested |
| Insecure CAPTCHA | Low / High | High testing blocked by missing reCAPTCHA configuration |
| Brute Force | Low | Repeated login attempts accepted without visible restrictions |
| Blind SQL Injection | Low | Boolean-based injection demonstrated |
| Weak Session IDs | Low | Predictable sequential test cookie identified |
| File Inclusion | Low | Local File Inclusion demonstrated |

## Key Findings

The assessment highlighted several security weaknesses, including insecure SQL query construction, inadequate handling of user-controlled input, predictable session identifiers and unrestricted local file access.

Testing at High security demonstrated that additional controls could block specific attack techniques. However, some vulnerabilities remained exploitable, particularly SQL Injection.

## Recommendations

- Implement parameterised SQL queries.
- Apply context-aware output encoding to prevent XSS.
- Validate file uploads and restrict executable content.
- Avoid executing shell commands using untrusted input.
- Use server-validated CSRF tokens.
- Implement rate limiting and secure session management.
- Restrict file inclusion to approved application resources.

## Conclusion

These exercises strengthened my understanding of web application vulnerabilities, exploitation techniques and defensive controls.

All testing was performed in an authorised local training environment.
