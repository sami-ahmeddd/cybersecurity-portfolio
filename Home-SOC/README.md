# Home SOC – Security Monitoring & Threat Detection

## Project Overview

This project documents a Home Security Operations Centre (SOC) environment developed during my cybersecurity internship.

The lab was designed to provide practical experience in security monitoring, log collection, detection engineering and alert investigation using Elastic Security and Kibana.

All security testing was conducted within an authorised laboratory environment.

## Lab Architecture

The environment uses Elastic Agent and Filebeat to collect security telemetry from monitored systems and forward it to Elasticsearch for centralised analysis.

**Monitoring workflow:**

Linux and DVWA log sources → Elastic Agent/Filebeat → Elasticsearch → Elastic Security/Kibana → Detection rules and dashboards

**Monitored activity includes:**
- DVWA web application access logs.
- Linux authentication and SSH activity.
- Linux system logs.
- Endpoint process execution and network activity.
- Security detection alerts.

## Tools and Technologies

- **Elastic Security:** SIEM monitoring, detection rules and alert investigation.
- **Kibana:** Log searching, visualisation and dashboards.
- **Elasticsearch:** Centralised log storage and querying.
- **Elastic Agent/Filebeat:** Log collection and forwarding.
- **DVWA:** Deliberately vulnerable web application used for authorised testing.
- **Linux:** System monitoring, authentication logs and security testing.

## Detection Rules Implemented

### 1. SQL Injection Detection

Created and tested a detection rule for suspicious SQL injection activity targeting DVWA.

Generated controlled test requests and investigated the resulting security events.

### 2. SSH Authentication Failure Detection

Configured a detection rule to identify failed SSH authentication attempts.

Generated controlled failed login attempts and verified that Elastic Security produced alerts.

### 3. DVWA Repeated Login Attempts

Created an ES|QL detection rule to identify five or more DVWA login submissions within a five-minute period.

The detection was assigned Medium severity, risk score 47 and MITRE ATT&CK technique T1110 (Brute Force).

Generated controlled login activity and successfully validated that the rule produced an alert.

The detection identifies repeated login submissions as potential brute-force activity; the Apache access logs alone do not confirm failed passwords.

## Dashboard

Created a custom Kibana dashboard titled **Home SOC | Security Monitoring & Threat Detection**.

The dashboard contains three visualisations:

1. **Web Application Attack Categories:** Displays simulated SQL injection, reflected XSS and command injection activity.
2. **Security Events Over Time:** Visualises security-related activity across the monitored period.
3. **DVWA Login Attempts Over Time:** Displays login submissions grouped into five-minute intervals.

### Home SOC Dashboard

![Home SOC Dashboard](images/Home%20SOC%20Dashboard%20Screenshot.jpg)

## Skills Developed

- SIEM deployment and monitoring.
- Centralised security log analysis.
- ES|QL querying and filtering.
- Detection rule creation and validation.
- Investigation of authentication and web application activity.
- Security dashboard development.
- Technical documentation and reporting.

## Conclusion

This Home SOC project provided practical experience with the security monitoring lifecycle, from log ingestion and threat detection to alert validation and visualisation.

The project strengthened my understanding of entry-level SOC Analyst responsibilities and provided practical examples that can be discussed during technical interviews.

**Disclaimer:** This project was completed in an authorised cybersecurity training environment. No unauthorised systems were targeted.
