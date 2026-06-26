# Metropolitan League — CLAUDE.md

## Project
Static multi-page website for the Metropolitan League, NYC's first competitive inter-borough pickleball league. Live at **metropolitanleague.com** (GitHub Pages, master branch root).

**Owner:** Joe De Perio (jad@igotitapp.com / jadeperio@gmail.com)  
**GitHub:** Metropolitan-LeaguePB/metropolitan-league

---

## Stack
- Pure static HTML/CSS/JS — no build step, no framework, no npm
- All CSS and JS are inline (`<style>` / `<script>` tags) inside each HTML file
- Fonts: Google Fonts (loaded via `<link>`)
- Some images in `index.html` are base64-encoded directly in the HTML (keeps them in one file but makes the file large ~1MB)
- External images live in `/images/`

**Never introduce a build system, bundler, or framework.** Keep it one-file-per-page.

---

## Pages

| File | URL | Purpose |
|---|---|---|
| `index.html` | / | Home — hero, ticker, standings, teams, schedule, sponsors, contact |
| `about.html` | /about | League background, mission, borough map |
| `rules.html` | /rules | Match format & rules |
| `sponsor.html` | /sponsor | Sponsorship tiers and contact |
| `allblacks.html` | /allblacks | HKPC All Blacks club page |

All five pages share the same sticky nav bar. When adding or renaming a nav link, update it in **all five files**.

---

## Nav structure (all pages)
```
Home | About | Format & Rules | Teams | All Blacks | Sponsor | [Join CTA]
```
- Nav is a single line of HTML inside `<nav class="links" id="nav">` near the top of each file
- Mobile: collapses behind `.menu-btn` hamburger, toggled with `classList.toggle('open')`
- Active page gets `class="active"` on its own link

---

## Design tokens

Defined in `:root` inside each file's `<style>` block:

```css
--navy: #15233F        /* primary dark blue */
--navy-2: #1C3056
--navy-deep: #0C152B   /* page background */
--gold: #B58A3C        /* accent */
--gold-soft: #D8B262   /* also --lime and --lime-deep */
--cream: #F4F1E8
```

**Borough accent colors:**
```
Manhattan  #C2922F   Brooklyn  #B5562F   Queens  #1E8A7A
The Bronx  #B23A48   Staten Is. #2F7D5B
```

**Fonts:** Space Grotesk (display/headings) · Hanken Grotesk (body) · Space Mono (labels/mono) · Anton (large numerals)

---

## Images

```
images/
  All_Blacks-Logo.png       ← used in index.html team card
  rhpc-logo.png
  ipx-logo.jpg
  conquer-logo.jpg
  gotham-logo.png
  allblacks/
    ab-logo.png             ← All Blacks logo (inverted in nav)
    photo-court1.jpg        ← team section top-right
    photo-court2.jpg        ← home court section top-left
    photo-court3.jpg        ← hero background + home court bottom
    photo-court4.jpg        ← story section (tall portrait)
    photo-team-walking.jpg  ← team section hero/wide + home court top-right
    photo-bar.jpg           ← team section bottom-right
```

Photo filenames must be lowercase `.jpg` — the server (Linux/GitHub Pages) is case-sensitive.

---

## allblacks.html — key layout notes
- **Hero:** full-viewport, `photo-court3.jpg` as background at `brightness(0.35)`
- **Team section:** 3-photo grid — `photo-team-walking` (wide, spans 2 cols), `photo-court1`, `photo-bar`
- **Story section:** `photo-court4` as tall portrait with "June 5, 2026" badge
- **Home Court section:** `photo-court2` + `photo-team-walking` (2-up), then `photo-court3` full-width at `aspect-ratio: 16/9`
- **Back link:** `← Metropolitan League` in the nav always points to `index.html`

---

## Deploy
Push to `master` → GitHub Pages auto-deploys in ~1 min.  
No CI, no preview URLs — check live site after pushing.

```bash
git add <files>
git commit -m "Description"
git push
```

`.nojekyll` at repo root prevents GitHub Pages from running Jekyll.  
`.buildtrigger` can be touched to force a cache-busting redeploy.

---

## League context

- **Inaugural match:** June 5, 2026 — HKPC All Blacks defeated RHPC Hookers
- **Founding clubs:** HKPC All Blacks (Manhattan), RHPC Hookers (Brooklyn), Indoor Pickleball X (Brooklyn), Conquer (Manhattan)
- **Year 1:** NYC five boroughs · **Year 2 target:** Tri-State (NY/NJ/CT)
- **First sponsor:** The Botanist Gin (signature "All Black" cocktail launched match night)
- Attendance June 5: ~100 on-site; forward projection 300+; ~8K total impressions
