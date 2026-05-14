# weddingguest-v2

A standalone **guest portal** for Aria & Marcus's destination wedding at AVA Resort Cancún. Spinoff of the All-In Weddings bride-side Wedding Portal — re-skinned to AVA's brand language (magenta primary, sunset coral, sandy-cream neutrals, Cormorant + Montserrat typography) and an itinerary-first home that surfaces Allie's recommended weekend upsells inline with the locked-in wedding events.

This is **v2** of the guest portal. It snapshots everything from `weddingguest-v1` plus two major surfaces added afterwards: a **Guest Registry** tab where guests can gift "wedding extras" (on-property experiences) or contribute to a shared honeymoon fund, and a **Profile screen** with a refer-a-friend program that earns guests a free $245 round-trip airport voucher when their friends book.

## What's in here

```
weddingguest-v2/
├── index.html      # the entire guest portal (self-contained, no build step)
├── vercel.json     # cleanUrls + no trailing slash
└── README.md
```

`index.html` is a single static HTML file with embedded CSS and vanilla JS. State persists to `localStorage` so guests can plan a trip across sessions without an account.

## Run locally

```bash
# any static server works
python3 -m http.server 8080
# then open http://localhost:8080
```

Or open `index.html` directly in a browser — it has no external dependencies beyond Google Fonts and a few Unsplash photos.

## Deployment

The repo is configured for Vercel out of the box. Connect on [vercel.com/new](https://vercel.com/new), import this repo, and it deploys as-is — `vercel.json` keeps URLs clean.

## What's new in v2 (vs v1)

- **Guest Registry tab** — six on-property "wedding extras" guests can gift in full (Honeymoon Suite upgrade, private oceanfront dinner, couples spa day, sunset catamaran charter, in-suite breakfast week, golden-hour photo session) plus a pooled **Honeymoon Fund** card with a live progress bar and quick-pick contribution chips ($50 / $100 / $250 / $500). Pre-claimed experiences show "Gifted by …" so they can't be double-claimed; the guest's gifts roll into the itinerary drawer as `Wedding gift` lines.
- **Profile screen** — reached by clicking the avatar (or the new "Refer · earn $245" pill) in the top bar. Shows account info, RSVP status, and a compact itinerary recap.
- **Refer-a-friend program** with a free Transportation Voucher reward. Deterministic referral code + share link (copy / email / SMS / native share), an inline invite form, and a friend list with per-friend status (Pending / ★ Booked). When a friend books, the cart picks up the earned voucher: it applies as a `−$245` discount line against the booked transportation, or surfaces as a `$0 · ready to apply` perk if transport isn't booked yet. The bar pill flips to a "★ voucher earned" state once unlocked.

Demo defaults seed one pending invite (Camila Reyes) and one booked friend (Marcus Pham), so the voucher-earned state is visible on first load.

## Routes / surfaces

- `/` — Email preview → Login (or, if a guest is already signed in via `localStorage`, the home timeline)
- **Home** — Hero countdown + the wedding-weekend timeline as the page anchor, with three Allie-recommended upsell cards spliced in chronologically. Four action tiles below: Stay, Spa, Excursions, **Registry**.
- **Stay** — Discounted room block at AVA Resort Cancún (5 room types, every room oceanfront per AVA's Oceanfront Promise™, group-code chip, live night recalculation, every card explicitly shows the rack-rate discount %)
- **Spa** — The Spa at AVA wedding rates
- **Excursions** — Off-property tours (Riviera Maya golf, Isla Mujeres catamaran, whale-shark snorkel, Tulum ruins, MUSA underwater museum, ATV + zipline, etc.)
- **Schedule** — Full timeline + logistics, plus three upsell modules: an Extend-Stay 10%-off banner at the top, a Book-Transportation-with-Allie callout inline with the timeline, and a Post-Wedding-Recovery bundle (extra night + 20%-off massage) at the bottom
- **Registry** — Wedding extras + honeymoon fund (see "What's new")
- **Profile** *(via avatar)* — Account info, refer-a-friend hero, itinerary recap

A floating itinerary drawer collects everything (room, add-ons, registry gifts, transportation, recovery, earned vouchers) and rolls up to a confirm-everything CTA.

## Demo defaults

The login screen pre-fills with `Sofía Vargas` / `sofia@vargas.co` (a bridesmaid from Aria's existing guest list) so the prototype is one click from a fully populated experience. The first visit also shows a simulated invitation email from Allie before the sign-in screen.
