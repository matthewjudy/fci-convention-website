# FCI Convention Website — Impeccable Critique and Planning Record

**Date:** August 15, 2026
**Target:** `index.html` (`index-html`)
**Evaluation:** `$impeccable critique`
**Design health score:** 19/32 (59%, acceptable)
**Status:** Planning and audit record only; no site code was changed
**Source snapshot:** [`.impeccable/critique/2026-08-15T18-16-22Z__index-html.md`](../../.impeccable/critique/2026-08-15T18-16-22Z__index-html.md)

## Purpose and Scope

This document preserves the complete substantive findings from the August 15, 2026 Impeccable critique, together with the product decisions supplied immediately afterward. It is the durable planning record for future GitHub issues and implementation passes.

The critique evaluated the current single-page convention site as a registration-oriented campaign surface. It reviewed the desktop experience at 1440×900 and the mobile experience at 390×844, inspected the source, ran the deterministic Impeccable detector, and verified findings in a rendered browser. It did not modify `index.html` or any other site code.

The original evaluation treated the page as a **Persuade-mode campaign page**. The subsequent decision record below clarifies that its primary job is operational: expected franchisees should receive all of the convention information they need and be able to complete registration. Future planning should therefore use a **registration-first blend** of operational clarity and event appeal.

## Method and Provenance

The critique used a dual-agent assessment:

- Assessment A: `/root/critique_design_a`
- Assessment B: `/root/critique_evidence_b`

The two assessments were isolated. Assessment A was completed before the deterministic detector findings were released, reducing the likelihood that automated warnings would anchor the design review.

The evidence pass included source inspection, a deterministic CLI scan, fresh desktop and mobile browser tabs, screenshots, console and DOM checks, and verified visual overlays. The original page remained unchanged.

## Design Health Score

| # | Heuristic | Score | Key issue |
|---|---|---:|---|
| 1 | Visibility of System Status | 2 | Tabs and video state are clear, but registration and contact have no completion, success, or failure state. |
| 2 | Match System / Real World | 3 | Dates, roles, and rates are familiar; “Participating Business,” “Convention Contribution,” and “October 16” need clarification. |
| 3 | User Control and Freedom | 3 | Video, dialogs, lightbox, and new tabs have exits; mobile navigation and modal positioning weaken control. |
| 4 | Consistency and Standards | 3 | The visual system is cohesive, but “Send Message” unexpectedly launches an email client. |
| 5 | Error Prevention | 2 | Native validation helps, but separate registration and hotel workflows lack prerequisite and completion guidance. |
| 6 | Recognition Rather Than Recall | 2 | Mobile pricing comparison and the split booking process create memory demands. |
| 7 | Flexibility and Efficiency | n/a | Not meaningful for the Persuade-mode campaign-page framing used in this critique. |
| 8 | Aesthetic and Minimalist Design | 3 | Strong hierarchy; the very long mobile journey, repeated logistics, and suppressed imagery dilute focus. |
| 9 | Error Recognition and Recovery | 1 | Contact has no page-level failure, retry, fallback, or draft-preservation path. |
| 10 | Help and Documentation | n/a | FAQ and contact were assessed as part of the campaign journey. |
| **Total** |  | **19/32** | **Acceptable (59%): strong foundation with significant conversion and mobile-flow gaps.** |

## Design Specificity Verdict

**Moderately authored: high content specificity, medium design specificity.**

The page is unmistakably FCI because it uses authentic convention footage, exact Riviera Maya logistics, FCI identity, and Daymond John. Its composition is still largely interchangeable with a corporate-event template: video hero, glass details card, role tabs, pricing cards, agenda rows, resort split, galleries, FAQ accordion, and contact card.

The authentic imagery gives the site character, but the journey does not consistently turn that material into a distinctive FCI-community story. The strongest opportunity is to transform the page from a long information stack into a distinctly FCI journey: choose a role, register attendees, reserve the hotel, and clearly understand what happens next.

## Deterministic Detector Evidence

The deterministic CLI scan returned three warnings in `index.html`:

- **`side-tab` at `index.html:611`:** The coral left border on the informational notice. The match is real, but it is a reasonable intentional notice treatment rather than a demonstrated UX defect.
- **`layout-transition` at `index.html:1062`:** A false positive caused by the regex fallback matching `border-width` as `width`.
- **`dark-glow` at `index.html:395`:** Low-confidence. The shadow is conventional low-opacity elevation rather than a chromatic glowing halo.

The parser dependencies were unavailable, so the CLI used a regex fallback. That fallback could not evaluate computed contrast or selector relationships and therefore undercounted potential findings. The scan ran once, exited with code 2, and was not treated as a complete audit.

## Rendered Overlay Evidence

The rendered browser detector produced **32 verified overlay nodes**. The written category breakdown from the run was:

- 13 line-length warnings
- 5 glow warnings
- 4 hairline-border/wide-shadow warnings
- 4 rendered low-contrast warnings
- 2 cramped-padding warnings
- 1 hero-eyebrow warning
- 1 side-tab warning
- 1 all-caps-body warning

The category counts represent 31 element-label overlays; the 32nd rendered node is the summary banner. Many eyebrow and shadow findings are stylistic warnings rather than defects. The four rendered low-contrast warnings deserve manual remediation.

At the time of the critique, the verified overlays remained in the **`[Human] Convention critique overlays`** Chrome tab. Injection succeeded, the console reported 32 anti-patterns, and the rendered page visibly showed the labels; the overlay was not merely claimed.

## Overall Impression

This is a credible, visually disciplined registration page with an excellent opening and unusually thoughtful interaction semantics. The largest weakness is the conversion journey: users are asked to understand pricing, compliance, external forms, hotel booking, and unfinished logistics without a clear step-by-step completion model.

The biggest opportunity is not necessarily a wholesale redesign. It is to turn the page from a long information stack into a reassuring journey: choose a role, register attendees, reserve the hotel, and know what happens next. Following the later product clarification, convention registration completion—not completion of the entire trip—is the primary success state.

### Cognitive Load

Cognitive load is **moderate**, with 3 of 8 checks failing:

- Chunking
- Minimal choices
- Working-memory support

The largest choice clusters are six primary navigation links, 13 FAQ questions, five hotel-image actions, and 11 convention photographs.

### Emotional Journey

- The hero creates anticipation.
- Pricing introduces an early anxiety valley.
- The keynote and resort restore excitement.
- Repeated “coming soon” and “TBD” language reduce confidence and readiness.
- The sparse footer ends without a final conversion peak.

## What Is Working

1. **The hero earns attention.** It immediately answers what, when, and where while pairing authentic convention footage with a decisive registration CTA (`index.html:1440` at the time of review).

2. **The visual language is disciplined.** Navy, teal, lime, coral, editorial serif headings, compact labels, and restrained geometry produce a professional event identity.

3. **Core interaction semantics are unusually thoughtful.** The site includes a skip link, visible focus indicators, reduced-motion support, keyboard-operated registration tabs, native dialogs, meaningful image alt text, and new-tab announcements.

## Priority Issues

### [P1] The mobile back-to-top control obstructs content and actions

**GitHub issue:** [#2 — Prevent the mobile back-to-top control from covering content and actions](https://github.com/matthewjudy/fci-convention-website/issues/2)

**Finding:** At 390×844, the fixed control overlapped the Owner Registration CTA, pricing copy, keynote imagery, FAQ rows, resort photography, and part of **Send Message**. Its 40px mobile height is also below the usual 44px touch-target minimum.

**Why it matters:** It directly blocks reading and conversion on the most constrained viewport.

**Recommended fix:** Reserve safe bottom space, hide the control while it intersects actionable content, and use a compact 44×44 control only after meaningful scroll or upward-scroll intent.

**Suggested command:** `$impeccable adapt index.html`

### [P1] “Send Message” is a misleading pseudo-submit

**GitHub issue:** [#4 — Replace the misleading contact mailto pseudo-submit with a reliable completion flow](https://github.com/matthewjudy/fci-convention-website/issues/4)

**Finding:** The visible form at `index.html:1794` looks like an in-page submission, but its handler at `index.html:1983` constructs a `mailto:` link. There is no sending, success, failure, retry, fallback, or preserved-draft state.

**Why it matters:** A user without a configured email client can complete the form and receive no useful result.

**Recommended fix:** Connect a real endpoint with inline feedback and preserved input. If that is unavailable, rename the action to **Open email draft**, expose the destination address, and add a copy-address fallback.

**Suggested command:** `$impeccable harden index.html`

### [P1] Mobile navigation hides destinations without an overflow cue

**GitHub issue:** [#3 — Replace the mobile nav rail with a compact Register-first header](https://github.com/matthewjudy/fci-convention-website/issues/3)

**Finding:** The six-link navigation becomes a horizontal rail. At 390px, FAQ and Photos are initially invisible, and scrolling can partially clip Register. The two-row sticky header consumes approximately 124px, about 15% of the viewport.

**Why it matters:** Users cannot reliably recognize all available destinations and lose valuable vertical space throughout a page that exceeds 10,000px at 390px wide.

**Recommended fix from the critique:** Keep Register dominant, group the remaining destinations under three anchors plus a labeled More menu, or add unmistakable overflow cues and an active-section state.

**Planning recommendation after the user’s clarification:** Prefer a compact sticky header with one persistent **Register** CTA and a clearly labeled **Menu** control. Place secondary anchors inside the menu, target a total sticky-header height of approximately 64px or less, and do not retain an unlabeled horizontal rail. This is a planning recommendation, not an approved implementation decision.

**Suggested command:** `$impeccable distill index.html`

### [P2] Pricing and booking create a mobile memory bridge

**GitHub issue:** [#5 — Create a clear registration-to-hotel booking completion path](https://github.com/matthewjudy/fci-convention-website/issues/5)

**Finding:** Desktop pricing compares well side by side, but mobile stacks three tall cards. Users must remember `$749 + $75/person` while reading `$1,149 + $199/person`. “October 16” lacks a year. Convention registration and hotel booking are separate external workflows without a visible completion model.

**Why it matters:** The highest-stakes decision requires mental arithmetic and remembering state across sites.

**Recommended fix:** Label amounts as **business fee + attendee fee**, include the full deadline and savings, provide a compact mobile comparison, and introduce an explicit checklist: **1. Register attendees → 2. Reserve hotel**. Registration completion should be identified as the primary success state; hotel booking is an important subsequent task, not the definition of registration success.

**Suggested command:** `$impeccable shape index.html`

### [P2] The strongest persuasive evidence arrives late and is visually suppressed

**GitHub issue:** [#1 — Move keynote, community, and destination proof earlier in the registration journey](https://github.com/matthewjudy/fci-convention-website/issues/1)

**Finding:** Pricing and compliance language precede the keynote, destination, and community proof. Desktop photographs start desaturated, translucent, and blurred until hover. The 2026 attendee gallery appears only after the 13-item FAQ.

**Why it matters:** The page asks users to absorb cost and obligation before it fully earns desire and confidence.

**Recommended fix:** Move a compact keynote/community/destination proof band above pricing, display imagery in full color, add outcome-oriented captions, and end with a final registration CTA, deadline, and reassurance. The compliance charge should become a supporting note rather than a visual highlight.

**Suggested command:** `$impeccable layout index.html`

## Persona Red Flags

### Jordan — First-Timer

- Registration does not explain required information, payment, expected time, or what happens after opening the external form.
- “Design Associate/Employee,” “team member,” “Participating Business,” and “Diamond Tier Vendor” assume internal knowledge.
- Repeated “coming soon” and “TBD” statements make the event feel unfinished.
- Contact provides no confirmation that help was requested.

### Riley — Stress Tester

- No configured/default email client can strand the contact workflow.
- Registration, hotel booking, and resort details span external tabs without shared state or return guidance.
- “October 16” omits the year.
- On mobile, the speaker dialog opened internally scrolled, landing on the lower portrait instead of the top.

### Casey — Distracted Mobile User

- FAQ and Photos are hidden beyond an un-signposted scrolling header.
- The sticky header and floating control consume or cover content.
- The page exceeds 10,000px at 390px wide, making resumption difficult.
- The 16MB autoplay hero video and non-lazy gallery images are expensive on a slow connection.
- The speaker modal opens at an unexpected internal position.

## Minor Observations

- The desktop speaker modal and hotel lightbox are attractive and legible.
- Hover-lifting static pricing, FAQ, and form containers can imply whole-card clickability.
- Navigation does not identify the section currently in view.
- The 2026 photo mosaic has strong alt text but no visible captions or attendee outcomes.
- The footer contains only the event title and functions as a dead end.
- The site requests a missing `/favicon.ico`.
- The hotel rail’s partial next image supplies a better scrolling cue than the mobile navigation.

## Questions Considered and Answers

### Is the page primarily persuading optional attendees or operationally guiding franchisees already expected to attend?

**User decision:** The goal is to operationally guide franchisees expected to attend so that they have all of the information they need regarding the convention and are able to register.

### Why does the compliance charge appear before the strongest evidence of community, keynote value, and destination appeal?

**User decision:** It should not. The compliance charge should be a note, not a highlight.

### Should success mean “registration started,” “convention registration completed,” or “the entire trip is booked”?

**User decision:** Success means the registration is completed and submitted.

### Does mobile need six persistent anchors, or one dominant Register action and a compact route to everything else?

**User response:** Open to a recommendation.

**Planning recommendation:** Use one persistent **Register** CTA plus a clearly labeled **Menu** control in a compact sticky header, with secondary anchors inside the menu. Target approximately 64px or less in total height and avoid an unlabeled horizontal rail. This recommendation remains open for approval and is not authorization to implement.

## Decision Record

| Decision area | Recorded direction | Status |
|---|---|---|
| Primary product job | Operationally guide expected franchisees with all convention information needed to register. | Approved direction |
| Conversion success | Registration is completed and submitted. | Approved direction |
| Compliance charge | Present it as a supporting note, not a visual highlight. | Approved direction |
| Dominant character | Registration-first blend of operational guidance and aspirational event experience. | Approved direction |
| First issue group | Lead with mobile blockers: navigation and back-to-top control. | Approved priority |
| Current work breadth | Planning/audit only; make no code changes. | Approved constraint |
| Mobile navigation pattern | Compact sticky header, persistent Register CTA, labeled Menu control, secondary anchors inside menu, approximately 64px or less, no unlabeled horizontal rail. | Planning recommendation; not yet approved for implementation |

## Recommended Action Sequence

This sequence is planning-only. It records the recommended order for later authorized implementation and does not authorize changes now.

1. **Define mobile acceptance criteria first.** Treat the mobile navigation and back-to-top issues as the lead workstream. Specify the compact header, persistent Register CTA, labeled Menu behavior, secondary anchor placement, maximum approximate header height, focus/keyboard behavior, and non-overlap requirements before editing.

2. **Remove mobile obstruction and hidden wayfinding.** In a later implementation pass, address the back-to-top control and mobile navigation together, then validate that actions and content remain unobstructed at the reviewed 390×844 viewport and that all destinations are recognizable.

3. **Make the completion path explicit.** Plan the registration journey around the stated success condition: registration completed and submitted. Explain what users need, what happens on the external registration surface, what confirmation they should expect, and that hotel reservation is the next supporting task.

4. **Harden contact as a support path.** Decide whether the site will use a real form endpoint. If it will not, plan explicit email-draft language, a visible destination address, a copy fallback, and preserved input so the interaction does not imitate a successful submission.

5. **Clarify pricing and reduce working-memory demands.** Plan a compact mobile comparison, label business and per-attendee amounts plainly, supply the full deadline including the year, and show registration followed by hotel reservation as an ordered checklist.

6. **Reorder information around registration readiness.** Move keynote, community, and destination proof early enough to support confidence; demote the compliance charge to a note; and finish with a clear registration CTA and completion-oriented reassurance.

7. **Run a bounded verification pass after future implementation.** Recheck desktop and mobile together, review contrast and the missing favicon, confirm speaker-dialog starting position, test slow-loading media behavior, and verify the actual registration and contact outcomes rather than only inspecting source code.

## GitHub Issue Links

The five priority findings are tracked in these verified issues:

- [#2 — [P1] Prevent the mobile back-to-top control from covering content and actions](https://github.com/matthewjudy/fci-convention-website/issues/2)
- [#4 — [P1] Replace the misleading contact mailto pseudo-submit with a reliable completion flow](https://github.com/matthewjudy/fci-convention-website/issues/4)
- [#3 — [P1] Replace the mobile nav rail with a compact Register-first header](https://github.com/matthewjudy/fci-convention-website/issues/3)
- [#5 — [P2] Create a clear registration-to-hotel booking completion path](https://github.com/matthewjudy/fci-convention-website/issues/5)
- [#1 — [P2] Move keynote, community, and destination proof earlier in the registration journey](https://github.com/matthewjudy/fci-convention-website/issues/1)

## Run Notes

- Target slug: `index-html`
- Ignore list: absent
- Assessments: isolated; Assessment A completed before detector findings were released
- CLI detector: ran once; exit code 2; three warnings; regex fallback undercount
- Browser: fresh desktop and mobile tabs at 1440×900 and 390×844
- Overlay: injection verified; 32 nodes rendered
- Visibility API: unsupported; screenshot, console, and DOM verification used instead
- Servers: both stopped; ports verified closed
- Temporary files: cleaned successfully
- Site code: unchanged
- Snapshot: `.impeccable/critique/2026-08-15T18-16-22Z__index-html.md`
- Trend: 19/32; first run for this target, so there is no trend yet
