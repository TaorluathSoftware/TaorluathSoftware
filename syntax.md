# The `.pipe` file syntax

Taorluath saves tunes as human-readable `.pipe` text files. This is the format
you'll see in the built-in **Live `.pipe` Editor** (press **Ctrl + Shift + Tab**),
and it's what every saved file now uses. Older JSON `.pipe` files still open
automatically — the app detects the format on load.

This document is the full reference for writing tunes by hand.

---

## 1. Document structure

A file is one or more **tune blocks**:

```
tune:1[
  <header lines>

  <music, one stave per line>
]
tune:2[
  ...
]
```

- Number the blocks `tune:1`, `tune:2`, … in order down the page.
- Everything for a tune goes between its `[` and `]`.
- The blank line between the header and the music is optional but tidy.

---

## 2. Header lines

Each header line is `tune.<key>: <value>`. All are optional.

| Key                | Meaning                                   | Example                              |
|--------------------|-------------------------------------------|--------------------------------------|
| `tune.name`        | Tune title                                | `tune.name: "Scale"`                 |
| `tune.comp`        | Composer                                  | `tune.comp: "Constantine Ferreira"`  |
| `tune.type`        | Tune type                                 | `tune.type: "Exercise"`              |
| `tune.bpm`         | Tempo in beats per minute                 | `tune.bpm: 85`                       |
| `tune.time_sig`    | Time signature (use `_` for the slash)    | `tune.time_sig: 4_4`                 |
| `tune.name.style`  | Title font style (see below)              | `tune.name.style: b,i,"Times New Roman",14` |
| `tune.comp.style`  | Composer font style                       | `tune.comp.style: i,"Arial",9`       |
| `tune.type.style`  | Tune-type font style                      | `tune.type.style: i,"Arial",9`       |

### Style format

`[b],[i],"Font Name",size`

- `b` = bold, `i` = italic (include only if you want them)
- `"Font Name"` = any font installed on your system
- `size` = point size

```
tune.name.style: b,i,"Times New Roman",14
```

### Document-wide settings (put these in `tune:1`)

These apply to the whole file and are written once, in the first tune's header:

| Key                 | Meaning                                    | Example                       |
|---------------------|--------------------------------------------|-------------------------------|
| `tune.mode`         | `pipe` (default) or `drum`                 | `tune.mode: drum`             |
| `tune.drum`         | Drum voice (drum mode): Snare/Tenor/Bass   | `tune.drum: Snare`            |
| `tune.font`         | Default score font                         | `tune.font: "Sans Serif"`     |
| `tune.gap.staves`   | Vertical gap between staves (px)           | `tune.gap.staves: 85`         |
| `tune.gap.grace`    | Gap after gracenotes (px)                  | `tune.gap.grace: 14`          |
| `tune.gap.tunes`    | Gap between tunes (px)                      | `tune.gap.tunes: 40`          |
| `tune.tie.height`   | Tie arc height (px)                        | `tune.tie.height: 12`         |
| `tune.tempo_mark`   | Print a `♩ = bpm` marking: `on` / `off`    | `tune.tempo_mark: on`         |
| `tune.explorer`     | Custom name in the app's tune explorer     | `tune.explorer: "My Set"`     |
| `tune.page.style`   | Page-number font style                     | `tune.page.style: "Arial",6`  |
| `tune.timing.style` | 1st/2nd-time number font style             | `tune.timing.style: "Arial",5`|
| `tune.text`         | A free text box (repeatable, see §7)       | `tune.text: "D.C.", 900, 400, 8, "Arial", b` |

> **Per-tune vs app-wide.** The keys above are saved *inside the tune file*
> because they belong to the score (its fonts, gaps, tie height, tempo marking).
> The **Customise** tab's appearance and rendering choices — theme, accent
> colour, Compact UI, which tabs/buttons are shown, the beam **tail length /
> join depth / join gap**, and the **stave line thickness** — are **app-wide**
> and live in `%APPDATA%\Taorluath\settings.py`, *not* in the `.pipe` file. The
> same tune therefore renders with whatever Customise settings the current
> machine has.

---

## 3. Notes

A note is **pitch + duration**, written with no space between them.

### Pitches (lowercase = low octave, capital G/A = high octave)

| Note   | Letter |     | Note    | Letter |
|--------|--------|-----|---------|--------|
| Low G  | `g`    |     | E       | `e`    |
| Low A  | `a`    |     | F       | `f`    |
| B      | `b`    |     | High G  | `G`    |
| C      | `c`    |     | High A  | `A`    |
| D      | `d`    |     |         |        |

### Durations

| Value               | Letter |
|---------------------|--------|
| Whole               | `w`    |
| Half                | `H`    |
| Quarter             | `Q`    |
| Quaver (eighth)     | `q`    |
| Semiquaver          | `s`    |
| Demisemiquaver      | `d`    |
| Hemidemisemiquaver  | `h`    |

> Note the case split: **`Q`** = quarter, **`q`** = quaver; **`H`** = half,
> **`h`** = hemidemisemiquaver. The pitch is always the *first* letter, so
> `dd` = a **D** demisemiquaver and `dQ` = a **D** quarter.

**Examples:** `eq` = E quaver, `GQ` = High G quarter, `aw` = Low A whole note.

Separate every note with a space: `gq aq bq cq`

### Note modifiers (add after the duration)

| Modifier | Meaning   | Example |
|----------|-----------|---------|
| `-`      | Dotted    | `eQ-`   |
| `~`      | Fermata (held note) | `eQ~` |

Combine freely: `eQ-~` is a dotted E quarter held under a fermata. (Accent and
staccato aren't supported — neither can be played on Highland pipes.)

### Triplets

Wrap the notes of a triplet in `3( … )` — up to **three** notes played in the
time of two. The bracket (a tie arc with a **3** above it) is drawn above the
stave over the group:

```
3(gq aq bq)
```

### Rests

`r` + duration, e.g. `rQ` (quarter rest), `rq-` (dotted quaver rest).

### Ties

Attach `^` between two notes of the **same pitch** to tie them — **no spaces**:

```
eQ^eQ
```

---

## 4. Gracenotes and embellishments

`g:` followed by one or more pitch letters. The gracenotes attach to the **next**
note.

- Single gracenote: `g:A cq` → a High-A gracenote on a C quaver.
- Embellishment (several gracenotes): `g:gdc dq` → a D Throw (`Low G, D, C`)
  on a D quaver.

---

## 5. Bar lines

| Symbol | Meaning                    |
|--------|----------------------------|
| `\|`   | Normal bar line            |
| `\|-`  | Part **start** (double bar) |
| `-\|`  | Part **end** (double bar)   |
| `\|:`  | Repeat start               |
| `:\|`  | Repeat end                 |

Write them with spaces around them: `gq aq | bq cq -| dq eq`

> The double barline is written as **`|-`** (start of a part) and **`-|`** (end of
> a part) — two distinct tokens so they never get confused with the repeat marks
> `|:` / `:|`. Older files that used `||` for a part end still load correctly.

### Bar-line positions (pixel widths)

Each bar line is written with its **position in pixels from the previous bar
line** as a prefix — the first bar line is always `0`:

```
0| gq aq bq cq 368| dq eq fq Gq 400:|
```

Here `0|` is the opening, `368|` is a normal bar line 368 px after it (so bar 1
is 368 px wide), and `400:|` is a repeat end 400 px further on. The app fills
these in automatically (auto-fit sizes each bar to its contents, and dragging a
bar line updates its number); once a stave has explicit widths they're kept
(auto-fit leaves it alone) until you add or remove a bar.

---

## 6. Staves and 1st / 2nd timings

- **A stave is one line.** Everything on a single line is one stave; start a new
  line to start a new stave. Put as many bars on a line as you like.
- **1st / 2nd timings:** wrap the notes/bars in `1[ … ]` (first time) or
  `2[ … ]` (second time). Bar lines are allowed inside, and a timing may begin
  or end **in the middle of a bar** — the bracket is drawn over exactly the run
  of notes you wrap.

```
|: aq bq | 1[ cq dq :| ] 2[ eq fq ||
aq bq 1[ cq dq ] 2[ eq ] fq
```

### Harmony staves

Prefix a stave line with `H<n>:` to make it **Harmony n** — drawn in a titled
"Harmony n:" box below the tune, and played **in sync with the tune at the same
volume**. Add as many as you like (each number is its own box):

```
gq aq bq cq | dq eq fq Gq
H1: Gq Gq Gq Gq | aq aq aq aq
H2: eq eq eq eq | fq fq fq fq
```

### Pages

The score flows onto new pages automatically when a stave would run off the
bottom, and pages are numbered. To force a **manual page break** (start a new
page at a stave), put `page.break` on its own line before that stave:

```
gq aq bq cq | dq eq fq Gq
page.break
Gq fq eq dq | cq bq aq gq
```

To **pin a stave to a specific page**, put `p<N>` at the **end** of the stave
line (`p1`, `p2`, `p3`, …):

```
0| gq aq bq cq 368| dq eq fq Gq p1
0| Gq fq eq dq 368| cq bq aq gq p2
```

The second stave is placed on page 2. A stave with no `pN` flows onto a page
normally (after the previous stave, or the next page if it would overflow).

---

## 7. Text boxes

`tune.text: "content", x, y, size, "font", [b], [i]`

- `x`, `y` = position on the page (page pixels)
- `size` = point size, `"font"` = any installed font, `b`/`i` = bold/italic

```
tune.text: "3 times through", 900, 380, 8, "Arial", i
```

---

## 8. Drum mode

Set `tune.mode: drum` and a `tune.drum` voice. Drum notes use:

| Token     | Meaning                       |
|-----------|-------------------------------|
| `x<dur>`  | Beat above the line           |
| `X<dur>`  | Beat below the line           |
| `*`       | Rimshot (append: `xq*`)       |
| `r<dur>`  | Rest                          |

```
tune:1[
tune.name: "Roll"
tune.bpm: 90
tune.time_sig: 2_4
tune.mode: drum
tune.drum: Snare

xq xq* Xq rq
]
```

---

## 9. Full example

```
tune:1[
tune.name: "Scale"
tune.comp: "Constantine Ferreira"
tune.type: "Exercise"
tune.name.style: b,i,"Times New Roman",14
tune.comp.style: i,"Times New Roman",9
tune.type.style: i,"Times New Roman",9
tune.bpm: 85
tune.time_sig: 4_4

|: gq aq bq cq dq | eq fq Gq Aq :|
]
```

---

## 10. Comments

Anything after `--com:` on a line is a comment and is ignored when the file is
read (it can be a whole line or trail after music):

```
--com: this whole line is a note to yourself
|: gq aq bq cq :|   --com: the opening phrase
```

## 11. Notes on compatibility

- **Loading:** the app reads both this text format and the older JSON `.pipe`
  files automatically.
- **Saving:** all new saves use this text format.
- The older key `tune.sime_sig` is still accepted on load as an alias for
  `tune.time_sig`, but `tune.time_sig` is the correct spelling and what the app
  writes.
