# Hannah Convention Content Release Record

**Status:** In progress; implementation and production verification are pending.
**Recorded:** August 21, 2026
**Source:** Katherine Judy's forwarded Outlook thread `Fw: convention website`, received August 21, 2026, specifically Hannah Connolly's August 20 edits
**Tracking:** [Issue #26](https://github.com/matthewjudy/fci-convention-website/issues/26), [Issue #27](https://github.com/matthewjudy/fci-convention-website/issues/27), and [Issue #28](https://github.com/matthewjudy/fci-convention-website/issues/28)

This document is the durable source, scope, and verification record for the August 21 convention-content update. It deliberately separates requested content from release evidence. Nothing in this record alone establishes that the changes have reached production.

## Source boundary

The Katherine-forwarded thread and Hannah's edits are the content authority for this release. The public site remains the authority for what visitors can currently see, and the merged repository source is the authority for what has been shipped. When those sources differ, do not describe requested copy as live until the pull request is merged and `https://www.fciconvention.com/` has been checked directly.

The source email itself is not stored in this public repository. This record retains only the operational facts needed to implement and verify the website changes.

### Source reconciliation note

Issue #26's initial description said to preserve the current Convention Team email. A direct recheck of Hannah's source established that the requested address is `fciconvention@fcifloors.com`, not the site's current `fciconvention@floorcoveringsinternational.com`. The rechecked source controls: update visible text and `mailto:` destinations consistently, and treat the earlier issue wording as superseded.

## Planned changes

### Agenda and attendee guidance — Issue #26

- Replace the placeholder schedule and the claim that the agenda is TBD with the supplied agenda covering Tuesday, February 2 through Saturday, February 6, 2027.
- Represent every supplied day and time block with semantic, scannable markup that remains readable at desktop and mobile widths.
- Update adjacent hero or supporting copy where necessary so that it does not contradict the supplied schedule.
- Preserve the registration-first sequence and the site's existing keyboard and accessibility behavior.

### Hotel, transportation, roommate, and FAQ content — Issue #27

- Rename the hotel action to **Book Hotel Reservation** everywhere it appears and use the supplied Hard Rock `/signin` group-booking URL consistently.
- Explain that the FCI discount is automatically applied and show group code `270122FCIA`.
- Add the supplied hotel-policy disclaimer, maximum-occupancy combinations, and children's-rate check-in note.
- Add the supplied Roommate Finder link with a descriptive label.
- Add the approximately 1.5-hour airport travel estimate and a distinct **Ground Transportation** section marked **Coming Soon**.
- Add the supplied guidance for passport-name spelling, weather, drinking water, and official language.
- Replace the Convention Team address everywhere it appears with `fciconvention@fcifloors.com`.
- Keep external destinations explicit and use safe new-tab behavior (`target="_blank"` with `rel="noopener noreferrer"`) where a link leaves the site.

## Preserved truths and constraints

- The existing **Hotel** fact label already matches Hannah's request and should remain unchanged.
- The requested Convention Team address is `fciconvention@fcifloors.com`; replace the current long-domain address consistently in visible text and `mailto:` destinations.
- Convention registration occurs in Jotform, hotel booking occurs in the separate Hard Rock flow, and this static page cannot observe completion in either external system.
- The honest visitor sequence remains **Complete Convention Registration** followed by **Book Hotel Reservation**; the update must not imply cross-system completion tracking.
- Published pricing and policy copy must not acquire promises, guarantees, or inferred terms that were not supplied by the source.
- The repository contains a static site. Responsive behavior, focus order, keyboard access, semantic headings, and reduced-motion behavior must survive the content expansion.

## Editorial normalization

Hannah's approved meaning should remain intact while presentation-level defects are corrected:

- correct obvious spelling, punctuation, and spacing errors in the supplied source;
- use Title Case for short UI fragments, action labels, and section labels where that matches the existing site;
- retain sentence case for explanatory paragraphs and policy text;
- normalize date and time presentation consistently without changing a day, time block, condition, rate, code, or destination;
- use descriptive link text instead of exposing raw URLs; and
- do not silently resolve a substantive ambiguity—escalate it to the content owners.

## Verification checklist

### Source and content

- [ ] Compare the final implementation line by line with the Katherine-forwarded/Hannah source.
- [ ] Confirm every Tuesday–Saturday agenda day and supplied time block is present.
- [ ] Confirm no visitor-facing agenda copy still says `TBD`.
- [ ] Confirm every hotel CTA says **Book Hotel Reservation** and points to the supplied `/signin` URL.
- [ ] Confirm the automatic-discount explanation and group code `270122FCIA` are present and consistent.
- [ ] Confirm the hotel disclaimer, occupancy combinations, children's-rate note, roommate link, airport estimate, Ground Transportation status, and four FAQ topics are present.
- [ ] Confirm the existing Hotel fact label was preserved and every Convention Team email was changed to `fciconvention@fcifloors.com`.

### Links and behavior

- [ ] Check the hotel, Roommate Finder, email, and internal fragment links.
- [ ] Confirm external links have descriptive names and safe new-tab attributes.
- [ ] Confirm the registration-first sequence and Jotform completion boundary remain truthful.
- [ ] Confirm keyboard navigation, visible focus, disclosure controls, modal behavior, and reduced-motion behavior.

### Responsive and visual quality

- [ ] Review the full page on a representative desktop viewport.
- [ ] Review the full page on a representative mobile viewport.
- [ ] Confirm long schedule entries, occupancy guidance, policy copy, link labels, and FAQ answers wrap without clipping or overflow.
- [ ] Record the focused Impeccable check and any accepted exceptions.

### Release and production

- [ ] Run focused source checks and repository validation.
- [ ] Link the pull request to Issues #26–#28.
- [ ] Merge only after review and focused checks pass.
- [ ] Confirm the GitHub Pages deployment succeeded for the merged commit.
- [ ] Verify the canonical site at `https://www.fciconvention.com/` on desktop and mobile.
- [ ] Record production evidence before closing any of Issues #26–#28.

## Release evidence

Complete these fields during release closeout. Until then, they are intentionally marked pending.

| Evidence | Record |
| --- | --- |
| Pull request | Pending |
| Reviewed head commit | Pending |
| Merge commit | Pending |
| GitHub Pages workflow run | Pending |
| Canonical production URL | `https://www.fciconvention.com/` — verification pending |
| Desktop evidence | Pending |
| Mobile evidence | Pending |
| Link and keyboard/accessibility evidence | Pending |
| Impeccable result | Pending |
| Production verification date | Pending |

## Closeout rule

Issues #26, #27, and #28 remain open until the merged commit is deployed and the canonical production site confirms the new agenda, hotel booking action and destination, policy and occupancy guidance, transportation content, Roommate Finder link, and FAQs. Replace the pending evidence above with exact URLs, commit identifiers, and observed results at closeout.
