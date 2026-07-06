[CHANGELOG.md](https://github.com/user-attachments/files/29719923/CHANGELOG.md)
# Changelog

All notable changes to **Taorluath** are documented here. This project is in
**Pre-Alpha**. Versions follow `MAJOR.MINOR.PATCH` (see `src/version.txt`):
**MAJOR** = full revamp, **MINOR** = new features, **PATCH** = fixes & tweaks.

The format is based on [Keep a Changelog](https://keepachangelog.com/).

## [0.2.3] — 2026-07-06 — Pre-Alpha

### Added
- **Print settings menu.** Printing now opens a dialog to choose the printer,
  paper size (Letter, A4, Legal, A3, Tabloid, A5), orientation, quality (DPI),
  and page margin before printing. The page is still squeezed to fit inside the
  margins and never cropped.
- **Autosave on close.** Closing the app (the window X, File → Exit, Ctrl+F12, or
  returning to the menu) now saves your current score first, so work is never
  lost on exit.

### Changed
- **Playback no longer highlights notes.** The moving highlight could drift out
  of sync with the sound, so it has been removed; playback is now audio only.

### Fixed
- **Playback audio delay.** Tunes now play from memory instead of a temporary
  file, removing a long start delay caused by Windows/antivirus opening and
  scanning the file before sound began.
- **Loading screen now reliably appears** on launch. It was flashing past too
  quickly on fast startups; it now stays on screen long enough to be seen.

## [0.2.2] — 2026-07-06 — Pre-Alpha

### Added
- **Loading / splash screen** on startup — the app logo on a white background
  with a percentage progress bar, so launching the app gives immediate feedback.

### Changed
- **Smaller installer.** The installer now downloads Taorluath during
  installation instead of bundling it, shrinking the download from ~55 MB to
  ~11 MB and avoiding antivirus false positives from a nested executable.
- **Update handling for the installed app.** When a new version is available the
  packaged app now opens the Releases page to download the latest installer.

## [0.2.1] — 2026-07-06 — Pre-Alpha

### Added
- **First public Pre-Alpha release.**
- **Notation editor** for the Great Highland Bagpipe and practice chanter:
  beat-based beaming, gracenotes and embellishments (doublings, throws, birls,
  strikes, leamluath, taorluath), ties, dots, per-bar start/end styles, and
  multiple staves with per-stave time signatures.
- **Pipe-band drum scores** — snare, tenor and bass in Berger uniline notation,
  with rimshots, rests, and one-hit-per-note playback (`.drum`).
- **Gapless playback** with real instrument samples; the playing note and its
  gracenotes are highlighted.
- **Files & output** — save/open `.pipe` and `.drum`, import/export `.bww`,
  export PDF, and print from the app.
- **Light and dark themes**, configurable app font and accent colour.
- **Licensing** — Firebase-verified activation keys.

[0.2.3]: https://github.com/TaorluathSoftware/TaorluathSoftware/releases/tag/Pre-Alpha_v0.2.3
[0.2.2]: https://github.com/TaorluathSoftware/TaorluathSoftware/releases/tag/Pre-Alpha_v0.2.2
[0.2.1]: https://github.com/TaorluathSoftware/TaorluathSoftware/releases/tag/Pre-Alpha_v0.2.1
