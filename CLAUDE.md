# Suji Shin portfolio

Personal portfolio for Suji Shin, third-year Interaction Design student in Toronto (George Brown College).
Live site: https://suji-s-design.github.io (GitHub Pages, repo `suji-s-design/suji-s-design.github.io`, branch `main`).
Pushing to `main` deploys the site in about a minute.

## Structure

- `index.html`: the whole site in one file. Home plus case study "views" (`#ergoscan`, `#shleep`, `#pawloop`, `#stuview`) switched by the `go(id)` function. No build step, no framework.
- `images/`: homepage thumbnails (`ergoscan-01.jpg` is the ErgoScan card image).
- `images/ergoscan/`: case study media. Every `.media` box has a `data-src`. If a file with that exact name exists, it replaces the placeholder automatically. If not, a dashed placeholder shows the filename and size. Do not remove this loader.

## Design system

- Background `--bg: #F7F3ED` with an aida cloth texture (SVG pattern set in JS), stitch colour `#8B1A2F`, ink `#2C1A10`, soft ink `#9C7A6A`, lines `#DDD5C8`.
- Fonts: Space Grotesk (headings, project names), Open Sans (body), Playfair Display italic (accents, taglines). Keep Open Sans for body text.
- Hero: "Hi, I'm Suji." stitched in cross stitch on a canvas. Text is sampled from Georgia italic, regular weight (not bold).
  - Cell size: 3px on retina, 4px otherwise. The page cloth uses the same cell size and is snapped to the canvas so every X sits in one cell, hole to hole.
  - Legibility matters more than texture. Thread shadow and sheen stay faint. Do not add jitter or a dark under stitch. Suji rejected big cells (8px) and noisy texture.
- Project cards, caption order: tag row (Platform · Role · Team, same three slots for every project) → project name (19px Space Grotesk 600) with year → problem-focused title (16px) → one-line description.
  - Platforms used: "Mobile app" (ErgoScan, Shleep, PawLoop), "Web" (Stu-View).
  - ErgoScan has a small "RGD Honorable Mention" chip. Do not put the award in the hero.
- Layout: two versions exist. `index-swatch.html` is the staggered "fabric swatch" layout (12-column grid underneath, slight tilt on the image only, white pearl sewing pin on each card). The grid version is the plain two-column layout. Suji is choosing between them. Whichever she picks becomes `index.html`.
- Case study pages follow the Dishcovery structure from sierrahopkins.com: title, meta row, hero media, TL;DR (problem / what I did / outcome), overview, problem, process, exploration (before/after per decision), final solution (screen gallery + features), impact and reflection, CTA, next project. Text is real HTML text, not slide images.

## Writing rules (important)

- Never use em dashes in any text written for Suji.
- Copy must sound like Suji, not like AI. English is her second language at an advanced level, so keep it natural and plain, not polished marketing copy.
- Do not invent facts about her projects. Leave a visible placeholder and ask her instead.

## Facts about the projects

- ErgoScan (2026): AR iOS app that measures a desk setup and gives AI fixes. Team of 2 with Diana Amriyeva. Suji: UX/UI from lo-fi to hi-fi, front-end prototype in Xcode (SwiftUI + ARKit) built with help from Claude, two rounds of user testing (in-class showcase, then a survey with about 20 visitors at the year-end show). Diana: concept, UX flow, backend including the OpenAI API. RGD Student Award 2026, Honorable Mention.
- Shleep (2025): speculative sleep-tech concept, 4-day hackathon, team of 4 (George Brown Polytechnic and OCAD U). Suji did UI design.
- PawLoop (2025): solo, local toy exchange app for cat owners (trade, sell, free). Problem framing, 3 concepts explored, sitemap, hi-fi UI in Figma, coded HTML/CSS/Bootstrap prototype.
- Stu-View (2025): solo moderated usability study of GBC's student portal. 5 participants, 4 tasks, think-aloud. Task 2 had a 60% completion rate and 2 critical errors. 3 of 5 participants gave up on the menu and used search.

## To do

- [ ] Fix the crowded nav on mobile (Work, About, name, Email, LinkedIn on one line).
- [ ] Pick swatch or grid layout and make it `index.html`.
- [ ] Add ErgoScan images to `images/ergoscan/` (Suji is making them herself).
- [ ] Fill ErgoScan timeline and the three reflection cards with Suji's own words.
- [ ] Build PawLoop, Shleep and Stu-View case studies in the same structure.
- [ ] Add the Resume link (currently `#`).

## Workflow

- Preview locally with a live-reload server and keep it open in Chrome so Suji can watch changes.
- When Suji is happy, commit with a clear message and push to `main`.
