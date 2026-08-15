# Impeccable Pre-Edit Layout Assessment

**Date:** 2026-08-15
**Branch:** `agent/registration-first-improvements`
**Target:** `index.html`
**Visitor mode:** Persuade
**Snapshot status:** Transitional pre-layout baseline
**Scope:** Isolated layout assessment only; `index.html` and site assets were not modified

> **Baseline integrity note:** The temporary server's only page request was at 15:09:53 ET, while a parallel agent first modified `index.html` at 15:13:31 ET. This assessment therefore captures the intended pre-edit baseline (Git blob `3c98dd4`), not the later in-progress implementation now visible in the shared worktree. Source line references below refer to that baseline. This assessment did not create, alter, or revert the concurrent site changes.

## Assessment Verdict

The registration-first reading path is structurally sound, responsive, and easy to recognize. The hero, registration choice, pricing, schedule, hotel, FAQ, proof imagery, and contact sequence all have understandable local layouts. The page does not need a new topology.

The pre-edit layout problem is **priority flattening**. Seven major desktop sections reuse the same 82 px vertical slab rhythm and nearly every repeated group receives a bordered/shadowed container, so pricing, schedule, galleries, FAQ, and the primary registration task increasingly feel equal in weight. The registration panel itself uses a full-width 1180 px shell around a maximum 760 px content column, leaving roughly 360 px of unused internal width on desktop. At the opposite extreme, the 390 px experience becomes 10,859 px tall, with FAQ and convention photos alone consuming 3,981 px—about 37% of the document.

The layout phase should preserve the current identity and component semantics while tightening the task funnel, reducing equal-weight section chrome, and making lower-priority proof content more compact.

## Mechanical Scan Status

**The prior detector command did not use `--scope layout`.** It was:

```sh
node /Users/matthewjudy/.agents/skills/impeccable/scripts/detect.mjs --json index.html
```

That one-time audit scan ran in degraded regex mode and cannot satisfy layout.md's scoped mechanical pass. Per the current instruction, the detector was **not rerun**. This document therefore remains the required isolated human/rendered assessment; a future implementation/final verification pass still needs an explicit scoped layout scan.

## Rendered Baseline

The current page was served in a fresh browser tab and inspected at 1440 × 900 and 390 × 844. Same-session evidence for the unchanged file also includes the 720 CSS-pixel reflow state used as a 200% desktop-zoom equivalent.

| Evidence | Wide: 1440 × 900 | Narrow: 390 × 844 |
|---|---:|---:|
| Sticky header height | 71 px | 123.7 px |
| Hero height | 675.9 px | 999.5 px |
| H1 box | 728 × 268.3 px | 362 × 131 px |
| Fact panel | 410 × 330.9 px | 362 × 330.9 px |
| Primary CTA group | 728 × 46 px | 362 × 104 px |
| Document height | 8,136 px | 10,859 px |
| Document horizontal overflow | None | None |
| Primary-nav viewport/content | Fits | 362/500 px horizontal scroller |

At 720 CSS px the document also remained 720 px wide with no page-level overflow. The main containers became one column and the navigation fit within its 680 px inner width.

## 1. Reading Order

**Verdict: strong at the top; progressively flatter below registration.**

The wide squint test has an unmistakable order: the large white H1 leads; the left hero copy and green registration CTA form the primary action cluster; the glass convention-facts panel supports on the right; the registration heading begins at the lower viewport edge. At 1440 px the hero uses a `1fr / 300–410 px` split (`index.html:263-272`), and the rendered H1 is almost twice the width of the facts panel. This makes the page's purpose legible even with detail blurred.

At 390 px the DOM and visual order remain: brand/navigation → H1/copy → full-width primary and secondary CTAs → convention facts → registration. The H1, both CTAs, and the beginning of the facts panel appear in the first viewport. Registration itself starts at document y = 1,123 px, but the in-viewport **Start Registration** anchor prevents the tall hero from blocking the task.

Below registration, the repeated section formula—eyebrow, large serif H2, bordered/shadowed content—makes every destination read as another coequal chapter. The source applies 82 px section padding globally (`index.html:471-480`), and the desktop render confirms the same padding on registration, pricing, schedule, hotel, hotel photos, FAQ, and convention photos. The sequence remains understandable, but priority contrast weakens.

## 2. Grouping

**Verdict: meaning is grouped correctly; container chrome is doing more work than necessary.**

- Hero copy, actions, and facts are correctly separated into one persuasive cluster and one supporting facts cluster.
- Registration tabs and the active role panel belong together and are correctly enclosed by one `.form-shell` (`index.html:618-681`). The tab/panel relationship is both visually and semantically clear.
- Three pricing cards are genuinely comparable choices, so an equal grid is appropriate (`index.html:517-529`, `index.html:1552-1570`).
- Schedule rows, FAQ disclosures, hotel thumbnails, and convention images are each internally consistent groups with meaningful repetition.
- The navy hotel section is a useful phase break rather than decorative variation.

The weakness is repeated enclosure. Cards, price cards, form shell, FAQ items, and event rows all receive borders, white surfaces, shadows, and hover elevation (`index.html:531-553`, `index.html:767-783`). Proximity already establishes many of these relationships, so the repeated component chrome gives support content the same visual mass as the registration decision.

The desktop registration shell is also wider than its content relationship warrants. After panel padding, approximately 1,122 px is available, but `.registration-card` stops at 760 px (`index.html:658-681`), leaving about 362 px unused on the right. The rendered panel therefore reads as a large container around a small task rather than a deliberately composed task region.

## 3. Rhythm

**Verdict: good local spacing scale; monotonous global cadence.**

Local rhythm has useful contrast:

- 6–18 px gaps bind labels, controls, cards, FAQ rows, and local metadata.
- 28–42 px gaps separate actions, columns, and section introductions.
- 62/82 px padding creates major phase changes at mobile/desktop.

This is not an arbitrary one-value implementation. The problem is where the largest interval is applied: seven sections repeat 82 px top and bottom padding on desktop, while all mobile sections settle at 62 px (`index.html:1293-1347`). Only desktop contact initially uses a distinct 58 px treatment (`index.html:743-755`), and the mobile breakpoint overrides it back to 62 px. Alternating white/gradient backgrounds helps, but the long page still becomes a sequence of similarly paced slabs.

The intended edit should retain tight local gaps, use medium separation within task-support clusters, and reserve the most generous breaks for true changes of phase—for example, from registration/decision support to destination information, and from practical information to social proof.

## 4. Structure

**Verdict: the topology matches the content; lower-priority visual proof is structurally overrepresented.**

The component models are generally correct:

- Hero split for promise plus facts.
- Role tabs for mutually exclusive registration paths.
- Equal pricing columns for comparable fees.
- Linear schedule rows for chronological content.
- Copy/image split for the venue.
- Horizontal hotel gallery for optional browsing.
- Disclosures for a long FAQ.
- Dense photo grid for social proof.
- Simple contact form at the end.

The main structural opportunity is to demote rather than delete proof content. Hotel photos currently receive their own 688 px desktop/584 px mobile section immediately after the hotel block, while 2026 convention photos consume 1,431 px desktop and 2,133 px mobile. The single-column mobile photo grid is eleven 160 px rows with 12 px gaps (`index.html:1123-1138`, `index.html:1358-1370`, `index.html:1398-1410`). That is faithful to the gallery but disproportionate to a registration task.

The page should keep the images, but the hotel gallery can behave as part of the hotel phase and the convention gallery can be a compact proof module rather than a full-length coequal chapter.

## 5. Density

**Verdict: appropriate in decision-heavy regions; too sparse in the desktop registration shell and too expansive in lower-priority mobile regions.**

- The hero's density is appropriate for Persuade mode: one promise, one concise paragraph, two actions, and four facts.
- Pricing uses enough detail to compare three outcomes without overloading the cards.
- FAQ correctly uses progressive disclosure; thirteen questions do not all compete at once.
- Schedule density is intentionally low because much of the agenda is still pending.
- The desktop registration panel is under-filled: its active content occupies only about two-thirds of the available inner width.
- On mobile, the 124 px sticky header consumes 14.7% of the viewport before content begins, and its final two primary links require horizontal discovery.
- Mobile FAQ (1,848 px) plus convention photos (2,133 px) dominate the lower document. Their combined height is larger than registration, pricing, and hotel sections together.

The layout edit should increase information efficiency around registration without making controls smaller, then reduce lower-page travel by compacting proof imagery and avoiding unnecessary card height/chrome.

## 6. Adaptation

**Verdict: technically robust reflow with two mobile navigation issues and no validated localization contract.**

Current structural adaptation is coherent:

- At 900 px and below, hero, pricing, field grids, schedule rows, hotel split, footer, newsletter, and speaker modal collapse to one column (`index.html:1293-1322`).
- Registration tabs stack vertically, and the active panel follows them in DOM order (`index.html:1349-1356`).
- At 560 px and below, CTA, registration, and form buttons become full width; the photo grid becomes one column (`index.html:1373-1411`).
- Schedule date → content → speaker image, hotel copy → image, and hero copy → facts retain the same DOM and visual order after stacking.
- The 720 CSS-pixel zoom-equivalent layout has no document overflow.

The two mobile navigation concerns are:

1. The header grows from 71 to 123.7 px because brand and navigation become two rows.
2. `.nav-links` uses `white-space: nowrap` plus horizontal scrolling (`index.html:198-212`, `index.html:1293-1304`). At 390 px, **FAQ** begins beyond the right edge and **Photos** is fully offscreen without a continuation cue.

Localization was not available to render. Source resilience is mixed but reasonable: global links can wrap anywhere, actions flex-wrap, grids use `minmax(0, 1fr)`, and narrow buttons become full width. Longer primary-navigation labels would simply increase the hidden horizontal extent, however, and the nearly full-width brand block leaves little reserve at 390 px. Treat translated expansion as unverified, not passed.

## 7. Extremes

**Verdict: ordinary long content holds; overlays, touch size, and safe-area handling expose the remaining structural risks.**

- **Long content:** The longest FAQ summary and hotel rate item wrap without page overflow. `minmax(0, 1fr)`, flexible heights, and `overflow-wrap: anywhere` prevent hard clipping.
- **Empty states:** The static page has no conditional empty-state surface. No layout behavior exists to assess; future dynamic schedule/gallery removal should not leave an empty full-height section.
- **Dialog overlay:** Same-session 390 × 844 testing of the unchanged source found that the speaker dialog opens at `scrollTop: 191` because focus moves to the bottom **Close bio** control. The dialog card begins at y = −172, so its leading media is already scrolled away. The title remains visible, but the initial orientation is not top-aligned (`index.html:880-931`, `index.html:1825-1845`).
- **Sticky/fixed elements:** The sticky header remains stable and the sampled visible 89 × 40 px **Back to top** control did not intersect another interactive target. It still occupies bottom-right content space whenever visible.
- **Safe areas:** No CSS uses `env(safe-area-inset-*)`. The mobile floating control is fixed 14 px from the bottom/right (`index.html:1390-1395`), so home-indicator clearance is not guaranteed on an installed/full-screen mobile surface.
- **Touch targets:** Same-session rendered measurements found 34 px for the brand link, 37.7 px for primary nav links, 21.7 px for **View speaker bio**, and 40 px for **Back to top**. The visual marks can stay compact, but the interaction boxes need a 44 px floor.
- **Dense placement:** The convention gallery uses `grid-auto-flow: dense`; current one-column mobile order agrees with DOM order. Any future spanning-card changes at wider widths must be checked so visual placement does not outrun source/reading order.

## Spatial Thesis for the Layout Edit

### Primary reading and task path

**Promise and essential facts → start registration → choose role → understand price and schedule → resolve hotel/FAQ questions → review optional social proof → contact support.**

### What belongs together

- Hero promise, core facts, and the registration CTA are one entry phase.
- Role tabs and one active registration action are one indivisible task unit.
- Pricing, schedule, hotel logistics, and FAQ are decision-support information; they should feel related without becoming one giant container.
- Hotel imagery belongs with the hotel phase.
- Convention imagery is optional proof and should be visually subordinate to registration and planning information.
- Contact is a separate recovery/support phase.

### Lead and support

Registration leads. Event facts, price, schedule, hotel, and FAQ support the decision. Photography supplies confidence and energy; it must not own more page travel than the task it supports.

### Intended density and rhythm

Use a dense, decisive top half; tight spacing inside semantic groups; medium separation between related decision-support sections; and generous spacing only at phase boundaries. Reduce empty shell area and repeated card elevation before reducing readable control padding.

### Structural adaptation

- Wide: preserve the asymmetric hero and comparable pricing grid; size the registration task region to its content or use the spare width for genuinely useful support.
- Intermediate/zoomed: retain one-column reflow and no document overflow; keep primary navigation fully discoverable.
- Narrow: compact the header, preserve full-width primary actions, keep DOM/visual order aligned, and compress galleries without shrinking touch targets.
- Long/localized content: allow height growth and wrapping without offscreen primary actions; do not rely on a hidden horizontal nav as the only expansion strategy.
- Overlays/safe areas: start long dialogs at their beginning, maintain focus order, and respect bottom/right safe-area insets.

## Pre-Edit Priorities

1. Tighten the desktop registration shell around the task or give its spare column a real purpose.
2. Replace the equal 82 px section cadence with semantic phase spacing.
3. Reduce repeated card/shadow enclosure where proximity and dividers can carry grouping.
4. Fold hotel imagery into the hotel phase and compact the convention proof gallery, especially on mobile.
5. Rework the mobile header/navigation so all primary destinations are discoverable without a hidden horizontal continuation.
6. Correct mobile dialog start/focus, 44 px interaction boxes, and safe-area offsets.
7. Preserve the current hero hierarchy, DOM order, tab relationships, progressive FAQ density, and overflow-free reflow.

After the layout edit, run the missing `--scope layout` detector pass, verify the same wide/narrow/zoom states, and hand the result to `$impeccable polish`.
