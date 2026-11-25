# Troubleshooting

Most problems fall into one of these. If yours is not here, [open an issue](https://github.com/xRedxDevilx/kestrel-clipper-releases/issues)
and attach a diagnostics zip — **Settings → Download diagnostics** makes one, with every key and token removed.

---

## "Windows protected your PC"

![The blue SmartScreen warning, with More info and Run anyway circled](images/08-smartscreen.png)

**This is expected.** Windows shows it for any program it has not seen many times before, and a certificate that
would quiet it costs several hundred pounds a year while still showing the warning until enough people have
downloaded the file. Kestrel Clipper is a small independent app, so you get the warning.

Click **More info**, then **Run anyway**.

**Only do that for a file you downloaded from
[this repository's releases page](https://github.com/xRedxDevilx/kestrel-clipper-releases/releases/latest).**
If you got the installer anywhere else, delete it. You can check a download is genuine: each release lists an
SHA-256 checksum, and in PowerShell `Get-FileHash "$HOME\Downloads\Kestrel Clipper Setup 1.3.5.exe"` should print
the same value.

---

## Setup says it cannot close the app

Older versions showed *"Setup was unable to automatically close all applications"*. Version 1.3.5 closes the
running copy itself, so this should not happen again. If it does: right-click the Kestrel icon in the system
tray (bottom-right, next to the clock), choose **Quit**, then run the installer again.

---

## It installed, but nothing happens when I open it

The app has no window of its own until it is ready — it starts the engine first, which takes a few seconds on
first run. Look for the kestrel icon in the system tray. Click it to open the dashboard.

If the dashboard never appears, open `http://127.0.0.1:8765` in any browser. If that page loads, the app is
running fine and only the window failed to open; if it does not, see the next section.

---

## Antivirus or the firewall is blocking it

The app is new and unsigned, so some security software stops it talking to the internet. Symptoms: streamers
never show as live, or the dashboard never loads.

- **Windows Defender Firewall:** when the prompt appears, allow Kestrel Clipper on **private networks**.
- **Third-party antivirus** (Avast, AVG, Norton, McAfee, Bitdefender): add an exception for
  `%LOCALAPPDATA%\Kestrel Clipper`.
- The app only talks to the streaming sites, the AI provider you choose, and its own update check. It never
  uploads your video anywhere.

---

## No clips are appearing

Work through these in order.

1. **Is clipping on?** The button at the bottom-left should say **Stop clipping**. If it says Start clipping, it is off.
2. **Is anyone live?** The **Streamers** page shows a red LIVE badge and *rec* while recording. Nothing live means nothing to clip.
3. **Has anything happened yet?** It only cuts a clip when chat reacts or the streamer does. A quiet stream makes no clips, by design.
4. **Is it being too fussy?** **Settings → How picky** sets the score a clip must reach. Lower it to around 55 and more will come through.
5. **Check the skipped pile.** **Review → AI skipped** shows what it rejected and why. If good moments are in there, the score is set too high.

---

## Clips take a long time to make

Editing is the slow part, and on a processor alone it is several minutes per clip.

- **NVIDIA card?** **Settings → GPU speed-up** downloads what it needs and makes editing many times faster.
- **Recording several streams at once** divides the machine between them. Pause the ones you care less about on the Streamers page.

---

## It is using a lot of disk space

Recording keeps a rolling buffer per stream, and source footage is kept for 48 hours so clips can be re-edited.

- **Settings → Storage and cleanup** sets how long rejected clips and source footage are kept.
- Clips you have approved are never deleted automatically.

---

## Closing the window did not close the app

That is deliberate: closing the window leaves it clipping in the background, and the tray icon brings it back.
To quit properly, right-click the tray icon and choose **Quit**.

To make the window's close button quit instead, turn on **Settings → Quit when I close the window**.

---

## The update will not install

- Make sure the app is not open twice. Right-click the tray icon, **Quit**, then run the installer from the releases page by hand.
- If the download fails its checksum, the app deletes it and says so. That usually means the download was
  interrupted — try again.
- You can always install the newest version straight over the top from the
  [releases page](https://github.com/xRedxDevilx/kestrel-clipper-releases/releases/latest). Your clips, streamers and settings are kept.

---

## Starting over

Uninstall from **Settings → Apps** in Windows. Your clips and settings stay in
`%LOCALAPPDATA%\Kestrel Clipper\data` so a reinstall picks up where you left off. Delete that folder too if you
want a genuinely clean start.
