---
name: 2027 FCI Convention Registration
description: A confident, registration-first FCI event experience with Riviera warmth and operational clarity.
colors:
  registration-navy: "#12314a"
  midnight-navy: "#0b2235"
  wayfinding-teal: "#007f86"
  accessible-action-teal: "#00636a"
  registration-lime: "#8cc63f"
  warm-signal-coral: "#e95f45"
  riviera-sky: "#d9f1f3"
  warm-program-paper: "#fbfaf6"
  operational-ink: "#162029"
  slate-copy: "#5d6770"
  clean-white: "#ffffff"
  quiet-divider: "#dfe4e2"
  attendance-notice: "#fff3ee"
  policy-ink: "#623126"
  corporate-footer-navy: "#1c294a"
  corporate-link-cyan: "#4bc5dc"
typography:
  display:
    fontFamily: "Georgia, 'Times New Roman', serif"
    fontSize: "clamp(46px, 7vw, 86px)"
    fontWeight: 700
    lineHeight: 1.04
    letterSpacing: "normal"
  headline:
    fontFamily: "Georgia, 'Times New Roman', serif"
    fontSize: "clamp(34px, 4.6vw, 58px)"
    fontWeight: 700
    lineHeight: 1.04
    letterSpacing: "normal"
  title:
    fontFamily: "Aptos, 'Segoe UI', Arial, sans-serif"
    fontSize: "21px"
    fontWeight: 900
    lineHeight: 1.2
    letterSpacing: "normal"
  body:
    fontFamily: "Aptos, 'Segoe UI', Arial, sans-serif"
    fontSize: "16px"
    fontWeight: 400
    lineHeight: 1.55
    letterSpacing: "normal"
  label:
    fontFamily: "Aptos, 'Segoe UI', Arial, sans-serif"
    fontSize: "14px"
    fontWeight: 900
    lineHeight: 1.2
    letterSpacing: "normal"
  metadata:
    fontFamily: "Aptos, 'Segoe UI', Arial, sans-serif"
    fontSize: "12px"
    fontWeight: 950
    lineHeight: 1.2
    letterSpacing: "0.12em"
rounded:
  compact: "4px"
  standard: "8px"
  pill: "999px"
spacing:
  xxs: "4px"
  xs: "8px"
  sm: "12px"
  md: "18px"
  lg: "24px"
  xl: "28px"
  section: "64px"
components:
  button-primary:
    backgroundColor: "{colors.registration-lime}"
    textColor: "{colors.registration-navy}"
    typography: "{typography.label}"
    rounded: "{rounded.standard}"
    padding: "0 16px"
    height: "46px"
  button-primary-hover:
    backgroundColor: "{colors.midnight-navy}"
    textColor: "{colors.clean-white}"
    typography: "{typography.label}"
    rounded: "{rounded.standard}"
    padding: "0 16px"
    height: "46px"
  button-text:
    backgroundColor: "transparent"
    textColor: "{colors.accessible-action-teal}"
    typography: "{typography.label}"
    rounded: "{rounded.standard}"
    padding: "0 2px"
    height: "44px"
  navigation-primary:
    backgroundColor: "{colors.midnight-navy}"
    textColor: "{colors.clean-white}"
    typography: "{typography.label}"
    padding: "10px 14px"
    height: "76px"
  card:
    backgroundColor: "{colors.clean-white}"
    textColor: "{colors.operational-ink}"
    rounded: "{rounded.standard}"
    padding: "24px"
  notice:
    backgroundColor: "{colors.attendance-notice}"
    textColor: "{colors.policy-ink}"
    rounded: "{rounded.standard}"
    padding: "18px 20px"
  tab-selected:
    backgroundColor: "{colors.clean-white}"
    textColor: "{colors.accessible-action-teal}"
    typography: "{typography.label}"
    padding: "0 16px"
    height: "58px"
  fact-panel:
    backgroundColor: "{colors.midnight-navy}"
    textColor: "{colors.clean-white}"
    typography: "{typography.body}"
    rounded: "{rounded.standard}"
    padding: "26px"
---

# Design System: 2027 FCI Convention Registration

## Overview

**Creative North Star: "The Riviera Registration Desk"**

The experience should feel like arriving at a well-run FCI registration desk set inside the Riviera destination: unmistakably branded, calm under pressure, and warm enough to build anticipation. Operational truth leads every composition, while approved photography and the sunlit accent palette keep the page from feeling administrative.

The system pairs a structured navy frame with warm paper surfaces, decisive lime actions, accessible teal wayfinding, and restrained coral signals. Real event and resort imagery supplies atmosphere; the interface supplies sequence, recovery, and confidence. It is a registration tool with hospitality, not a generic conference template.

**Key Characteristics:**

- Registration-first hierarchy with fees, attendee forms, and hotel follow-through kept explicit.
- Deep navy structure, warm paper reading surfaces, and rare high-energy lime actions.
- Editorial serif headlines paired with a practical system sans-serif for operations.
- Approved FCI, convention, speaker, and resort assets instead of invented visual proof.
- Responsive behavior that stays complete from 320px through wide desktop and at 200% reflow.
- Motion that supports state but disappears cleanly when reduced motion is requested.

## Colors

The palette balances FCI authority with Riviera light: navy establishes trust, teal guides, lime commits, coral warns, and warm neutrals carry long-form logistics.

### Primary

- **FCI Registration Navy:** The main structural color for headings, table headers, and authoritative information.
- **Midnight Lobby Navy:** The deepest surface for the header, hero, focused controls, and high-contrast states.
- **Registration Lime:** The scarce action color for primary calls to action and compact hero facts.

### Secondary

- **Wayfinding Teal:** A supporting brand accent for paths, borders, and progress controls.
- **Accessible Action Teal:** The contrast-safe text-action color on white, paper, and pale event surfaces.
- **Warm Signal Coral:** A selected-state and caution accent; it is not body-copy color on light surfaces.
- **Riviera Sky:** A quiet guidance surface for preparation and help content.

### Tertiary

- **Corporate Footer Navy:** The footer's distinct corporate FCI surface.
- **Corporate Link Cyan:** Footer underlines, separators, and linked-state details.
- **Attendance Notice / Policy Ink:** A paired warm notice surface for fee and attendance obligations.

### Neutral

- **Warm Program Paper:** The page canvas and the fade-out surface beneath the hero.
- **Operational Ink:** Primary long-form text.
- **Slate Copy:** Secondary explanatory text that remains WCAG AA on white and paper.
- **Clean White:** Cards, form surfaces, and inverse text.
- **Quiet Divider:** Low-emphasis rules and table separation.

**The Registration Color Rule.** Lime identifies the next primary action; do not spend it on general decoration.

**The Signal Rule.** Coral may mark selection, focus, or policy emphasis, but normal-size text on light surfaces uses the darker teal, navy, or policy-ink role.

## Typography

**Display Font:** Georgia (with Times New Roman and serif fallbacks)<br />
**Body Font:** Aptos (with Segoe UI, Arial, and sans-serif fallbacks)<br />
**Label Font:** Aptos (with the body stack)

**Character:** Georgia gives the event an established editorial voice; Aptos keeps fees, instructions, forms, and navigation crisp and familiar. Weight and scale—not novelty fonts or excessive tracking—create hierarchy.

### Hierarchy

- **Display:** Reserved for the single hero title; it is bold, tightly composed, and allowed to wrap deliberately on narrow screens.
- **Headline:** Section-level editorial headings with clear separation above and a shorter gap below.
- **Title:** Operational card, notice, footer, and disclosure headings in the sans-serif voice.
- **Body:** Practical reading copy with a 65–75 character target measure for instructions and policy context.
- **Label:** Strong navigation, button, fact, date, and state language. Increased tracking is reserved for compact metadata, not paragraphs.

**The Two-Voice Rule.** Serif type establishes destination and occasion; sans-serif type carries every task, status, and decision.

**The Sentence Rule.** Fragments and interface labels use Title Case; complete sentences retain sentence case and normal punctuation.

## Layout

The page uses a centered maximum-width container of 1180px with 20px minimum side gutters. Sections separate generously, while related controls and explanatory text use a compact 8–28px rhythm. Instructional and policy copy is normally constrained to 72 characters so scanning does not become a full-width reading task.

Desktop compositions may use two or three columns when comparison helps: hero copy and facts, pricing, schedule details, hotel content, and grouped footer navigation. Below 900px, the header becomes a disclosure menu and major grids stack. At 560px, action rows widen, galleries become a deliberate two-column mosaic or contained horizontal strip, and form padding tightens. At 420px, pricing becomes labeled rows. At 360px, Register moves inside the menu so the official horizontal logo remains legible.

Intentional horizontal movement is confined to the resort-photo rail; the document itself must keep `scrollWidth === innerWidth` at 320px, 390px, intermediate widths, and the 720px reflow proxy.

**The Operational-First Rule.** Fees, role selection, registration recovery, and hotel follow-through appear before galleries or optional sponsorship details.

## Elevation & Depth

The system uses a restrained hybrid of tonal layering and neutral elevation. Most surfaces are flat at rest with a quiet border; cards, modals, and the horizontal resort gallery use soft black shadows only where separation or interaction benefits from depth. The solid hero fact panel remains flat and readable independently of the video.

### Shadow Vocabulary

- **Resting Card:** A low, neutral shadow for pricing and content containers.
- **Interactive Lift:** A stronger neutral shadow paired with a small upward transform on hover/focus-capable devices.
- **Protected Overlay:** The deepest neutral shadow for modal and lightbox content over a dark backdrop.

**The Neutral Elevation Rule.** Shadows are black with transparency and a visible vertical offset; brand-colored glows and zero-offset halos do not belong in this system.

**The Reduced-Motion Rule.** Reduced motion keeps state, focus, and hierarchy visible while removing scroll animation, image scaling, lifts, and transition timing.

## Shapes

The standard surface radius is a gently compact 8px. Small menu items may use 4px corners. Fully rounded pills are reserved for compact navigation states and the floating Back to Top control; cards, forms, and callouts never become pills.

Borders are quiet and usually one pixel. Selected tabs use an inset bottom bar, and gallery focus uses an internal outline that does not change layout. The official logo keeps its native aspect ratio and is never reconstructed from CSS geometry or text.

**The One Silhouette Rule.** Use the 8px surface family for cards, notices, forms, images, and dialogs; reserve circles and pills for controls whose compact function earns them.

## Components

### Buttons

- **Shape:** Compact rectangular controls with the standard radius and a minimum 44px interaction height.
- **Primary:** Registration lime over navy, with strong sans-serif label weight.
- **Hover / Focus:** Midnight navy with white text, a coral border, visible external focus outline, and a slight lift when motion is allowed.
- **Secondary:** Transparent inverse treatment on dark photographic or navy surfaces.
- **Text:** Underlined accessible-action teal with no elevation; this is the embedded-form fallback and quiet-action pattern.

### Cards / Containers

- **Corner Style:** Standard 8px radius.
- **Background:** White for general content, Riviera Sky for guidance, Attendance Notice for fee/policy context, and navy for authoritative inverse panels.
- **Shadow Strategy:** Flat or low at rest; stronger only for clear interaction or overlay depth.
- **Internal Padding:** Usually 18–28px, tightening at mobile breakpoints.

### Navigation

The sticky navy header carries the official tertiary FCI logo and exactly five primary destinations. Links maintain a 44px target and use lime-on-navy current state. At smaller widths, Register remains visible while space permits; Menu opens a single-column, keyboard-operable disclosure and returns focus on Escape.

### Registration Tabs

Three tabs represent attendee badge roles only. The selected tab is white with dark teal text and a coral inset bar; hover/focus uses navy with lime confirmation. Arrow keys, Home, and End move the single active tab stop. Sponsorship remains a separate Vendor disclosure labeled “Does Not Register Attendees.”

### Embedded Form State

Every form presents its direct new-tab action before the embed. Loading reserves space and announces the specific form. Readiness is accepted only from a trusted Jotform sizing message. Failure removes the unusable iframe and provides a compact Retry Embedded Form action without removing the direct fallback. No-JavaScript mode exposes every direct path and never reports a busy state.

### Fact Panel

The hero fact panel is a solid Midnight Lobby Navy surface with lime labels and white values. Its contrast and meaning never depend on the optional background video.

### Galleries and Lightbox

Routine gallery views use responsive WebP candidates and preserve meaningful alternative text. Hotel thumbnails may open the full approved JPEG inside a named native dialog. Hover scaling is modest, contained, and absent under reduced motion or non-hover input.

### Footer

The footer follows the corporate FCI hierarchy: official identity and independent-owner statement, convention contact facts, grouped Convention/Attend/Connect navigation, then a cyan-separated legal strip. Content adapts to convention needs instead of copying consumer flooring menus.

## Do's and Don'ts

### Do:

- **Do** lead visitors from fee understanding to one form per attendee, then to the separate hotel step.
- **Do** use the approved FCI tertiary logo and approved event, speaker, and resort imagery at their natural aspect ratios.
- **Do** keep instructional copy within the 65–75 character reading measure and maintain document-level reflow at every supported width.
- **Do** keep direct-form fallbacks visible before cross-origin embeds and make loading, failure, retry, and no-JavaScript states truthful.
- **Do** preserve 44px controls, visible focus, WCAG AA text contrast, and the reduced-motion alternative in every new component.
- **Do** use responsive media candidates for routine views while retaining originals only when the lightbox or fallback requires them.

### Don't:

- **Don't** reconstruct the FCI mark with CSS, replace it with typed “FCI,” distort it, or place it on an unverified color treatment.
- **Don't** present sponsorship as attendee registration or imply that the host page can verify a Jotform submission.
- **Don't** use lime as ambient decoration, coral as normal-size text on light surfaces, or brand-colored shadows as depth.
- **Don't** add autoplaying or eagerly loaded video; playback remains explicit, desktop-only, Save-Data-aware, and disabled for reduced motion.
- **Don't** place essential fees, role choice, recovery, or hotel continuity behind decorative proof or a gallery.
- **Don't** introduce generic conference claims, fabricated testimonials, decorative icons, gradients in text, or a dark-mode contract without product approval.
