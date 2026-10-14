# Reusable WhatsApp Catalog

A static, data-driven product catalog with packaging quantities, estimated prices, a saved selection list and a WhatsApp handoff. **Every price in `data/products.json` is a placeholder estimate, not a verified retail price; replace and confirm all prices before launch.** No accounts or backend are used.

## Pricing

Pricing display and currency formatting are configured in `data/brand.json` under `pricing` (`enabled`, `currencySymbol`, `symbolPosition`, `locale` and `decimals`). Packaging-option prices live only in `data/products.json`; saved selections store quantities only and recalculate estimates from that file.

The current Gibs sample values are placeholders derived from the individual-box estimate: full cartons are 18 boxes less 5%, rounded to the nearest Rs 10; half cartons are half of the rounded carton estimate, rounded to Rs 10; individual boxes are rounded to Rs 5. These figures are for interface testing only and should not be used to quote or accept an order. Set `pricing.enabled` to `false` to hide prices and totals.

## Preview

Run a static server from this folder, then open its local address:

```sh
python3 -m http.server 8000 --bind 0.0.0.0
```

Visit `http://localhost:8000`. Do not open `index.html` directly; browsers block the JSON fetches on `file://`.

## Add a product

1. Put a 600 × 400 WebP package image in `assets/products/`.
2. Add a unique product object to `data/products.json` with its image path, category, availability and packaging options.
3. Use category IDs from `data/categories.json` and packaging type IDs from `packagingTypes`.
4. Reload the page. Products are ordered as they appear in the JSON array.

## Make another brand

Edit `data/brand.json` (brand ID, name, logo, theme, language, direction and WhatsApp number), then replace the logo and favicon under `assets/brand/`. Update `data/categories.json`, `data/products.json` and `data/i18n/en.json` as needed. Use international digits for the WhatsApp number. The selection is stored separately for each brand ID.

The first six product visuals are local crops from the supplied design reference. Full Carton and Half Carton use plain, unbranded local illustrations; Individual Box reuses the selected product's image. The 14 later product images are locally saved, normalized packaging photos from the official SM Foods bakery page: Crispee Banana, Orange and Strawberry Wafers; JoyStik Chocolate Stick; Makhan Waala Butter Cookies; Zeera Waala Bakery Style Cookies; Coconut Waala Cookies; Tea Time Fine Line Biscuits; Cookiez Pineapple & Coconut Cookies; Crispy Zeera Biscuits; Classic Lemon Sandwich Biscuits; Mango Masti Sandwich Biscuits; Panjeeri Traditional Biscuits; and Milkoney Honey & Milk Biscuits. No external image requests are made at runtime.
