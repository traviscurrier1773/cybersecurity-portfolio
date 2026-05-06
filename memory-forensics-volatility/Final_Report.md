# Final Report: WIN8TCDumpit.raw RAM Analysis

**Examiner:** Travis Currier
**Tools Used:** Volatility Framework (via SIFT Linux VM)

**Files Reviewed:**
- `WIN8TCDumpit.raw` — memory dump
- Output files: `pslist.txt`, `pstree.txt`, `malprocfind.txt`, `dlllist.txt`, `hashdump.txt`

---

## 1. What Was Analyzed

This analysis focused on a live memory capture taken from a Windows 8.1 virtual machine, provided as `WIN8TCDumpit.raw`. The RAM dump was analyzed to identify active processes, DLL usage, possible malware indicators, and user credentials retained in memory. The objective was to surface traces of malicious activity, user behavior, or sensitive information that persisted in volatile memory at the time of acquisition.

## 2. Tools and Techniques

The Volatility memory forensics framework was used inside a SIFT Linux virtual machine. The investigation began with profile identification using the `imageinfo` and `kdbgscan` plugins. After testing candidate profiles, `Win81U1x64` produced the most consistent results and was used for the remainder of the analysis.

The following Volatility plugins were run against the image:

- `pslist` — enumerate active processes
- `pstree` — visualize process parent/child relationships
- `malprocfind` — detect anomalies suggesting malicious processes
- `dlllist` — enumerate loaded DLLs per process
- `hashdump` — extract cached credential hashes

Output from each plugin was redirected to a text file for offline review and to preserve a record of the findings.

## 3. Key Findings

**Process listings (`pslist` / `pstree`)** — Revealed normal process activity. Core processes such as `smss.exe`, `winlogon.exe`, and `explorer.exe` were active. Parent-child hierarchies were consistent with typical Windows behavior, with `services.exe` correctly launching service-related processes.

**Malicious process detection (`malprocfind`)** — No anomalies were reported. No signs of spoofed names, path mismatches, or process hollowing were detected. All entries passed integrity checks.

**DLL enumeration (`dlllist`)** — Showed legitimate system libraries loaded in each process. No evidence of malicious DLL injection was observed.

**Credential extraction (`hashdump`)** — Retrieved a user credential stored in memory. The user `badguy` had an NTLM hash corresponding to the password `pa$$word`, confirmed via CrackStation. No credentials were found for a user named `jcloudy`, despite the assignment hint suggesting one might be present.

## 4. Why This Matters

The RAM analysis confirmed the presence of normal system operations and indicated that no active malware was running at the time of capture. Recovering the password for `badguy` demonstrated the forensic value of live memory analysis — sensitive credentials cached in volatile memory can be recovered when an image is captured before reboot. This capability is particularly relevant for timeline reconstruction, privilege escalation analysis, and detecting lateral movement during incident response engagements.
