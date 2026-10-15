# Privacy pages for five apps — 2026-10-15

Goal: publish `clipsync/`, `kek/`, `moneta/`, `securevault/`, `giftfolio/` `privacy.html` on the GitHub Pages site, same layout as `applockguard/privacy.html` (EN + UK, effective 2026-10-15, contact Osvald.studio26@gmail.com), every statement verified against the app code on `origin/feat/l10n-complete-2026-10-15` (Moneta also `origin/feat/apartment-car-payments-2026-10-13`).

## Checklist
- [x] Read manifests, gradle deps, network/crypto/permission code of all five apps
- [x] clipsync/privacy.html
- [x] kek/privacy.html
- [x] moneta/privacy.html
- [x] securevault/privacy.html
- [x] giftfolio/privacy.html
- [x] Links in index.html
- [x] HTML validation (python html.parser: 9 pages OK, exit 0; macOS tidy 2006 only complains about HTML5 `<main>` and UTF-8, same as the existing applockguard page) + relative link check
- [x] Push branch `feat/privacy-pages-2026-10-15` (owner publishes)

## Files
`clipsync/privacy.html`, `kek/privacy.html`, `moneta/privacy.html`, `securevault/privacy.html`, `giftfolio/privacy.html`, `index.html`, this plan.

## Verification
`python3 -I check_html.py` (scratch script, not committed) over every `*.html`: well-formed tags, no `<script>`, no external requests, every relative `href` resolves.

## Findings / risks
- GiftFolio *does* request `READ_CONTACTS` at runtime (only when importing from contacts, to read the picked contact's birthday); the page says so instead of "no permission".
- ClipSync has an opt-in Notification Listener (mirrors notifications to paired devices, encrypted, LAN only) and an optional biometric app lock — both documented.
- Moneta also calls NBU / CoinGecko / stooq (rates), NHTSA / fueleconomy.gov / baza-gai.com.ua (vehicle lookup), Binance / OKX (read-only keys), ML Kit on-device OCR for receipts; documented. Google Wallet notification capture exists only on the PR #8 branch (not merged) — documented as optional/opt-in.
- KEK and GiftFolio keep `allowBackup="true"` (Android system backup may copy local data); ClipSync leaves the default (true). Stated as-is.
