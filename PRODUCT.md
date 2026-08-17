# Product

<!-- impeccable:product-schema 1 -->

## Platform

web

## Users

The primary users are Floor Coverings International franchise owners who are expected to attend the 2027 convention and need an authoritative operational guide. Design associates, other employees, vendors, and suppliers also use the page to find the registration path that matches their role. Visitors may be planning travel on a phone, comparing fees, or returning later to finish hotel arrangements.

## Product Purpose

The site gathers the available convention information a franchisee needs, routes each attendee to the correct external registration form, and then guides the visitor to the separate hotel-reservation step. The primary success condition is that convention registration is completed and submitted. Hotel booking is an important follow-on task, not the definition of registration success.

## Positioning

This is the operational registration home for the 2027 FCI Convention at Hard Rock Riviera Maya. Its role-specific registration paths, FCI event logistics, participation pricing, keynote information, and hotel group link are specific to this event. Approved prior-convention imagery supplies authentic FCI atmosphere and cannot be replaced with generic conference claims.

## Operating Context

- The convention runs Tuesday, February 2 through Friday, February 5, 2027 at Hard Rock Riviera Maya.
- Franchise owner, employee, and vendor badge registrations are separate public Jotform workflows. One form is required per badge, and hotel booking is explicitly separate.
- Diamond Tier vendor signup is a sponsorship intake, not attendee badge registration.
- Hotel reservations use the Hard Rock group flow for “FCI 2027 Annual HRRM,” group code `270122FCIA`.
- External registration and hotel pages open cross-origin. This static site can observe an outbound click but cannot verify a submitted registration or completed hotel booking without an approved redirect, webhook, API, or reconciliation feed.

## Capabilities and Constraints

- The implementation is one static `index.html` file with local image/video assets and no application framework.
- The repository contains no contact-form backend and no configured analytics provider.
- Contact must therefore use truthful email-draft language with a visible address and copy fallback unless a real endpoint is separately authorized.
- Registration copy may explain how users recognize the external confirmation, but a link click must never be labeled as a completed submission.
- Published fees, policies, eligibility language, deadlines, speaker claims, and hotel terms must come from the existing approved content or another verified source.
- The early-bird deadline is currently published as October 16. Its year and exact boundary have not been verified and must not be invented.
- Preserve the existing role-specific Jotform URLs, hotel group URL, event dates, fee amounts, policy language, and factual FAQ content unless an approved source changes them.
- The page must remain useful without motion, hover, a configured email client, or a fast connection.
- Routine raster imagery must be responsive and bandwidth-aware, with intrinsic dimensions and truthful `sizes`; full JPEG originals are reserved for explicit enlargement or fallback.
- Fixed and sticky controls, full-bleed layouts, and essential content must respect device safe-area insets.

## Brand Commitments

Preserve the Floor Coverings International name, existing event identity, real approved prior-convention photography, Hard Rock Riviera Maya imagery, and verified Daymond John keynote content. The experience should feel like a registration-first blend of operational confidence and authentic event anticipation, not a generic promotional redesign.

## Evidence on Hand

- Incumbent page copy and links in `index.html`; fee, deadline, and policy authority still require the production approval recorded below.
- Approved prior-convention photography in `assets/convention-photos/`; public labels and alternative text describe visible scenes year-neutrally unless a capture year is materially relevant and independently verified.
- Resort photography in `assets/hotel-photos/`.
- Keynote image in `assets/speakers/daymond-john.jpg`.
- Convention video in `assets/videos/fci-convention-2026-hero-720p.mp4`.
- Read-only verification of the public Jotform registration fields and Hard Rock group reservation flow, recorded in `docs/design/2026-08-15-impeccable-technical-audit.md` and the planning record.
- No approved testimonials, attendee outcome claims, response-time promise, privacy statement, submission webhook, or completion analytics contract is present; future work must not fabricate them.

## Product Principles

1. Lead every visitor toward the correct completed convention registration.
2. Make the real-world sequence explicit: understand the fee, register each attendee, recognize confirmation, then reserve the hotel.
3. Tell the truth about external handoffs and observable state; never equate a click or email draft with completion.
4. Treat mobile readability, unobstructed controls, accessible targets, and low-bandwidth behavior as release gates.
5. Use keynote, community, and destination proof to support operational confidence without displacing essential logistics.

## Accessibility & Inclusion

The primary journey must support keyboard and screen-reader navigation, visible focus, meaningful headings and alternative text, WCAG 2.2 AA text contrast, 44 × 44 CSS-pixel primary touch targets where practical, 200% zoom/reflow, reduced motion, and layouts from 320px mobile through wide desktop. Focus indicators maintain at least 3:1 non-text contrast against their adjacent surface. Motion never lowers readable or interactive content below WCAG AA at any intermediate frame, and reduced motion keeps the same state and hierarchy without movement. Important meaning and content may not depend on hover, blur removal, color perception, or animation.
