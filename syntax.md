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
| `>`      | Accent    | `eQ>`   |
| `.`      | Staccato  | `eQ.`   |
| `~`      | Fermata   | `eQ~`   |

Combine freely: `eQ->` is a dotted, accented E quarter.

### Rests

`r` + duration, e.g. `rQ` (quarter rest), `rq-` (dotted quaver rest).

### Ties

Put `^` between two notes of the **same pitch** to tie them:

```
eQ ^ eQ
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

| Symbol | Meaning              |
|--------|----------------------|
| `\|`   | Normal bar line      |
| `\|\|` | Part end             |
| `\|:`  | Repeat start         |
| `:\|`  | Repeat end           |

Write them with spaces around them: `gq aq | bq cq`

---

## 6. Staves and 1st / 2nd timings

- **A stave is one line.** Everything on a single line is one stave; start a new
  line to start a new stave. Put as many bars on a line as you like.
- **1st / 2nd timings:** wrap the notes/bars in `1[ … ]` (first time) or
  `2[ … ]` (second time). Bar lines are allowed inside.

```
|: aq bq | 1[ cq dq :| ] 2[ eq fq ||
```

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

## 10. Notes on compatibility

- **Loading:** the app reads both this text format and the older JSON `.pipe`
  files automatically.
- **Saving:** all new saves use this text format.
- The older key `tune.sime_sig` is still accepted on load as an alias for
  `tune.time_sig`, but `tune.time_sig` is the correct spelling and what the app
  writes.
