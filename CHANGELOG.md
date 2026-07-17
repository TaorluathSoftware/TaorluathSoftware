[CHANGELOG.md](https://github.com/user-attachments/files/30135150/CHANGELOG.md)
# Changelog

All notable changes to **Taorluath** are documented here. This project is in
**Pre-Alpha**. Versions follow `MAJOR.MINOR.PATCH` (see `src/version.txt`):
**MAJOR** = full revamp, **MINOR** = new features, **PATCH** = fixes & tweaks.

The format is based on [Keep a Changelog](https://keepachangelog.com/).

## [0.2.5] — 2026-07-10 — Pre-Alpha
*Last updated 2026-07-17.*

### Added
- **Five new embellishments** on the Embellishments tab: **Gracenote Strike**
  (`High G, D, C`), **Heavy Gracenote-Strike** (`High G, Low G, C`),
  **High G-D Strike** (`High G, D, Low G`), **Dre** (`E, Low A, F, Low A`) and
  **Hornpipe Shake** (`High G, D, E, D, B`).
- **Melody-aware ornaments.** A **Taorluath** played after a **D** sounds
  `Low G, B, Low G, E`, and after a **Low G** it sounds `D, Low A, E`. A
  **doubling** or **G birl** played after a **High G** shifts its leading High G
  gracenote up to **High A**, and after a **High A** drops it entirely (**High G**
  and **High A** doublings are left unchanged).
- **Text tab.** Add free text anywhere on the page — click **Add Text Box**, then
  click where you want it. Click an existing box to edit it (clear the text to
  delete it).
- **Stylable page number and text boxes.** Set the font, size and weight
  (bold/italic) of the page number (Settings → **Page Number**, or double-click
  it) and of each custom text box.
- **Stylable 2nd-time numbers.** Double-click a 1st/2nd-time number to set its
  font, size and weight, and choose whether the bracket sits **above or below**
  the stave.
- **Duplicate a saved score** — select it on the dashboard and press **D** to
  make a copy titled "Copy of <name>".
- **Print Preview** — File → **Print Preview** (or `Ctrl+Shift+P`) shows the
  composed page as it will be printed, with a **Print…** button to go straight to
  the print dialog.
- **Harmonies tab.** **Add Harmony Part** appends a harmony part as its own
  stave under the tune (labelled "Harmony", matching the melody's bars and time
  signature); write its notes with the Notes tab, and **Delete Harmony Part**
  removes it. Harmony staves are for reading/printing and are not included in
  playback.
- **Tune tab — multiple tunes per document.** **Add Tune** appends a blank,
  untitled 4-stave tune to the end (also available on the **Stave** tab) and
  **Delete Selected Tune** removes the selected tune and its staves. Click a
  stave to select its tune; double-click a tune's title to rename it. Every
  tune's header sits **1 cm from the top** of its section with a fixed **100 px**
  gap down to its first stave; the **tune type sits on the left** with the title
  centred and composer on the right; and each later tune **prints its own time
  signature** (even if it matches the tune above).

### Changed
- **Note & embellishment buttons show a picture, not a name.** The Notes and
  Embellishments tabs now render each note/embellishment on a small bare five-line
  stave instead of a text label. Embellishments are drawn on their own (no melody
  note), referenced to G.
- **Smaller note & embellishment buttons.** The picture buttons on the Notes and
  Embellishments tabs are smaller, so more fit without crowding the ribbon.
- **Sharps removed.** The `F♯`/`C♯` key signature is no longer drawn — those
  sharps are implied by the highland scale and were not otherwise used.
- **Redrawn gracenotes.** A cleaner single-gracenote glyph (new
  `Assets/notes/gracenote.png`), and the barred embellishment heads are now
  **angled noteheads** that match the melody notes, instead of flat ovals.
- **Dashboard scores are sorted alphabetically** by tune name, ignoring leading
  articles (The/A/An/And) and any numbers (so "The 2nd Battalion" files under B).
- **Smaller embellishment heads.** Gracenote/embellishment noteheads are now 25%
  smaller.
- **Page number only when it's needed.** The page number is shown only when the
  tunes span **more than one page**; single-page tunes have no number.
- **Automatic updates.** Choosing **Yes** on the update prompt now downloads and
  installs the new version and reopens the app for you — no more manual download.
- **Font sizes are now set in points** (not pixels), so text prints at a true
  typographic size. Existing tunes are converted automatically.
- **Lighter placement ghost.** The hover preview now **snaps** to where the note
  or embellishment will land instead of pushing the other notes apart on every
  move — this removes the constant page redraw and its heavy memory use.
- **Sharper editor rendering.** The score now renders at full resolution on
  screen — crisp noteheads, gracenotes and beams — while keeping the thin, clean
  staff lines.
- **"Save to .pipe" now saves anywhere you choose.** Use it to keep a copy of a
  tune outside the app's library; **Save Changes** still commits to the tune's
  own file in your library.
- The app and installer are now **digitally signed**.

### Fixed
- **Lone gracenotes are sized correctly** — big enough to read clearly on paper
  (they were nearly invisible before) but not so large they compete with the
  melody notes; about three-quarters the height of a full note. Barred
  embellishment heads are unchanged.
- **Embellishment / doubling heads fixed.** The barred gracenote heads were
  rendering as tiny dashes at the reduced size; they now draw as clean filled
  noteheads, sized correctly and sitting at each pitch, with the stem at the
  head's right edge (connected at any zoom).
- **Tie Height now actually changes the tie arc.** A width-based cap was
  overriding the setting for all but very wide ties, so it looked like it did
  nothing; the setting now drives the height (clamped only so a tie never
  balloons taller than its own width).
- **"Play from Selected Bar" now honours repeat barlines** — it previously
  ignored them and played straight through; it now expands repeats just like
  "Play Entire Score".
- **Page number no longer clipped when printing** — moved up from the very
  bottom edge so print margins don't cut it off.
- **Everything now prints in pure black.** Notes, staff lines, beams, clefs, time
  signatures, ties and all text were a very dark grey; they are now true black,
  which also makes prints look much sharper.
- **Print quality now genuinely scales with the DPI setting.** The higher-DPI
  page was being discarded during the final resize onto the printer (the printer
  device context defaulted to nearest-neighbour scaling); the page is now drawn
  with high-quality (HALFTONE) interpolation, so 1200 DPI is visibly sharper than
  150. (The v0.2.4 note claimed this was fixed, but the resize step still threw
  the extra resolution away — this is the real fix.)
- **Corrected the D, F and B doublings:** D is now `High G, D, E`, F is now
  `High G, F, High G` and B is now `High G, B, C`.
- **Corrected the Leamluath (grip)** to `Low G, D, Low G`.
- **Corrected the Taorluath and Crunluath.** Taorluath is now
  `Low G, D, Low G, E` and Crunluath is now
  `Low G, D, Low G, E, Low A, F, Low A`.
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
