[README.md](https://github.com/user-attachments/files/29718136/README.md)

# Taorluath

A desktop **bagpipe & pipe-band drum sheet-music editor and player** for the
Great Highland Bagpipe (GHB) and Practice Chanter, plus snare / tenor / bass
drum parts. Write tunes on a Letter-sized page, hear them back with real
instrument samples, and export or print the result.

Built with **Python + Tkinter** (UI) and **Pillow** (rendering). Audio uses the
Windows `winsound` module. Access requires a **purchased activation key**
verified against Firebase.

---

## Features

- **Score editor** on a US-Letter-proportioned page with an editable title /
  composer / tune-type header (double-click to edit) and a page number.
- **Multiple staves** with a G-clef, key signature (sharps sit just after the
  clef), and a time signature shown only where the timing changes.
- **Notes** from whole down to hemidemisemiquaver, with **dots** and **ties**.
  A dot on a note that sits on a line is nudged just above the line.
- **Bagpipe beaming** — sub-crotchet notes barred by beat with correct beam
  counts and partial beams.
- **Gracenotes & embellishments** — singles plus **Doubling**, **Throw on D**,
  **Birl**, **High G Birl**, **Double-Strike**, **Leamluath**, **Taorluath**,
  and **Heavy D Throw**, with placement rules and ledger lines above the stave.
- **Pipe-band drum mode** — Berger uniline notation for snare, tenor and bass,
  with rimshots and rests, saved as `.drum` files.
- **Bar editing** — copy / paste / delete a bar (Ctrl+C / Ctrl+V / Del),
  per-bar start/end styles (Normal / Repeat / Part), and draggable barlines.
- **Gapless playback** — notes ring until the next note; the playing note *and
  its gracenotes* are highlighted.
- **Save/Open** `.pipe` / `.drum` files, **import/export `.bww`**, **Export to
  PDF**, and **real in-app printing** (paper size & DPI selection, 1.75 cm
  margins, squeeze-to-fit).
- **Light / dark theme**, configurable app font, accent & highlight colours.
- **Splash screen** on launch (logo + percentage bar) so the slow-loading exe
  gives immediate feedback.

---

## Requirements (running from source)

- **Windows** (audio uses `winsound`; header text uses Windows fonts).
- **Python 3.8+** (developed on 3.13).
- `pip install pillow pywin32` — Tkinter ships with Python. `pywin32` is only
  needed for printing.
- An internet connection for first-time **activation**.

```
python main.py
```

`main.py` is a thin launcher that shows the splash, then hands off to
`src.app.run_app`.

---

## Where data is stored

All **writable** user data lives under **`%APPDATA%\Taorluath`** (created on
first run) — a packaged `.exe` cannot rely on writing next to itself. Settings
and the licence are stored as small **`.py`** files (not JSON), because a
PyInstaller one-file exe cannot reliably read data files bundled beside it:

```
%APPDATA%\Taorluath\
├── user_scores\        # saved *.pipe and *.drum tunes
├── settings.py         # SETTINGS = { ... }
└── license.py          # LICENSE = { ... }   (written after activation)
```

Bundled read-only **Assets** are resolved from the PyInstaller temp dir
(`sys._MEIPASS`) when frozen, or the project folder when run from source.

---

## Project structure

```
Pipers Friend/
├── main.py                 # launcher: splash screen -> src.app.run_app
├── installer.py            # builds taorluathinstaller.exe (GUI installer)
├── console.py              # developer console (Firebase-gated repo push)
├── taorluath.ico           # app icon
├── taorluath_splash.png    # native splash image (extraction phase)
├── README.md
├── src/
│   ├── constants.py        # paths, settings load/save, themes, fonts, maps
│   ├── model.py            # BagpipeScore: document + .pipe/.drum (de)serialization
│   ├── dialogs.py          # UnifiedSetupDialog (new-tune wizard)
│   ├── licensing.py        # Firestore activation-key verification
│   ├── updater.py          # GitHub version check + update
│   ├── bww.py              # .bww import / export
│   ├── app.py              # PipersFriendApp: UI, rendering, audio, events
│   └── version.txt         # MAJOR.MINOR.PATCH
└── Assets/                 # notes/, bar/, time_sigs/, drums/, audio/, menu/
```

---

## Building the Windows executables

**App** (`dist\Taorluath.exe`):

```
python -m PyInstaller --noconfirm --onefile --windowed --name Taorluath \
  --icon taorluath.ico --splash taorluath_splash.png \
  --add-data "Assets;Assets" --add-data "src/version.txt;src" \
  --hidden-import win32ui --hidden-import win32con --hidden-import win32print \
  --hidden-import win32gui --hidden-import pywintypes --hidden-import pythoncom \
  main.py
```

**Installer** (`dist\taorluathinstaller.exe`) — bundles the app, creates the
data folder, and makes shortcuts. Stage the freshly built app first:

```
copy dist\Taorluath.exe build_payload\taorluath_payload.bin
python -m PyInstaller --noconfirm --onefile --windowed --name taorluathinstaller \
  --icon taorluath.ico --add-data "build_payload/taorluath_payload.bin;." \
  --hidden-import win32com --hidden-import win32com.client \
  --hidden-import pythoncom --hidden-import pywintypes installer.py
```

The app is bundled under the non-`.exe` name `taorluath_payload.bin` so
antivirus doesn't quarantine a nested executable.

---

## Releasing / pushing updates

Versions are `MAJOR.MINOR.PATCH` in `src/version.txt`:

- **MAJOR** — a full revamp (e.g. v2).
- **MINOR** — new features.
- **PATCH** — bug fixes / cosmetic tweaks.

1. Make your changes and **bump `src/version.txt`**.
2. Rebuild `Taorluath.exe`, re-stage the payload, rebuild the installer, and zip
   `taorluathinstaller.exe` into `TaorluathInstaller.zip`.
3. On GitHub, **draft a new release** with a tag matching the version (e.g.
   `v0.2.2`), attach `TaorluathInstaller.zip` in the **binaries** box (2 GB
   limit — not the 25 MB description box), and **publish** it as the latest
   release.
4. The website Download button points at `.../releases/latest/download/…`, so it
   picks up the new build automatically.

On launch the app compares its bundled `version.txt` with the repo's via
`src/updater.py` (`REPO_OWNER` / `REPO_NAME`). If they differ it offers to
update: the **compiled exe opens the Releases page** to download the new
installer (a one-file exe can't overwrite itself); running **from source**, it
pulls the repo zip and overwrites files, never touching `%APPDATA%\Taorluath`.

> If you rename the GitHub repo, update `REPO_OWNER` / `REPO_NAME` in
> `src/updater.py` and the links in the website's `download.html`.

---

## File formats

- **`.pipe`** — score document (JSON payload): metadata, per-stave bar lines and
  styles, and a timeline of note/gracenote nodes. Pitches:
  `High A, High G, F, E, D, C, B, Low A, Low G`.
- **`.drum`** — pipe-band drum score (snare / tenor / bass, uniline positions,
  rimshots, rests).
- **`.bww`** — Bagpipe Music Writer interchange (import & export).
- **`settings.py` / `license.py`** — app settings and the local activation token
  (see *Where data is stored*).

---

## Audio

Per-pitch `.wav` samples in `Assets/audio/{GHB,chanter}` (and `Assets/drums`)
are trimmed by `audio_start_sec` (default 3 s, to skip the reedy warm-up) and
amplified toward the `volume` setting. On playback the selection is concatenated
into one continuous WAV and played via `SND_FILENAME`, so notes are gapless.
Drum hits play a single onset per note (no carry).

---

## Licensing / activation

The app is gated behind a **purchased activation key** verified against
**Firebase Firestore**. On first launch the user enters a key; once activated, a
local token (`%APPDATA%\Taorluath\license.py`) opens the app straight to the
dashboard.

Keys always start with `PF` and look like `PF-83K2-91QA-PL09`.

### Firestore setup

1. Create a Firestore project, then a collection named **`licenses`**.
2. Add one document **per key** (the **document ID is the key**) with fields:
   | field | type | value |
   |-------|------|-------|
   | `activated` | boolean | `false` |
   | `tier` | string | `"Personal 6-month"`, `"Personal 12-month"`, or `"Personal Lifetime"` |
   | `expiration-date` | string | blank; written on activation as `MM-DD-YYYY` |
   | `email` | string | the buyer's email (must match at activation) |
3. In **`src/licensing.py`**, set `PROJECT_ID` (and optionally `FIREBASE_API_KEY`).

### Tiers and expiry

The **`tier`** sets the licence length; the **expiration date is computed at
activation** (activation date + duration) and stored as `MM-DD-YYYY`:

| tier | duration |
|------|----------|
| `Personal 6-month` | 6 months |
| `Personal 12-month` | 12 months |
| `Personal Lifetime` | never expires (`expiration-date` = `never`) |

### Anti-tamper

The local token is **not trusted on its own**. On every launch the app
**re-validates against Firestore**: the key must still exist, be `activated`,
its `tier` / `expiration-date` must **match the database exactly**, the email
must match, and the licence must not be expired. Editing `license.py` fails the
moment the app is online. When the database is unreachable, the app falls back to
the locally-recorded expiry as an offline grace period.

Activation uses the **Firestore REST API** via the standard library — no bundled
service-account secret (a distributed desktop app must never ship
`firebase-admin` credentials).

---

## Known limitations

- **Windows only** (winsound + Windows font files; printing uses `pywin32`).
- The local activation token is not strong DRM (see *Anti-tamper*).
- The full-page render buffer is large; very dense editing/playback can feel
  heavy on slower machines.
- At very slow tempos a long note can exceed its sample length, in which case
  the sample is tiled to fill.
