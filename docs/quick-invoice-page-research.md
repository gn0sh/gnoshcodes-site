# Quick Invoice pages: research notes

For `/quick-invoice/` (product), `/quick-invoice/support/` and `/quick-invoice/privacy/`. Written 2026-11-12.
The pages name no competitor. These notes are the evidence behind the "What sets it apart" section.

## What the pages claim, and where it is true in the app (quick-invoice repo, version 1.2)

| Claim on the page | Evidence |
|---|---|
| No account, no sign-up | `store/app-store-listing.md` (Private by design; App Review notes: "no account or sign-in") |
| Records stay on the iPhone, no server | `src/app/privacy.tsx:35,45`; no `fetch(` anywhere in `src/` |
| No ads, tracking or usage analytics; subscription check uses an anonymous ID | `src/app/privacy.tsx:95`; listing "App Privacy" section (RevenueCat, anonymous IDs) |
| First 5 invoices or quotes free; what counts; what stays free | `src/lib/plan.ts:8` (`FREE_LIMIT = 5`), `:52-56` (`WHAT_COUNTS_LINE`, `ALWAYS_FREE_LINE`) |
| Pro $9.99 a month or $79.99 a year (US) | listing, "In-app purchases" table. The app itself shows the App Store's local price (`src/app/subscribe.tsx:189`) |
| Quote to invoice in one tap | `src/app/doc/[id].tsx:1503` ("Convert to invoice") |
| Sent invoices locked; Edit unlocks; voided, not deleted | `src/lib/records.ts:26-35`; `src/app/doc/[id].tsx:1276-1282,1524`; `src/lib/sending.ts:378` |
| A number that left the phone is never reused | `docs/release-1.2.md` (ADR 0017) |
| Three styles, seven colors, logo, license and tax numbers | `src/lib/pdfStyles.ts:15-30`; `src/lib/types.ts:60-62,104,112` |
| "Made with" line can be switched off | `src/app/settings/defaults.tsx:59-63` (no Pro check) |
| Client documents in Spanish; app screens in English | listing, What's New 1.1; `src/app/client/[id].tsx:278`; `src/app/settings/defaults.tsx:31` |
| Pay links to the owner's own PayPal, Venmo, Cash App or card page; app never handles money | `src/lib/payLinks.ts:1-4` |
| Reminders and follow-ups are suggestions; nothing sends itself | `src/lib/types.ts:66`; listing, App Review notes 1.2 ("the app never sends anything by itself") |
| Follow-ups at 3 days, then 7 days later, then stop | `src/lib/quoteFollowUps.ts:14`; listing, What's New 1.2 |
| Repeating invoices: every week, 2 weeks, month | `src/app/schedule/[id].tsx:64-68` |
| Up to 6 job photos, On PDF switch, free on every plan | `src/lib/photoRules.ts:6`; listing, What's New 1.2 |
| Up to two taxes, labor taxed or not | `src/lib/tax.ts:7`; `src/components/TaxSettings.tsx:246-247,282` |
| High-glare mode; Larger Text and VoiceOver | `src/app/(tabs)/settings.tsx:47-63`; listing, What's New 1.1 |
| CSV export; backup; 7-day Undo restore | `src/components/ExportCard.tsx:58-59`; `src/components/BackupCard.tsx:205,279-280`; `src/lib/store.tsx:75` |
| Currencies USD, CAD, GBP, EUR, AUD, NZD; iPhone only | `src/lib/currency.ts:2`; `app.json` (`supportsTablet: false`) |

The sample quote and invoice on the product page are the app's own output: `buildDocHtml` (`src/lib/pdfHtml.ts`) run on a
made-up business, with the print CSS from `src/lib/pdfStyled.ts` scoped to `.pdf` in `quick-invoice/sample-doc.css`.
The logo is drawn for the sample. The Venmo line is not a live link.

## Competitors (checked 2026-11-12)

| Product | What the source says | Source |
|---|---|---|
| Invoice Simple | Essentials $6.99/mo, "Up to 3 invoices per month"; Premium $21.99/mo, unlimited. Client signatures and premium templates are Premium only. | https://www.invoicesimple.com/pricing |
| Joist | "Joist's free plan is no longer available." Basics $10/mo (5 documents a month), Pro $17/mo (adds logo on documents, photos), Elite $32/mo (adds license and insurance fields). 14-day trial with "instant signup". "Anywhere access on mobile & web". | https://www.joist.com/pricing/ |
| Invoice2go | Starter 5.99/mo (2 invoices a month), Professional 9.99/mo (5 a month), Premium 39.99/mo (unlimited, recurring invoices). | https://www.getapp.com/finance-accounting-software/a/invoice2go/pricing/ |
| Jobber | No free plan; Core from $49/mo; a field-service suite (scheduling, teams), not a single-purpose invoicing app. | https://www.getonecrew.com/post/jobber-pricing (secondary source) |
| Square Invoices | Not read in depth. Runs on a Square account and Square's card processing. | https://squareup.com/us/en/invoices (not fetched) |
| Zoho Invoice | Not checked. | |

## Differentiators chosen

1. **No account, no sign-up.** The competitors read are web-and-mobile services with sign-up (Joist says so on its pricing page).
2. **Records stay on the iPhone.** No server of ours. The reverse of "anywhere access on mobile & web".
3. **No ads, no tracking, no usage analytics.**
4. **The customer's business leads the page.** Logo, license number, styles and colors are in every plan, including the free sends. (At Joist, a logo starts at Pro and license fields at Elite.) The page says only what we do.
5. **Money goes straight to the owner.** Pay links only; no payment processing, so no processing fee of ours.
6. **Nothing sends itself**, and **records are never held back** (payments, receipts, backup and export stay free).
7. **5 free sends, then one price.** No per-month invoice caps on the paid plan.
8. **Client documents in Spanish.**

The one sentence about other tools on the page is general and unnamed: "Many invoicing tools start by asking for an email
and a password, then keep your records on their computers." Support: Joist pricing page (sign-up, web access).

## Not verified

- The live App Store prices. $9.99 and $79.99 come from the listing file, not from App Store Connect.
- `https://support.apple.com/118428` (Apple's cancel-a-subscription guide) could not be opened from the build sandbox. `https://support.apple.com/118223` (refunds) was confirmed by search.
- The exact row labels in iOS Settings › Subscriptions ("Quick Invoice", "Cancel Subscription") are Apple's standard wording, not checked on a device.
