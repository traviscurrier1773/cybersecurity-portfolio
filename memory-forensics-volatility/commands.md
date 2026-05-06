# Volatility Command Reference

A reference of the Volatility 2 commands used during the WIN8TCDumpit.raw analysis. Useful as a quick-start checklist for triaging an unknown Windows memory image.

## Profile Identification

Volatility 2 requires a profile that matches the OS and build of the captured system. Identify it before running any analysis plugins.

```bash
vol.py -f memory.raw imageinfo
vol.py -f memory.raw kdbgscan
```

`imageinfo` is faster and sufficient most of the time. `kdbgscan` is more thorough and useful when `imageinfo` returns ambiguous or incorrect suggestions. If suggested profiles fail, try adjacent ones — the profile that runs cleanly without errors across multiple plugins is usually the correct one.

## Core Triage Plugin Set

Run these against any unknown Windows memory image to get a baseline picture of system state:

```bash
# Active processes (flat list)
vol.py -f memory.raw --profile=<profile> pslist > pslist.txt

# Process tree (parent/child relationships)
vol.py -f memory.raw --profile=<profile> pstree > pstree.txt

# Anomaly detection — name spoofing, path mismatches, hollowing
vol.py -f memory.raw --profile=<profile> malprocfind > malprocfind.txt

# DLLs loaded per process — useful for spotting injected modules
vol.py -f memory.raw --profile=<profile> dlllist > dlllist.txt

# NTLM/LM hashes from SAM
vol.py -f memory.raw --profile=<profile> hashdump > hashdump.txt
```

## What Each Plugin Tells You

| Plugin | What to look for |
|---|---|
| `pslist` | Unexpected processes, processes with no parent, suspiciously short-lived ones |
| `pstree` | Processes with the wrong parent (e.g. `cmd.exe` spawned by something other than `explorer.exe` or a script host) |
| `malprocfind` | Misspellings (`scvhost.exe`), wrong execution paths, unusual command lines |
| `dlllist` | Non-standard DLLs in critical processes, DLLs loaded from user directories |
| `hashdump` | NTLM hashes that can be cracked offline or used directly via pass-the-hash |

## Tips from This Investigation

- Save each plugin's output to a separate file. It preserves a record of what was observed at examination time and lets you grep across results without re-running.
- If `imageinfo` suggests a server profile but the image is from a desktop OS, try the matching client profile — they share kernel internals and the suggested profile is often "close but not quite."
- The presence of VM-specific processes (`vmacthlp.exe`, `vmtoolsd.exe`) is a useful early signal that the captured system was virtualized.
