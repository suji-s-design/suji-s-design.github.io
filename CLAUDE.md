# Suji Shin portfolio

Personal portfolio for Suji Shin, third-year Interaction Design student in Toronto (George Brown Polytechnic). She is applying for UX / product design internships and co-ops.
Live site: https://suji-s-design.github.io (GitHub Pages, repo `suji-s-design/suji-s-design.github.io`, branch `main`). Pushing to `main` deploys in about a minute.

## Current task: move the new "Tuning" design into the real site

The old cross-stitch design is retired. The new design is final and lives in `portfolio-tuning.html` (single file, hash-routed). It becomes the new `index.html`.
The old design notes are kept in `CLAUDE-old-stitch-design.md` for reference only. Do not follow them for visuals.

Steps:
1. Back up the current `index.html` as `index-old-stitch.html`.
2. Copy `portfolio-tuning.html` to `index.html`. Do not rewrite or "clean up" its JS or CSS. The hero (dots, tuner, sound, cursor) took a long time to tune and is easy to break.
3. Port the existing ErgoScan case study from the old `index.html` (`#view-ergoscan`) into the new design. Keep the content, structure and copy exactly as they are. Change only the look: fonts, colors, outlines, spacing, radius (see Design system below). Keep the `.media` loader (every `.media` has `data-src`; if the file exists it replaces the placeholder, otherwise a dashed placeholder shows the filename and size). Do not remove this loader.
4. Wire routing. The new page uses hash routes (`#about` shows the About page, anything else shows Home, `#work` scrolls to the work section). Add `#ergoscan` as a case study view the same way, and link the ErgoScan card to it. The other cards (Shleep, PawLoop, Stu-View) stay `#` placeholders until their case studies are built.
5. Reuse the existing images in `images/` (`ergoscan-01.jpg` is the ErgoScan card image) as the card thumbnails. The thumbnail box is `.ph` (16:10, 1px black border, radius 14px). Put the image inside it.
6. Preview locally, check desktop (1440x900, 1280x680) and phone (390x844), then commit and push to `main`.

## Structure of `portfolio-tuning.html`

- `#home`: hero (`#hero`), work section (`#work`), "Want to know who's behind it?" band (`.meet`).
- `#aboutPage` (hidden by default): intro with photo placeholder, bio, Education, Awards, "When I log off, I like to *" tiles.
- Shared `<footer class="end">` (blue, "Stay tuned.", email, LinkedIn, Resume, Toronto clock, Back to top).
- `#ergoscanPage` (hidden by default, route `#ergoscan`): ErgoScan case study, redesigned 2026-10-15 from Suji's award slides, poster, app code and screen recording. Blue header with award chip, title, one-line summary, meta and a phone frame playing `images/ergoscan/demo.mp4` (trimmed, 600px, no audio). Then stats row, sticky section list (1100px+), TL;DR, Problem, My role, Process (UX flow), Testing (before/after), Solution (features, screen gallery, Under the hood), Impact (poster), Reflection, blue lineup of three phones, CTA, next. CSS is a separate `<style>` block scoped to `#ergoscanPage`; the `.media` loader and the section-list script are a separate `<script>` after the main one. Placeholder labels use `.mph` (not `.ph`).
- `#shleepPage` (route `#shleep`): Shleep case study built 2026-10-19 from the FigBuild deck and the Figma prototype, same structure and CSS as ErgoScan (case study CSS is scoped with `:is(#ergoscanPage,#shleepPage)`). Screens are 2x Figma exports in `images/shleep/`. Long screens use `.media.scroll` with a `--shift` value so they scroll slowly inside the phone frame. No Reflection section yet (nothing from Suji to base it on).
- `#stuviewPage` (route `#stuview`): Stu-View case study built 2026-10-19 from Suji's test plan (Assignment 4), one-page report (Assignment 5), observation sheet and survey. Screens are stills from session video E.mov, cropped to the page, with Suji's name, student number and the instructor's name blurred. Never publish unblurred frames from the session videos.
- PawLoop card is marked work in progress (`.card.wip`): band says "Work in progress", cursor pill says "Soon", click does nothing.
- About "When I log off" tiles show a small black "WIP" tag on hover (`.tile::after`).
- About photo is a 3D lanyard ID card: `lanyard.js` (plain-JS port of React Bits `<Lanyard />`, three.js 0.170.0 from jsDelivr), mounted into `.pic#lyard` the first time `#about` opens. Desktop (≥900px): text on the left (heading cols 1–7, bio 1–6, bio text clamp(16px,1.3vw,18px)), card on the right (cols 7–end, rows 1–2), the canvas reaches up to the page top and out to the right screen edge so the band comes from the top; anchor 0.44 (card on the right, band clear of the WORK link). Desktop card: size 0.6, band length 0.2. A script (`placeTip`) sets the heading's margin-top so the top of its letters lines up with the card's top edge, puts the hint 40px under the card, and pushes the bio down (bio margin-top) so its last line ends on the hint's line. 22px gap under the heading; grid rows `auto 1fr` so extra height never opens under the heading. Phones (<900px): stacked, the card area is full width (no 420px cap) so the card hangs in the center; band length 0.2 too, hint at 78% + 18px, and a negative margin-bottom pulls the bio up under the hint. Front = `images/suji.jpg` moved down 70px so the clip slot sits in the gray background; back = yellow card (SUJI SHIN, PRODUCT DESIGNER, TORONTO); band = black with "SUJI SHIN · PRODUCT DESIGNER" (a blue band would vanish on the blue About background). The faces and band are drawn on canvas in the module script at the end of `index.html`. Visitors drag or throw it and click to flip; the cursor pill says "Drag" on the card (`body.lyhov`). The custom cursor listens to `pointermove`, not `mousemove`: the card captures the pointer while dragging, which stops mouse events, so a mousemove cursor would freeze. A small sentence-case hint sits just under the resting card, centered on it: "Drag it around, or click to flip" ("tap" on touch screens). No all-caps mono labels here. Without WebGL the plain photo stays.
- Hero to work transition: the blue hero scrolls away normally (not sticky). `#workWave`, an SVG added by script at the top of `.work`, is one soft blue wave hanging from the hero's bottom edge over the flat white section. Its height follows scroll: flat at the start and end, so no blue is left at the top. Suji wants this simple: one layer, same blue, the white is never cut into a wave, no extra scroll distance. The first screen must show only blue. `history.scrollRestoration` is manual so a reload opens at the top. A tiny script moves `#tuner` to `<body>`; `body.pg-about .tuner` hides it on About and case study pages.
- Scroll reveal: a separate script adds `.rv` to sections, cards and media (not the hero) and `.rvin` when they scroll into view (fade + 18px rise, cards staggered 80ms). It checks scroll position directly instead of IntersectionObserver, and does nothing with prefers-reduced-motion. Do not put `.rv` on elements that have their own transform or transition on hover (tiles, pills, buttons); reveal their container instead.
- Email links with `data-copy` (case study "Email me" button, footer email) copy the address instead of opening mail: black "Copy email" cursor pill (same look as the "View" pill) on desktop, "Email copied" toast everywhere. Clipboard API first, then a textarea fallback.
- `body.pg-about` is set on `#about` and `#ergoscan` (pages without the tuner) so the corner sound button always sits in the corner and also shows on phones.
- Fixed corner speaker button `#snd`, custom cursor `#cur` (whole note) and `#curv` ("View" pill).
- One `<script>` IIFE. Careful with variable names inside it: `cv` is the hero canvas. A new variable named `cv` once broke the whole dot field. Use unique names.

## Design system

Palette (CSS tokens in `:root`):
- `--blue #2d19f8` (hero, About top, footer), `--y #fff70d` (name, labels), `--pink #ff4ba7` (the "Want to know who's behind it?" text only), `--black #0a0a0a`, white page background.
- Tuner: body `#d6dade`, LCD `#fbe94a`, needle `#e5262d`, in-tune lamp `#25e06a`.
- Do not lower the pink saturation. Suji tried it and rejected it. Avoid gradients on the tuner, avoid hot pink dominance.

Fonts:
- DM Sans for body and headings (Google Fonts, with a Helvetica fallback). Suji chose it because plain Helvetica felt dull. Big headings use `letter-spacing: -.025em` (tighter looked squashed in DM Sans).
- DM Mono for nav, small labels and the tuner. TikTok Sans for the SUJI SHIN nav logo.
- Do not use Open Sans.

Outline system (one visual rule across the page):
- Big yellow headings (name, About "Hi, I'm Suji.", footer "Stay tuned."): `-webkit-text-stroke: 3px #0a0a0a; paint-order: stroke fill`. The "Want to know who's behind it?" text uses 2px.
- Pills and labels are fully rounded. Role pill: white fill, black text, 1.5px black border, weight 500. Section labels (Selected work, Education, Awards): yellow fill, 1px black border. "Meet Suji" button: black text, 1.5px black border, fills yellow on hover.
- Work thumbnails: 1px black border. Tuner body: 1.5px black border. Speaker button: 1.5px black border (yellow fill when sound is on). Off-duty tiles: 2px.
- Keep lines thin. Suji does not like a puffy, over-bold, or AI-looking style, too much glow, or busy UI.

Hero behavior (do not change without asking):
- Name `Suji Shin` is the biggest element, then the role pill "Product Designer", then the 3-line intro. Name and role must stay the most prominent.
- Dot field on a canvas (CSS blur 1.1px). When sound is off the dots are dimmed to about 62%; they brighten smoothly when sound is on. A cursor lens turns nearby dots yellow. Ghost ripples play when sound is off. Dots are hidden or pushed away from the intro text and role pill.
- Tuner (hardware style, KORG-like): fixed bottom-right, drag only the needle (±100 cents). When detuned the name gets a soft "gooey" SVG filter (sharp merges and blooms, flat thins slightly). Lamp turns green when in tune. After dragging, the label changes to "click outside to retune" and clicking outside the tuner retunes. When already in tune, clicking scatters the dots.
- Tuner scales 1.18x at 1400px wide and 760px tall or more, and slides away on scroll. The speaker button sits to its left.
- Tuner shine: a soft diagonal white highlight slowly sweeps across the tuner, soft and wide with almost no gap between passes (3.6s sweep, 3.8s loop) via `.tuner.dev::after`, with a synced edge glint on the black border via `.tuner.dev::before`, and keeps going until the visitor first presses the needle (`body.dragged`), then fades out. It replaced the old white glow pulse. The "drag the needle" label (10px, weight 600) blinks until the first needle press too (`body:not(.dragged)`). The pulsing speaker ring still runs only during `body.hint` (until the first interaction).
- Sound is a generative BGM, off by default, and never autoplays. Nav `SOUND[OFF]` and the corner speaker are linked.
- Custom cursor (desktop with a fine pointer only): a whole note (black oval, white tilted hole). Over links, buttons and the tuner it becomes the normal cursor. Over a work thumbnail (`.ph`) it becomes a black "View" pill.

## Copy

The final copy is whatever is in `portfolio-tuning.html`. Do not replace it with older wording from the previous `index.html`. Do not add these back anywhere: Korea-based experience, server/host or music instructor jobs, Shleep in the About text, ShelfGuard. Do not add more "tune" puns (it appears only in the hero intro and "Stay tuned.").

## Writing rules (important)

- Never use em dashes in any text written for Suji.
- Copy must sound like Suji, not like AI. English is her second language at an advanced level, so keep it natural, plain and short. Not polished marketing copy.
- On case studies, describe only Suji's own role. Never describe what teammates did (professor feedback, 2026-10-18). No TL;DR and no number/stat summaries.
- Do not invent facts about her or her projects. Leave a visible placeholder and ask her instead. (A made-up "Mostly by ear" caption on the piano tile was already removed because it was not true.)
- Minimal words. Simple English.

## Facts about the projects

- ErgoScan (2026, 4 weeks): AR iOS app that measures a desk setup and gives AI fixes. Team of 2 with Diana Amriyeva. Suji: UX/UI from lo-fi to hi-fi, front-end prototype in Xcode (SwiftUI + ARKit) built with help from Claude, two rounds of user testing (in-class showcase, then the year-end show, where about 20 visitors tried the app and about 5 filled out the survey. Never say 20 people were surveyed). Diana: concept, UX flow, backend including the OpenAI API. RGD Student Award 2026, Honorable Mention.
- Shleep (2026): sleep and dream tracking concept from FigBuild 2026 (Figma's student design-a-thon), team of 4. Suji's role is UI design: she set the visual style (type, spacing, card design, corner radius; defined as she designed, kept every screen consistent. Frame it positively, never as "no time") and designed many of the screens, shaping the flow while designing them. Some screens were designed by teammates (she doesn't remember which), so never say she designed all screens. Ideation and the overall flow were team work; do not list UX flow as her role.
- PawLoop (2025): solo, local toy exchange app for cat owners (trade, sell, free). Problem framing, 3 concepts explored, sitemap, hi-fi UI in Figma, coded HTML/CSS/Bootstrap prototype.
- Stu-View (2025): solo moderated usability study of GBC's student portal. 5 participants, 4 tasks, think-aloud. Task 2 had a 60% completion rate and 2 critical errors. 3 of 5 participants gave up on the menu and used search.
- Case study structure (from the existing ErgoScan page, keep it): title, meta row, hero media, TL;DR (problem / what I did / outcome), overview, problem, process, exploration (before/after per decision), final solution (screen gallery + features), impact and reflection, CTA, next project. Text is real HTML text, not slide images.

## To do

- [x] Move the new design into `index.html` and port the ErgoScan case study (done 2026-10-15).
- [x] About photo (`images/suji.jpg`, 900px), shown on the lanyard card (plain 4:5 photo is the fallback).
- [ ] Piano tile caption is empty on purpose. Ask Suji what to write.
- [ ] Resume link and LinkedIn link (Resume is `#` for now).
- [x] ErgoScan media in `images/ergoscan/`. App screens (`screen-*.jpg`) and looping clips (`clip-*.mp4` + same-name `.jpg` fallback) come from Suji's screen recording `IMG_9004.MP4` at full resolution, shown inside a CSS phone frame (`.dv > .device`). Only `before-*.jpg` (old versions), `problem.jpg`, `ux-flow.jpg` and `poster.jpg` come from the slides/poster, rendered at high resolution. Do not use low-res slide crops. A real photo from the year-end show would still be good.
- [ ] ErgoScan Reflection is a DRAFT written from the RGD 2026 judge feedback (marked on the page with a dashed "Draft" note). Suji edits it, then remove the note.
- [ ] Build the PawLoop case study in the same structure, then link its card and remove `.wip`. (Shleep and Stu-View done.)
- [ ] Check in a real browser: DM Sans rendering, needle drag, cursor, the 700px to tablet layout, and the phone hero.

## Workflow

- Preview locally with a live-reload server and keep it open in Chrome so Suji can watch changes.
- Suji gives opinions as "어때?" or "할까?". Answer with an opinion and options first, and change the file when she says yes.
- When Suji is happy, commit with a clear message and push to `main`.
