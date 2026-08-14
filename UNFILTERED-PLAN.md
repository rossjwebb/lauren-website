# Plan: "Unfiltered" Exhibition Section — laurensuper.com

**Status:** Awaiting execution. Do not modify the live `index.html` until Ross/Lauren choose a version (Step 5).
**Branch:** All work on `claude/lauren-website-access-tdkl8g`. Never push elsewhere.
**Goal:** Announce Lauren Super's solo show "Unfiltered" at the top of the homepage — as a designed, native section (NOT the flyer image pasted in). Build **two distinct versions** for Lauren to choose from.

---

## 1. The facts (single source of truth — use exactly these)

- **Show:** *Unfiltered* by Lauren Super — her solo exhibition
- **Venue:** Sonya Winner Rug Studio, 14 York Rise, London NW5 1ST
- **Opening:** Saturday 5 September 2026, 12–6pm — coinciding with the 2026 **York Rise Street Party**. Meet the artist; British wine + artisan cheese at the rug showroom.
- **Continues:** Monday–Friday, 10am–6pm, until **24 October 2026**
- **Host credit:** Presented at Sonya Winner Rug Studio — link to https://www.sonyawinner.com
- **Curatorial arc (condense, don't copy verbatim):** It begins in the garden — botanical paintings (Cape Town sunsets, hibiscus, cosmos on deep black grounds), made as survival and mindfulness, standing for a natural beauty the modern world is losing. From there the work darkens: masks drawn from her African heritage; a teenager's "goldfish existence" seen through a Snapchat filter; a mother slowly consumed by the fish; the architects of the feed, fishing for the next generation.
- **Maps link:** `https://maps.google.com/?q=Sonya+Winner+Rug+Studio,+14+York+Rise,+London+NW5+1ST`

Today is mid-August 2026, so the section launches in "opening soon" state (~3 weeks out).

## 2. Design constraints (both versions)

- Site language: single-file pages, inline CSS, Georgia serif, paper palette (`--bg:#f5f0eb`, `--ink:#2c2c2c`, `--rule:#d4cdc3`). Both versions must feel like *this site*, not like the Sonya flyer. No bunting, no Sonya branding beyond the credit line.
- Use existing repo images only (see §4). The flyer JPGs are not in the repo and must not be embedded.
- Mobile-first: most visitors will arrive from Instagram/WhatsApp on phones. Test at 390px.
- Placement: the very top of the homepage, per Lauren's request. Everything currently on the page stays, pushed down.

## 3. The two versions

### Version A — "Editorial announcement" (quiet, gallery-journal style)

Fully inside the existing aesthetic. Structure, top to bottom:

1. A slim full-width ribbon at the very top of the page (above the `Lauren Super` header): small-caps text — "Solo exhibition · *Unfiltered* · Opens 5 September — Sonya Winner Rug Studio, London NW5" — the whole ribbon anchors down to the section. Paper-dark background (`--accent` on `--bg` inverted or a thin-ruled band), no loud colour.
2. Existing header (`Lauren Super` / tagline) unchanged.
3. **Exhibition section between the header and the hero video**, framed by dotted rules (a quiet nod to the flyer's dotted dividers): eyebrow "First Solo Exhibition", large serif *Unfiltered*, dates/venue block in letterspaced small caps, 2–3 sentence curatorial text from §1, then a **triptych image strip** mirroring the show's arc — one botanical painting, one resin fish, the Unfiltered sculpture (suggest `hibiscus-purple.jpg` / `lucky-close.jpg` / `unfiltered.jpg`, but judge crops on screenshots).
4. Text CTAs (underlined text links, not buttons): "RSVP for the opening" → anchors to the inquiry form; "Getting there" → Maps link; "Presented at Sonya Winner Rug Studio" → sonyawinner.com.

### Version B — "Immersive takeover" (bold, full-bleed hero)

The show takes over the top of the page before the regular site begins:

1. Full-viewport-height (min ~85vh) dark hero at the very top: background `camo-install.jpg` or `unfiltered.jpg`, dimmed toward near-black with a gradient — echoing the deep-black grounds of the paintings. Light Georgia type: eyebrow "Lauren Super — Solo Exhibition", huge *Unfiltered*, dates + venue, one line on the Street Party opening.
2. A **countdown to the opening** ("Opens in 21 days") that automatically flips state — see §5 date logic.
3. Two CTAs as buttons: "RSVP for the opening" (anchor to form) and "Directions" (Maps). One restrained accent colour drawn from the resin-fish turquoise (~`#2b9aa8` family) for hover/accents only — never for body text.
4. A scroll cue ("↓ Enter the work") leading into the untouched existing homepage below (header, video, statement, cards…).

### Shared mechanics (both versions)

- **RSVP wiring:** add `<option value="Private View RSVP">Private View RSVP — 5 September</option>` to the inquiry `select`. RSVP CTAs link `#inquiries` and a tiny script preselects that option when the hash/query indicates RSVP (e.g. `#rsvp` → scroll to form + preselect). Keep the existing Web3Forms setup untouched otherwise.
- **Date-aware copy** (small inline script, no libraries):
  - Before 5 Sept 2026: "Opening Saturday 5 September, 12–6pm"
  - 5 Sept – 24 Oct: "Now on view · Mon–Fri 10–6 until 24 October" (Version B countdown becomes "Now on view")
  - After 24 Oct: render a single quiet line ("*Unfiltered* was on view Sept–Oct 2026 at Sonya Winner Rug Studio") — so the site never advertises a finished show. Server-side dates aren't available; client `Date` is fine here.
- **SEO/metadata:** update the meta description to mention the show; add JSON-LD `ExhibitionEvent` (name, startDate 2026-09-05, endDate 2026-10-24, location with full postal address, organizer Sonya Winner Rug Studio).
- **Performance:** create resized copies for any image the section uses (max 1600px wide, target < 350KB; e.g. `show-hibiscus.jpg`). Do not overwrite originals. `unfiltered.jpg` (1.3MB) and `camo-install.jpg` (2MB) are too heavy to use raw, especially as a hero. Use ImageMagick if present, else a tiny Python/PIL script.

## 4. Available assets (repo root)

Namesake piece: `unfiltered.jpg`, `unfiltered-side.jpg`, `unfiltered-back.jpg`. Resin fish (on the flyer): `lucky-wide.jpg`, `lucky-close.jpg`, `lucky-closer.jpg`, `camo-fish.jpg`, `camo-close.jpg`, `camo-install.jpg`. Botanicals: `cosmos.jpg`, `cosmos-eye.jpg`, `hibiscus-*.jpg`, `bliss*.jpg`, `peony.jpg`. Artist at work: `golden-child-lauren.jpg`. Stone/ceramic: `leroy*.jpg`, `mark-*.jpg`, `smother.jpg`, `seed-*.jpg`, `milk-splat.jpg`.

If Lauren later wants the actual flyer downloadable, Ross must add the flyer JPGs to the repo first (they exist only in chat); an optional "View the flyer" lightbox can then be added to the chosen version. Not part of this build.

## 5. Execution steps (Opus)

1. `git fetch origin claude/lauren-website-access-tdkl8g` and work on that branch.
2. Build both variants as **full copies of the homepage** at `/preview-a/index.html` and `/preview-b/index.html` (fix root-relative asset paths if needed — they're `/foo.jpg`, so they resolve fine when served from repo root; note `file://` viewing will break them, so screenshot via a local HTTP server, e.g. `python3 -m http.server`).
3. Screenshot both versions at 1440×900 and 390×844 (Chromium is pre-installed for Playwright; do **not** run `playwright install`). Send all four screenshots to Ross via SendUserFile with a one-line comparison.
4. Commit + push the branch (`git push -u origin claude/lauren-website-access-tdkl8g`, retry with backoff on network failure only).
5. **Stop and wait for the choice.** When Ross/Lauren pick: integrate the chosen version into `/index.html`, delete both `/preview-*` folders and this plan file, update meta/JSON-LD, re-screenshot, commit, push. PR/merge to `main` only if Ross explicitly asks.

## 6. Acceptance checks

- Live `index.html` untouched until Step 5's second half.
- Both previews render correctly at 390px and 1440px; no horizontal scroll; text legible over imagery.
- Every image in the new section < 350KB; hero paint is not blocked by a multi-MB download.
- RSVP CTA scrolls to the form with "Private View RSVP" preselected; form still submits (don't spam real submissions — verify preselection only).
- Date logic verified by temporarily overriding the date in DevTools/script during testing (remove overrides before commit).
- All facts match §1 exactly — dates, times, postcode NW5 1ST, sonyawinner.com credit.
