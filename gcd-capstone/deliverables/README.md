# GCD Capstone — Public Deliverables

Sanitized excerpts from the deliverables produced during the Gulf Coast Family Dental capstone engagement. Specific environment details (IP ranges, domain names, hostnames, account names, service principal names, and consultant account usernames) have been redacted from all files in this folder.

## Engagement at a glance

- **Engagement type:** Gray-box internal penetration test of a HIPAA-regulated environment, plus full infrastructure documentation
- **Team:** Sentinel Ridge Security — Travis Currier, Timothy Powell, Josue Quinones (Consultants); Noah Whalen (Project Manager)
- **Course:** Senior Capstone, Pensacola Christian College
- **Testing window:** April 8–17, 2026
- **Methodology:** PTES, NIST SP 800-115, CVSS v3.1, MITRE ATT&CK
- **Findings:** 3 High, 3 Medium, 1 Low (1 Medium remediated and verified during the engagement)

For the full engagement narrative, see [`../README.md`](../README.md).

## Available publicly

### `executive-summary.pdf`
Three-page sanitized executive summary from the Internal Network Penetration Test Report. Includes the engagement overview, overall risk rating, full findings table with business-impact column, a highlighted finding (SIEM detection gap), prioritized recommendations across three time horizons, and positive security observations. Written for a non-technical decision-maker; readable in five minutes.

### `ops-manual-toc.pdf`
Four-page table of contents from the IT & Cybersecurity Infrastructure Operations Manual (100+ pages). Demonstrates the scope of standing operational documentation produced for the engagement — environment summary, system architecture, network design, server configuration, database documentation, security policies, software inventory, operational procedures, monitoring & logging, maintenance procedures, troubleshooting guide, and access matrix appendix.

### `ops-manual-sample-chapter.pdf`
Two-page sample chapter from the operations manual: Section 7.7 — Current Security Gaps & Recommendations. Selected as the public excerpt because it demonstrates analytical security writing — identifying known gaps in an environment and recommending remediation — rather than step-by-step procedural documentation. Covers third-party consultant account lifecycle, Windows activation status, MD5 password hashing in a HIPAA context, and GPO documentation hygiene.

## Available on request

The full unredacted versions of all engagement deliverables are available for hiring discussions:

- **Internal Network Penetration Test Report** — Complete report including all seven findings with technical evidence, reproduction steps, command output, screenshots, and detailed remediation guidance
- **IT & Cybersecurity Infrastructure Operations Manual (v1.0)** — Full 100+ page operations manual covering all sections listed in `ops-manual-toc.pdf`
- **Disaster Recovery Plan (v1.0)** — Recovery objectives, breach notification procedures, system restoration playbooks, and incident-specific recovery procedures

To request access for hiring discussions, contact:

**Travis Currier**
[tcurrier1819@gmail.com](mailto:tcurrier1819@gmail.com)
[LinkedIn](https://www.linkedin.com/in/travisjcurrier)

## Notes on attribution

These deliverables were produced collaboratively by the four-person Sentinel Ridge Security team. Travis Currier served as Lead Tester (AD enumeration, exploitation, post-exploitation) and Budget Manager. Specific contributions to each deliverable are noted in the engagement writeup.

## Notes on sanitization

These public versions were prepared specifically for portfolio use. The redactions applied are:

- Domain name → "the client's Active Directory domain"
- Internal IP range → "the internal network segment"
- Hostnames → generic descriptors (e.g., "the primary domain controller," "the database server")
- Service Principal Names → "a service account SPN"
- User and service account names → role descriptors
- Consultant account usernames → "consultant accounts"
- Fictional client signatories and signatures → removed entirely
- Office address and team contact details → removed entirely

Technical content (attack names, methodology, CVSS scores, MITRE ATT&CK mappings, HIPAA Security Rule citations, tools used) is preserved unchanged.
