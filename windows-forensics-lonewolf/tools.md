# Toolchain Reference

A reference for the tools used in the LoneWolf examination, with notes on what each one is for, what it produces, and lessons learned during this engagement.

## Mounting

### FTK Imager
A free imaging and lightweight examination tool from Exterro. *File > Image Mounting* mounts a disk image as a virtual drive on the examiner's machine.

**In this case:** the resulting mount produced KAPE warnings. Switched to Arsenal Image Mounter.

### Arsenal Image Mounter
A more flexible mounting tool. Supports mounting in **Disk device, read only** mode, which exposes the image as a real disk device while preventing writes.

**Lesson:** if a downstream tool flags warnings about the mount, don't continue against the questioned mount. Switch tools.

## Triage

### KAPE (Kroll Artifact Parser and Extractor)
Two-stage Windows triage tool:

- **Targets** — collect underlying artifacts (registry hives, event logs, browser data, recent items, etc.) from a source
- **Modules** — run parsers against collected Targets, producing CSV and text output suitable for review

KAPE is fast, scriptable, and the de facto standard for first-pass Windows triage in incident response and forensics.

## Timeline

### Plaso (`log2timeline` / `psort`)
Open-source super-timeline framework.

```
log2timeline    →    .plaso storage file
psort           →    timeline.csv
```

`log2timeline` does the heavy lifting of extracting events from every supported artifact type. `psort` filters, sorts, and renders the storage file as something human-readable.

**Lesson:** Plaso is also distributed as a Docker image. If Docker won't cooperate on your machine, the native install from source is a reliable fallback. Verify with `log2timeline --help` before running anything important.

### Eric Zimmerman's Timeline Explorer
A viewer purpose-built for large CSV files (hundreds of thousands of rows) with column filtering, grouping, and search. Far more usable than Excel for timeline review.

## Case Examination

### Autopsy
Open-source GUI digital forensics platform from Basis Technology. Builds a structured case from a disk image and surfaces:

- Operating system info (build, hostname, users, logins)
- Installed programs
- External device history
- Network activity (downloads, browser history, web searches)
- Recycle bin contents
- Files of interest by hash, name, or location

Autopsy is good as a *case* tool — KAPE is good as a *triage* tool. They complement each other; running both against the same image and cross-referencing findings is a practical default.

## Choosing Among Them

| Goal | Tool |
|---|---|
| Mount an `.E01` for downstream tools | Arsenal Image Mounter (read-only) |
| Fast triage of Windows user activity | KAPE |
| Build a super-timeline | Plaso (`log2timeline` → `psort`) |
| Browse a timeline CSV | Eric Zimmerman's Timeline Explorer |
| Full structured case examination | Autopsy |
