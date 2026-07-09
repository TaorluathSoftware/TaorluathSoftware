[CHANGELOG.md](https://github.com/user-attachments/files/29866882/CHANGELOG.md)
# Changelog

All notable changes to **Taorluath** are documented here. This project is in
**Pre-Alpha**. Versions follow `MAJOR.MINOR.PATCH` (see `src/version.txt`):
**MAJOR** = full revamp, **MINOR** = new features, **PATCH** = fixes & tweaks.

The format is based on [Keep a Changelog](https://keepachangelog.com/).

## [0.2.5] — 2026-07-09 — Pre-Alpha

### Changed
- **Sharper editor rendering.** The score now renders at full resolution on
  screen — crisp noteheads, gracenotes and beams — while keeping the thin, clean
  staff lines.
- **"Save to .pipe" now saves anywhere you choose.** Use it to keep a copy of a
  tune outside the app's library; **Save Changes** still commits to the tune's
  own file in your library.
- The app and installer are now **digitally signed**.

### Fixed
- The app now **reports its own version correctly**, so the update check no
  longer offers an update on every launch (the version file wasn't being bundled
  into the build).

## [0.2.4] — 2026-07-07 — Pre-Alpha

### Added
- **Delete saved scores from the dashboard** — select one and press Delete or
  Backspace (with confirmation).
- **Drag a selected note up/down** to change its pitch; a doubling in front
  follows the new pitch. Notes with a throw/heavy-throw are locked to D and
  birls to Low A.
- **Tie / Dot before placing** — with nothing selected, the Tie or Dot button
  arms the next note you place.
- **Tie Height** setting (Settings tab) — pixel height of tie arcs (flatter or
  more mountainous), saved per tune.
- **Click the top of an embellishment to select the whole embellishment**, then
  Delete removes it as a unit.
- **Ultra (1200 DPI)** print quality, plus **Default DPI** and **Default margin**
  settings that pre-fill the Print dialog.

### Changed
- **The placement ghost now pushes the real notes apart** as you hover (and is
  much faster), so you see exactly how the bar will look once placed.
- **Leaving the Notes/Embellishments tab clears its ghost**; clicking the Notes
  tab defaults to Quarter and Embellishments to a single Gracenote.
- **Editing a note deselects it** — dotting, tying, changing duration.
- **Embellishments corrected to the Piper's Dojo guide:** leumluath = `Low G, D`;
  taorluath = `Low G, D, E`; heavy D throw = `Low G, D, C`; double strikes use a
  thumb gracenote on High G and omit it on High A. Birls follow the requested
  `Low A, Low G, Low A, Low G` (or `Low G, Low A, Low G` from Low A).
- **Gracenotes redrawn:** 50% larger heads, three thin uniform beams on barred
  groups, a ledger line through High A gracenotes, and non-doubling gracenotes in
  a space nudged to sit just above the line.
- Bars start **right after the clef** on staves with no time signature; **bar
  lines are thicker/darker** so they print; dotted notes and notes never flood
  past the barline.
- **1st/2nd-time brackets** raised so they clear the gracenotes.
- **Settings dialog** is now two-column and wider.
- **Activation keys are now `TL-XXXX-XXXX-XXXX`** (digits only), replacing `PF-…`.
- **Purchasing is by request/email** instead of on-site checkout: choose a plan,
  request it, and we email the payment method — keys issued after payment.
  "Buy for 3" requests three licences.
- **Update check is release-based** — on launch it compares the newest GitHub
  release and offers the download; it never touches saved scores or licences.

### Fixed
- **Playback:** consecutive same-pitch notes now play as one continuous tone
  (no phantom articulation); audio plays from memory with a working Stop.
- **Print DPI now actually changes the output quality** (cosmetic since v0.2.3).
- The **App font size** setting now actually resizes the interface.
- **Loading screen** reliably appears on launch.
- Smaller, download-based **installer** (avoids the antivirus nested-exe flag) and
  fixed HTTPS certificate handling in the frozen build.

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

[0.2.5]: https://github.com/TaorluathSoftware/TaorluathSoftware/releases/tag/Pre-Alpha_v0.2.5
[0.2.4]: https://github.com/TaorluathSoftware/TaorluathSoftware/releases/tag/Pre-Alpha_v0.2.4
[0.2.3]: https://github.com/TaorluathSoftware/TaorluathSoftware/releases/tag/Pre-Alpha_v0.2.3
[0.2.2]: https://github.com/TaorluathSoftware/TaorluathSoftware/releases/tag/Pre-Alpha_v0.2.2
[0.2.1]: https://github.com/TaorluathSoftware/TaorluathSoftware/releases/tag/Pre-Alpha_v0.2.1
