# Travis Currier — Cybersecurity Portfolio

Security+ certified cybersecurity student finishing my B.S. in Computer Science (Cybersecurity concentration) at Pensacola Christian College in May 2026, with an MBA in IT Management to follow. Currently preparing for CySA+.

This repository documents projects, lab work, and writeups across penetration testing, incident response, SIEM, and digital forensics. Targeting SOC analyst, incident response, and detection engineering roles.

## Contact

- **Email:** tcurrier1819@gmail.com
- **LinkedIn:** [linkedin.com/in/travisjcurrier](https://www.linkedin.com/in/travisjcurrier)
- **Location:** East Peoria, IL (open to relocation; remote considered)

## Certifications

- CompTIA Security+ ce
- CompTIA CySA+ *(in progress)*

## Projects

### [Gulf Coast Family Dental — Penetration Test & Infrastructure Engagement](./gcd-capstone/README.md)

*Senior Capstone | Pensacola Christian College | Fall 2025 – Spring 2026*

Gray-box internal penetration test of a simulated HIPAA-regulated dental practice environment. Served as Lead Tester and Budget Manager for a four-person consulting team (Sentinel Ridge Security).

**Tools:** Nessus, Wazuh, Zeek, RITA, Wireshark, Impacket, Responder, Active Directory, RHEL 10, VMware vSphere, PostgreSQL

**Highlights:**

- Identified 7 confirmed vulnerabilities across AD, database, and network layers (3 High / 3 Medium / 1 Low)
- Executed Kerberoasting and LLMNR/NBT-NS poisoning attacks against a Windows domain
- Discovered a Wazuh SIEM agent outage creating an undetected attack window
- Triaged 18 Nessus findings with HIPAA-aligned remediation guidance
- Co-authored a 100+ page IT & Cybersecurity Operations Manual and Disaster Recovery Plan

[Full writeup →](./gcd-capstone/README.md)

*Simulated client environment for academic capstone — no real patient data or live production systems involved. Specific environment details (IP ranges, domain names, hostnames) have been redacted from this public writeup; full technical details available on request.*

---

### [Memory Forensics — Windows 8.1 RAM Analysis with Volatility](./memory-forensics-volatility/README.md)

*CS 472 Digital Forensics | Pensacola Christian College | Spring 2025*

Triage of a Windows 8.1 memory image using the Volatility framework on the SIFT Workstation. Identified the correct kernel profile, enumerated processes and loaded DLLs, screened for malicious activity, and recovered cached credentials from memory.

**Tools:** Volatility Framework, SIFT Workstation, CrackStation

**Highlights:**

- Identified the correct Volatility profile (`Win81U1x64`) after initial `imageinfo` and `kdbgscan` results suggested an incorrect server profile
- Ran the standard triage plugin set (`pslist`, `pstree`, `malprocfind`, `dlllist`, `hashdump`) and validated process tree integrity
- Extracted an NTLM hash from memory and recovered the corresponding password via offline lookup
- Documented methodology and findings in both formal-report and contemporaneous-notes formats

[Full writeup →](./memory-forensics-volatility/README.md)

*Controlled training environment provided by the course — no real-world credentials or systems involved.*

---

*Additional projects in progress: TryHackMe SOC Level 1 path and a home Active Directory detection lab.*

## Skills

**Offensive:** Penetration testing, Active Directory exploitation (Kerberoasting, LLMNR/NBT-NS poisoning), Impacket, Responder, Nessus

**Defensive:** SIEM (Wazuh), log analysis, network traffic analysis (Zeek, RITA, Wireshark), incident response, vulnerability management

**Forensics:** Memory analysis (Volatility), credential recovery, evidence handling

**Infrastructure:** Windows Server, Active Directory, RHEL/Linux, VMware vSphere, PostgreSQL, DNS, Ansible

**Frameworks & Standards:** NIST CSF, HIPAA Security Rule, MITRE ATT&CK

**Leadership & Communication:** Technical writing (100+ page operations manual), team leadership, project budgeting

## Education

**B.S. Computer Science, Cybersecurity Concentration** — Pensacola Christian College *(Aug 2022 – May 2026)*
Minor: Criminal Justice | Dean's List (multiple semesters)

**MBA, IT Management** — Pensacola Christian College *(enrolling 2026)*
