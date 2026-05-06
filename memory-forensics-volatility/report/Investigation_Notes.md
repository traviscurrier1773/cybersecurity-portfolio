# Investigation Notes: RAM Analysis

*Contemporaneous examiner's notes recorded during the analysis. Preserved as a record of methodology and decision points rather than rewritten as polished prose.*

## Setup

Launched the SIFT Linux virtual machine. After inserting the hard drive containing the memory dump, copied `WIN8TCDumpit.raw` into the following directory for case organization:

```
Desktop/cases/memory/
```

Obtained root access:

```bash
sudo su
```

To streamline Volatility commands, set an environment variable for the image path so the `-f` argument did not need to be retyped on every invocation.

## Profile Determination

To identify the correct Volatility profile for this Windows memory image:

```bash
vol.py -f WIN8TCDumpit.raw imageinfo
vol.py -f WIN8TCDumpit.raw kdbgscan
```

`imageinfo` and `kdbgscan` initially suggested `Win2012x64`. However, that profile failed to yield useful output for several plugins. After testing alternatives, `Win81U1x64` returned consistent and complete results across the plugin set, so that profile was used going forward.

## Volatility Commands Executed

Each command was run with the working profile and output saved to a file for documentation:

```bash
vol.py --profile=Win81U1x64 pslist > pslist.txt
vol.py --profile=Win81U1x64 pstree > pstree.txt
vol.py --profile=Win81U1x64 malprocfind > malprocfind.txt
vol.py --profile=Win81U1x64 dlllist > dlllist.txt
vol.py --profile=Win81U1x64 hashdump > hashdump.txt
```

## Initial Triage

- **`pslist` / `pstree`** — Provided a list and hierarchy of active processes at the time of the snapshot. Common system processes were present. Reviewed for processes like `cmd.exe` or suspiciously spawned children.
- **`malprocfind`** — Checked for misspelled or hidden process names. Most entries looked normal; flagged for closer inspection of any potential obfuscation or hollowing.
- **`dlllist`** — Showed DLLs loaded per process. Useful for identifying potential injection points or unusual libraries that could indicate malware.
- **`hashdump`** — Provided NTLM password hashes. The user `jcloudy` was not listed, but the user `badguy` appeared with the NTLM hash:

  ```
  931299a158028c08a0bd348df6b84da5
  ```

  This hash was submitted to CrackStation and resolved to the password `pa$$word`. The assignment had hinted at recovering `Jcloudy2018!!`, but no `jcloudy` account or matching credential was present in memory at acquisition time.

## Detailed Plugin Analysis

### 1. `pslist` (Process List)

The process list showed a fully running Windows session with over 30 processes. Core system services appeared intact, and no unrecognized or malicious process names were present. Examples include `smss.exe`, `csrss.exe`, `wininit.exe`, and `lsass.exe`. The presence of `vmacthlp.exe` indicated the system was running inside a virtual machine.

### 2. `pstree` (Process Tree)

Parent-child process relationships aligned with standard Windows behavior. `services.exe` correctly parented multiple service-related executables such as `svchost.exe`, `vmtoolsd.exe`, and `spoolsv.exe`. The presence of `explorer.exe` as a child of `winlogon.exe` confirmed an interactive login session, indicating user activity on the system.

### 3. `malprocfind` (Malicious Process Detection)

The `malprocfind` scan returned no obvious anomalies. All processes passed checks related to name integrity, execution path, priority, and command line arguments. No process was flagged for hollowing. System processes such as `explorer.exe` and `svchost.exe` appeared properly aligned and non-malicious.

### 4. `dlllist` (DLL Enumeration)

DLL inspection revealed standard Windows libraries loaded in expected memory locations for each process. For example, `smss.exe` and `csrss.exe` loaded system libraries like `ntdll.dll`. No injected or suspicious DLLs were found in critical processes, indicating no obvious in-memory tampering.

### 5. `hashdump` (Credential Recovery)

Password hashes recovered from memory revealed a valid credential for user `badguy`, whose NTLM hash was `931299a158028c08a0bd348df6b84da5`. This hash matched the password `pa$$word` via CrackStation. Although the assignment hinted at the password `Jcloudy2018!!`, no such password or corresponding user `jcloudy` was found in the captured RAM image.
