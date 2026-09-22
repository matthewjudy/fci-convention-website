# Attendance and Compliance Note Update

**Date:** September 22, 2026  
**Tracking and deployment evidence:** [Issue #43](https://github.com/matthewjudy/fci-convention-website/issues/43)

Matthew Judy supplied and authorized publication of this exact replacement for the Attendance and Compliance Note:

> Per the Franchise Agreement, least one Franchise owner from the branch is required to attend the Annual Convention. Branches that do not send at least one owner from their business will be considered out of compliance and subject to default of their Franchise Agreement

The paragraph replaces the prior statement about sending at least one person and receiving a $1,999 convention contribution charge. The supplied wording, including “least one” and the absence of a final period, is preserved exactly. The disclosure heading and native expand/collapse behavior remain unchanged.

At the time of this release, the separate **Fee and Attendance Reminder** still said “No Branch Attendee: $1,999 charge and out of compliance.” [Issue #44](https://github.com/matthewjudy/fci-convention-website/issues/44) tracked confirmation of that separate policy; this request did not establish a fee repeal. Matthew subsequently authorized aligning that reminder with the owner-attendance requirement; see the [follow-up release record](2026-09-22-owner-attendance-reminder.md).

## Release Verification

Before merging, confirm the exact paragraph appears once in `index.html`, the prior paragraph is absent, and desktop and mobile layouts display the expanded disclosure without clipping. Confirm the diff changes only the requested paragraph and this release record.

Local verification passed: exact replacement comparison against the baseline, `git diff --check`, desktop visual review at a 1532 px viewport, and mobile visual review at 390 px. The expanded paragraph wrapped within its container, no horizontal page overflow was observed, and keyboard Enter successfully collapsed and reopened the disclosure. Independent review found no blocking defects.

After merging, confirm the GitHub Pages workflow succeeds for the merge commit and the canonical [convention website](https://www.fciconvention.com/) serves HTML matching the committed source. Record the PR, commit, deployment run, exact-copy check, and browser results in Issue #43 before closing it. That issue is the authoritative live release status.

The repository wiki is enabled in GitHub metadata, but its Git remote was unavailable when checked for this release. This repository record and the linked issue provide the durable documentation.

## Rollback

Revert the implementation commit through a reviewed pull request, allow the normal GitHub Pages workflow to deploy, and verify the restored paragraph on the canonical domain. No DNS, hosting, registration, or hotel configuration changes are required.
