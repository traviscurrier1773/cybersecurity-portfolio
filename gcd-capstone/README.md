# Gulf Coast Family Dental — Penetration Test & Infrastructure Engagement

**Role:** Lead Penetration Tester & Budget Manager
**Team:** Sentinel Ridge Security (4-person consulting team)
**Course:** Senior Capstone, Pensacola Christian College
**Duration:** [Fall 2025 – Spring 2026]
**Status:** Delivered

> *Simulated client engagement for academic capstone. Gulf Coast Family Dental is a fictional dental practice; no real patient data, live production systems, or unauthorized testing was involved.*

---

## Engagement Summary

Sentinel Ridge Security was engaged by Gulf Coast Family Dental, P.A. to assess the security posture of a small HIPAA-regulated healthcare environment and to deliver standing operational documentation. The scope combined a gray-box internal penetration test with full infrastructure documentation — a pen test report, a 100+ page IT & Cybersecurity Operations Manual, and a Disaster Recovery Plan.

The environment simulated a realistic small-practice deployment: a Windows Active Directory domain, a PostgreSQL database server, a Wazuh SIEM, Zeek and RITA for network analysis, a Squid forward proxy, and Samba file shares — all running on VMware vSphere across multiple RHEL 10 and Windows hosts.

**Environment:**
- Hypervisor: VMware vSphere
- Endpoints: Windows 10 clients, RHEL 10 servers, Windows Server domain controller

## My Role

As Lead Tester, I directed testing methodology and executed the Active Directory and credential-based attack chain. As Budget Manager, I tracked engagement costs and resource allocation across the four-person team.

Specific contributions:
- Designed and executed the AD attack path (Kerberoasting, LLMNR/NBT-NS poisoning)
- Performed authenticated Nessus vulnerability scanning across the environment
- Triaged 18 Nessus findings and authored remediation guidance
- Co-authored the IT & Cybersecurity Operations Manual (Incident Response, Patch Management, and Change Management chapters)
- Contributed to the final client-facing pen test report

## Tools & Technologies

| Category | Tools |
|---|---|
| Vulnerability scanning | Nessus |
| AD enumeration & exploitation | Impacket, Responder |
| SIEM | Wazuh |
| Network analysis | Zeek, RITA, Wireshark |
| Infrastructure | Active Directory, VMware vSphere, RHEL 10, PostgreSQL, Samba, Squid |
| Configuration management | Ansible |

## Findings

Seven confirmed vulnerabilities were validated and documented in the final report. Severity was assigned using a CVSS-aligned internal rubric.

| ID | Finding | Severity |
|---|---|---|
| F-01 | Kerberoastable SQL service account with weak password | High |
| F-02 | LLMNR / NBT-NS poisoning enabled domain-wide | High |
| F-03 | AD password policy weaker than documented baseline | High |
| F-04 | PostgreSQL service exposed across multiple hosts | Medium |
| F-05 | Wazuh SIEM agent outage created undetected attack window | Medium |

In addition, 18 Nessus findings (N-001 through N-018) were triaged and integrated into the report with prioritized remediation aligned to the HIPAA Security Rule.

### Highlighted Finding: SIEM Detection Gap

During testing, a Wazuh agent outage was discovered on a critical host. The outage created a window during which attacker activity would not have been recorded or alerted on. The gap was reproduced, documented, and presented to the client as a Medium-severity finding with recommendations for agent health monitoring, watchdog alerting, and routine connectivity verification.

This finding is worth highlighting because it captures a class of risk that's easy to miss in checklist-driven assessments — the SIEM was technically deployed and "working," but a silent agent failure rendered detection blind on one host. Identifying it required correlating attack timestamps against SIEM log presence rather than relying on the SIEM's own self-reporting.

## Deliverables

1. **Penetration Test Report** — Executive summary, technical findings, evidence, and prioritized remediation recommendations. Written for both an executive and a technical audience.
2. **IT & Cybersecurity Operations Manual (v1.0)** — 100+ pages covering firewall management, endpoint protection, encryption standards, incident response, patch management, change management, and standing operational procedures.
3. **Disaster Recovery Plan (v1.0)** — Recovery objectives, breach notification procedures, system restoration playbooks, and incident-specific recovery procedures.

## What I Learned

A few things stand out from this engagement that I'll carry into future work:

**Documentation is half the job.** The pen test was a few weeks of testing; the operations manual was months of writing. Hiring managers I've talked to have all confirmed the same thing — the ability to write clearly about technical work is one of the most underweighted skills in junior candidates. Authoring 100+ pages of standing documentation forced me to think about how a technician on a Tuesday morning would actually use what I wrote.

**Detection gaps live in the seams.** The Wazuh finding wasn't a misconfiguration in the SIEM itself — it was a process gap around agent health monitoring. Real-world security failures often look like that: each individual control is "working" but the connections between them aren't being verified.

**Reporting is where the engagement actually lands with the client.** The findings only matter if a non-technical decision-maker can read the executive summary and know what to fix first. Writing the report taught me more about prioritization and stakeholder communication than the testing itself did.


---

*If you'd like to discuss this engagement, my methodology, or any of the findings in more detail, the best way to reach me is via [LinkedIn](https://www.linkedin.com/in/travisjcurrier) or email at tcurrier1819@gmail.com.*
