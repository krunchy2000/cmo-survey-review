# CMO Survey — Copy Review Tool
**Sparks × Adweek** · Internal production tool  
**Last updated:** 2026-04-15 · **Version:** v4

A self-contained HTML copy review tool that bridges Design (Figma HD), Producers, and Dev for the CMO Survey experience. Open `index.html` in any browser — no server, no install, no dependencies.

---

## Quick start

1. Clone or download this repo
2. Open `index.html` in a browser
3. Frame preview images load automatically from the PNGs in the same folder
4. Make reviews, then hit **⬇ Save file** to export a versioned copy with all state baked in

> To pass to the next reviewer, share the exported `.html` — all approvals, notes, and audit history travel with the file.

---

## File structure

```
/
  index.html      ← the review tool
  01.png          ← Figma HD frame exports
  02.png
  03.png
  04.png
  05.png
  06.png
  07.png
  08.1.png
  08.2.png
  08.3.png
  08.4.png
  08.5.png
  09.png
  README.md
```

PNG filenames match Figma frame numbers exactly. Export them directly from the Figma HD page.

---

## What's in the tool

### Topbar
| Control | What it does |
|---|---|
| ↗ Figma HD | Opens the source Figma file |
| Collapse all / Expand all | Toggle all sections |
| Dev mode | Toggle switch — reveals Component, Layer, Template columns |
| A− / 100% / A+ | Text scale control (default 14px) |
| Export JSON | Downloads `cmo-survey.json` in the format dev requires |
| ⬇ Save file | Exports versioned HTML with all state baked in |

**Audit strip** (dark row below the controls) — always visible. Shows reviewer name, live feed of last 4 actions, and a **History ▾** button for the full log.

### Per section
- Click the frame preview to enlarge in a lightbox
- Drag the ⠿ handle on the section header to reorder sections
- ▾ toggle on the right to collapse / expand

### Per row
- **Click any copy** to edit inline — original copy is preserved and shown as `was: [original]` in Notes
- **Yes / No** — approve or flag. Reset × clears the selection.
- **Drag** the ⠿ row handle to reorder within a section — moved rows show a `↕ Reordered (was #N)` badge
- **Notes / Comments** — free-text field. When a note is present, `○ Mark actioned` appears below it. Click to mark as `✓ Actioned`.
- **⚠ Flag pills** — pre-flagged rows show an amber pill. Dismiss with × to clear.

---

## Sections

| Frame | Screen | Type |
|---|---|---|
| 01 | Splash | Single row |
| 02 | Intro | Headline, body, CTA |
| 03 | Q1 — Radio | 9 options |
| 04 | Q2 — Pills | 4 options |
| 05 | Q3 — Checkbox | 8 options, select up to 3 |
| 06 | Q4 — Radio | 9 options |
| 07 | Q5 — Pills | 5 options (persona question) |
| 08.1 | Persona – Storyteller | Result screen |
| 08.2 | Persona – Challenger | Result screen |
| 08.3 | Persona – Connector | Result screen |
| 08.4 | Persona – Experimenter | Result screen |
| 08.5 | Persona – Coach | Result screen |
| 09 | Outro | Thank you screen |

---

## JSON export

**Export JSON** produces `cmo-survey.json` ready for dev. Copy edits made in the tool flow through automatically.

### Structure
```json
{
  "offlineSync": true,
  "cookie": "cmo-survey",
  "display": "cmo",
  "personaQuestion": 4,
  "submitLabel": "See your trait",
  "questions": [ ... ],
  "personas": [ ... ]
}
```

### Persona export order
`storyteller → challenger → connector → experimenter → coach`

### What's hardcoded vs editable
| Field | Source |
|---|---|
| `offlineSync`, `cookie`, `display`, `personaQuestion` | Hardcoded config |
| `submitLabel` | Hardcoded — `"See your trait"` |
| `accentColor`, `image`, `imageScale`, `imagePosition` | Hardcoded per persona |
| `layout: "pills"` on Q2 and Q5 | Hardcoded |
| `personaMap` on Q5 | Hardcoded |
| All question text, options, persona names, descriptions | Live from copy in tool |

### Quote conventions
- Smart quotes (`'` `"` `"`) are used throughout — intentional, correct for display
- `personaMap` keys and Q5 option strings both use smart apostrophes — matching is consistent, no lookup failures
- `Self-education` and `On-the-job experience` use standard hyphens per dev spec

---

## Dev columns

Hidden by default. Toggle on with the **Dev mode** switch to reveal:

| Column | Example |
|---|---|
| Component | `btn_radio [1]` |
| Layer | `txt_response` |
| Template | `WF-C` |

---

## Open items

- [ ] Confirm `"See your trait"` in frame 07 `btn_select [1]` — likely placeholder, needs producer sign-off
- [ ] Confirm `btn_primary` copy placement in frame 07
- [ ] Confirm `"Continues self improvement"` typo in frame 05 `btn_radio [8]` — likely `"Continued self-improvement"`
- [ ] **Confirm with dev: is the `mantra` field in the JSON actively used in the build?** If not, remove from spec and export
- [ ] SVG swap for ⠿ drag handle and ▾ chevron (currently Unicode dingbats) — coordinate in Figma + HTML together

---

## Figma files

| File | ID | Purpose |
|---|---|---|
| Figma HD (source of truth) | `hS98TLAaV2OMpheRFaH18Z` | Production design |
| Copy Review UI | `69gZLZqKha69MqeXQGDL9u` | Design spec for this tool |

The Copy Review UI file contains three frames: **Topbar** (`1:2`), **Section Block** (`9:2`), and **Component Library** (`2:2`).

To apply design changes: share the updated Figma URL or node IDs with Claude — it will read the updated properties and apply them back to the HTML.

---

## Continuing development with Claude

Share `README.md` and `index.html` together in a new Claude session. Claude can read the current state of both files and pick up exactly where things left off — no context needed from the previous session.
