# Owner Attendance Reminder Update

**Date:** September 22, 2026  
**Tracking and deployment evidence:** [Issue #44](https://github.com/matthewjudy/fci-convention-website/issues/44)

After the Attendance and Compliance Note was published through [PR #45](https://github.com/matthewjudy/fci-convention-website/pull/45), Matthew Judy explicitly directed that the separate $1,999 attendance-charge reminder be revised to match the owner-attendance requirement.

The **Fee and Attendance Reminder** now reads:

> No Franchise Owner From the Branch Attends: $1,999 charge and out of compliance

This replaces “No Branch Attendee” so sending only an employee no longer appears to satisfy the attendance requirement. The $1,999 charge and out-of-compliance consequence are retained. The exact owner-attendance paragraph, including its Franchise Agreement default language, remains as published in PR #45. No layout, registration, hotel, or other fee changes are included.

## Release Verification

The release starts from `8e5b68fdc8e93346ae867528dd015bdb12d9bd95`. Exact replacement comparison passed: the HTML diff changes only the reminder label, the revised label appears once, and the previous label is absent. `git diff --check` passed. Local browser verification passed at the default desktop viewport (1713 pixels wide) and at 390 × 844 pixels: the full reminder is readable, the longer owner-attendance label wraps within its card, and the document has no horizontal overflow.

After merging, confirm the **Deploy convention site** GitHub Pages workflow succeeds for the merge commit and the canonical [convention website](https://www.fciconvention.com/#register) serves HTML matching the committed source. Record the PR, commit, deployment run, exact-copy check, and local/live browser results in Issue #44 before closing it. That issue is the authoritative release status; deployment and production browser verification are pending at the time this record is authored.

## Rollback

Revert the reminder change through a reviewed pull request, allow the normal GitHub Pages workflow to deploy, and verify the restored reminder on the canonical domain. No DNS, hosting, registration, or hotel configuration changes are required. Reverting this follow-up does not revert the separately published Attendance and Compliance Note.
