# Vendor Step 1 Cleanup

**Date:** September 24, 2026  
**Tracking and final deployment evidence:** [Issue #35](https://github.com/matthewjudy/fci-convention-website/issues/35)

Matthew Judy requested that Vendor Step 1 omit the orange Fee and Attendance Reminder and move the existing blue Before You Begin guidance into its space. The Vendor path also removes Looking for Diamond Tier Sponsorship?, the normal Open Vendor Form in a New Tab link, and the entire Diamond Tier Sponsorship Intake disclosure.

The franchisee reminder remains available on Franchise Owner and Design Associate/Employee. The Vendor attendee Jotform remains the registration path. No replacement vendor fee claim is introduced. This direction supersedes Issue #35’s earlier hold for replacement wording.

## Verification

Local checks passed: requested text and sponsorship endpoint are absent; Owner and Employee panel markup is unchanged; inline JavaScript parses; `git diff --check` is clean. Browser checks passed at 1440, 390, and 320 pixels with no horizontal overflow. Vendor guidance starts at the former reminder’s left edge and fills the row; mouse/keyboard tab changes restore the reminder for Owner and Employee. The Vendor iframe reported ready, a simulated iframe failure displayed valid retry/contact guidance, and retry returned to ready. With page scripts disabled, Vendor remains exposed and its noscript link points to the existing registration URL. No browser errors were recorded. The mechanical scan ran with its documented regex fallback and reported only the existing 2px pause-icon radius advisory.

Production acceptance requires a successful GitHub Pages run and canonical HTML matching the merged source. Issue #35 holds the final PR, deployment, and production evidence.

## Rollback

Revert this change through a pull request and allow the normal Pages workflow to publish it. No DNS, Jotform configuration, or hotel setup changes are involved.
