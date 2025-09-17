# <p align="center"> HomeFortress </p>
<p align="center">
    <img src="https://github.com/RJM-HF/Mail-Security/blob/main/Media/mail-security-banner.png?raw=true" alt="Alt text"/>
</p>

## <p align="center"> Website · Security & Compliance </p>
<h3 align="center">RFC alignment</h3>
    <p align="center">
      <a href="https://www.rfc-editor.org/rfc/rfc7489"><img alt="RFC 7489" src="https://img.shields.io/badge/RFC%207489-DMARC-0ea5e9"></a>
      <a href="https://www.rfc-editor.org/rfc/rfc8461"><img alt="RFC 8461" src="https://img.shields.io/badge/RFC%208461-MTA--STS-22c55e"></a>
      <a href="https://www.rfc-editor.org/rfc/rfc6698"><img alt="RFC 6698" src="https://img.shields.io/badge/RFC%206698-DANE-16a34a"></a>
      <a href="https://www.rfc-editor.org/rfc/rfc6844"><img alt="RFC 6844" src="https://img.shields.io/badge/RFC%206844-CAA-f59e0b"></a>
      <a href="https://www.rfc-editor.org/rfc/rfc4033"><img alt="RFC 4033" src="https://img.shields.io/badge/RFC%204033-DNSSEC-8b5cf6"></a>
    </p>
  </br>


</div> </br>

Quick links:
- [HomeFortress Website](https://www.homefortress.space/) </br>
- [CVE Monitor](https://www.homefortress.space/cve-monitor) </br>
- [CSAF Feed](https://www.homefortress.space/csaf-feed) </br>
</br>

Note: /.well-known/* assets are stored using Cloudflare KV and served by a Worker.

## Well-known endpoints
    Path                                     Purpose
    /.well-known/mta-sts.txt                 MTA-STS policy (HTTPS)
    /.well-known/security.txt                Security contact & policy
    /.well-known/pgp-key.txt                 Public PGP key
    /.well-known/csaf/index.json             CSAF index
    /.well-known/csaf/provider-metadata.json CSAF provider metadata
    /.well-known/dnssec.json                 DNSSEC details
    /security.txt, /pgp-key.txt              Friendly root aliases that map to the well-known paths
</br>

## Content Security Policy (CSP)

To enhance the security of the front-end, a Content Security Policy (CSP) is enforced.
This is an essential security layer that helps to mitigate Cross-Site Scripting (XSS) and other data injection attacks by specifying which sources of content are trusted and allowed to be loaded by the browser.

The policy is implemented as a response header, which is configured directly at Cloudflare. This is done using a **Modify Response Header** rule under the **Transform** section, ensuring the CSP is applied to all pages before they reach the user's browser.

The CSP headers are set at Cloudflare (Transform → Modify response header)


## <h3>License</h3>
- [MIT License](https://en.wikipedia.org/wiki/MIT_License)
