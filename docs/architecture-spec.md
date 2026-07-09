# Dreamstinct Website — Architecture Spec

## What this is

Dreamstinct is the umbrella brand. It hosts company-level content plus one marketing site per product, all under one domain, one path each.

## URL structure

Path-based, not subdomains:

```
dreamstinct.com/                    company home
dreamstinct.com/blog/               company blog (consulting, AI, founder content)
dreamstinct.com/about/              company info + contact

dreamstinct.com/bank-of-todays/             product landing
dreamstinct.com/bank-of-todays/philosophy/
dreamstinct.com/bank-of-todays/features/
dreamstinct.com/bank-of-todays/pricing/
dreamstinct.com/bank-of-todays/faq/
dreamstinct.com/bank-of-todays/changelog/
dreamstinct.com/bank-of-todays/support/
dreamstinct.com/bank-of-todays/privacy/
dreamstinct.com/bank-of-todays/terms/
dreamstinct.com/bank-of-todays/blog/
dreamstinct.com/bank-of-todays/vs/apple-journal/    (comparison pages, added as needed)
```

Every future product repeats this same shape under its own slug.

Why path-based: one domain compounds SEO authority instead of splitting it across subdomains; easier to cross-link company blog ↔ product pages; one product's identity still lives entirely in its own subfolder, so it can look and feel completely different from the company site or other products.

## Tech stack

**Astro.** Static output, markdown/MDX for blog and SEO pages, shared layout components so a new product later means "add a content folder," not "rebuild the site." Deploys to Netlify with zero extra config.

## Design direction

Simple, and distinctly not "generic AI-generated template." Concretely:
- No stock gradient-blob-hero-with-3-feature-cards layout, no default AI-tool font pairing (Inter + generic sans), no centered-everything symmetry.
- Each product picks its own type, color, and layout personality — company site stays plain/minimal by comparison.
- Bank of Todays should visually echo the app itself (Theme.swift palette: Gallery Grey / Warm Paper / Charcoal / Muted Gold) so the site and the product feel like one thing, not a generic wrapper around it.
- Favor a few deliberate, slightly unconventional choices (asymmetric layout, one strong typographic voice, real photography/screenshots over icons) over polish-by-committee.

## Migration from current state

Current repo (`dreamstinct/dreamstinct-site`, private) has:
- A placeholder homepage card linking to `/bankoftodays/`
- Duplicate legal pages under both `bank-of-todays/` and `bankoftodays/` (rename artifact)

Plan:
- Keep `bank-of-todays` (hyphenated) as the canonical slug going forward.
- Reuse the existing `privacy.html` / `terms.html` content as-is (just re-skin into the new layout) — no legal text changes needed.
- 301-redirect `/bankoftodays/*` → `/bank-of-todays/*` via Netlify `_redirects`.
- Homepage card gets replaced by the real company home page once built; until then it keeps working as-is (no downtime).

## Out of scope for now

No CMS, no forms backend beyond Netlify Forms, no multi-language, no second product yet. Add these when there's an actual need, not preemptively.
