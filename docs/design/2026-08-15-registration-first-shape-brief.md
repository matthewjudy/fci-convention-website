# Registration-First Shape Brief

**Target:** `index.html`
**Status:** Confirmed from the user’s August 15 direction; implementation authorized in the requested sequence
**Visitor mode:** Operate-first blend with supporting Persuade moments

## 1. Job and Audience

Expected FCI franchisees arrive needing one reliable place to understand the 2027 convention, determine the applicable fee, register every attendee through the correct role-specific form, and continue to hotel booking. Employees and vendors need the same clarity with role-appropriate paths. Mobile visitors may be interrupted, comparing details, or returning to continue the trip-planning sequence.

## 2. Outcome and Proof

The primary outcome is a convention registration completed and submitted through the external Jotform flow. The page cannot verify that cross-origin submission, so it must explain the external confirmation cue and never treat an outbound click as completion. Real Daymond John keynote content, approved FCI convention photography, verified dates, role-specific forms, pricing, and the Hard Rock group flow supply the proof.

## 3. Selected Direction

Preserve the incumbent visual identity and make the structure registration-first:

1. compact sticky header with persistent Register and labeled Menu on mobile;
2. hero with dates, destination, and primary registration action;
3. compact keynote, FCI community, and destination proof band;
4. directly comparable fee and deadline guidance;
5. Step 1 — select a role and complete convention registration;
6. Step 2 — reserve the hotel after registration;
7. schedule and operational details;
8. resort and community photography;
9. FAQ and truthful contact help;
10. closing registration action with confirmation guidance.

The focal interaction is the Step 1 role choice. Proof supports confidence but never becomes a second promotional hero. Compliance language becomes a secondary policy note rather than a highlighted price option.

## 4. Scope and Boundaries

- Production-ready refinement of the single existing page, not a replacement visual world.
- Preserve verified fees, policies, event dates, external links, speaker facts, FAQ content, and approved imagery.
- Do not add a backend, analytics provider, external-form configuration, invented completion state, testimonial, savings claim, response-time promise, or unverified deadline year.
- Do not redesign the Jotform or Hard Rock experiences.
- The existing desktop identity remains recognizable; mobile navigation, completion guidance, media loading, and end-of-page conversion are in scope.

## 5. States and Ranges

- Mobile menu: closed, open, Escape close, link-activation close, resize reset, and focus return.
- Registration tabs: owner, employee, vendor; keyboard roving behavior retained.
- External registration: ready, outbound link opened, and user-recognized external confirmation; no locally verified submitted state.
- Contact: email draft available, email address copied, clipboard unavailable, and manual-copy fallback.
- Hero media: poster-only mobile/save-data/reduced-motion state, desktop video available, paused, and playback unavailable.
- Speaker and photo dialogs: open at top, deliberate initial focus, internal overflow, Escape/backdrop/close, and opener focus restoration.
- Layout: 320px, 390px, 428px, mobile landscape, 200% zoom/reflow, tablet, 1024px, 1280px, and 1440px desktop.

## 6. Interaction and Layout

- On mobile, use a single-row sticky header approximately 64px high where accessible sizing permits: compact brand, persistent Register CTA, and visibly labeled Menu button. Secondary anchors live in the disclosed menu; no unlabeled horizontal rail remains.
- Hide the floating back-to-top control at mobile/tablet widths. If retained on wide desktop, it must be at least 44 × 44px and remain outside content.
- Use semantic ordered steps and a compact fee comparison that does not require horizontal scrolling or memory across stacked cards.
- Explain before each external handoff what the user is doing, that the destination opens in a new tab, and what to do afterward.
- Default meaningful photography to full color and legible contrast; hover and focus may enhance but never reveal required meaning.
- End with one clear return to Step 1 and a truthful statement that successful registration is confirmed on the external registration form.

## 7. Constraints and Open Decisions

- Web, static HTML/CSS/JavaScript, no build system.
- Meet the accessibility and responsive commitments in `PRODUCT.md`.
- The exact early-bird year and whether October 16 is inclusive remain unverified; preserve the approved published wording until confirmed.
- The site cannot measure `registration_submitted` without Jotform configuration. A future integration must define redirect/webhook behavior and an analytics event contract before claiming automated completion.
- The owner Jotform opening-year choices currently stop at 2025; that external configuration issue is outside this page’s code scope and should be corrected by the form owner.
