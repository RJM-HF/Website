# <p align="center"> HomeFortress </p>
<p align="center">
    <img src="https://github.com/RJM-HF/Mail-Security/blob/main/Media/mail-security-banner.png?raw=true" alt="Alt text"/>
</p>
## <p align="center"> Website · Security & Compliance </p>



A minimal, security-first landing page for homefortress.space.
Fronted by Cloudflare (headers, HSTS, TLS, Workers/KV) and served from GitHub Pages.

</div>
Quick links

Website: https://www.homefortress.space/

CVE Monitor: /cve-monitor.html

CSAF Feed: /csaf-feed.html
  </br>
<h3 align="center">RFC alignment</h3>
    <p align="center">
      <a href="https://www.rfc-editor.org/rfc/rfc7489"><img alt="RFC 7489" src="https://img.shields.io/badge/RFC%207489-DMARC-0ea5e9"></a>
      <a href="https://www.rfc-editor.org/rfc/rfc8461"><img alt="RFC 8461" src="https://img.shields.io/badge/RFC%208461-MTA--STS-22c55e"></a>
      <a href="https://www.rfc-editor.org/rfc/rfc6698"><img alt="RFC 6698" src="https://img.shields.io/badge/RFC%206698-DANE-16a34a"></a>
      <a href="https://www.rfc-editor.org/rfc/rfc6844"><img alt="RFC 6844" src="https://img.shields.io/badge/RFC%206844-CAA-f59e0b"></a>
      <a href="https://www.rfc-editor.org/rfc/rfc4033"><img alt="RFC 4033" src="https://img.shields.io/badge/RFC%204033-DNSSEC-8b5cf6"></a>
    </p>
  </br>
<h2>How it’s built</h2>

Static site in this repo (index.html, /assets/main.css, images in /img).

GitHub Pages hosts the content.

Cloudflare sits in front:

Transform Rules set security headers (CSP, HSTS, etc.).

Minimum TLS enforced at the edge.

Worker + KV serves well-known security files (MTA-STS, security.txt, CSAF) and handles apex → www redirects.

# <h3 align="center">Repository layout</h3>
  ├─ assets/</br>
  │  └─ main.css</br>
  ├─ img/</br>
  │  ├─ hf-logo.png</br>
  │  ├─ favicon-16x16.png</br>
  │  └─ favicon-32x32.png</br>
  ├─ cve-monitor.html</br>
  ├─ csaf-feed.html</br>
  └─ index.html</br></br>


Note: /.well-known/* assets are stored in Cloudflare KV and served by the Worker (not in this repo).

Well-known endpoints
Path	Purpose
/.well-known/mta-sts.txt	MTA-STS policy (HTTPS)
/.well-known/security.txt	Security contact & policy
/.well-known/pgp-key.txt	Public PGP key
/.well-known/csaf/index.json	CSAF index
/.well-known/csaf/provider-metadata.json	CSAF provider metadata
/.well-known/dnssec.json	DNSSEC info (optional)
/security.txt, /pgp-key.txt	Friendly root aliases that map to the well-known paths
Security headers

Set at Cloudflare (Transform → Modify response header):

Strict-Transport-Security: max-age=31536000; includeSubDomains; preload
Content-Security-Policy: default-src 'self'; base-uri 'self'; object-src 'none'; frame-ancestors 'none'; form-action 'self'; img-src 'self' data:; font-src 'self' data:; style-src 'self'; script-src 'self' 'sha256-6B6nJpMew4nODwWsyP0FE2UREshfKBDoWxy+O4pic54='; upgrade-insecure-requests;
Referrer-Policy: no-referrer
Permissions-Policy: geolocation=(), microphone=(), camera=()
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
Cross-Origin-Resource-Policy: same-origin
Cross-Origin-Opener-Policy: same-origin
Cross-Origin-Embedder-Policy: require-corp


If you move the tiny inline script into /assets/app.js, you can drop the CSP sha256-… and keep script-src 'self' only.

Domain & mail posture

DNSSEC: signed

DANE (TLSA): published for MX

SPF / DKIM / DMARC: configured

MTA-STS: mode=enforce with TLS-RPT enabled

(Validated with Hardenize, Internet.nl, and common mail/security toolchains.)

Local preview

Any static server works:

# Python 3
python -m http.server 8080

# or Node
npx http-server -p 8080


Open http://localhost:8080

Deploy

Push to main → GitHub Pages publishes → Cloudflare serves.

Cloudflare Worker/KV: publish via Wrangler or the CF dashboard to update well-known files.

Report a security issue

Please email advisory@homefortress.space
 (PGP available via /.well-known/pgp-key.txt).
For coordinated disclosure, include relevant details, proof-of-concept, and impact where possible.

Credits

Cloudflare (edge security & Workers)

GitHub Pages (static hosting)

RFCs & Internet standards bodies (IETF, CAB Forum)

License

This repository’s website content is © its authors.
If you intend to reuse assets or code, see the LICENSE file (or open an issue to discuss).
