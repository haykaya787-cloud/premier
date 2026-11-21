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

## Page format v2 (since 2026-11-20)
- Guides are built as reviews: verdict box (`.verdict`), table of contents (`.toc`), facts table (`table.facts`), pros/limits (`.pc` with `.pro`/`.con`), a Quebec section, and an FAQ (`section.faq` with `<details>`).
- Byline under the H1: `p.byline` with the author avatar, linking to the About page, plus the update date.
- Every page has favicon, Open Graph/Twitter tags (image `/og-image.png`) and JSON-LD (Organization; guides also Article + BreadcrumbList + FAQPage when there is an FAQ). Keep FAQ JSON-LD identical to the visible FAQ.
- Titles target what people search: "<Tool> avis 2026", "<Tool> au Québec", "X vs Y". Keep them under ~65 characters where possible.
- Only claim hands-on experience for what we actually did (Systeme.io account, form, automation, domain). We do NOT run a Shopify store; Shopify pages say so.
- New Shopify subId placements: taxes-top, taxes-end; YouTube descriptions use youtube-<slug>.
- Builder used for the v2 pages: tools kept outside the repo; edit the HTML directly following the existing pages.

## Starting-a-business series (Nov 2026)
- Pages: /demarrer-entreprise-quebec/, /inscription-tps-tvq-quebec/ and EN twins, defined in tools/pro/pages_start.py.
- Videos: IbpSrc9yuU4 (autonome ou société), Bcrxxq2Z2FY (ARC + TPS/TVQ), 2-hiargWqsw (incorporation Québec vs fédéral; pages /incorporer-entreprise-quebec/ and /en/incorporate-in-quebec/, list INC). Pages take a `video=` dict; build_site.py embeds via youtube-nocookie and adds VideoObject.
- Paid-registration affiliate (e.g. Ownr) pending the owner's approval: add the link to the "Ou payer un service" section and to both video descriptions.

## Video series « Démarrer au Québec » (Léa, fictional example) — Nov 21 2026
- Ep1 IMzdiRwDDRg, Ep2 UsAV__SPIQQ, Ep3 aOnhkUOaqHA, Ep4 KiUPRsnjato (public). Earlier versions IbpSrc9yuU4, Bcrxxq2Z2FY, 2-hiargWqsw, gJutB3Nl4r4 set to Unlisted (not deleted).
- Animated renderer: /home/claude/vid/build2.py (per-frame Chrome render, reveals synced to narration, count-ups, speech bubbles, confetti, soft SFX). Scripts: /home/claude/vid/story/ep1-4.py. Upload encode: enc.sh (fits the 3.8 MB browser upload limit).
