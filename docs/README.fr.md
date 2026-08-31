<div align="center">
  <img src="../assets/logo.png" alt="ARK: Survival Ascended logo" width="200">

  <p align="center">
    <img src="https://img.shields.io/badge/donn%C3%A9es-JSON-000000?logo=json&logoColor=white" alt="JSON">
    <img src="https://img.shields.io/badge/mise%20%C3%A0%20jour-quotidienne-4FC07D" alt="Mise à jour quotidienne">
    <img src="https://img.shields.io/badge/licence-CC%20BY%204.0-2EA44F" alt="CC BY 4.0">
    <img src="https://img.shields.io/badge/sans%20cl%C3%A9%20d'API-libre%20d'acc%C3%A8s-FFB454" alt="Sans clé d'API">
  </p>

  <p align="center">
    <img src="https://img.shields.io/badge/PlayStation-0070D1?logo=playstation&logoColor=white" alt="PlayStation Store">
    <img src="https://img.shields.io/badge/Xbox-107C10?logo=xbox&logoColor=white" alt="Microsoft Store">
    <img src="https://img.shields.io/badge/Steam-1B2838?logo=steam&logoColor=white" alt="Steam">
    <img src="https://img.shields.io/badge/march%C3%A9s-FR%20%C2%B7%20BE%20%C2%B7%20CA-8B93A7" alt="Marchés FR, BE, CA">
  </p>

  <p align="center">
    <i>Relevé quotidien des prix du catalogue ARK: Survival Ascended sur PlayStation, Xbox et Steam.</i><br>
    <a href="https://devredious.github.io/asa-prices/fr/">Consulter les prix</a> &nbsp;·&nbsp;
    <a href="https://devredious.github.io/asa-prices/en/">English</a> &nbsp;·&nbsp;
    <a href="https://devredious.github.io/asa-prices/asa-prices.json">Jeu de données JSON</a> &nbsp;·&nbsp;
    Dépôt <a href="https://github.com/DevRedious/asa-prices">DevRedious/asa-prices</a>
  </p>
</div>

> 🇬🇧 This document is also available in [English](../README.md).

---

Le fichier [`asa-prices.json`](../asa-prices.json) est régénéré chaque jour vers 9 h (Europe/Paris).
L'historique des prix est l'historique Git de ce dépôt : `git log -p asa-prices.json`.

## Utilisation

```
https://devredious.github.io/asa-prices/asa-prices.json
```

Le site est publié en français (`/fr/`) et en anglais (`/en/`). La racine aiguille
selon la langue du navigateur, avec des liens visibles si JavaScript est désactivé.

Fichier statique servi par CDN : appelez-le autant que vous voulez.

```js
const data = await fetch('https://devredious.github.io/asa-prices/asa-prices.json').then(r => r.json());
const astraeos = data.products.find(p => p.name.includes('Astraeos'));
console.log(astraeos.best_price_eur, astraeos.best_store);   // 4.4 'steam'
```

## Format

| Champ | Sens |
|---|---|
| `schema` | version du format ; n'augmente qu'en cas de rupture |
| `generated_at` | horodatage ISO du relevé |
| `rates` | taux de conversion vers l'euro au moment du relevé |
| `counts` | nombre de produits, d'offres, et de produits en promotion |
| `products[]` | un objet par produit, tous magasins confondus |

Pour chaque produit :

| Champ | Sens |
|---|---|
| `name` | libellé le plus complet trouvé parmi les boutiques |
| `free` | `true` si le produit n'est vendu nulle part (carte gratuite) |
| `on_sale` | `true` si au moins une boutique le solde |
| `best_price_eur` / `best_store` / `best_market` | l'offre la moins chère, convertie en euros |
| `offers[]` | le détail par boutique et par marché |

Et pour chaque offre : `store`, `market`, `currency`, `price`, `price_eur`,
`original`, `discount_pct`, `offer_until`, `url`, et `status`
(`sale` vendu · `free` gratuit · `no_price` inclus dans un pass, pas vendu seul).

## Précisions

- Les prix canadiens sont convertis à titre indicatif, au taux du jour du relevé.
- PlayStation publie une fiche unique pour toute la zone euro : la France et la
  Belgique y partagent le même prix, et le Canada relève d'une autre fiche, non suivie.
- Le catalogue est redécouvert à chaque passage : un nouveau DLC entre seul dans le suivi.

Données relevées sur les boutiques publiques de Sony, Microsoft et Valve.
Ce dépôt n'est affilié ni à ces sociétés ni à Studio Wildcard.

## Attribution

Sous licence [CC BY 4.0](../LICENSE). Toute réutilisation doit créditer la source :

> Données de prix ARK: Survival Ascended par DevRedious, CC BY 4.0 — https://github.com/DevRedious/asa-prices
