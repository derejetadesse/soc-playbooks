# Incident Response Playbook — Ransomware
**Goal:** Contain spread, preserve evidence, restore safely, and meet reporting obligations.

## 1) Triage & Scope
- Confirm encryption/ransom note; capture screenshots & sample files.
- Identify initial vector (phish, RDP, vuln, supply chain).
- Determine scope: affected hosts, domains, shares, backup impact.
- Note time window (first signs → now).

## 2) Containment (ASAP)
- Isolate infected hosts (EDR containment / VLAN / pull cable).
- Disable SMB shares for affected segments; block C2 IOCs.
- Suspend compromised accounts; enforce MFA; reset high-value creds.
- Stop scheduled tasks/services the malware created.

## 3) Evidence Preservation
- Memory/image of 1–2 representative hosts (if feasible).
- Collect ransom note, sample encrypted file, dropped binaries, logs (EDR, Security, Sysmon).
- Export IOCs: hashes, mutexes, C2 domains/IPs, TOR addresses, emails.

## 4) Eradication
- Remove malware + persistence (run keys, services, tasks, startup).
- Patch exploited vulns; restrict/lock down RDP; require MFA.
- Hunt laterally for credential reuse/admin tool abuse.

## 5) Recovery
- Verify clean backups (immutable/offline). Don’t restore into infected network.
- Reimage/rebuild priority systems; rotate AD krbtgt, local admin, service creds.
- Reconnect gradually; monitor closely in SIEM/EDR.

## 6) Communications / Legal
- Notify leadership, legal, privacy, insurers. Consider law enforcement.
- Manage external notifications if regulated data may be impacted.

## 7) Related Detections
- **Sigma:** `powershell_encoded_command.yml`, `suspicious_admin_logon.yml`
- **Suricata:** `http_user_agent.rules`
- **Zeek:** `detect_dns_exfiltration.zeek`

## 8) Lessons Learned
- Harden backups (immutability, offline).
- EDR + allow-listing; remove legacy protocols; enforce MFA.
- Tabletop exercises; update asset inventory and RTO/RPO.
