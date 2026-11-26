# Tools Used

The command examples below are present in the supplied report or screenshots. They describe this lab activity and should only be run against an authorized, isolated target.

| Tool | Purpose and project use | Evidence-backed example |
|---|---|---|
| Kali Linux | Attacker operating system used for network and service assessment. | `ifconfig` (shown in the interface screenshot). |
| Nmap | Host discovery, service/version detection, and protocol/vulnerability checks. | `nmap -sV 10.0.2.3`; `nmap -p 21 --script vuln 10.0.2.3`; service-specific commands in [methodology](../methodology/methodology.md). |
| Metasploit Framework | Searched for and ran the module matching vsftpd 2.3.4 to validate the finding in the lab. | `msfconsole`; `search vsftpd`; `use exploit/unix/ftp/vsftpd_234_backdoor`; `show options`; `set RHOSTS 10.0.2.3`. The screenshot shows an attempted `LHOSTS` typo, then `LHOST`; module options shown do not list LHOST as required. |
| Gobuster | Enumerated common HTTP paths and recorded status codes. | `gobuster dir -u http://10.0.2.3/ -w /usr/share/wordlists/dirb/common.txt` |
| Nikto | Checked the HTTP server for configuration and exposed-path observations. | `nikto -h http://10.0.2.3/` |
| Netcat | Connected to SMTP to inspect its banner and EHLO extensions. | `nc -nv 10.0.2.3 25` |
| `curl` | Requested HTTP response headers. | `curl -I http://10.0.2.3/` |
| `nbtscan` | Discovered the Metasploitable host on the lab subnet. | `nbtscan -r 10.0.2.0/24` |

The materials also mention FTP and Telnet clients and a browser as prerequisites. No additional example commands are presented for those tools beyond the captured Telnet connection.
