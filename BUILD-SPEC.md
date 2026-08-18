# Maths Toolkit — Build Spec

Reference document for building new topic pages. Upload this to Project
Knowledge so any chat in this project can generate a page that matches
the rest of the site without needing to see the other pages first.

## Folder structure

```
/index.html                                    ← the menu (already built)
/assets/style.css                               ← shared design system (already built)
/unit-01/topic-01-priority-of-operations.html   ← already built
/unit-01/topic-02-....html                      ← not yet built
/unit-02/topic-01-....html
...
/unit-10/topic-06-....html
```

One folder per unit (`unit-01` through `unit-10`), one HTML file per
topic inside it. Nothing else lives at the root except `index.html`,
`assets/`, and this spec.

## Filenames

Format: `topic-NN-slug.html`, where `NN` is the topic's number within
its unit, zero-padded to two digits, and `slug` is the topic title
lowercased with punctuation stripped and spaces replaced by hyphens.
The topic's leading number (e.g. "3. ") is dropped from the slug.

Examples:
- Unit 4, "3. Multiplying fractions" → `unit-04/topic-03-multiplying-fractions.html`
- Unit 6, "3. Alternate angles" → `unit-06/topic-03-alternate-angles.html`
- Unit 1, "2. The symbol ≠" → `unit-01/topic-02-the-symbol-not-equal.html`

**The full manifest of all 134 filenames is in `manifest.json`** in
this same folder — generate the exact filename for any topic by
looking it up there rather than re-deriving it, to avoid drift.

## Every page must:

1. Link the shared stylesheet with a relative path back to the root:
   `<link rel="stylesheet" href="../assets/style.css">`
2. Load the same three Google Fonts (Barlow Condensed, Inter, JetBrains
   Mono) — see any existing page's `<head>` for the exact `<link>` tag.
3. Include a "← All topics" link back to the menu:
   `<a class="btn" href="../index.html">← All topics</a>`
4. Wrap all content in `<div class="wrap">...</div>` so the shared
   layout, background, and max-width apply.
5. Use only the shared tokens and components already defined in
   `assets/style.css` (colours, `.eyebrow`, `.tag`, `.btn`, `.card`,
   `section`, `.section-head`, footer) rather than redefining them
   inline. Anything page-specific (a stepper, a toggle demo, flip
   cards, a bespoke diagram) gets its own scoped CSS in a `<style>`
   block in that page only.
6. End with a `<footer>` matching the pattern:
   `<span>GCSE Maths Tools</span><span>Unit N · Topic N · [Title]</span>`

## Design tokens (do not redefine — these live in assets/style.css)

| Token | Value | Use |
|---|---|---|
| `--bg` | `#07070c` | page background |
| `--panel` | `#0f0f18` | card background |
| `--panel-2` | `#151522` | secondary panel (toggles, flip-card fronts) |
| `--magenta` | `#ff2ec8` | primary accent |
| `--violet` | `#9b5cff` | secondary accent |
| `--cyan` | `#2be8ff` | tertiary accent / "correct" / interactive state |
| `--text` | `#f4f4fb` | primary text |
| `--muted` | `#9998ad` | secondary text |
| `--muted-2` | `#6d6c82` | tertiary / disabled text |
| `--radius` | `18px` | standard card corner radius |
| `--grad` | magenta → violet → cyan | headline text, primary buttons |

Fonts: **Barlow Condensed** italic bold for all headings, **Inter**
for body text, **JetBrains Mono** for numbers, labels, tags, and code.

## Content mapping (spreadsheet column → page section)

Using the corrected spreadsheet
(`Units_Pearson_Key_Points_FULL_Detailed_updated.xlsx`):

| Spreadsheet column | Page section |
|---|---|
| Learning question | Hero subheading (the big question) |
| So what are pupils actually learning? (now bespoke, 3 lines) | "Where students get stuck" — one bubble/card per line |
| Key point | "The rule" — core statement panel |
| Detailed knowledge students need | Explanation card |
| What students need to understand | "Why it matters" card |
| Typical examples | Worked example section — adapt to a stepper, a toggle, or a plain example depending on what the topic needs |
| Common misconceptions to address | Misconception flip-cards — split on semicolons/commas into 2–3 cards |

**MWB Link and MW Clip are out of scope** — not used anywhere in the
build. Ignore both columns.

## Interaction library

Don't invent a new interactive component per topic. Pick from this
set, matching what the topic's own misconceptions actually call for:

- **Worked-example stepper** — click-through Next/Back reveal of a
  calculation, one operation highlighted per step. Good for anything
  procedural (solving, simplifying, converting).
- **Before/after toggle** — a switch that changes one detail (e.g.
  adding brackets, changing a sign) and shows the answer change live.
  Good when the misconception is "students don't realise X changes
  the result."
- **Flip-card misconceptions** — tap to reveal the fix. Used on every
  page regardless of topic.
- **Plain example card** — no interactivity, just a clearly laid-out
  worked example. Fine for topics where a stepper or toggle wouldn't
  add real value — not every topic needs a bespoke interaction.

## What NOT to do

- Don't rename or restructure `index.html` or `assets/style.css` from
  a topic-page-building chat — those are the menu's responsibility.
  If a shared token needs to change, that's a deliberate edit to
  `assets/style.css` alone, done once, not per-page.
- Don't add MWB/MW Clip content back in.
- Don't hardcode colours — always reference the CSS variables.
