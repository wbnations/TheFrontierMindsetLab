# Frontier Mindset Lab landing page: build report and AEM handover

**Pairs with:** Build brief v1.0 and wireframe v0.3 (November 24, 2026)
**What this is:** a working HTML/CSS prototype of the brief, built without an AEM license, for the web team to rebuild in AEM.
**Files:** `index.html` (the page), `styles.css` (design tokens and style variants, organised like an AEM client library). Neither uses JavaScript.
**Preview:** open `index.html` in a browser. Once this folder is on the branch GitHub Pages publishes, it's also at `/TheFrontierMindsetLab/landing-prototype/`. The page is `noindex, nofollow`.

---

## 1. Read this first: the brief's component assumption

The brief asks for **AEM Core Components** (Container, Title, Text, Teaser and so on) plus Style System variants. The page the team pointed to as the model, [microsoft.com/en-us/events/local-events/microsoft-cybersecurity](https://www.microsoft.com/en-us/events/local-events/microsoft-cybersecurity), doesn't use Core Components. It's built from Microsoft's own AEM component set, which appears under `/components/content/reimagine/...` in its source:

| Seen on the reference page | What it does |
|---|---|
| `section-master` | Full-width section band with a heading area and a content slot; supports 2-column layouts, background images and themes |
| `block-heading` | Eyebrow + title + paragraph + button group |
| `layout layout--cols-2/3/4` | Column grid |
| `card`, `block-feature` | Card with optional media, eyebrow/label, title, paragraph and a link |
| `card-grid`, `three-up-cards` | Grids of cards |
| `action`, `btn btn--secondary` | Buttons and links |
| `secondary-sticky-nav` | Sticky in-page navigation |
| `accordion` (FAQ) | Expand/collapse list |
| UMP video player | Video with poster |
| `universalheader`, `universalfooter` | Microsoft site header and footer |
| Themes: `theme-day`, `theme-night`, `theme-darkblue`, `bg--neutral-fade`, `card--event-gradient-blue/orange` | Fixed colour treatments |

These names come from the public page source. **The web team should confirm** the real component names and options available to the field landing-page template.

The prototype uses that vocabulary for its structure (`section-master`, `block-heading`, `layout`, `card`, `block-feature`) and the brief's names for the style variants (`band-warm`, `display-gradient`, `primary-pill`…). That way each element can be matched either way.

### Questions for the web team before build

1. **Which component set does the field template use:** the Reimagine components above, Core Components, or both?
2. **Can we add custom style variants and colours?** The reference page only uses Microsoft's fixed themes and Microsoft blue buttons. The Lab look depends on: gradient H1 text, the indigo → peach gradient rule, warm/lavender bands with soft glows, indigo pill buttons. If custom colours aren't allowed, which theme is closest?
3. **Header:** the prototype now assumes the page uses the template's **standard Microsoft site header**, as the reference page does. Which header (site name and menus) will this page get? The prototype shows the events header as a stand-in.
4. **Forms:** does the template support a Form Container (Section 8), or should it be a "Follow on LinkedIn" button?
5. **Journey row (Section 4B):** is there a component for a horizontal sequence with a connecting line? If not: a 5-column layout of plain block-features (dropping the line) is the fallback.
6. **Pull quote (Section 3):** is there a quote component? If not, a Text component with a style variant.
7. **Video:** confirm the UMP video player supports captions (VTT) and a transcript link.

---

## 2. Design tokens (exact values)

The brief's hex values were approximated from screenshots. These are the exact values from the prototype's stylesheet (`index.html` at the repository root). Use these.

| Token | Brief approx. | **Exact** | Use |
|---|---|---|---|
| `--indigo` | #25239A | **#1A2397** | Headings, primary buttons, numerals, links |
| `--purple` | #7B4FC4 | **#8551C7** | Tag outlines, chip hover/selected, focus ring |
| `--pink` | #D06C9F | **#D25BA4** | Gradient midpoint |
| (coral) | n/a | **#FB96A4** | Gradient, between pink and peach |
| `--peach` | #F3C9A4 | **#FCDAB0** | Gradient end, warm glow |
| `--navy` | #1F2A8F | **#1A2397** | Campaign bar, footer (the prototype bar uses indigo) |
| `--warm-bg` | #F6F4F0 | **#F6F5F1** + peach glow top right | Warm band |
| `--lavender-bg` | #F4F3FA | **#FAF9FC** + purple glow top left, peach glow bottom right | Lavender band |
| `--ink` | #1B1B1F | **#323130** body, #000 strongest | Body text |
| `--muted` | #5B5B66 | **#605E5C** | Secondary text, eyebrows |
| `--line` | #DCDBE4 | **#E1DFDD** | Dividers, card borders |

- Signature gradient: `linear-gradient(90deg, #1A2397, #8551C7 38%, #D25BA4 68%, #FB96A4 88%, #FCDAB0)`
- Display gradient (H1 only): `linear-gradient(90deg, #1A2397 25%, #8551C7)`; falls back to solid indigo.
- Type: Segoe UI stack. H1 56/36px, H2 40/30px, H3 20px, statement 28/22px, body 17/16px, line-height 1.55, eyebrow 12px uppercase 0.12em.
- Layout: max content width 1280px, side margins 64/32/20px (desktop/tablet/phone), section padding 96px desktop / 56px mobile, grids collapse to one column below 768px (4-up goes to 2-up below 1024px).

All of these are CSS custom properties at the top of `styles.css`.

---

## 3. Components used, per section

"Reimagine" is the closest match seen on the reference page; "Core" is what the brief specified. Style variant = class in `styles.css`.

| Section | Element | Reimagine (likely) | Core (brief) | Style variant |
|---|---|---|---|---|
| **Header** | Standard Microsoft site header. **Stand-in only**: copies the reference page's header (Microsoft logo, "Microsoft events", 4 menus, "Search all events"); its menus do nothing | Universal header (`universalheader`), supplied by the template | Experience Fragment (template default) | none. Not built: the template supplies it |
| **Campaign bar** | One-line link to `#live` | `section-master` with dark theme | Container | `band-navy` |
| **In-page nav** | 7 anchor links, sticky | `secondary-sticky-nav` | Container of text buttons | none (sticky via CSS) |
| **1 Hero** `#top` | Lab logo mark + eyebrow, H1, subhead, 2 CTAs, video | `section-master` 2-col + `block-heading` + UMP video | Container, Title ×2, Text, Button ×2, Embed | `band-warm`, `eyebrow`, `display-gradient`, `primary-pill`, `secondary-pill`, `rule-gradient` after |
| **2 Why now** `#why-now` | H2, intro, 2 belief rows, statement, close | `section-master` + `block-heading` + `layout--cols-2` ×2 | Container, Title, Text, Container 2-col ×2 | `band-lavender`, `eyebrow`, `statement` |
| **3 The Frontier Mindset** `#mindset` | H2 + tag, pull quote, body, 3-col spine | `section-master` + `block-heading` + `layout--cols-3` of `block-feature` | Title, Text ×3, Container 3-col | `band-warm`, `tag-outline`, `pull-quote`, `topline-grid`, `eyebrow` |
| **4A Mindsets** `#mindsets` | H2, intro, 4 teasers with clip | `layout--cols-4` of `card`/`block-feature` with media | Container 4-col, Teaser ×4 | `band-lavender`, `topline-grid` |
| **4B Journey** | Eyebrow, H3, intro, 5 unnumbered stops | `layout` 5-col of `block-feature` (question 5) | Container 5-col, Title + Text ×5 | `eyebrow`, `rule-gradient` connector |
| **5 Paths** `#paths` | H2, 2 chips, 2 cards (`#leaders`, `#individuals`) | `layout--cols-2` of `card` + `action` | Button ×2, Container 2-col, card Containers | `band-white`, `chip`, `card`, `statement`, `primary-pill`, `secondary-pill` |
| **6 Offerings** `#offerings` | H2, intro, 4-step ladder, 5 offer cards | `layout--cols-4` + `card-grid` with tags | Container 4-col, Teaser ×5 | `band-warm`, `card`, `tag`, `secondary-pill` |
| **7 Live** `#live` | Key art, tag, H2, body, 2 CTAs, media row | `section-master` 2-col + `card-grid` | Image/Embed, Text, Title, Button ×2, Container 3-col, Teaser ×3 | `band-lavender`, `tag-outline`, `primary-pill`, `secondary-pill` |
| **8 Connect** `#connect` | H2 + text; card with H3, text, email form, CTA | `section-master` 2-col + `card` (form: question 4) | Container 2-col, Title, Text, Form Container, Button | `band-warm`, `card`, `primary-pill`, `secondary-pill` |
| **Footer** | Standard Microsoft footer | `universalfooter` | Experience Fragment | none |

---

## 4. Placeholders still showing

Every bracketed placeholder from the brief is rendered as written. Buttons whose **link** is still a placeholder have a dashed border (and the placeholder in their tooltip), so reviewers can spot them.

**Visible copy**
- Campaign bar: `[Date, week of January 18]`
- Section 4: `[Lead / Coach]` (title and clip label)
- Section 6: `[Available now / Confirm]` ×3, `[Description TBD]`
- Section 7: `[Date, week of January 18]`, `[Premiere title]`, `[and guest TBD]`, `[January blog title]`
- Footer: `[Standard Microsoft footer…]`

**Links (dashed buttons)**
- `[AI Skills Navigator playlist URL]`: "Send your people the playlist", "Start the playlist" (Section 5)
- `[Leader 30/60/90-day plan PDF, ASSET-07]`: "Get the leader plan"
- `[URL]`: "Start the playlist" (offer card 1)
- `[ASSET-07]`: "Download the plan" (offer card 2)
- `[LinkedIn Live event URL]`: "Save your seat" (Section 7)
- `[.ics link]`: "Add to calendar"
- `[blog URL]`: January blog title
- `[interest form or mailto TBD]`: "Bring the Lab to your organization"

**Assets (labelled placeholder boxes with the brief's alt text)**
- ASSET-01 hero film (alt: "Aneesh Raman introduces the Frontier Mindset Lab."); also the `og:image` social share image
- ASSET-02 to ASSET-05 mindset clips
- ASSET-06 premiere key art (alt: "[Premiere title] — LinkedIn Live premiere.")
- ASSET-08, ASSET-09 short clips; blog teaser image
- ASSET-00 logo: **supplied**, using `assets/brand/lab-logo-web.png` from the prototype. It now sits beside the hero eyebrow, since the Lab header was replaced by the standard Microsoft header.

**Stand-ins (not to be built)**
- The site header copies the reference page's standard Microsoft header so reviewers see the page in context. Its menus and "Search all events" button do nothing.

**Demo-only behaviour**
- The "Notify me" form sends nothing: the email field has no name and the form only jumps back to `#connect`.
- Offer cards 4 and 5 ("Coming soon") are shown; hide them if the Nov 30 decision is to launch with cards 1–3 only.

---

## 5. Checklist (brief section 7)

| Check | Status |
|---|---|
| One H1; H2 per section; logical heading order | Pass (1 H1; H3/H4 used inside sections) |
| Gradient H1 contrast, solid indigo fallback | Pass. Large-text minimum is 3:1. Indigo end on the warm band: 11.1:1. Purple end: 4.8:1 on the warm band, 3.95:1 where it crosses the peach glow. Falls back to solid indigo via `@supports`. Other text: muted on lavender 6.2:1, purple tag on white 5.3:1, white on navy 12.1:1 |
| Video captions, transcript, no autoplay | Not testable yet: video placeholders only |
| Alt text as specified; glows and gradients CSS-only | Pass |
| Every anchor resolves | Pass (checked automatically: `#top`, `#why-now`, `#mindset`, `#mindsets`, `#paths`, `#leaders`, `#individuals`, `#offerings`, `#live`, `#connect`) |
| Works without JavaScript | Pass (the page has none) |
| Mobile: one column; buttons ≥ 44px | Pass at 390px; no sideways scrolling at 390, 768, 1024 and 1280px; every button ≥ 44px |
| Bracketed placeholders visible and listed | Pass (section 4 above) |
| `noindex, nofollow` | Pass |

## 6. Deliberate choices to review

- **Header:** "Start here: Choose your path" and the Lab header were dropped in favour of the standard Microsoft header. The paths are still reachable from the in-page nav ("For leaders", "For you") and the hero CTAs.
- **Side margins** match the reference page: content starts 64px from the edge on desktop (32px on tablet, 20px on phones).

- The **journey** has no numbers or "1 of 5", per the guardrail. Its stops are hollow circles joined by the signature gradient (vertical on phones).
- The **offerings ladder** is numbered 1–4, as the brief specifies (it's a sequence of actions, not a maturity ladder).
- **Choosing a path** highlights the matching card (via the `#leaders` / `#individuals` anchor), with no script.
- The **in-page nav** is sticky, since the reference page has a native sticky nav component.
