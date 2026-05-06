# Memory Forensics: Windows 8.1 RAM Analysis with Volatility

A digital forensics investigation of a Windows 8.1 memory image using the Volatility framework on SIFT. Conducted as a course project for CS 472 Digital Forensics.

> **Note:** All evidence in this project comes from a controlled training environment provided by the course. The "badguy" account, recovered hash, and cracked password are intentionally placed exercise artifacts — not real-world credentials.

## Overview

A raw memory dump (`WIN8TCDumpit.raw`) was provided for analysis. The goal was to triage the image for active processes, loaded DLLs, signs of malware, and any credentials retained in memory at the time of capture.

## Tools

- **Volatility Framework** — open-source memory forensics platform
- **SIFT Workstation** — Linux forensic VM (SANS)
- **CrackStation** — NTLM hash lookup for password recovery

## Key Findings

| Area | Finding |
|---|---|
| Profile identification | `imageinfo` and `kdbgscan` initially suggested `Win2012x64`, but `Win81U1x64` produced consistent results across all plugins |
| Process activity | ~30 processes, all consistent with a normal Windows session; `vmacthlp.exe` confirmed the system was a VM |
| Process tree integrity | Parent-child relationships matched expected Windows behavior; `explorer.exe` under `winlogon.exe` confirmed an interactive login |
| Malicious process detection | `malprocfind` flagged no anomalies — no process hollowing, name spoofing, or path mismatches |
| DLL injection | `dlllist` showed only legitimate system libraries; no injected modules |
| Credential recovery | NTLM hash for user `badguy` was extracted and cracked to `pa$$word` via CrackStation |

## Repository Contents

- [`report/Final_Report.md`](report/Final_Report.md) — formal writeup of the investigation
- [`report/Investigation_Notes.md`](report/Investigation_Notes.md) — examiner's working notes, kept contemporaneously during analysis
- [`commands.md`](commands.md) — Volatility command reference used in this investigation

## Methodology Summary

1. Booted the SIFT VM and staged the memory image under `Desktop/cases/memory/`
2. Identified the correct Volatility profile via `imageinfo` and `kdbgscan`, then validated by running plugins against candidate profiles
3. Ran the standard triage plugin set: `pslist`, `pstree`, `malprocfind`, `dlllist`, `hashdump`
4. Captured each plugin's output to a separate text file for review and chain-of-evidence
5. Cross-referenced findings against the assignment hints; documented discrepancies

## Skills Demonstrated

- Memory forensics workflow on Windows artifacts
- Linux command-line and VM operation (SIFT)
- Volatility framework plugin selection and interpretation
- Hash extraction and password recovery via NTLM lookup
- Investigative methodology — verification, falsification of initial leads, evidence preservation
- Technical writing for both technical and non-technical audiences

## Course Context

Completed for CS 472 Digital Forensics, Spring 2025, Pensacola Christian College. The original deliverables were submitted as `.docx`; the Markdown versions in this repo are converted for readability on GitHub.

The memory image itself is not redistributed in this repository.
