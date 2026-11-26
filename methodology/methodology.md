# Methodology

The sequence below follows the supplied report and screenshot evidence. Commands are included only where the report or screenshots show them.

1. **Lab setup and interface identification.** Kali Linux and Metasploitable 2 were placed on the project's virtual lab network. The report records the target at `10.0.2.3`; the `ifconfig` screenshot shows Kali `eth0` at `10.0.2.2`, while the report and exploitation screenshot also use `10.0.2.4`. The discrepancy is documented rather than reconciled by assumption.
2. **Host discovery.** `nbtscan -r 10.0.2.0/24` identified `10.0.2.3` as METASPLOITABLE.
3. **Port and service scanning.** `nmap -sV 10.0.2.3` recorded service/version information, including FTP, Telnet, SMTP, and HTTP.
4. **FTP vulnerability identification.** `nmap -p 21 --script vuln 10.0.2.3` reported the vsftpd backdoor finding associated with CVE-2011-2523.
5. **Module review and controlled validation.** Metasploit was started, the vsftpd module searched and selected, and its options reviewed. The screenshots show the target configured as `10.0.2.3`, the module run, and a Meterpreter session opened. Session evidence shows limited file reading and directory listing; it does not establish an unshown privilege level.
6. **Telnet enumeration.** Screenshots show `nmap -sV -p 23 10.0.2.3`, `nmap -p 23 --script telnet-ntlm-info 10.0.2.3`, and `telnet 10.0.2.3 23`. The connection reached a login prompt; no successful login is evidenced.
7. **SMTP enumeration.** Screenshots show `nmap -sV -p 25 10.0.2.3`, `nmap -p 25 --script smtp-commands 10.0.2.3`, `nmap -p 25 --script smtp-open-relay 10.0.2.3`, and `nc -nv 10.0.2.3 25`. The relay result says the server does not appear to be an open relay.
8. **HTTP assessment.** Screenshots show `nmap -sV -p 80 10.0.2.3`, `curl -I http://10.0.2.3/`, `gobuster dir -u http://10.0.2.3/ -w /usr/share/wordlists/dirb/common.txt`, and `nikto -h http://10.0.2.3/`. Their outputs are observations requiring validation; no HTTP exploitation is evidenced.
9. **Evidence collection and reporting.** Screenshots and the project report record the results. Findings are separated into confirmed FTP validation, observed service exposure, and unconfirmed scanner leads.
