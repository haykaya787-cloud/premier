# Premier Client

Static bilingual (French / English) affiliate site served at https://www.premierclient.ca by Cloudflare Pages.

- `site/` is the published folder. Cloudflare Pages deploys it as-is on every push to `main` (no build command, output directory `site`).
- French pages live at the root (`site/<slug>/index.html`), English pages under `site/en/<slug>/index.html`.

## Adding an article

1. Copy an existing article page pair (for example `site/shopify/index.html` and `site/en/shopify/index.html`) into new folders named with the new French and English slugs.
2. In each copy, update `<title>`, the meta description, the canonical link, the three `hreflang` links (they must point at each other), the language switch link in the nav, and the article body.
3. Add the article to the numbered list on both home pages (`site/index.html` and `site/en/index.html`).
4. Add both new URLs to `site/sitemap.xml`.

## Rules for content

- Every page keeps the affiliate disclosure line under the header.
- Affiliate links use `rel="sponsored noopener"`. Current links: Systeme.io `https://systeme.io/?sa=sa02865662993b51891b959daf857a33a6a54575a3`, Shopify `https://shopify.pxf.io/k4d03x`.
- Never claim hands-on testing, personal results, income figures, ratings or testimonials that cannot be sourced. Do not state specific prices; point readers to the official pricing page.
- Keep the `impact-site-verification` meta tag in every page head.
