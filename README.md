# Vault — Secure Password & Secret Generator

**Vault** is a privacy-first, zero-dependency security utility created by **Emmanuel**. It generates strong passwords, passphrases, PINs, patterns, API-style tokens, and infrastructure-grade secrets directly in the browser.

The application is designed around a simple rule: **your generated secrets should stay on your device.**

## Description

Vault is a lightweight web app/PWA for generating and evaluating credentials without requiring an account, backend, database, or build system. Cryptographically secure browser randomness (`crypto.getRandomValues`) is used for generated secrets.

It includes:

- Strong random password generation
- Passphrase generation
- PIN generation
- Phone-style pattern generation
- Custom password templates
- Bulk generation
- Password strength and entropy estimates
- Stateless deterministic password derivation using PBKDF2-SHA-256
- Infrastructure presets for SSH, ERP/admin, networks, Wi-Fi, services and databases
- Hex, Base64 and UUID-style token generation
- Optional Have I Been Pwned breach checking using k-anonymity
- English, Hindi and Kannada UI
- Light/dark theme
- Installable PWA with offline support
- Security-focused response headers for Vercel

## Privacy

Vault does not require an account or application server.

Generated values are created locally with the Web Crypto API. The optional breach check is the only external request and uses the Have I Been Pwned range API: only the first five characters of the SHA-1 hash are sent.

Session history is held only in the current browser tab/session memory and is not persisted to localStorage or a database.

## Security notes

- Password and token generation uses `crypto.getRandomValues()`.
- Weighted pattern selection also uses the same cryptographically secure RNG.
- Reveal-animation masking uses the secure RNG as well.
- No generated secret is sent to a server by the generator itself.
- The breach-check API uses k-anonymity rather than sending the plaintext password.
- Vercel headers include CSP, HSTS, frame protection, MIME sniffing protection, referrer policy and a restrictive permissions policy.
- The service worker uses network-first navigation so deployed HTML changes are not unnecessarily trapped behind stale cache entries.

## SEO and discoverability

The app includes:

- Search-friendly title and meta description
- Author/creator metadata for Emmanuel
- Robots directives
- Open Graph metadata
- Twitter card metadata
- JSON-LD `WebApplication` structured data
- PWA application metadata
- Semantic visible product description and footer attribution

## Project structure

```text
index.html      Main app, CSS and JavaScript
manifest.json   PWA manifest and app metadata
sw.js           Service worker and offline cache
icon.png        512×512 app icon
icon-192.png    192×192 app icon
vercel.json     Security headers and deployment configuration
LICENSE         MIT license
```

## Run locally

A service worker requires `http://localhost` or HTTPS.

```bash
npx serve .
```

or:

```bash
python3 -m http.server 8000
```

Then open the local address shown by the server.

## Deploy to Vercel

No build step is required.

```bash
npm i -g vercel
vercel --prod
```

You can also push the folder to GitHub and import the repository into Vercel.

## Updating deployments

The service worker cache version is bumped whenever the app shell changes. Navigation requests are network-first and fall back to the cached shell when offline.

## Author

**Emmanuel**

Vault is released under the MIT License.
