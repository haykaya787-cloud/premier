# Premier Client

Static bilingual (French / English) affiliate site served at https://www.premierclient.ca by Cloudflare Workers static assets.

- `site/` is the published folder. Cloudflare deploys it as-is on every push to `main` (`npx wrangler deploy`, configured by `wrangler.jsonc`).
- French pages live at the root (`site/<slug>/index.html`), English pages under `site/en/<slug>/index.html`.

## Adding an article

1. Copy an existing article page pair (for example `site/shopify/index.html` and `site/en/shopify/index.html`) into new folders named with the new French and English slugs.
2. In each copy, update `<title>`, the meta description, the canonical link, the three `hreflang` links (they must point at each other), the language switch link in the nav, and the article body.
3. Add the article to the numbered list on both home pages (`site/index.html` and `site/en/index.html`).
4. Add both new URLs to `site/sitemap.xml`.

## Page pattern for guides

- Right under the `<h1>`: `<p class="updated">Mis à jour le …</p>` (English: `Updated …`) with the date of the last real change.
- Right under the lede: a `<div class="cta-row">` with the main affiliate button and a short `<span class="cta-note">` saying whether there is a free plan or a free trial (only if verified on the vendor's site).
- At the end: the same button again. Comparison pages also get a button row as the last row of the table.
- When it can be verified, add a short "Au Québec" / "In Quebec" section (taxes, French interface, Canadian payments). Skip it rather than guess.
- Button classes: `cta` (main), `cta alt` (secondary, outlined). Styles are already in every page's `<style>` block; copy them if a new page lacks them.

## Click tracking

- Shopify links take placement tags: `https://shopify.pxf.io/k4d03x?subId1=<placement>&amp;subId2=<fr|en>`. Placements in use: `home-chooser`, `home-featured`, `compare-top`, `compare-table`, `compare-section`, `guide-top`, `guide-end`, `quebec-guide`. For a new article use `<slug>-top` and `<slug>-end`. These show up in Impact's reports by Sub ID.
- Systeme.io links have no placement tags; use them as listed below.

## Rules for content

- Every page keeps the affiliate disclosure line under the header.
- Affiliate links use `rel="sponsored noopener"`. Current links: Systeme.io `https://systeme.io/fr?sa=sa02865662993b51891b959daf857a33a6a54575a3` on French pages and `https://systeme.io/?sa=sa02865662993b51891b959daf857a33a6a54575a3` on English pages, Shopify `https://shopify.pxf.io/k4d03x`.
- Never claim hands-on testing, personal results, income figures, ratings or testimonials that cannot be sourced. Do not state specific prices; point readers to the official pricing page.
- Keep the `impact-site-verification` meta tag in every page head.
