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
| `index.html` | aurora hero | trust + audience band, who we serve, story teaser, framework, client-experience teaser, team snippet, recognition, closing CTA |
| `about.html` | **"What We Believe"** over the aurora | Chris's story, five questions, principles, **The Lume Framework**, credentials |
| `services.html` | — (solid Banner Text header) | who we serve, what we coordinate, closing CTA |
| `client-experience.html` | — (solid Banner Text header) | the rhythm, the year framed, seven disciplines, the service calendar, closing CTA |
| `calculators.html` | — (solid Banner Text header) | calculator index, closing CTA |
| `newsletters.html` | — (solid Banner Text header) | issue archive, closing CTA |
| `team.html` | — (solid Banner Text header) | team with contact + bios, credentials, community |
| `contact.html` | — (solid Banner Text header) | contact |

**Onward path:** About → Services → Client Experience → Team → Contact. Each interior page
ends in a `.next-step` card pointing at the next one, so no page dead-ends. Resources is a
side branch off that arc, not a stop on it: Calculators → Newsletters → back to Client
Experience, which is where a visitor in research mode is best handed off.

**Resources is the site's only nav submenu.** "Resources" is a primary item that drops down
to Calculators and Newsletters. Still no JavaScript: hover opens it and `:focus-within`
opens it for keyboard users. The closed state uses `opacity` + `pointer-events` rather than
`display:none` or `visibility:hidden`, because either of those makes the submenu links
unfocusable — Tab would skip them and Newsletters would be unreachable by keyboard. The
parent is also a real link to Calculators, so the menu is never the only route in, and the
mobile drawer has no dropdown at all: Resources is a group label with both pages already
listed beneath it.

**Both Resources pages are deliberately plain** — a category heading over a list of links,
no cards, no icons, no counts, no per-item blurbs on Calculators. Someone on those pages
arrived knowing what they wanted. Newsletters carries a one-paragraph summary per issue
because an archive needs it to be scannable; the issues themselves are PDFs, not pages.

**The homepage is a hub.** Every band previews an interior page and ends in a link to it,
so a referral visitor can answer *who are these people, do they work with people like me,
are they legitimate, and what happens if I call* without clicking. Nav is a fallback for
people already convinced, not a bridge.

**The Framework is split.** The five process stages live on About (how the firm works is
identity); "what we coordinate" — the three disciplines — stays on Services (scope of
service is offering). They were always two separate TWM sections sharing one heading.

**Client Experience carries the Private Wealth Service Calendar** — 34 planning activities
across 7 disciplines, mapped to the two annual meetings. It maps to Banner Text 1,
Multi-Item Content 4, Sequential Content 2, Highlights 2, Multi-Item Content 1 and
Singular Content 3, and leaves its Hero Banner allowance unspent like its siblings.
Everything reuses an existing shell except the calendar rows themselves, which add one
new component (`.cal-*`, marked `PROPOSED ADDITIONS` in `lume.css`).

**The calendar is deliberately not an accordion.** Those 34 rows are the page's entire
argument, so none of them sits behind a click: all seven discipline groups render open.
Multi-Item Content 1 is documented as an accordion, which makes this the one section on
the site that is not a verbatim reuse of an approved pattern — see Known gaps.

**Numbers only where there is a sequence.** Decorative `01–0n` badges were sitting on
things that aren't ordered — five kinds of question, four commitments, seven disciplines,
four client types — which implies a rank or a running order none of them have, and reads
as ornament rather than information. They are gone from the About questions and
principles, the service calendar, and Who We Serve on both Services and the homepage.
**The Lume Framework keeps its 01–05**: those are five stages that genuinely run in order.
The same rule applies to prose — "Seven disciplines, coordinated as one engagement" and
"Three disciplines, run as one engagement" were counting for emphasis rather than saying
anything, and were rewritten.

**The About questions are no longer an accordion.** Nothing signalled the cards could be
clicked, so the answers read as missing rather than hidden — the disclosure was working
against the content. Question and answer are now both visible in a 2-column card grid
(Multi-Item Content 4), with type size carrying the hierarchy instead of a control. Same
reasoning as the service calendar on Client Experience.

**One section, one job.** Services used to run Who We Serve → What We Coordinate →
Capabilities, and the third restated the first two: "Executive & Equity Compensation"
repeated Who We Serve card 02, "Risk & Protection" repeated What We Coordinate's Wealth
Protection, and so on. Capabilities is removed. Services is now WHO and WHAT; Client
Experience is WHEN, and proves the depth claim with dated activities instead of asserting
it a third time. Its icon tiles reuse `.cap-grid`/`.cap-card`, which is why those rules
stay in `lume.css`.

**Forbes badges, not text pills.** The awards were previously rendered as text with a gold
star drawn in-house, which reads as a self-awarded ribbon. They are now the licensed
Forbes/SHOOK badges, cropped from the supplied composite (which was one image saved under
three identical filenames). Both appear on the homepage only, and the SHOOK
disclosure travels with them — About and Team carry credential marks
alone, which make no ranking claim and so need no disclosure.

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
- **Bios are flip cards.** An accordion was wrong for a grid: a row stretches to its
  tallest item, so opening one bio pushed every card in that row taller. Clicking anywhere
  on a card turns it over. Driven by a visually-hidden checkbox — still no JavaScript,
  still keyboard-operable — with contact links layered above the trigger so they stay
  independently clickable. Reduced-motion users get an instant face swap.

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
- **A second nav level is unconfirmed.** The Resources dropdown is the one piece of chrome
  in this build with no equivalent already proven elsewhere on the site — whether the TWM
  nav component supports a submenu at all is unknown. If it does not, the fallback is two
  flat primary items, but see the width note below: there is no room for them.
- **The nav bar is full.** Six primary items, two of them long ("Client Experience",
  "Resources"), plus the two-logo lockup, phone and CTA is roughly 1170px of content in a
  1200px container. The drawer breakpoint moved 1080px → 1120px and the squeeze band to
  1121–1319px to hold it. **A seventh primary item does not fit** — anything further has
  to go under a submenu or into the footer.
- **Newsletter content is entirely placeholder.** All six issues on `newsletters.html` are
  invented for visual reference; no real issues were supplied. Their hrefs point at
  `newsletters/<slug>.pdf`, which does not exist — clicking one 404s deliberately rather
  than resolving to `#` and looking functional. Drop the real PDFs into a `/newsletters`
  directory and the links resolve as written. Replace every title, date and summary.
- **"Retirement Income Calculator" is filed under Insurance,** as supplied. It reads oddly
  beside life, LTC and disability. Left where it was given rather than moved — confirm with
  Lume whether it wants its own Retirement category, which would make the grid seven and
  wrap 3 + 3 + 1.
- **Calculator links leave the site** for Northwestern Mutual properties and open in a new
  tab. The new tab is announced once above the grid rather than on each of the 28 links,
  which at that density would be noise rather than help — worth confirming that satisfies
  NM's accessibility standard.
- **Centred incomplete final row.** The framework's five stages used to run 3 + 2 with the
  bottom-right cell empty, which read as a missing sixth stage. `.steps` is now a six-track
  grid with each tile spanning two, so stages 04 and 05 centre under the three above.
  Whether Sequential Content 2 centres an incomplete final row is unconfirmed — most
  builders left-align. Fallback: delete the two `nth-child` rules and set
  `grid-template-columns: repeat(3, 1fr)`. Nothing else depends on it.
- **The Forbes disclosure omits "Best-in-State"; the badges don't.** Confirmed against
  Lume's live site: the artwork for both awards reads **BEST-IN-STATE**, and the body copy
  beside it says "in the state of Ohio" — but the approved SHOOK disclosure names the
  lists as "Forbes Top Financial Security Professionals" and "Forbes Top Next-Generation
  Wealth Advisors", with no Best-in-State. The discrepancy exists in the source copy and
  has not been silently corrected here: approved regulated language is quoted, not
  edited. Raise with NM — either the disclosure should name the Best-in-State lists, or
  the badges are the wrong artwork. **Resolved for now:** "Ohio" stays on both captions
  and in the homepage trust bar, because dropping it from a state ranking would overstate
  the award.
- **The live disclosure carries a malformed date.** It reads "Forbes Top Financial
  Security Professionals list (July 2025.2024)", which appears to fold the 2025 and 2024
  lists under a single data date. Only the 2025 badge is shown, so the copy here resolves
  to "(July 2025)". This is also why the 2024 Best-in-State badge in the supplied
  composite is still unused: every award shown must carry an unambiguous data date, and
  that date is precisely what the typo obscures. Worth fixing on the live site too.
- **Always-expanded Multi-Item Content 1** — the service calendar needs its seven items
  rendered open, not as an accordion. If TWM cannot suppress the reveal, the fallback is
  Multi-Item Content 4 (2-column) with Tax Planning spanning both columns; the other six
  balance 5\|4, 4\|4, 2\|3.
- **The service calendar's activity counts are unverified.** The source PDF labels
  Investments "6 planning activities" but lists 5. No count — per discipline or sitewide —
  is stated anywhere in live copy until Lume resolves it. All 34 EY/MY/YE tags were
  hand-transcribed from a dot-matrix table and want a second proofread against the source.
- **Client Experience needs its own compliance pass.** The source PDF is approved print
  collateral, but permanent public web content is reviewed differently. The
  "activities and cadence may vary by individual circumstances" caveat wording is
  provisional.
- **Geography claims were removed, not replaced.** "Serving Central Ohio" is gone from the
  hero, title, meta and all footers, but no national claim replaced it — the site's own
  disclosure states Chris is licensed in Ohio and California. An affirmative "nationwide"
  claim needs compliance sign-off and licensing to match. The office address, the Forbes
  "Ohio · 2025" captions (the SHOOK award is state-scoped) and the community section are
  deliberately untouched.
- **Contact form field configurability** is unconfirmed.
- **Third-party award logos sit outside the NM brand library.** The Forbes badges are
  licensed, but their use on the site still wants compliance sign-off, and they are black
  tiles with red/green accents — off both the site palette and the NM PCG palette.
- **The supplied composite also held a 2024 badge** — the prior year of Top Financial
  Security Professionals, the same award as one of the 2025 badges rather than a separate
  accreditation. It is not used: its disclosure data date could not be sourced from
  approved collateral, and every award shown must carry one.
- **Chris Moore has no published email.** The current site omits it too, so it is treated
  as deliberate; his card carries his phone plus a link to the contact form.
- **614-221-5287 is a shared office line** for Connor, Sydney and Kevin, not a direct line.

## Local preview

```
python -m http.server 8940
```
