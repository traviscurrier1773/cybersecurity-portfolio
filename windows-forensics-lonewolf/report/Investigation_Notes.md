# Investigation Notes: LoneWolf Case

*Contemporaneous examiner's notes recorded across the KAPE triage, timeline generation, and Autopsy examination phases.*

---

## Phase 1 — KAPE Triage

### Mounting

Launched FTK Imager and used *File > Image Mounting* to mount `LoneWolf.E01`. When KAPE was run against the mount, KAPE produced warnings suggesting the mount was not in a state it could safely process. Rather than ignore the warnings, decided to switch mounting tools.

Unmounted the image. Launched Arsenal Image Mounter, used *File > Mount Disk Image File*, selected `LoneWolf.E01`, and set the mount type to **Disk device, read only**. This produced `Local Disk (G:)` containing the full image contents. KAPE accepted this mount without warnings.

### Running KAPE

Configured KAPE with Targets and Modules appropriate for Windows user-activity triage. KAPE produced two output trees:

- **Target output** — collected artifacts (registry hives, log files, browser data, recent items, etc.)
- **Module output** — CSV and text reports produced by parsers run against the collected Target data

### Reviewing the Output

Browsed the Target output to surface user-activity artifacts. Two paths were particularly productive:

- `Users\jcloudy\AppData\Roaming\Microsoft\Windows\Recent` — recent file list for the `jcloudy` user
- `Users\jcloudy\AppData\Local\Google\Chrome\User Data\Default` — Chrome browser data including history database

### Findings of Investigative Interest

Files surfaced from the Recent list and elsewhere:

- `Cloudy Manifesto`
- `SelfDefeseisMurder`
- `DeathToll`
- `AIRPORT INFORMATION`

Browser searches surfaced from the Chrome history:

- "most beautiful contries with non extraditionk"
- "Buy 9mm ammo Online at Gunbroker.com"

Also noted: browser activity referenced Washington D.C., the Democratic National Committee headquarters, and "gun free zones."

### Preliminary Conclusion

Based on the combination of file names and search history, there are reasonable grounds to support further investigation of the user. The searches are not in themselves illegal, but read in context with the named files they warrant follow-up.

---

## Phase 2 — Timeline Generation with Plaso

### Tooling Path

Original plan was Option 1 from the assignment: run Plaso via Docker.

- Downloaded Docker.
- Pulled the `log2timeline/plaso` image.
- Spent 10+ hours trying to get Docker to run Plaso reliably; could not.

Switched to a native installation:

- Installed Plaso from source (GitHub).
- Verified the install by running `log2timeline` and confirming it responded as expected.

### Running the Timeline

```
log2timeline    →    Plaso storage file (.plaso)
psort           →    timeline.csv
```

Opened `timeline.csv` in Eric Zimmerman's Timeline Explorer and reviewed the events.

---

## Phase 3 — Case Examination with Autopsy

Launched the existing Autopsy case for LoneWolf and worked through the artifact categories systematically.

### Operating System Information

- OS: Windows 10 Education
- Hostname: `DESKTOP-PM6C56D`
- Last login: 2018-04-06 07:26:27 CDT
- Additional fields recorded: login count, password hint, failed-password attempt date

### External Device History

| Device | Device ID | First Connected |
|---|---|---|
| SanDisk SDCZ80 Flash Drive | `AA010215170355310594` | 2018-03-27 07:13:16 CDT |
| SanDisk SDCZ80 Flash Drive | `AA010603160707470215` | 2018-03-27 16:45:44 CDT |
| Microdia Dell Integrated HD Webcam | `6&c0f0d73&0&5` | 2018-03-27 16:45:44 CDT |
| Microdia Dell Integrated HD Webcam | `7&2bca401f&0&0000` | 2018-03-27 16:45:44 CDT |
| Dell BCM20702A0 Bluetooth Module | `28E347017777` | 2018-03-27 16:45:44 CDT |
| Intel Integrated Rate Matching Hub | `5&182c2717&0&1` | 2018-03-27 16:45:43 CDT |
| Intel Integrated Rate Matching Hub | `5&2cd6d949&0&1` | 2018-03-27 16:45:43 CDT |

### Network Activity

Internet downloads, web history, and web searches were exported to CSV files for inclusion with the report.

For SRUM data (system performance, application runs, user accounts, network activity), referred to the KAPE Module output from Phase 1 rather than re-extracting in Autopsy.

### Installed Software

Notable items in the installed-programs list:

- Dropbox v46.4.65
- Google Drive

A Google Chrome account was found linked to the email `jimcloudy1@gmail.com`.

### Recycle Bin

Deleted files recovered from the recycle bin included documents discussing the Second Amendment and the accessibility of firearms.

### Desktop / Recent Files

Files appearing on the Desktop or in the Recent items list that warranted closer review (and were saved separately):

- `Cloudy Manifesto`
- `SelfDefeseisMurder`
- `DeathToll`
- `AIRPORT INFORMATION`

These match the files surfaced in Phase 1 (KAPE), providing cross-tool corroboration.

### Wrap-Up

Autopsy findings in this phase corroborated and added context to what KAPE had surfaced. The combination — `jcloudy` user, `jimcloudy1@gmail.com` Google account, USB device history, named files of concern, and the recycle bin contents — gives a coherent picture supporting the preliminary conclusion from Phase 1.
