# Remediation Recommendations

## FTP: vsftpd 2.3.4 backdoor

- Remove the affected build and install a trusted, supported, patched FTP service; verify package provenance.
- Disable FTP if file transfer is not required. Prefer SFTP over SSH for administrative file transfer.
- Restrict access to required hosts and networks with firewall rules.
- Review file ownership, permissions, accounts, and credentials. Rotate any credentials that may have been exposed during testing.
- Re-scan the service and verify the vulnerable version and behavior are absent.

## Telnet: exposed remote terminal

- Disable Telnet and use SSH for remote administration.
- Restrict management access to trusted hosts and networks.
- Enforce strong authentication and monitor failed and unexpected login attempts.
- Verify port 23 is no longer reachable after the change.

## SMTP: Postfix service

- Keep Postfix supported and patched.
- Permit relay only for authenticated users or explicitly trusted networks; retain the observed non-open-relay behavior.
- Configure TLS according to the deployment's mail-flow requirements and limit unnecessary banner details where practical.
- Monitor relay attempts, authentication failures, and unusual mail volume.

## HTTP: Apache and enumerated paths

- Replace the old Apache build with a supported, patched release and review enabled modules, including DAV and content negotiation.
- Manually review the Gobuster-discovered paths. Remove unnecessary content and restrict administrative or status paths.
- Disable directory indexing where it is not needed; verify the Nikto-reported indexes individually.
- Configure appropriate security headers and HTTPS where the application requires browser access.
- Re-run enumeration after remediation and verify each validated issue is resolved.

## General lab controls

- Keep Metasploitable 2 on an isolated virtual network and confirm the intended network mode before testing.
- Limit assessment activity to the authorized target and defined ports; capture commands and results accurately.
- Use least privilege and take a recoverable VM snapshot before future testing.
