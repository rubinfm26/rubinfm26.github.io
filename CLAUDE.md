# CLAUDE.md

Guidance for Claude Code when working in this repository.

## Overview

Static website for **Deploying Foundation Models on the Rubin Alert Stream: A SkAI × LINCC
Frameworks Hack-Week** (November 4–6, 2026, SkAI Institute, 172 E. Chestnut St., Chicago IL).
Funded by the LSST Discovery Alliance through the LINCC Frameworks Community Events program
(awarded 2026-07-18). PI Gautham Narayan (UIUC), Co-PI Adam Miller (Northwestern); Adam runs
the event on site. Pure HTML/CSS, no build step. Cloned from `~/work/rubinalerts26.github.io/`.

Source of truth for scope, SOC, program and budget: the funded proposal at
`~/Dropbox/work/Proposals/2026A/LSST_DA_DP2_Hyrax_Workshop/proposal/submitted_20260710/`.
The proposal was written for Nov 16–20 at DPI; the move to Nov 4–6 at SkAI was settled in
Slack with Elise Ahn and Adam Miller (Sept 2026). The site follows the Slack decision.

## Structure

- `index.html` — hero, purpose, six goals, important dates
- `program.html` — at-a-glance cards + three daily schedule tables (draft) + program notes
- `participants.html` — application box, SOC cards, LINCC partner cards, empty participant grid
- `travel.html` — SkAI venue + map, getting to Chicago, lodging stub, about Chicago
- `css/styles.css` — single stylesheet; fall palette: burnt orange `#b5451b`, amber `#e8912d`, goldenrod `#f3c26b` on espresso `#2a1c16`
- `assets/images/` — sponsor logos, `skai.jpg` (venue, Barry Butler Photography), `rubin-sunset.jpg` (hero; NOIRLab `noirlab2417b`, O. Bonin/SLAC, CC BY 4.0), `hancock-autumn.jpg` (purpose section; the Hancock Center from Lincoln Park, Wikimedia Commons "John_Hancock1.JPG", Ronincmc, CC BY-SA 3.0). Credits are printed on the page; keep them if the images stay.

The nav, footer, and inline script are copied by hand into each page. A change to any of them
goes into all four files.

## Placeholders still to fill

| Item | Where | Status |
|---|---|---|
| Contact email | footer of every page, `participants.html`, `travel.html` | `gsn@illinois.edu` (PI, from the proposal); swap for an event list when one exists |
| Application form URL | `participants.html` registration box | disabled button, `href="#"` |
| Applications open / deadline dates | `index.html` Important Dates | badges read `Date TBA` |
| Code of Conduct link | `program.html` Program Notes | text only, no URL |
| Hotel block | `travel.html` Lodging | "coming soon" box; replace with the hotel card pattern from rubinalerts26 `travel.html` |
| Daily program | `program.html` | 3-day compression of the proposal's 5-day agenda; unconfirmed with Adam / Ayan; labelled "Draft" on the page |
| Speakers | `program.html` Day 1 primer | `TBD` |

Each placeholder is marked with an HTML comment starting `PLACEHOLDER:`; `grep -n PLACEHOLDER *.html` lists them.

## Deployment

Intended: GitHub Pages from `main`. Not yet a git repo and no GitHub repo exists.

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

- No white backgrounds outside the footer logo strip; every section uses the espresso/orange tints
- Colors are CSS custom properties under `:root`; use `var(--...)`, never hardcoded hex
- Navigation links use class `jiggle-link`
- Hero background is the local `rubin-sunset.jpg` (set in `.hero` in `styles.css`); the `--color-purple*` variable names are legacy and hold the orange/amber values
- Never call the event a "flagship"; "hack-week" is the funded event type
- Vocabulary: no leverage / robust / transformative / harness / notably / importantly
