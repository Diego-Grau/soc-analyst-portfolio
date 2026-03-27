# Phishing Investigation – SOC Simulator

## Overview
This project documents the investigation of multiple security alerts related to phishing activity within a simulated SOC environment provided by TryHackMe.

The analysis focuses on identifying phishing attempts, evaluating real impact by correlating logs in Splunk, and determining response actions based on email, firewall, and web traffic data.

---

## Objectives
- Identify phishing attempts and distinguish them from legitimate emails.
- Analyze indicators such as sender domains, URLs, and IP addresses.
- Correlate email events with network logs to verify user interaction.
- Evaluate the effectiveness of controls (Firewall/Filters).
- Determine escalation requirements and recommend remediation actions.

---

## Incident Summary

| Alert ID | Type                   | Description                                      | Interaction                  | Escalation        |
|----------|------------------------|--------------------------------------------------|------------------------------|------------------|
| 8814     | False Positive         | Legitimate onboarding email                      | N/A                          | No               |
| 8815     | Phishing               | Malicious email (Amazon spoofing)               | Not confirmed                | Yes (L2)         |
| 8816     | Connection Attempt     | Connection blocked towards suspicious URL       | Yes (Firewall blocked)       | Yes (L2)         |
| 8817     | Phishing Campaign      | Typosquatting domain (Microsoft spoofing)       | Not confirmed                | Yes (Urgent)     |

---

## Key Findings

### Phishing Techniques Identified
- Domain spoofing (`amazon[.]biz`)
- Typosquatting (`m1crosoftsupport[.]co`)
- URL shorteners (`bit[.]ly`)
- Social engineering based on urgency and technical support

---

### Event Correlation and Network Activity

**Click / Connection Analysis:**  
- Alert 8815: email received, **no evidence of URL click**.  
- Alert 8816: host 10.20.2.17 attempted to access the suspicious URL; connection **blocked by firewall**.  
- Alert 8817: email received, **no evidence of URL interaction**.

**Detection Gaps:**  
- The domain `m1crosoftsupport[.]co` was not categorized as malicious, but no user access was observed.

---

## Impact Assessment
- User interaction: confirmed only in the connection attempt of 8816 (blocked).  
- Outbound traffic: only recorded in 8816 and blocked by firewall.  
- System compromise: no malware downloads or data exfiltration detected; risk limited to phishing exposure.

---

## Escalation Logic
- Not escalated: false positives or no interaction.  
- Medium priority: blocked IOC connection attempts (8816).  
- High priority: allowed connections to malicious infrastructure (none confirmed).

---

## Response Actions
- Block malicious domains and IPs in SIEM.  
- Review and educate users on phishing awareness.  
- Mass removal of suspicious emails (purge).  
- Review authentication logs for unusual events.  
- Improve filtering rules on firewall and proxy.

---

## Indicators of Compromise (IOCs)

**Domains:**
- amazon[.]biz
- m1crosoftsupport[.]co
- bit[.]ly/3sHkX3da12340

**IP Addresses:**
- 67.199.248.11
- 102.89.222.143
- 45.148.10.131

---

## Conclusion
Email detection is only the first step of analysis.

Splunk correlation shows that **only one connection attempt was blocked by the firewall** (alert 8816), while the other emails were delivered but not accessed.  

This indicates that, although no compromise is confirmed, the incident reinforces the need for user education and preventive blocking measures in security infrastructure.
