# Impeccable Technical Audit — 2027 FCI Convention Registration

**Date:** 2026-08-15
**Branch:** `agent/registration-first-improvements`
**Target:** `index.html`
**Mode:** Read-only pre-implementation audit; no site code was changed

> **Baseline note:** This audit records the page state inspected before the registration-first implementation was complete. Its findings are intentionally preserved as the technical baseline. See `2026-08-15-impeccable-post-implementation-qa.md` for the final disposition and current-branch verification.

## Implementation Integrity Verdict

**PASS, with release-significant performance and interaction gaps.** The implementation is a coherent, product-specific convention registration surface rather than an interchangeable template: it uses FCI identity and event-specific dates, pricing, registration paths, hotel links, approved convention photography, and a named keynote speaker. The document also has a clear semantic spine, consistent component vocabulary, and focused vanilla JavaScript.

The main integrity weakness is functional expectation-setting: the contact form's **Send Message** action does not send a message or call a form endpoint; it constructs a `mailto:` URL and depends on a configured local mail client. Performance is the largest technical weakness. A 17.15 MB autoplay video and every below-the-fold image are loaded eagerly.

The bundled detector was run **exactly once**. It exited in degraded regex mode because `htmlparser2`, `css-select`, `css-tree`, and `domutils` were unavailable, so custom-property resolution, selector matching, and computed contrast were not evaluated. Its output is an undercount, not a clean bill of health. All three emitted findings were checked against source context; one is retained as P3 and two are false positives described below.

## Audit Health Score

| # | Dimension | Score | Key finding |
|---|---|---:|---|
| 1 | Accessibility | 2/4 | A 12 px coral keynote label is approximately 3.1–3.4:1 on its light card, below WCAG AA. |
| 2 | Performance | 1/4 | The initial experience can fetch a 17.15 MB autoplay video plus about 5.48 MB of unique still-image files. |
| 3 | Theming | 3/4 | Core colors are tokenized, but several component surfaces bypass those tokens and there is no alternate theme contract. |
| 4 | Responsive Design | 3/4 | No document overflow at tested widths, but mobile navigation discoverability, touch targets, and modal start position need work. |
| 5 | Implementation Integrity | 3/4 | Product-specific and coherent; contact transport and one reduced-motion control state are misleading. |
| **Total** |  | **12/20** | **Acceptable — significant work needed** |

## Executive Summary

- **Audit Health Score:** 12/20 (Acceptable)
- **Verified issues:** 9 total — P0: 0, P1: 3, P2: 4, P3: 2
- **Top risks:** oversized eager media payload, mail-client-dependent contact form, failing small-text contrast, a reduced-motion video control that can claim an invisible video is playing, and a mobile dialog that opens 191 px down its own scroll area.
- **Release priority:** fix the three P1 findings before release; address modal orientation, touch/navigation ergonomics, and reduced-motion state in the same hardening pass.

## Scope and Evidence

The page was served temporarily at `http://127.0.0.1:4173/` and inspected in a fresh browser-managed Chrome tab. Verification covered:

- Desktop at 1440 × 900.
- Mobile at 390 × 844.
- A 720 CSS-pixel layout, equivalent to the reflow width produced by 200% browser zoom from a 1440-pixel baseline; native page scaling at 2× was also available and reset after inspection.
- `prefers-reduced-motion: reduce`, applied and then reset.
- Keyboard/focus behavior for the registration tabs and dialog focus return.
- Mobile touch-target dimensions, sticky/fixed elements, document overflow, intentional horizontal scrollers, and modal initial scroll position.
- Runtime image/video readiness and local asset sizes.
- Contact form validity structure, direct `mailto:` links, and generated `mailto:` construction. The final mail-client handoff was not invoked because it would leave the browser and does not prove delivery.

Observed runtime facts:

- No broken image assets; the video reached ready state 4 with a 1280 × 720 intrinsic size.
- No document-wide horizontal overflow at 1440 px, 720 px, or 390 px.
- At 390 px, the primary navigation is a deliberate 362/500 px horizontal scroller and the hotel gallery is a deliberate 362/1384 px scroller.
- Nineteen `<img>` nodes are present and none uses `loading="lazy"`; the browser observed 18 image URL entries, including a repeated local image under two query strings.
- The 20-second H.264/AAC hero video is 17,146,463 bytes at approximately 6.86 Mbps. Unique still-image files used by the page total approximately 5.48 MB.
- Registration tabs responded correctly to click, Arrow Right, Home, and End, updating focus, `aria-selected`, roving `tabindex`, and the visible tabpanel.
- Closing the speaker dialog returned focus to **View speaker bio** on both desktop and mobile.

## Detailed Findings by Severity

### P1 — Major

#### [P1] Autoplay media and eager galleries create an excessive initial payload

- **Location:** `index.html:238-252`, `index.html:1140-1148`, `index.html:1441-1444`, `index.html:1637-1659`, `index.html:1769-1780`; `assets/videos/fci-convention-2026-hero-720p.mp4`
- **Category:** Performance
- **Impact:** Visitors on mobile, constrained Wi-Fi, or metered connections can spend more than 22 MB to reach a single static page. The autoplay video is 17.15 MB by itself, and all below-the-fold galleries load immediately. This delays useful content, consumes data, and makes the page fragile under real convention travel conditions.
- **WCAG/Standard:** Web performance best practice; related to WCAG 2.2 usability for users with limited bandwidth, although no single WCAG success criterion sets a byte budget.
- **Recommendation:** Re-encode the hero into materially smaller modern and fallback sources, provide a lightweight poster-first experience, and defer video loading until interaction or an appropriate connection/device signal. Add `loading="lazy"`, `decoding="async"`, intrinsic dimensions, and responsive `srcset`/`sizes` to below-the-fold images. Keep the keynote image and first meaningful hero asset prioritized; do not lazy-load the initial visual needed for LCP.
- **Suggested command:** `$impeccable optimize`

#### [P1] “Send Message” only opens a local email draft

- **Location:** `index.html:1456`, `index.html:1754-1756`, `index.html:1794-1819`, `index.html:1983-1999`
- **Category:** Implementation Integrity
- **Impact:** The contact form looks like a web submission, but submitting it only navigates to a `mailto:` URI. Users without a configured mail handler may see nothing useful; other users can abandon the draft without any delivery confirmation. There is no server receipt, loading state, success state, failure state, or durable copy, so a registration-support request can be lost.
- **WCAG/Standard:** Functional integrity and clear feedback; if retained as a form workflow, apply WCAG 2.2 3.3.1/3.3.3 and 4.1.3 to error, guidance, and status feedback.
- **Recommendation:** Prefer a reliable server-backed submission with explicit success/error states, spam protection, and a visible email fallback. If `mailto:` is intentionally the only transport, rename the action to **Open Email Draft**, explain that an email app is required, and keep the address selectable nearby. Do not present draft creation as message delivery.
- **Suggested command:** `$impeccable harden`

#### [P1] Small coral keynote text fails WCAG AA contrast

- **Location:** `index.html:847-864`, markup at `index.html:1590`
- **Category:** Accessibility / Theming
- **Impact:** The 12 px all-caps **Featured Keynote** label is difficult to read for low-vision users and in glare. `--coral` (`#e95f45`) measures about 3.12:1 on `#fff3ee` and 3.39:1 on white; both are below the 4.5:1 requirement for normal-size text.
- **WCAG/Standard:** WCAG 2.2 1.4.3 Contrast (Minimum), Level AA.
- **Recommendation:** Use a darker semantic coral/text token that reaches at least 4.5:1 across the entire featured-card gradient, or use an existing high-contrast token such as navy/teal-dark while retaining coral as a non-text accent. Recheck every state, not only the gradient endpoint.
- **Suggested command:** `$impeccable colorize`

### P2 — Minor

#### [P2] Reduced-motion users can “play” a video that remains visually hidden

- **Location:** `index.html:114-126`, `index.html:1175-1179`, `index.html:1879-1900`
- **Category:** Accessibility / Implementation Integrity
- **Impact:** Reduced motion initially behaves well: smooth scrolling is disabled, the video pauses, and the poster remains. However, the still-visible control changes to **Play background video preview** while CSS permanently sets the video to `display: none`. Activating it was verified to set `aria-pressed="false"`, change the label to **Pause**, and start the hidden video. The announced state and visible result diverge.
- **WCAG/Standard:** WCAG 2.2 4.1.2 Name, Role, Value; reduced-motion interaction consistency.
- **Recommendation:** In reduced-motion mode, either hide/disable the toggle and leave the poster as the intentional alternative, or let explicit user activation reveal and play the video while preserving a clear way to pause. Keep the visible result, playback state, `aria-pressed`, and accessible name synchronized.
- **Suggested command:** `$impeccable harden`

#### [P2] Mobile speaker dialog opens partway down its own scroll area

- **Location:** `index.html:880-931`, `index.html:1293-1334`, `index.html:1825-1845`, `index.html:1947-1960`
- **Category:** Accessibility / Responsive Design
- **Impact:** At 390 × 844, opening the dialog produced `scrollTop: 191` in an 806 px-tall dialog with 997 px of content. The card began at y = −172 and focus landed on the only focusable control, **Close bio**, near the bottom. The title remained visible, but the leading image and top-of-dialog orientation were skipped, which is disorienting for keyboard and magnification users.
- **WCAG/Standard:** WAI-ARIA Authoring Practices modal-dialog initial-focus guidance; related to WCAG 2.2 2.4.3 Focus Order.
- **Recommendation:** Put an accessible close control near the dialog start and move initial focus to it, or make the title/static introductory element programmatically focusable (`tabindex="-1"`) and focus it when long content would otherwise scroll. Explicitly reset the dialog scroll position before focus and verify the full 390 × 844 state.
- **Suggested command:** `$impeccable adapt`

#### [P2] Repeated interactive targets are below the 44 × 44 px touch recommendation

- **Location:** `index.html:208-212`, `index.html:415-424`, `index.html:1258-1291`, `index.html:1373-1395`; instances at `index.html:1428-1435`, `index.html:1594`, `index.html:1869`
- **Category:** Accessibility / Responsive Design
- **Impact:** At 390 px, the brand link measured 34 px tall, primary navigation links 37.7 px, **View speaker bio** 21.7 px, and **Back to top** 40 px. The controls are usable, but they demand more precision from users with motor impairments or while holding a phone one-handed. The text-style speaker button is the weakest target.
- **WCAG/Standard:** WCAG 2.2 2.5.8 Target Size (Minimum) uses 24 px with spacing exceptions; WCAG 2.5.5 and common mobile guidance recommend 44 × 44 px. The isolated speaker control may qualify for the spacing exception but still misses the requested 44 px touch floor.
- **Recommendation:** Give text actions a real minimum block size using padding/min-height while keeping their visual treatment quiet. Raise mobile nav and floating-control hit areas to at least 44 px without relying on the text's line box.
- **Suggested command:** `$impeccable adapt`

#### [P2] Mobile primary navigation hides destinations without an overflow cue

- **Location:** `index.html:198-212`, `index.html:1293-1304`; markup at `index.html:1428-1435`
- **Category:** Responsive Design
- **Impact:** At 390 px, the navigation viewport is 362 px wide while its content is 500 px. **FAQ** begins beyond the right edge and **Photos** is completely offscreen. Horizontal scrolling works and prevents document overflow, but there is no visible fade, continuation cue, wrapping, or menu affordance, so visitors can miss two primary destinations.
- **WCAG/Standard:** Responsive-navigation usability; no direct WCAG failure was verified because the links remain keyboard-reachable and the scroller is operable.
- **Recommendation:** Use a compact disclosure menu, wrap the links into a deliberate second row, or add a clear overflow affordance that survives 200% zoom and keyboard focus. Preserve anchor semantics and visible focus.
- **Suggested command:** `$impeccable adapt`

### P3 — Polish

#### [P3] Component colors partially bypass the token system

- **Location:** token definitions at `index.html:12-30`; raw component values at `index.html:531-540`, `index.html:610-626`, `index.html:702-713`, `index.html:767-775`, `index.html:1005-1009`, `index.html:1041-1053`, `index.html:1213-1223`, `index.html:1241-1245`
- **Category:** Theming
- **Impact:** The main palette is coherent, but repeated borders, notice colors, tab surfaces, gallery placeholders, hover backgrounds, and the footer use direct hex/rgba values. Future contrast fixes or campaign theming will require scattered edits and can drift across components.
- **WCAG/Standard:** Design-token maintainability; no direct WCAG violation.
- **Recommendation:** Document semantic surface, border, notice, elevation, and inverse-text tokens, then replace repeated raw values where they represent the same role. Do not force dark mode unless it becomes a product requirement.
- **Suggested command:** `$impeccable document`

#### [P3] Pricing clarification uses the detector's generic side-tab accent pattern

- **Location:** `index.html:610-616`, instance at `index.html:1572`
- **Category:** Implementation Integrity
- **Impact:** The 5 px coral left border is coherent and readable, but it is a common generic callout treatment and is the detector's only verified visual-pattern finding. It does not block comprehension or interaction.
- **WCAG/Standard:** Impeccable implementation-pattern guidance; no WCAG violation.
- **Recommendation:** In a later polish pass, express the clarification through the existing label/card vocabulary or a quieter full-border/background treatment while retaining its strong text contrast.
- **Suggested command:** `$impeccable polish`

## Detector Verification and False Positives

The exact one-time command was:

```sh
node /Users/matthewjudy/.agents/skills/impeccable/scripts/detect.mjs --json index.html
```

| Detector result | Verification | Disposition |
|---|---|---|
| `side-tab` at line 611 | Literal `border-left: 5px solid var(--coral)` on the pricing clarification. | Verified; retained as P3. |
| `layout-transition` at line 1062, snippet `transition: width` | The source is `transition: border-color 220ms ease, border-width 220ms ease` on an absolutely positioned decorative pseudo-element. There is no `width` transition, no loop, and no document reflow failure in tested viewports. | Regex false positive for `width`. The border animation can still be simplified opportunistically, but it is not counted as an issue. |
| `dark-glow` at line 395 | The button uses `0 10px 22px rgba(18, 49, 74, 0.16)`: a directional, low-opacity elevation shadow, not a zero-offset chromatic halo. | Contextual false positive; not counted. |

## Patterns and Systemic Issues

- **Eager media is systemic:** every `<img>` lacks lazy-loading/responsive source hints, while the hero autoplays a very high-bitrate source.
- **Touch sizing is systemic:** several navigation/text-link patterns inherit visual line-box height rather than an explicit interaction floor.
- **Some semantic colors are systemic only at the root:** many components use variables, but repeated surface/border variants still bypass the token layer.
- **Functional labels occasionally overpromise:** **Send Message** describes delivery, and the reduced-motion video control describes visible playback, while the implementation provides neither in those states.

## Positive Findings

- Strong landmark and heading structure: one H1, orderly H2/H3 sections, labeled primary navigation, main, complementary convention facts, and footer.
- The skip link is first in the DOM and targets `main#main`, which is programmatically focusable; focus-visible outlines are defined for links, buttons, and FAQ summaries.
- Registration tabs implement the expected ARIA relationships, roving `tabindex`, arrow keys, Home/End, and synchronized hidden panels. These behaviors were verified live.
- Form controls have associated labels, meaningful input types, autocomplete hints, and required attributes.
- Images have contextual alternative text; decorative hero video is hidden from the accessibility tree and has a user pause control.
- Reduced-motion mode correctly disables smooth scrolling and pauses/hides autoplay on entry before the explicit-play inconsistency described above.
- Native `<dialog>` provides modality and focus containment; closing the speaker dialog returns focus to its opener.
- External registration/hotel links use `noopener noreferrer` and include screen-reader-only new-tab warnings.
- No broken assets, duplicate IDs, document-wide horizontal overflow, or JavaScript framework/bundle overhead were found.
- Most motion uses transform, opacity, color, and shadow; the passive scroll listener performs a single class toggle.
- The 390 px and 720 px layouts reflow into single-column content without clipping the main document.

## Recommended Actions

1. **[P1] `$impeccable optimize`:** Replace the 17.15 MB autoplay path with a poster-first, connection-aware video strategy and lazy/responsive gallery images.
2. **[P1] `$impeccable harden`:** Make contact delivery reliable with explicit success/error states, or truthfully present the action as opening an email draft.
3. **[P1] `$impeccable colorize`:** Introduce a contrast-safe semantic accent for small keynote text and verify it across the featured-card gradient.
4. **[P2] `$impeccable adapt`:** Fix mobile dialog initial focus/scroll, enlarge touch targets, and make navigation overflow discoverable.
5. **[P2] `$impeccable harden`:** Synchronize reduced-motion video visibility, playback, label, and pressed state.
6. **[P3] `$impeccable document`:** Capture the incumbent semantic tokens and component roles before broader theming work.
7. **[P3] `$impeccable polish`:** Recheck the pricing notice and final hover/focus details after functional fixes land.

You can ask me to run these one at a time, all at once, or in any order you prefer.

Re-run `$impeccable audit` after fixes to see your score improve.
