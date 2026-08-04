# Lume Capital — TWM structural variant

A parallel build of the Lume Capital site, restructured to fit the section catalogue in
Northwestern Mutual's **TWM** page builder (`NWM - Site Structure.pdf`). It exists to be
evaluated side by side against the current single-page site, which lives in its own repo
and is unchanged.

The bar is not pixel fidelity — it is that the sections and layouts here can actually be
assembled from what TWM ships.

## Pages

| Page | Hero Banner (1 max per page) | Sections |
|---|---|---|
| `index.html` | aurora hero | trust + audience band, story teaser, capabilities teaser, closing CTA |
| `about.html` | **"What We Believe"** over the aurora | Chris's story, five questions, four pillars |
| `services.html` | — (solid Banner Text header) | who we serve, Lume Framework, capabilities |
| `team.html` | — (solid Banner Text header) | team, recognition & community |
| `contact.html` | — (solid Banner Text header) | contact |

**Why Believe moved to About.** In TWM, copy sits directly on a photograph only in a Hero
Banner or Banner Text. Every Singular Content variant with a background image forces a
*white text box*, which would invert the design entirely. Home spends its single Hero
Banner on the aurora hero, so Believe could not stay there. As the About page's Hero
Banner it keeps its treatment intact.

## What changed from the single-page site

- **Scroll-reveal JavaScript removed.** The IntersectionObserver and all 56 `.reveal`
  classes are gone — movement on scroll is the one interaction TWM rules out. The mobile
  drawer is the only remaining script. Every page renders fully with JS disabled.
- **All 12 eyebrow labels removed.** No TWM section has an element above the Title. Where
  an eyebrow carried real information it was folded into the heading.
- **Grids reflowed to 3 columns** — pillars 4→3, process steps 5→3, team 4→3. The five
  questions dropped their 6-column span arithmetic and became the single-column accordion
  stack that Multi-Item Content 1 actually renders.
- **Hero reconfigured** to Title + Subtitle + one CTA. The two-tone glow headline is flat,
  the lead is compressed to subtitle length, and the trust bar moved into the band below.
- **Contact form truncated** to a single step: name, email, phone, message. The step
  dividers, advisor toggle and goal select are gone.
- **Team placeholder tile dropped** — the dashed "Growing, carefully." card wasn't a
  person and has no Team-section equivalent; its message moved to the page header.
- **Styles extracted** to a shared `lume.css` rather than duplicated across five pages.

## Deliberately unchanged

Per direction, these are resolved outside this build: the dial motif (17 uses, pending
approval), all inline SVG icons (to be swapped for NM library equivalents), typography,
the section background colors, and the two aurora images at their current resolution.

## Known gaps

- **Image resolution.** `hero-northern-lights.jpg` is 1254×836 and
  `belief-section-northern-lights.jpg` is 1230×852, against TWM's 1920×1080 Hero Banner
  minimum. Team headshots are 400×560 against a 483×600 spec. Re-export needed.
- **Community stats are not Counting Numbers tiles.** That function takes digits only —
  "no special characters or letters" — which rules out both `$20M+` and `Beads of Courage`.
- **Bulleted lists inside multi-item paragraphs** (Who We Serve) are unconfirmed with NM.
- **Sequential Content maximum tiles** is undocumented; the framework has five steps.
- **Contact form field configurability** is unconfirmed.

## Local preview

```
python -m http.server 8940
```
