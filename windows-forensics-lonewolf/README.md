# Windows Forensic Examination — LoneWolf Case

A full Windows forensic examination of the LoneWolf training image, covering image mounting, KAPE triage, timeline reconstruction with Plaso, and case examination with Autopsy. Conducted as a course project for CS 472 Digital Forensics.

> **Note:** LoneWolf is a well-known training case used in academic digital forensics courses. The subject ("Jim Cloudy") and findings are part of the training scenario, not a real investigation.

## Overview

The LoneWolf disk image (`LoneWolf.E01`) was provided for analysis. The goal was to mount the image safely, triage it for artifacts of investigative interest, build a timeline of system activity, and document findings supporting whether further investigation was warranted.

## Tools

- **FTK Imager** (4.7.3.81) — initial image mounting
- **Arsenal Image Mounter** (3.11.303) — read-only mounting after FTK Imager produced KAPE warnings
- **KAPE** (1.3.0.2) — Kroll Artifact Parser and Extractor; triage
- **Plaso** (`log2timeline` / `psort`) — timeline generation
- **Eric Zimmerman's Timeline Explorer** — timeline review
- **Autopsy** (4.21.0) — case examination and artifact extraction

## Key Findings

| Area | Finding |
|---|---|
| Operating system | Windows 10 Education |
| Hostname | `DESKTOP-PM6C56D` |
| Last interactive login | 2018-04-06 07:26:27 CDT |
| Primary user account | `jcloudy` |
| Linked online identity | Google Chrome account `jimcloudy1@gmail.com` |
| External devices | Two SanDisk SDCZ80 USB flash drives, first connected 2018-03-27; integrated webcam, Bluetooth module, and rate matching hubs |
| Cloud storage | Dropbox v46.4.65 and Google Drive installed |
| Recycle bin | Deleted documents discussing the Second Amendment and firearm accessibility |
| Files of investigative interest (Desktop / Recent) | `Cloudy Manifesto`, `SelfDefeseisMurder`, `DeathToll`, `AIRPORT INFORMATION` |
| Browser searches of investigative interest | "most beautiful contries with non extraditionk"; "Buy 9mm ammo Online at Gunbroker.com" |
| Browser references | Washington D.C., the Democratic National Committee headquarters, "gun free zones" |

## Conclusion

The combination of named files, search history, and location references provides reasonable grounds for further investigation. The browser searches in isolation are not inherently illegal; the conclusion rests on their context alongside the recovered files and references.

## Repository Contents

- [`report/Final_Report.md`](report/Final_Report.md) — formal writeup of the examination
- [`report/Investigation_Notes.md`](report/Investigation_Notes.md) — examiner's notes from the KAPE, Autopsy, and timeline phases
- [`tools.md`](tools.md) — reference for the toolchain used in this examination

## Methodology Summary

1. Staged the `LoneWolf.E01` image on a dedicated partition of an external HDD (separate from where derived reports were written) to keep evidence and work product isolated
2. Attempted to mount with FTK Imager; KAPE produced warnings against the resulting mount, so switched to Arsenal Image Mounter in read-only mode
3. Ran KAPE triage with appropriate Targets and Modules; reviewed CSV/text output for artifacts of interest
4. Built a timeline with `log2timeline` → Plaso storage file → `psort` → CSV; reviewed in Timeline Explorer
5. Performed full case examination in Autopsy (OS info, user accounts, external devices, network history, installed programs, recycle bin, desktop)
6. Cross-referenced artifacts across all three tools before drawing conclusions

## Skills Demonstrated

- Full Windows examination workflow: mount → triage → timeline → case analysis
- Forensic decision-making under tool failure (FTK Imager → Arsenal Image Mounter; Docker Plaso → native install)
- Working knowledge of the standard professional toolchain (KAPE, Plaso, Autopsy, Timeline Explorer)
- Read-only evidence handling and partition-isolated staging
- Drawing conclusions in measured, evidence-bound language appropriate for a forensic report

## Course Context

Completed for CS 472 Digital Forensics, Spring 2025, Pensacola Christian College. The original deliverables were submitted as `.docx`; the Markdown versions in this repo are converted for readability on GitHub.

The disk image itself is not redistributed in this repository.
