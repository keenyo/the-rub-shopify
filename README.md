# The Rub — Shopify site code

Custom Liquid sections for the "The Rub" Shopify store, built outside the theme's
native section/schema system for speed. Organized here for version history and
as a handoff-ready reference.

## Status

| Page | Status |
|---|---|
| Homepage | ✅ Live — 9 sections, real content |
| Product page | ⚠️ Partially live — hero (price/variants/cart) is wired to real Shopify product data. Ingredients list and review count are still placeholder text. |
| Recipe page | ✅ Live — dynamic Blog Article template. Hero, stats (prep/cook/servings/difficulty), and the full story/ingredients/directions/tip layout are all driven by article metafields — not the content box (Shopify's rich text editor strips custom HTML on save, so metafields are the reliable path). "More from the test kitchen" pulls real data automatically for every other article. |

## Folder structure

```
homepage/        9 Custom Liquid sections, paste in this order onto the Home page
product/         7 Custom Liquid sections — MUST go on the Product template (uses
                 Shopify's `product` object for price/variants/cart, not a generic Page)
recipe-page/     5 Custom Liquid sections for the "Default article" template.
                 Requires 11 Article metafields (namespace "custom") — see table below.
reference/       Full standalone HTML previews of each page — open these directly in
                 a browser to see the intended design. NOT for pasting into Shopify.
```

## Recipe page metafields (Settings → Metafields and metaobjects → Articles)

Every new recipe needs these filled in (all under the "Articles" resource):

| Name | Type | Notes |
|---|---|---|
| Story | Multi-line text | 2-4 sentence intro |
| Ingredients main | Single line text, list | one ingredient per list item |
| Ingredients rub | Single line text, list | rub-specific ingredients |
| Rub callout | Multi-line text | optional upsell line |
| Step titles | Single line text, list | one per step |
| Step descriptions | Single line text, list | same order/count as Step titles |
| Pro tip | Multi-line text | |
| Prep time | Single line text | e.g. "10 min" |
| Cook time | Single line text | e.g. "20 min" |
| Servings | Single line text | e.g. "4" |
| Difficulty | Single line text | e.g. "Easy" |

Also set the article's **Tags** (category, e.g. "Grilling") and **Image** (featured photo) —
both are used by the hero and the related-recipes cards.

## How to install a page

1. Duplicate your theme first (Online Store → Themes → ⋮ → Duplicate). Never edit the live theme directly.
2. Add a **Custom Liquid** section for each numbered file, in order, pasting the file's contents in as-is.
3. `00-styles` must be first/topmost in the list — it loads fonts and CSS that every section after it depends on.
4. Preview before publishing.

## Known gaps / next steps

- Product page's ingredient list and review count are hardcoded — not tied to real data.
- Everything here is still raw Custom Liquid blocks, not real theme sections with
  `{% schema %}` settings. That's the next upgrade — turns image/link edits into
  point-and-click fields instead of code edits. Do this once content stabilizes.
- Hero photo on the homepage needs to be uploaded via Shopify Files and swapped in
  (see comments in `homepage/02-hero.liquid`).
- Fake `<nav>` sections have been removed site-wide in favor of the theme's real header.

## Brand system

Kraft paper background, painter's-tape blue accent, brushed steel, chili red, and an
acid yellow-green (pulled from the original "Wing Lab" brand deck). Type: Space Grotesk
(headlines), Space Mono (labels/lists), Syne (body), Permanent Marker (handwritten tape
callouts). All fonts load via Google Fonts in each page's `00-styles` file.
