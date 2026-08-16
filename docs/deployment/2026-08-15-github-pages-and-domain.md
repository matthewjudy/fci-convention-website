# GitHub Pages and `fciconvention.com` Deployment Runbook

**Status:** Complete. Site deployed, custom-domain DNS configured, certificate approved, and HTTPS enforced.  
**Recorded:** August 15, 2026  
**Repository:** [`matthewjudy/fci-convention-website`](https://github.com/matthewjudy/fci-convention-website)  
**Canonical production host:** `www.fciconvention.com`  
**Redirect host:** `fciconvention.com` → `www.fciconvention.com`

This document is the durable deployment, verification, and rollback record for the 2027 FCI Convention site. It covers the GitHub Pages workflow and the GoDaddy DNS records. It does not change or approve convention content, pricing, registration forms, hotel policy, or analytics.

## Deployment record

- GitHub Pages workflow: [PR #8](https://github.com/matthewjudy/fci-convention-website/pull/8)
- Merge commit: `2c9bef5` (`2c9bef565d1bb61295c3fe1f084c6a36fdaf05b4`)
- First successful deployment: [Actions run 31906362992](https://github.com/matthewjudy/fci-convention-website/actions/runs/31906362992)
- Pages build type: GitHub Actions workflow
- Workflow: `.github/workflows/deploy-pages.yml`
- Deployment environment: `github-pages`

The workflow deploys on relevant pushes to `main` and on manual dispatch. It uses official GitHub Actions pinned to immutable release SHAs.

### Public artifact boundary

The deployed artifact contains only:

- `index.html`
- `assets/`

The staging step copies those paths into `_site` before uploading the Pages artifact. Repository documentation, product notes, design audits, `.impeccable`, Git history, and workflow source are not part of the public website artifact.

Changes limited to repository documentation do not trigger a deployment. Changes to `index.html`, `assets/**`, or the deployment workflow do trigger one after they reach `main`.

## Default GitHub Pages URL

The pre-domain/default project URL is:

`https://matthewjudy.github.io/fci-convention-website/`

The first Actions deployment completed successfully and served the expected 82,990-byte `index.html` with its assets. After the custom domain was attached, the default URL began redirecting to the custom host, which is expected GitHub Pages behavior.

The default HTTPS URL now redirects to `https://www.fciconvention.com/`, which is the expected final behavior after the custom domain is attached.

## Custom-domain configuration

The Pages repository setting uses:

`www.fciconvention.com`

The `www` host is the canonical production hostname. With both DNS variants configured correctly, GitHub Pages should redirect the apex domain `fciconvention.com` to `www.fciconvention.com`.

Because this site publishes through a custom GitHub Actions workflow, it does not require a repository `CNAME` file. The custom domain is held in the GitHub Pages repository setting.

### Account-level domain verification

The domain was verified for the `matthewjudy` GitHub account before the production DNS cutover. Retain this TXT record permanently to protect the domain from Pages takeover:

| Type | Host | Value | TTL |
| --- | --- | --- | --- |
| TXT | `_github-pages-challenge-matthewjudy` | `87c153a1221a71ac7af1f7da85d7bc` | 1 hour |

Fully qualified host:

`_github-pages-challenge-matthewjudy.fciconvention.com`

Do not remove this record during ordinary site updates, certificate renewal, or a temporary hosting rollback.

## GoDaddy DNS target state

The apex uses GitHub Pages' four IPv4 addresses. The `www` host points directly to the GitHub account's Pages hostname, without a repository suffix.

| Type | Host | Value | Purpose |
| --- | --- | --- | --- |
| A | `@` | `185.199.108.153` | GitHub Pages apex |
| A | `@` | `185.199.109.153` | GitHub Pages apex |
| A | `@` | `185.199.110.153` | GitHub Pages apex |
| A | `@` | `185.199.111.153` | GitHub Pages apex |
| CNAME | `www` | `matthewjudy.github.io` | Canonical Pages host |

GoDaddy may display the CNAME value with or without a trailing dot. The target must be `matthewjudy.github.io`, not `matthewjudy.github.io/fci-convention-website` and not a GitHub repository URL.

### IPv6 decision

There are intentionally **no `AAAA` records** for the apex or `www`. Do not add GitHub Pages IPv6 records as part of this deployment. An unexpected or stale `AAAA` record can route IPv6 visitors somewhere different from the verified IPv4 target and can interfere with certificate issuance.

### Records preserved during cutover

The following non-web-routing records were preserved and must not be replaced as part of Pages maintenance:

| Type | Host | Value |
| --- | --- | --- |
| NS | `@` | `pdns05.domaincontrol.com` |
| NS | `@` | `pdns06.domaincontrol.com` |
| CNAME | `_domainconnect` | `_domainconnect.gd.domaincontrol.com` |
| TXT | `_dmarc` | `v=DMARC1; p=quarantine; adkim=r; aspf=r; rua=mailto:dmarc_rua@onsecureserver.net;` |

Preserve any other mail, ownership-verification, or service-specific records unless a separately approved change explicitly targets them. The Pages cutover concerns the apex web `A` records and the `www` CNAME only.

### Propagation note

At the last check, the authoritative GoDaddy nameserver returned the intended records:

- all four GitHub Pages apex `A` records;
- `www.fciconvention.com CNAME matthewjudy.github.io`;
- the retained GitHub account-verification TXT record; and
- no apex `AAAA` records.

The previous `www → fciconvention.com` answer remained in one recursive resolver until its one-hour TTL expired. At final acceptance, both authoritative GoDaddy nameservers and the tested Cloudflare, Google, and Quad9 resolvers returned the intended records.

## TLS certificate and HTTPS enforcement

### Current status

**Complete.** At final acceptance:

- `https_certificate.state` was `approved`;
- the certificate covered both `www.fciconvention.com` and `fciconvention.com`;
- the certificate expiration date reported by GitHub was November 13, 2026;
- hostname-verifying requests passed against all four GitHub Pages IPv4 edges for both domain names; and
- `https_enforced` was `true`.

The first certificate request remained pending for one hour despite valid DNS. Following GitHub's documented recovery, the custom domain was removed and re-added once in Pages settings without changing GoDaddy DNS. The replacement request was approved. One GitHub edge briefly lagged behind the other three; HTTPS enforcement was left off until all four edges presented the custom certificate.

### Enforcement procedure

1. Confirm that both authoritative GoDaddy nameservers return the intended four apex `A` records and the direct `www` CNAME.
2. Confirm that neither the apex nor `www` has an unexpected `AAAA`, competing `A`, forwarding rule, or alternate `CNAME`.
3. Check the Pages API and repository **Settings → Pages** until the certificate is issued and the **Enforce HTTPS** control is available.
4. In **Settings → Pages**, select **Enforce HTTPS**.
5. Recheck the Pages API and confirm `https_enforced` is `true`.
6. Verify HTTP-to-HTTPS and apex-to-`www` redirects, the browser certificate, and representative site assets.

For future certificate renewals or domain changes, do not repeatedly replace correct records or re-save the custom domain while issuance is pending.

## Verification commands

Run these from a machine with `dig`, `curl`, `openssl`, and authenticated GitHub CLI access.

### Authoritative DNS

```sh
dig @pdns05.domaincontrol.com +noall +answer fciconvention.com A
dig @pdns06.domaincontrol.com +noall +answer fciconvention.com A
dig @pdns05.domaincontrol.com +noall +answer www.fciconvention.com CNAME
dig @pdns06.domaincontrol.com +noall +answer www.fciconvention.com CNAME
dig @pdns05.domaincontrol.com +noall +answer fciconvention.com AAAA
dig @pdns06.domaincontrol.com +noall +answer fciconvention.com AAAA
dig @pdns05.domaincontrol.com +noall +answer _github-pages-challenge-matthewjudy.fciconvention.com TXT
```

Expected results:

- each nameserver returns exactly the four documented apex `A` values;
- `www` returns `matthewjudy.github.io`;
- the `AAAA` queries return no answer; and
- the GitHub verification TXT value remains present.

### Public DNS propagation

```sh
dig +short fciconvention.com A
dig +short fciconvention.com AAAA
dig +short www.fciconvention.com CNAME
```

Public resolvers should converge on the same target state. A temporarily stale CNAME can be a resolver cache; compare it with both authoritative nameservers before editing GoDaddy.

### GitHub Pages state

```sh
gh api repos/matthewjudy/fci-convention-website/pages \
  --jq '{html_url,cname,https_enforced,build_type,https_certificate}'

gh run list \
  --repo matthewjudy/fci-convention-website \
  --workflow deploy-pages.yml \
  --limit 5
```

Expected final state:

- `cname` is `www.fciconvention.com`;
- `build_type` is `workflow`;
- the latest deployment is successful;
- certificate issuance is no longer pending; and
- `https_enforced` is `true`.

### HTTP, redirect, and asset checks

```sh
curl -sSIL --max-time 20 http://fciconvention.com/
curl -sSIL --max-time 20 https://fciconvention.com/
curl -sSIL --max-time 20 http://www.fciconvention.com/
curl -sSIL --max-time 20 https://www.fciconvention.com/
curl -sSIL --max-time 20 https://matthewjudy.github.io/fci-convention-website/
curl -sSI --max-time 20 https://www.fciconvention.com/assets/speakers/daymond-john.jpg
curl -sSI --max-time 20 https://www.fciconvention.com/assets/videos/fci-convention-2026-hero-720p-optimized.mp4
```

Expected final behavior:

- both HTTP hosts redirect to HTTPS;
- `https://fciconvention.com/` redirects to `https://www.fciconvention.com/`;
- `https://www.fciconvention.com/` returns the convention page without a redirect loop;
- the default GitHub Pages project URL redirects to the canonical HTTPS custom host; and
- representative image and video paths return successfully.

### Certificate inspection

```sh
openssl s_client \
  -connect www.fciconvention.com:443 \
  -servername www.fciconvention.com \
  </dev/null 2>/dev/null \
  | openssl x509 -noout -subject -issuer -dates -ext subjectAltName
```

Confirm that the certificate is valid for `www.fciconvention.com`, is within its validity period, and is issued by a trusted authority. Also test the apex HTTPS redirect in a browser so any apex certificate problem is visible before launch acceptance.

## Final launch checklist

- [x] Latest Pages workflow completed successfully from the intended `main` commit.
- [x] Both authoritative nameservers return all four intended apex `A` records.
- [x] Both authoritative nameservers return `www CNAME matthewjudy.github.io`.
- [x] No apex or `www` `AAAA` record is present.
- [x] GitHub account-verification TXT remains present.
- [x] GitHub reports the custom-domain certificate as issued and healthy.
- [x] **Enforce HTTPS** is enabled and the API reports `https_enforced: true`.
- [x] HTTP redirects to HTTPS for both apex and `www`.
- [x] Apex HTTPS redirects once to canonical `https://www.fciconvention.com/`.
- [x] The canonical homepage, all 19 published assets, and the hero video load successfully.
- [x] The default GitHub Pages URL redirects to the canonical HTTPS host.
- [x] Mobile and desktop layouts received visual smoke tests on the custom domain.
- [x] Navigation, registration tabs, dialogs, email-copy behavior, and back-to-top behavior work on the custom domain.
- [x] All four Jotforms, the Hard Rock group reservation link, and the resort link resolve to their expected external destinations.
- [x] No mixed-content, certificate, or redirect-loop problem remained in final acceptance testing; the deployed artifact had already passed the documented browser-console QA.

### Final acceptance evidence

- Accepted August 15, 2026 after HTTPS edge propagation completed.
- Deployed commit: `2c9bef565d1bb61295c3fe1f084c6a36fdaf05b4`.
- Live `index.html` SHA-256: `6fb60d4bd1e7b48350583311fb9a3c7b83b139e35c3dc5feee14faa6132dd65c`, exactly matching the committed deployment source.
- All 19 files under the committed `assets/` tree returned HTTP 200 over the canonical HTTPS host.
- All eight direct TLS checks passed: two domain names against four GitHub Pages IPv4 edge addresses.
- Final routing: both HTTP hosts redirect to HTTPS, the HTTPS apex redirects to `https://www.fciconvention.com/`, and the canonical HTTPS host returns HTTP 200.
- Mobile emulation used a 390 × 844 CSS-pixel viewport; document and body scroll widths remained 390 pixels, with the intentionally horizontal resort-photo rail contained inside the viewport.

## Rollback to the prior GoDaddy parked state

The prior parked configuration was represented in GoDaddy as:

- apex `A` record: `@` → **Parked**; and
- `www` CNAME: `www` → `fciconvention.com`.

Use GoDaddy's managed parked-domain setting or record value to restore `A @ = Parked`. Do **not** infer, copy, or manually enter raw GoDaddy parking IP addresses from an old DNS lookup. Those addresses are provider-managed and can change.

### Rollback procedure

1. Record the current Pages and DNS state before changing it.
2. In GoDaddy, remove the four GitHub Pages apex `A` records and restore the apex using GoDaddy's **Parked** value or **Park domain** control.
3. Change the `www` CNAME from `matthewjudy.github.io` back to `fciconvention.com`.
4. Leave the `NS`, `_domainconnect`, `_dmarc`, GitHub verification TXT, and unrelated mail/service records unchanged.
5. Query both authoritative nameservers until they show the parked apex state and `www → fciconvention.com`.
6. Verify the parked behavior from both apex and `www` without relying only on a cached local resolver.
7. After DNS no longer routes the domain to GitHub, remove the repository's custom-domain setting or disable Pages if the rollback is intended to be permanent. Keeping the account-verification TXT is safe and preserves takeover protection.

If the site merely needs to revert to an earlier application version while remaining on GitHub Pages, do not change DNS. Revert the relevant repository commit through a reviewed PR, allow the workflow to deploy, and repeat the custom-domain smoke tests.

## Operational caveats

### Static hosting and external completion

GitHub Pages serves static files only. This site has no server-side registration endpoint, contact-form endpoint, user authentication, or submission-status integration. Registration is completed on external Jotform pages, hotel booking is completed on the external Hard Rock reservation site, and convention support uses the visitor's email client. A successful outbound click is not proof of a submitted registration.

Any future requirement for server-side form handling, authenticated attendee content, webhooks, secrets, dynamic redirects, custom response headers, or reliable submission analytics requires an additional service or a move to a host designed for those capabilities.

### Video and bandwidth

The optimized desktop hero video is **4,238,929 bytes (approximately 4.24 MB)**, a 75.3% reduction from the superseded 17.15 MB file. The entire current asset set is **12,880,653 bytes (approximately 12.28 MiB)**, 44.0% smaller than the prior asset tree despite adding responsive variants. The nine displayed gallery images have 480px, 960px, and 1440px WebP candidates totaling 2,320,676 bytes, and the hero poster is 279,206 bytes. The implementation selects an appropriate image candidate and avoids loading the hero video on mobile, for reduced-motion users, and for visitors with data-saving enabled. The video remains the largest single bandwidth risk.

GitHub Pages documents a soft bandwidth limit of 100 GB per month. The expected franchisee audience is likely compatible with that limit, but a materially broader campaign or repeated uncached video traffic should trigger bandwidth review and potentially move the video to a dedicated media/CDN service.

### GitHub Pages policy and availability

GitHub describes Pages primarily as static project hosting and states that it is not intended as free hosting for an online business, e-commerce site, or a site primarily facilitating commercial transactions. The current page is a static informational guide whose registration and hotel transactions occur on external services. If the site begins collecting payment, sensitive data, or submissions directly, re-evaluate hosting before release.

Pages is also a public service with documented usage limits and without an application-specific availability commitment in this repository. Monitor deployments and the public site during registration deadlines. For stronger production controls, custom headers, edge logic, access restrictions, or a commercial hosting posture, evaluate a platform such as Cloudflare Pages rather than extending this static deployment beyond its intended role.

## Routine deployment procedure

1. Make site changes on a branch and validate them locally.
2. Merge an approved PR into `main`.
3. Confirm the **Deploy convention site** workflow succeeds.
4. Verify the canonical custom domain, not only the source or default GitHub URL.
5. Exercise representative assets and the external registration/hotel handoffs.
6. Record any production-specific failure in a GitHub issue before considering the change complete.
