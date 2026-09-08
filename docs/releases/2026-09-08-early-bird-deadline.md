# Early bird deadline extension

Matthew requested on September 8, 2026 that the website and registration reflect an early bird deadline of midnight October 23.

- Updated both pricing rows, the pricing requirement, and the registration fee reminder to include October 23 through midnight; standard pricing begins October 24.
- Preserved fee amounts and the requirement to complete both convention and hotel registration.
- Updated PRODUCT.md with the approved deadline. No timezone was supplied or added.
- Inspected all four linked public Jotforms (262185030603144, 262185769189172, 262185864037160, 260975696840069). All returned HTTP 200 and none publishes an early bird deadline; no external form changes were necessary.
- Desktop and 390px mobile browser checks confirmed readable deadline copy and no horizontal overflow. The registration reminder displays the revised deadline.
- Source diff is limited to deadline copy and documentation; git diff --check passed.

Tracking: https://github.com/matthewjudy/fci-convention-website/issues/41
Production deployment and final verification evidence will be recorded on the issue after release.
