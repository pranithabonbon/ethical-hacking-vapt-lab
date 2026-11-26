# Assessment Findings

This document distinguishes confirmed evidence from service observations and scanner leads. No CVSS score is assigned because the project does not document a scoring method.

| Finding | Affected service | Evidence | Risk | Recommendation | Validation |
|---|---|---|---|---|---|
| vsftpd 2.3.4 backdoor associated with CVE-2011-2523 | FTP, `10.0.2.3:21` | Nmap `--script vuln` screenshot reports `ftp-vsftpd-backdoor` as vulnerable. Metasploit output reports the backdoor spawned and a Meterpreter session opened from `10.0.2.4` to `10.0.2.3`. | Successful session demonstrates remote command access in this lab and could lead to severe compromise on an affected system. No formal CVSS score is documented. | Remove/replace the affected vsftpd build with a trusted patched release; disable FTP if unnecessary; prefer SFTP; restrict network reachability; review permissions and credentials. | The project screenshot records the module run and opened session. Re-test after remediation with the same authorized checks and confirm the vulnerable version/path is no longer present. |
| Telnet reachable; cleartext protocol exposure | Telnet, `10.0.2.3:23` | Nmap identifies Linux telnetd; `telnet` screenshot reaches the Ubuntu login prompt. No login is shown. | Credentials and session contents may be exposed to network observers. This is a protocol risk, not evidence of successful access or exploitation. | Disable Telnet and use SSH with strong authentication; limit management access to trusted hosts. | Confirm port 23 is closed after remediation and verify authorized SSH management access. |
| SMTP service and extensions disclosed; no open relay indicated | SMTP, `10.0.2.3:25` | Nmap identifies Postfix smtpd; command enumeration and Netcat EHLO outputs show server information. `smtp-open-relay` reports "Server doesn't seem to be an open relay." | Service exposure and banner detail are observations. The supplied relay check did not confirm an open relay. | Restrict relay to authenticated/trusted clients, patch Postfix, configure appropriate TLS, and monitor mail traffic. | Repeat the authorized relay check and confirm expected banner/TLS policy; no relay vulnerability is claimed by this evidence. |
| HTTP paths and server configuration observations | HTTP, `10.0.2.3:80` | Nmap identifies Apache httpd 2.2.8 (Ubuntu) with DAV/2. Gobuster lists paths/status codes. Nikto reports missing headers, content negotiation, junk-method response behavior, and directory indexing on several paths. | Potential information exposure or misconfiguration; scanner output requires validation. No HTTP exploitation is shown. | Upgrade to a supported server version; remove unnecessary paths; disable indexing where not required; review DAV and content negotiation; configure appropriate security headers and HTTPS. | Manually verify each exposed path and configuration, then repeat scans after remediation. Treat tool warnings as leads until confirmed. |

## Evidence index

- [Nmap service/version scan](../evidence/scanning/nmap-service-version-scan.jpg)
- [vsftpd vulnerability detection](../evidence/vulnerability-identification/nmap-vsftpd-cve-2011-2523-detection.jpg)
- [Meterpreter session opened](../evidence/exploitation/vsftpd-meterpreter-session-opened.jpg)
- [Telnet login prompt](../evidence/service-enumeration/telnet-login-prompt.png)
- [SMTP open-relay check](../evidence/service-enumeration/smtp-open-relay-check.png)
- [Gobuster enumeration](../evidence/web-assessment/gobuster-directory-enumeration.png)
- [Nikto assessment](../evidence/web-assessment/nikto-web-server-assessment.png)
