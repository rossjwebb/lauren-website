# Plan: "Unfiltered" Exhibition Section — laurensuper.com

**Status:** Awaiting execution. Do not modify the live `index.html` until Ross/Lauren choose a version (Step 5).
**Branch:** All work on `claude/lauren-website-access-tdkl8g`. Never push elsewhere.
**Goal:** Announce Lauren Super's solo show "Unfiltered" at the top of the homepage. Build **three versions** for Lauren to choose from:

- **Version A** — designed editorial section, built from the flyer's text and images
- **Version B** — designed immersive hero, built from the flyer's text and images
- **Version C** — the literal option: the flyer JPGs themselves placed at the top, existing content moved around them

**Hard requirement for A and B:** the copy comes from the flyer (verbatim or near-verbatim, see §1) and the imagery focuses on the works the flyer features (see §4). Layout may differ from the flyer; content may not.

---

## 1. Flyer content (single source of truth)

### Facts

- **Show:** *Unfiltered* by Lauren Super — Contemporary Multidisciplinary Artist
- **Venue:** Sonya Winner Rug Studio, 14 York Rise, London NW5 1ST
- **Opening:** Saturday 5 September 2026, 12–6pm — coinciding with the 2026 **York Rise Street Party**
- **Continues:** Monday to Friday, 10am–6pm, until **24 October 2026**
- **Host credit:** Sonya Winner Rug Studio (vibrant contemporary rugs) — link https://www.sonyawinner.com
- **Maps link:** `https://maps.google.com/?q=Sonya+Winner+Rug+Studio,+14+York+Rise,+London+NW5+1ST`

### Flyer copy — use these lines, not paraphrases

Invitation side:

> You are invited to the opening of 'Unfiltered' by Lauren Super
> Saturday 5th September 12–6pm, to coincide with the 2026 York Rise Street Party
> Meet Artist Lauren Super and sample British Wine + Artisan Cheese at the rug showroom during The York Rise Street Party

About side (use all four paragraphs in A and B; light tidying of punctuation allowed, no rewording):

> Lauren Super is a British multidisciplinary artist working across oil painting, hand-carved stone, ceramic, glass and resin installation.
>
> Her work explores the tension between natural beauty and the digital masks we wear; and, at its heart, what a filtered, always-observed culture is doing to childhood.
>
> It begins in the garden — Super's botanical paintings: Cape Town sunsets, hibiscus and cosmos set against deep black grounds, made as survival and mindfulness during a difficult time, and stand for a natural beauty the modern world is losing.
>
> From there the work darkens and complicates: masks drawn from her African heritage; a teenager's "goldfish existence" seen through a Snapchat filter; a mother slowly consumed by the fish; the architects of the feed, fishing for the next generation.

Street-party context (may condense for space): one of North London's most-loved neighbourhood festivals — live music, artisan makers, street food, family entertainment. Sonya's studio hosts a pop-up by @goldlightlyjewellery alongside curated ceramics, glass and jewellery by Alice Rose, Jars, Karola Torkos, Tim Rawlinson and more.

Today is mid-August 2026: the section launches in "opening soon" state (~3 weeks out).

## 2. Design constraints

- Site language: single-file pages, inline CSS, Georgia serif, paper palette (`--bg:#f5f0eb`, `--ink:#2c2c2c`, `--rule:#d4cdc3`). Versions A and B must feel like *this site* — no bunting, no Sonya branding beyond the credit line. Version C is exempt: it shows the flyer as-is.
- Mobile-first: visitors arrive from Instagram/WhatsApp on phones. Test at 390px.
- Placement: the very top of the homepage. Everything currently on the page stays, pushed down.

## 3. The three versions

### Version A — "Editorial announcement" (quiet, gallery-journal style)

1. Slim full-width ribbon at the very top (above the `Lauren Super` header): small-caps — "Solo exhibition · *Unfiltered* · Opens 5 September — Sonya Winner Rug Studio, London NW5" — anchors down to the section.
2. Existing header unchanged.
3. **Exhibition section between header and hero video**, framed by dotted rules (nod to the flyer's dotted dividers): eyebrow "You are invited to the opening of", large serif *Unfiltered* by Lauren Super, dates/venue block in letterspaced small caps (opening day + street party line, then continues-until line), then the four "About" paragraphs from §1 at readable measure.
4. **Image strip of flyer-featured works** (see §4): suggest `bliss.jpg` (the sunset painting on the flyer), `camo-fish.jpg` (the goldfish/Lucky Charms painting), `unfiltered.jpg` (the namesake glass piece), `golden-child-lauren.jpg` (the artist-with-stone-fish photo from the flyer). Judge final crops on screenshots.
5. Text CTAs: "RSVP for the opening" → inquiry form; "Getting there" → Maps; "Presented at Sonya Winner Rug Studio" → sonyawinner.com.

### Version B — "Immersive takeover" (bold, full-bleed hero)

1. Full-viewport (min ~85vh) dark hero at the very top: background one of the flyer-featured works dimmed toward near-black (suggest `camo-install.jpg` or `bliss.jpg` — echoing the deep-black grounds named in the flyer text). Light Georgia type: eyebrow "You are invited to the opening of", huge *Unfiltered*, "by Lauren Super", dates + venue, the street party / wine + cheese line.
2. Below the fold of the hero (still within the new section, on paper background): the four "About" paragraphs from §1 beside a **flyer-image collage** — `golden-child-lauren.jpg`, `unfiltered.jpg`, `bliss.jpg`, `camo-fish.jpg` (grid or offset stack).
3. Countdown to opening ("Opens in N days") with date-aware states (§3-shared).
4. CTAs as buttons: "RSVP for the opening" + "Directions". One restrained accent from the resin-fish turquoise (~`#2b9aa8` family), hover/accents only.
5. Scroll cue ("↓ Enter the work") into the untouched existing homepage.

### Version C — "The flyer, literally"

1. Directly under the existing header (`Lauren Super` / tagline), insert the two flyer JPGs — invitation side first, about side second. Desktop: side by side, max-width ~1100px, generous whitespace, soft shadow matching `.hero-video`'s. Mobile: stacked full-width.
2. Each flyer is clickable → opens the full-resolution file (plain link or minimal lightbox; no library).
3. One text line beneath: "RSVP for the opening" → inquiry form (same wiring as A/B).
4. Everything else on the page unchanged, pushed down. No other redesign — this version is deliberately literal.
5. Serve compressed display copies (~1200px wide, < 350KB) linking to the full-res originals.

**Unblocked:** `flyer-invite.jpg` (bunting/invitation side) and `flyer-about.jpg` (QR/about side) are in the repo root on this branch — 1131×1600 progressive JPEGs, ~320KB each, verified visually. Already light enough to serve directly; display copies per §6 are optional for these two.

### Shared mechanics (all versions)

- **RSVP wiring:** add `<option value="Private View RSVP">Private View RSVP — 5 September</option>` to the inquiry `select`. RSVP CTAs link `#inquiries`; a tiny script preselects that option when the hash indicates RSVP (e.g. `#rsvp`).
- **Date-aware copy** (small inline script, no libraries): before 5 Sept 2026 → "Opening Saturday 5 September, 12–6pm"; 5 Sept–24 Oct → "Now on view · Mon–Fri 10–6 until 24 October" (Version B countdown becomes "Now on view"); after 24 Oct → collapse to one quiet line ("*Unfiltered* was on view September–October 2026 at Sonya Winner Rug Studio"). Version C after 24 Oct: hide the flyers behind the same single line.
- **SEO/metadata:** update meta description to mention the show; add JSON-LD `ExhibitionEvent` (startDate 2026-09-05, endDate 2026-10-24, full postal address, organizer Sonya Winner Rug Studio).
- **Performance:** create resized copies of any image the sections use (max 1600px wide, target < 350KB, named `show-*.jpg`). Never overwrite originals. `unfiltered.jpg` (1.3MB), `camo-install.jpg` (2MB) and `golden-child-lauren.jpg` (2.6MB) are too heavy raw. Use ImageMagick if present, else Python/PIL.

## 4. Image mapping — flyer photos ↔ repo files (verified by inspection)

Confirmed matches — these are the images the flyer features, so A/B imagery draws from this set first:

| Flyer image | Repo file |
|---|---|
| Sunset painting (orange sky, blue sea, purple/sand bands) — about side, bottom-left | `bliss.jpg` (gallery shot; painting fills most of frame) |
| Lauren beside the carved sand-stone fish sculpture — about side, right | `golden-child-lauren.jpg` |
| Goldfish camouflaged in Lucky Charms painting (the "goldfish existence") | `camo-fish.jpg` (single canvas), `lucky-wide.jpg` (gallery install with rose painting), `lucky-close.jpg` (raking-light detail) |
| Namesake glass piece — teenage girl + strawberry Snapchat-style mask in glass tank | `unfiltered.jpg` (plus `unfiltered-side.jpg`, `unfiltered-back.jpg`) |
| Mother-and-child stone egg ("a mother slowly consumed by the fish" thread) | `seed-1.jpg`, `seed-2.jpg`, related `smother.jpg` |

Flyer photos with **no confirmed repo equivalent** (do not guess-substitute; use only if Ross uploads them, otherwise omit):

- Clear resin fish with candy-colour inclusions on white plinth (invite side, top-left)
- Lauren carving the blue resin fish with a rotary tool (invite side, top-right)
- Gold-flake resin fish (about side, centre)
- Blue resin fish cutouts (about side, floating motifs)
- Lauren's signature graphic

(The individual photos above can be cropped from the flyer JPGs at reduced quality if truly needed, but prefer omitting them in A/B over using soft crops.)

If Ross uploads any of these (any sensible filename), prefer them in A/B where the flyer features them, and re-check §6 weight limits.

## 5. Execution steps (Opus)

1. `git fetch origin claude/lauren-website-access-tdkl8g`, work on that branch, `git pull` first — Ross may have uploaded flyer images via GitHub since this plan was pushed. Check repo root for new image files before deciding Version C is blocked.
2. Build the variants as **full copies of the homepage** at `/preview-a/index.html`, `/preview-b/index.html`, `/preview-c/index.html`. Asset paths are root-relative (`/foo.jpg`) so they resolve when served from repo root; screenshot via local HTTP server (`python3 -m http.server`), not `file://`.
3. Screenshot all versions at 1440×900 and 390×844 (Chromium pre-installed for Playwright; do **not** run `playwright install`). Send screenshots to Ross via SendUserFile with a one-line comparison.
4. Commit + push (`git push -u origin claude/lauren-website-access-tdkl8g`; retry with backoff on network failure only).
5. **Stop and wait for the choice.** When Ross/Lauren pick: integrate the chosen version into `/index.html`, delete all `/preview-*` folders and this plan file, keep meta/JSON-LD, re-screenshot, commit, push. PR/merge to `main` only if Ross explicitly asks.

## 6. Acceptance checks

- Live `index.html` untouched until Step 5's second half.
- A and B contain the flyer's four "About" paragraphs and the invitation lines from §1 — check against the blockquotes, not from memory.
- A and B imagery drawn from the §4 confirmed-match set (plus any new uploads); no unrelated repo images promoted over flyer-featured ones.
- All previews render at 390px and 1440px; no horizontal scroll; text legible over imagery.
- Every image in the new sections < 350KB (display copies); full-res only behind click-through links in Version C.
- RSVP CTA scrolls to the form with "Private View RSVP" preselected; form still submits (verify preselection only — no test submissions).
- Date logic verified by temporarily overriding the date during testing (remove overrides before commit).
- Facts match §1 exactly — dates, times, postcode NW5 1ST, sonyawinner.com credit.
