# HZRD — Shopify Theme

Custom Shopify theme for HZRD, ready-to-wear. Design language: **hazard
placard / spec-sheet industrial** — every product card reads like a
DOT/UN hazard label (diagonal caution-tape corner, spec-sheet data block,
a "HZRD IDX" meter in place of generic "bestseller" badges), tying the
visual system back to the brand name instead of a generic streetwear look.

Palette is monochrome: white background, black text and accents
throughout (no color accent). Sold-out flags keep a small red tag as
the only non-monochrome element.

## What's in here

```
layout/theme.liquid        Base HTML wrapper (header, footer, fonts)
sections/
  hero.liquid               Homepage hero
  collection-grid.liquid    Collection page: filter chips + sort + grid
  main-product.liquid       Product detail page
  main-cart.liquid          Cart page
  page-basic.liquid         Simple content page (Showroom / Archive / Contact)
snippets/
  product-card.liquid       Single hazard-placard product card
templates/
  index.json, collection.json, product.json, cart.json
  page.json                 Default page template
  page.showroom.json        Assign to the "Showroom" page
  page.archive.json         Assign to the "Archive" page (was "Stockists")
  page.contact.json         Assign to the "Contact" page
assets/
  theme.css                 Full design system (colors, type, grid, card)
config/
  settings_schema.json      Theme editor settings
preview/
  collection-preview.html   Standalone mock preview — open directly in a
                             browser, no Shopify needed, to see the look
```

## See it without Shopify

Just open `preview/collection-preview.html` in any browser. It uses
mock product data so you can check the design before connecting a
real store.

## Push this live on Shopify

1. **Install Shopify CLI** (needs Node.js 18+):
   ```
   npm install -g @shopify/cli @shopify/theme
   ```
2. **Log in and connect to your store** (create one at shopify.com if
   you haven't — you'll want at least the Basic plan to remove
   password-protection and take real orders):
   ```
   shopify theme dev --store your-store.myshopify.com
   ```
   This pushes this folder to your store as a live preview and
   watches for changes.
3. **Publish for real** once you're happy with it:
   ```
   shopify theme push --store your-store.myshopify.com
   ```
   Then set it live from Shopify admin → Online Store → Themes.
4. **Add real products** in Shopify admin (Products → Add product) —
   the theme pulls type, price, images, and variants automatically;
   `product.type` drives the filter chips on the collection page, so
   use consistent types (e.g. Outerwear, Tops, Pants, Accessories).
5. **Create the Showroom and Contact pages.** Go to
   Online Store → Pages → Add page, twice:
   - Title "Showroom", handle `showroom` → in the page's Theme
     template dropdown (bottom right), choose `page.showroom`
   - Title "Contact", handle `contact` → choose template `page.contact`

   The handle is what makes the nav links (`/pages/showroom`,
   `/pages/contact`) resolve; the template controls which layout
   renders. Whatever you type into each page's content editor shows
   up under the heading automatically.

6. **Set up the Archive.** "Archive" is a product collection, not a
   static page — that's what lets you drop past products into it the
   same way you add any other product. Go to Online Store → Collections
   → Add collection, title it "Archive" (handle must be `archive` so
   `/collections/archive` resolves), and add whichever past-drop
   products you want listed there. It renders with the same
   collection-grid layout (View / Sort / Refine controls included)
   as your main shop page — no extra template needed.

## Git

This folder is already a git repo (`git init` was run, first commit
made). To push it to your own remote:

```
git remote add origin <your-repo-url>
git push -u origin main
```

From then on, `shopify theme dev` and `git commit` work side by side —
CLI pushes to the store, git tracks your source history.

## Customizing further

- Colors, type, and the hazard-index logic all live in
  `assets/theme.css` and `snippets/product-card.liquid` — the "IDX"
  bars are currently derived from price tier as a placeholder; swap
  in whatever metric fits (e.g. limited-run size, material weight).
- Nav links in `layout/theme.liquid` point to placeholder pages
  (`/pages/showroom`, `/pages/stockists`, etc.) — create matching
  Pages in Shopify admin or edit the links.
