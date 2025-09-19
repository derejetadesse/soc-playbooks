# Incident Response Playbook — Phishing

**Goal:** Contain the incident quickly, prevent credential theft, and educate the user.

## 1) Triage
- Collect the email (.eml) and headers.
- Identify delivery path (mail gateway logs), attachments, and URLs.
- Check user actions (clicked? entered creds? downloaded?).

## 2) Containment
- Reset affected user passwords/sessions (SSO, MFA).
- Block sender domain/IP, malicious URLs, and file hashes on email gateway/EDR.
- Quarantine matching emails for other recipients.

## 3) Eradication
- Remove persistence (malicious add-ins/startup items).
- Clean infected endpoints with EDR/AV.

## 4) Recovery
- Re-enable access; monitor for abnormal logins.
- Add conditional access policy if needed (impose MFA, geo limits).

## 5) Evidence / Artifacts
- Email headers, URL list, attachment SHA256, affected user list, timestamps.
- SIEM events: login attempts, mailbox rules, OAuth grants.

## 6) Related Detections
- **Sigma:** suspicious_admin_logon.yml (after-hours admin logons)
- **Suricata:** http_user_agent.rules (curl/python-requests)
- **Zeek:** detect_dns_exfiltration.zeek (long DNS queries)

## 7) Comms & Lessons Learned
- Notify stakeholders, helpdesk, and end-user with safe-browsing guidance.
- Update user awareness content and block lists.

**NIST mapping:** Preparation → Identification → Containment → Eradication → Recovery → Lessons Learned.
