# CLAUDE.md

Guidance for Claude Code when working in this repository.

## Overview

Static website for **Deploying Foundation Models on the Rubin Alert Stream: A SkAI × LINCC
Frameworks Hack-Week** (December 7–9, 2026, SkAI Institute, 172 E. Chestnut St., John Hancock Center, Chicago IL).
Funded by the LSST Discovery Alliance through the LINCC Frameworks Community Events program
(awarded 2026-07-18). PI Gautham Narayan (UIUC), Co-PI Adam Miller (Northwestern); Adam runs the event on site with SkAI operations (Elise Ahn); Aritra Ghosh and Neven Caplar (LINCC) join by Zoom. Pure HTML/CSS, no build step. Cloned from `~/work/rubinalerts26.github.io/`.

Source of truth for scope, SOC, program and budget: the funded proposal at
`~/Dropbox/work/Proposals/2026A/LSST_DA_DP2_Hyrax_Workshop/proposal/submitted_20260710/`.
The proposal was written for Nov 16–20 at DPI. It moved to Nov 4–6 at SkAI (Slack, Sept 2026), then on
2026-09-29 to Dec 7–9 at CIERA (Adam's colloquium-room reservation), and on 2026-09-30 back to the SkAI
Institute on the same dates after Elise Ahn confirmed the SkAI floor is available (per GN). The Day-3
long-lunch constraint was CIERA-specific and is gone. The site follows the latest decision.

## Structure

- `index.html` — hero, purpose, six goals, important dates
- `program.html` — at-a-glance cards + three daily schedule tables (draft) + program notes
- `participants.html` — application box, SOC cards, LINCC partner cards, empty participant grid
- `travel.html` — SkAI venue + map + photo, getting to Chicago, lodging stub, about Chicago
- `css/styles.css` — single stylesheet; winter palette: steel blue `#3b82c4`, ice blue `#8fd3f4`, silver `#dbe7f3` on deep navy `#111a2e`
- `assets/images/` — sponsor logos, `rubin-snow.jpg` (hero; 1600×1066 frame `pasted-movie-5690.png` from GN's Keynote `Presentations/GenSci/Narayan_AoT_Pygmalion_Sep2026.key`: Rubin under construction in snow, blue sky. Credit on the page reads "Rubin Observatory/NOIRLab" `[INFERRED — verify: GN to confirm the source video/photo and exact credit; not found in the NOIRLab or rubinobservatory.org galleries on 2026-09-29]`), `skai.jpg` (purpose section and travel venue card; Hancock Center exterior, credit "Barry Butler Photography", copied from rubinalerts26 where it carried the same credit). Credits are printed on the page; keep them if the images stay. `northwestern-winter.jpg` was removed with the venue change.

The nav, footer, and inline script are copied by hand into each page. A change to any of them
goes into all four files.

## Placeholders still to fill

| Item | Where | Status |
|---|---|---|
| Application form URL | `participants.html` registration box | disabled button, `href="#"` |
| Applications open date | `index.html` Important Dates | badge reads `Date TBA`; deadline is set (Fri Dec 4, 2026, the Friday before the meeting, per GN 2026-09-29) |
| Hotel block | `travel.html` Lodging | "coming soon" box (Magnificent Mile, near SkAI); replace with the hotel card pattern from rubinalerts26 `travel.html` |
| Daily program | `program.html` | 3-day compression of the proposal's 5-day agenda; unconfirmed with Adam / Ayan; labelled "Draft" on the page |
| Speakers | `program.html` Day 1 primer | `TBD` |

Each placeholder is marked with an HTML comment starting `PLACEHOLDER:`; `grep -n PLACEHOLDER *.html` lists them.

## Deployment

GitHub Pages from `main` at https://rubinfm26.github.io/ (live since 2026-09-29). Repo `rubinfm26/rubinfm26.github.io`; gnarayan pushes as a collaborator. Push to main to deploy.

Jekyll runs passively (no Liquid or front matter). `_config.yml` only excludes non-web files
(`CLAUDE.md`, `README.md`, `_admin/`, `*.py`) from the built site. Do not add `.nojekyll`.

Preview locally:
```
python3 -m http.server 8000
```

## Common Content Updates

**Add a participant** (`participants.html`):
```html
<div class="participant-card">
    <div class="participant-avatar">AB</div>
    <h4>Full Name</h4>
    <p class="participant-affiliation">Institution</p>
</div>
```
Keep sorted by last name (A → Z).

**Add a schedule row** (`program.html`):
```html
<tr>
    <td class="schedule-time">09:00 - 10:00</td>
    <td>Session Title</td>
    <td class="schedule-speaker">Speaker Name</td>
</tr>
```
Use `class="schedule-break"` on `<tr>` for breaks, with `colspan="2"` on the content cell.

**Add an important date** (`index.html`):
```html
<div class="date-item">
    <div class="date-badge">
        <span class="month">Nov</span>
        <span class="day">4</span>
    </div>
    <div class="date-content">
        <h4>Event Title</h4>
        <p>Description.</p>
    </div>
</div>
```

**Event photos** (after the event): resize with ImageMagick and add a carousel; the pattern
(`.photo-carousel` CSS is already in `styles.css`, JS in rubinalerts26 `participants.html`).
```bash
magick input.jpg -resize '1920x>' -quality 82 -strip -interlace Plane \
    -sampling-factor 4:2:0 assets/images/photos/output.jpg
```

## Design Constraints

- No white backgrounds outside the footer logo strip; every section uses the navy/ice-blue tints
- Colors are CSS custom properties under `:root`; use `var(--...)`, never hardcoded hex
- Navigation links use class `jiggle-link`
- Hero background is the local `rubin-snow.jpg` (set in `.hero` in `styles.css`); the `--color-purple*` variable names are legacy and hold the steel-blue/ice-blue values
- Never call the event a "flagship"; "hack-week" is the funded event type
- Vocabulary: no leverage / robust / transformative / harness / notably / importantly

## Reviews

`_admin/` is gitignored and excluded from the built site. `_admin/review_2026-09-29.md` holds the
first-draft register review (vs Boom! 2022, rubinalerts26, the proposal) and the clarity/fidelity
review (vs the proposal, DESC/TVSSC grad-student persona). `_admin/register_negatives.md` is the
workshop-website register cache: read it before drafting any new copy for this site.

Contact email throughout: `rubinfm26@lists.skai-institute.org` (SkAI list, created 2026-09-29).
