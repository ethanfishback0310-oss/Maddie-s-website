# Catching Bubbles / 4 Haven

A website + platform for **Catching Bubbles** (the company), whose product platform is **4 Haven**. They are a niche team of **overnight & newborn postpartum specialists** who also support families through pregnancy, birth, postpartum, and beyond. The platform covers doula matching, education, resources, community, and caregiver coordination.

This is a standalone project with its own brand and design system, fully specified below. Everything needed to rebuild or extend the site lives in this file.

---

## Brand positioning

- **Company:** Catching Bubbles · **Platform:** 4 Haven
- **Niche (lead with this):** Overnight & newborn postpartum specialists. Do NOT lead with generic "pregnancy/birth/postpartum/beyond" — that's the broader offering, the overnight specialty is the hook.
- **Tagline / headline:** "Every family deserves a village."
- **Hero eyebrow:** "Overnight & Newborn Postpartum Specialists"
- **Voice:** soft, warm, nurturing, reassuring. Second-person, gentle. No corporate tone, no hard-sell.

---

## Aesthetic — locked design direction

Soft, calm, nurturing — "stepping into a peaceful sky." Floating clouds, bubbles (a nod to the name), rounded corners, soft shadows, gentle float animations. **No harsh edges, no corporate feel, no sharp corners.**

- **Layout:** centered hero on a warm background.
- **Hero background:** `linear-gradient(160deg,#FDFBF7 0%,#F4F0E6 44%,#EAF0F4 100%)`
- **Imagery:** mix of CSS-drawn clouds/bubbles + labeled placeholder blocks for real photos (we can't generate photos — placeholders read e.g. "Photo: Tori").

---

## Brand mark

- **Wordmark:** "Catching Bubbles" in Quicksand 700, color `#4B4660`, with a small uppercase tag "4 HAVEN PLATFORM" beneath it (`#9F8FCB`, 11px, letter-spacing 0.18em, uppercase).
- **Icon:** a cluster of 2–3 overlapping pastel bubbles (sage→sky and lavender→blush gradients) with a small white highlight circle. Built in CSS:

```html
<div style="position:relative; width:44px; height:44px; flex:none;">
  <div style="position:absolute; top:2px; left:2px; width:26px; height:26px; border-radius:50%; background:linear-gradient(135deg,#AFC9A6,#9FC4DD); opacity:.9;"></div>
  <div style="position:absolute; bottom:0; right:0; width:22px; height:22px; border-radius:50%; background:linear-gradient(135deg,#CBBDE9,#F6CFD7);"></div>
  <div style="position:absolute; top:14px; left:14px; width:13px; height:13px; border-radius:50%; background:#fff; opacity:.7;"></div>
</div>
```

---

## Typography

- **Display / headings:** **Quicksand** (weights 500–700)
- **Body:** **Nunito** (weights 400–800)
- Google Fonts import:
  `https://fonts.googleapis.com/css2?family=Quicksand:wght@400;500;600;700&family=Nunito:wght@400;500;600;700;800&display=swap`
- Headings: Quicksand 700, letter-spacing ~ -0.02em. Body: Nunito.
- Hero H1 ~74–76px; section H2 ~42–46px; never below ~13px for labels.

---

## Palette (use these literals — inline styles only, no CSS variables)

| Role | Hex |
|---|---|
| Off-white background | `#FDFBF7` |
| Cream | `#F4F0E6` / `#FBF5EC` / `#FBF9F4` |
| Sage | `#AFC9A6` · deep `#7FA98C` · tint `#E7EFE3` |
| Lavender | `#CBBDE9` · deep `#9F8FCB` · tint `#F1EEF8` |
| Sky | `#9FC4DD` / `#CFE3F0` · deep `#88A9D6` · tint `#EAF1F6` |
| Blush | `#F6CFD7` · deep `#E2A1B0` · tint `#FCEDF0` |
| Text dark | `#3f3b54` / `#4B4660` |
| Text muted | `#6b6679` / `#8B8699` / `#7a7589` |
| Footer background | `#3f3b54` |

- **Primary button:** `background:linear-gradient(135deg,#9DBE93,#88B0D4)`, white text, `border-radius:999px`, Quicksand 700, `box-shadow:0 14px 34px rgba(136,176,212,.42)`.
- **Secondary button:** white bg, `#5d5870` text, `border-radius:999px`, soft shadow `0 5px 18px rgba(0,0,0,.06)`.
- **"village" gradient text accent:** `linear-gradient(120deg,#7FA98C,#9F8FCB)` with `-webkit-background-clip:text; color:transparent`.

---

## Components & patterns

- **Cards:** white, `border-radius:28px`, `box-shadow:0 12px 34px rgba(95,110,130,.08)`. Smaller cards use radius 22–26px.
- **Section eyebrow:** 13px, weight 700, uppercase, `letter-spacing:0.14em`, sage `#7FA98C` (or lavender `#9F8FCB`).
- **Clouds:** white blob, large `border-radius` (60–80px), `filter:blur(24–36px)`, low opacity (.55–.85), `drift` / `driftSlow` animation.
- **Bubbles:** `radial-gradient(circle at 35% 30%, #fff, <pastel>)`, `bob` / `bobSm` float animation.
- **Highlighted/specialty card:** filled with the primary gradient `linear-gradient(150deg,#9DBE93,#88B0D4)`, white text, with a translucent white circle decoration.
- **Pills/chips:** pastel tint background + matching deep text color, `border-radius:999px`, weight 700.
- **Form fields (mock):** `height:52px`, `border-radius:14px`, `background:#FBF9F4`, `border:1.5px solid #EFEAF4`, placeholder text `#A7A2B4`.

### Keyframes (define once per page in `<helmet><style>`)

```css
@keyframes drift     { 0%,100%{transform:translate(0,0);} 50%{transform:translate(24px,-16px);} }
@keyframes driftSlow { 0%,100%{transform:translate(0,0);} 50%{transform:translate(-18px,14px);} }
@keyframes bob       { 0%,100%{transform:translateY(0);}  50%{transform:translateY(-12px);} }
@keyframes bobSm     { 0%,100%{transform:translateY(0);}  50%{transform:translateY(-7px);} }
```

---

## Navigation

Top nav order: **Find My Match · Our Village · Support Options · Resources · Community · Join Our Team** — plus **Login** and a **Get Started** primary button on the right. (Certification replaces some nav items on the Certification page; the dashboard uses its own sidebar.)

Pages are wired with working `<a href>` navigation using **relative, URL-encoded filenames** (filenames use a normal hyphen `-`, encoded as `%20-%20`). A global `a{color:inherit;text-decoration:none;cursor:pointer;}` rule (tagged `/*linkreset*/` in each page's `<style>`) keeps anchors looking like the original styled spans. **When editing nav, keep links as `<a>`, not `<span>`.**

Link map:
- Logo → Home
- Find My Match / Find My Care Match / Start the Quiz → Care Quiz
- Our Village / "View all of our village" → Our Village
- Support Options / Explore Support Options → Support Options
- Resources → Resources
- Community / Join for $50/mo / Start membership / 4 Haven Community → Community
- Join Our Team → Join Our Team
- Certification → Certification
- Login / Student Login → Parent Dashboard
- Get Started / Enroll / Start your pathway / Book Consultation / Schedule Intro Call → Get Started

---

## Care matching specifics

- **Care Archetypes:** The Nurtured Nest, The Guided Journey, **The Calm Harbor**, The Village Builder, The Supported Beginning. (The Calm Harbor is the demo result.)
- **Matching demo:** Primary = **Tori** (overnight & newborn specialist), Secondary = **Loren** (postpartum doula). Additional team members auto-assigned (lactation, birth, family coordination).
- **Team names in use:** Tori, Loren, Maya (birth), Priya (lactation), Jordan (overnight/twins), Amara (postpartum), Nina (family coordinator), Reese (birth & postpartum).

### The quiz is the primary funnel — keep it prominent

Drawing people to the Care Match quiz is the homepage's #1 job. The quiz entry must stay high on the page and visually dominant:
- Hero primary CTA = **Find My Care Match** (→ quiz).
- A full-width **"Start Here · Step 1"** quiz banner sits **directly below the hero**, before Support Options (gradient `linear-gradient(135deg,#9DBE93,#88B0D4)`, white text, the whole banner is a single `<a>` to the quiz). Do not bury or remove it.
- "How It Works" reinforces the quiz as step 1 → meet your team → rest easy.
- Every "Find My Care Match" / "Start the Quiz" CTA across all pages links to `Catching Bubbles - Care Quiz.dc.html`.

---

## QUIZ — build spec (for finishing the interactive version)

`Catching Bubbles - Care Quiz.dc.html` currently ships the **static design** of one question screen (showing "Question 3 of 7") plus the result screen, stacked with a divider. To finish it as a **working interactive quiz**, convert it to a single-screen flow driven by the logic class. Keep all existing inline styling/visuals — only add state + interactivity. Remove the stacked-divider layout and the "↓ Results screen" separator once it's interactive.

### Flow / state

- One question visible at a time; Continue advances, Back goes to the previous question, last question → computes result → shows the result screen. "Save & exit" → Home.
- Logic class state: `{ step: 0, answers: {} }` where `answers[questionId] = optionId`. Track progress as `(step+1)/questions.length`; update the progress bar width and the "Question N of 7" / "About X min left" labels from state.
- Continue is disabled until the current question has a selection. Selecting an option sets the green selected treatment (`border:2px solid #9DBE93`, check badge) — already designed, just bind it.
- Build option lists with `<sc-for>` over the current question's options (set `hint-placeholder-count`), and expose handlers (`select(optionId)`, `next()`, `back()`) from `renderVals()`. Persist `answers`+`step` to `localStorage` (key `cb_quiz`) so a refresh resumes; re-read on mount.

### Questions (7) — `id` · prompt · options (each option carries archetype weights)

Each option adds points to one or more archetypes. `archetype` keys: `nest` (The Nurtured Nest), `guided` (The Guided Journey), `harbor` (The Calm Harbor), `village` (The Village Builder), `beginning` (The Supported Beginning).

1. **`stage`** — "Where are you in your journey?" → Trying to conceive `{beginning:2}` · Currently pregnant `{guided:2}` · **Baby is here — newborn at home** `{harbor:2,nest:1}` · In postpartum recovery `{harbor:1,nest:2}`
2. **`support_type`** — "What kind of support matters most right now?" → Overnight newborn care `{harbor:2}` · Hands-on daytime help `{nest:2}` · Education & planning `{guided:2}` · Building my wider support network `{village:2}`
3. **`sleep`** — "How are you sleeping?" → Barely — nights are hardest `{harbor:3}` · Up and down `{harbor:1,nest:1}` · Managing for now `{nest:1}` · Not yet relevant `{guided:1,beginning:1}`
4. **`style`** — "What support style fits you?" → Structured & reassuring `{harbor:2,guided:1}` · Gentle & hands-off `{nest:2}` · Educational & empowering `{guided:2}` · Community & connection `{village:2}`
5. **`household`** — "Who's in your village today?" → Mostly just us `{harbor:1,nest:1}` · Partner, no nearby family `{harbor:1,village:1}` · Some local family/friends `{village:1,nest:1}` · Lots of help, need coordination `{village:2}`
6. **`worries`** — "What's weighing on you most?" → Exhaustion & rest `{harbor:2}` · Feeding `{nest:1,harbor:1}` · Knowing what's normal `{guided:2}` · Feeling isolated `{village:2}`
7. **`timing`** — "When would you like support to begin?" → As soon as possible `{harbor:2}` · Before baby arrives `{guided:2,beginning:1}` · In the first few weeks `{nest:1,harbor:1}` · Still exploring `{village:1,beginning:1}`

### Scoring → archetype

Sum weights across all answers; the archetype with the highest total wins (ties → priority order: `harbor` > `nest` > `guided` > `village` > `beginning`, reflecting the overnight niche). Compute a display "match %" as `round(85 + min(winningScore,8))` capped at 98 (purely cosmetic — keep it in the 85–98 range).

### Archetype → result content + team mapping

Result screen already designed for **The Calm Harbor**; make its archetype name, blurb, match %, and team list data-driven from this table:

| Archetype | One-line blurb | Primary | Secondary | Auto-assigned |
|---|---|---|---|---|
| **The Calm Harbor** | Thrives with structured guidance and hands-on overnight support. | Tori (Overnight & Newborn Specialist) | Loren (Postpartum Doula) | Priya (lactation), Maya (birth), Nina (coordination) |
| **The Nurtured Nest** | Wants gentle, hands-on daytime care and a soft landing at home. | Loren (Postpartum Doula) | Amara (Postpartum Doula) | Priya (lactation), Nina (coordination) |
| **The Guided Journey** | Values education, planning, and feeling prepared. | Maya (Birth Doula) | Reese (Birth & Postpartum) | Priya (lactation), Loren (postpartum) |
| **The Village Builder** | Wants community, connection, and coordinated support. | Nina (Family Coordinator) | Reese (Birth & Postpartum) | Loren (postpartum), Priya (lactation) |
| **The Supported Beginning** | Early in the journey; wants a steady guide from the start. | Reese (Birth & Postpartum) | Maya (Birth Doula) | Loren (postpartum), Nina (coordination) |

Result CTA = **Book Consultation** → `Catching Bubbles - Get Started.dc.html`. Keep the avatar-cluster "+N support team members" row.

## Community

- **4 Haven Community — $50/mo.** Includes a private Discord, peer discussions, expert responses, live Q&A, monthly workshops. "First week free · Cancel anytime."

---

## Build status — ALL PAGES COMPLETE

Every page is a Design Component (`.dc.html`), inline styles only, wired with working navigation.

| Page | File |
|---|---|
| Homepage | `Catching Bubbles - Home.dc.html` |
| Care Matching Quiz (question + result screens) | `Catching Bubbles - Care Quiz.dc.html` |
| Our Village (team grid + featured profile) | `Catching Bubbles - Our Village.dc.html` |
| Support Options | `Catching Bubbles - Support Options.dc.html` |
| Resources library | `Catching Bubbles - Resources.dc.html` |
| Community ($50/mo) | `Catching Bubbles - Community.dc.html` |
| Certification program | `Catching Bubbles - Certification.dc.html` |
| Join Our Team (application) | `Catching Bubbles - Join Our Team.dc.html` |
| Get Started (inquiry form) | `Catching Bubbles - Get Started.dc.html` |
| Parent Dashboard (4 Haven logged-in) | `4 Haven - Parent Dashboard.dc.html` |
| Hero directions (early exploration, A/B/C) | `4 Haven - Hero Directions.dc.html` |

---

## Working notes

- **Fidelity:** high-fidelity design. Photo spots are labeled placeholder blocks for real imagery.
- **Everything is a Design Component (`.dc.html`), inline styles only** — no stylesheets, no CSS variables, no CSS classes for layout. The only thing in `<helmet><style>` is font links, body reset, and the `@keyframes` + the `/*linkreset*/` anchor rule.
- When adding pages, copy the nav block and footer from an existing page, keep the brand mark, palette, and keyframes identical, and wire new links the same way.
- The Care Quiz and Parent Dashboard are intentionally focused screens (minimal/no top nav); their logos still link home.
