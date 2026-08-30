<div align="center">
  <img src="assets/logo.png" alt="ARK: Survival Ascended logo" width="200">

  <p align="center">
    <img src="https://img.shields.io/badge/data-JSON-000000?logo=json&logoColor=white" alt="JSON">
    <img src="https://img.shields.io/badge/updated-daily-4FC07D" alt="Updated daily">
    <img src="https://img.shields.io/badge/licence-CC0%201.0-2EA44F" alt="CC0 1.0">
    <img src="https://img.shields.io/badge/no%20API%20key-free%20access-FFB454" alt="No API key">
  </p>

  <p align="center">
    <img src="https://img.shields.io/badge/PlayStation-0070D1?logo=playstation&logoColor=white" alt="PlayStation Store">
    <img src="https://img.shields.io/badge/Xbox-107C10?logo=xbox&logoColor=white" alt="Microsoft Store">
    <img src="https://img.shields.io/badge/Steam-1B2838?logo=steam&logoColor=white" alt="Steam">
    <img src="https://img.shields.io/badge/markets-FR%20%C2%B7%20BE%20%C2%B7%20GB%20%C2%B7%20US%20%C2%B7%20CA-8B93A7" alt="Markets">
  </p>

  <p align="center">
    <i>Daily price tracking for the ARK: Survival Ascended catalogue on PlayStation, Xbox and Steam.</i><br>
    <a href="https://devredious.github.io/asa-prices/en/">Browse prices</a> &nbsp;·&nbsp;
    <a href="https://devredious.github.io/asa-prices/fr/">Français</a> &nbsp;·&nbsp;
    <a href="https://devredious.github.io/asa-prices/asa-prices.json">JSON dataset</a> &nbsp;·&nbsp;
    Repository <a href="https://github.com/DevRedious/asa-prices">DevRedious/asa-prices</a>
  </p>
</div>

> 🇫🇷 Ce document est aussi disponible en [français](docs/README.fr.md).

---

[`asa-prices.json`](asa-prices.json) is rebuilt every day around 09:00 (Europe/Paris),
covering **five markets** — France, Belgium, United Kingdom, United States and Canada —
across all three storefronts. The price history is this repository's Git history:
`git log -p asa-prices.json`.

## Usage

```
https://devredious.github.io/asa-prices/asa-prices.json
```

A static file on a CDN: call it as often as you like, no key and no authentication.

```js
const data = await fetch('https://devredious.github.io/asa-prices/asa-prices.json').then(r => r.json());
const astraeos = data.products.find(p => p.name.includes('Astraeos'));
console.log(astraeos.best_price_eur, astraeos.best_store, astraeos.best_market);
```

The site is published in English (`/en/`) and French (`/fr/`). The root redirects
according to the browser's language, with visible links if JavaScript is disabled.

## Format

| Field | Meaning |
|---|---|
| `schema` | format version; only bumped on a breaking change |
| `generated_at` | ISO 8601 timestamp of the collection run |
| `rates` | conversion rates to the euro at collection time |
| `counts` | number of products, offers, and products on sale |
| `products[]` | one object per product, across every store |

For each product:

| Field | Meaning |
|---|---|
| `name` | the most complete label found across the storefronts |
| `free` | `true` when the item is sold nowhere (a free map) |
| `on_sale` | `true` when at least one store discounts it |
| `best_price_eur` / `best_store` / `best_market` | the cheapest offer, converted to euros |
| `released_at` / `released_ts` | release instant, in UTC and as a Unix timestamp |
| `released_by_store` | release instant per storefront — they genuinely differ |
| `offers[]` | the per-store, per-market breakdown |

And for each offer: `store`, `market`, `currency`, `price`, `price_eur`, `original`,
`discount_pct`, `offer_until`, `released_at`, `url`, and `status` — `sale` when sold,
`free` when free, `no_price` when bundled into a pass and not sold separately.

## Notes

- **All instants are UTC**, in ISO 8601. Render them in your reader's own time zone.
  A release listed as 13 February locally may well be the 14th in UTC.
- Foreign prices are converted to euros for indication only, at the collection day's rate.
- **PlayStation issues one product listing per commercial zone, not per country**:
  one covers Europe (euro and pound sterling), another the Americas. France and
  Belgium therefore share the same listing and the same price.
- `no_price` means *not sold separately* — it does not mean free.
- The catalogue is rediscovered on every run: new content enters the dataset on its own.
- Prices are identical across all three stores within the eurozone, but diverge
  noticeably elsewhere. Bundles follow no rule at all: each store sets its own
  contents and discount.

Collected from the public storefronts of Sony, Microsoft and Valve.
This project is affiliated with neither those companies nor Studio Wildcard.
All trademarks belong to their respective owners.
