# Cayman Bid Desk: how the site works

A plain static website. No build step, no framework, no database. GitHub Pages serves the files exactly as they are in this repo at www.caymanbiddesk.com (set by the `CNAME` file).

## Pages

| File | What it is |
|---|---|
| `index.html` | Homepage: services, readiness checker, Procurement Watch, Regulatory Watch, guides, FAQ, contact form |
| `cayman-government-tender-guide.html` | Guide: how to respond to a Cayman Islands Government tender |
| `cima-aml-audit-independence.html` | Analysis: who can audit your AML programme under the new CIMA rule |
| `privacy.html`, `terms.html` | Legal pages |
| `cima-aml-audit-checklist.pdf` | Free one-page download, linked from the homepage and the CIMA article |

Each page has its own CSS inside a `<style>` tag in its `<head>`, and its own small script at the bottom.

## Email address

The address is never written out in the HTML, so spam bots can't scrape it. Each page rebuilds it in the browser from two pieces:

```
var USER = ['con','tact'].join('');
var HOST = ['caymanbid','desk','.com'].join('');
```

To change the address, edit those two lines on all four HTML pages. Links marked `data-mailto` become `mailto:` links. Forms marked `data-mailform` send through formsubmit.co to the same address.

## SEO pieces

- Each page has a `<title>`, a meta description (keep under 155 characters), a canonical link and Open Graph tags.
- Structured data (JSON-LD, near the bottom of each page):
  - Homepage: `FAQPage` (must match the visible FAQ) and `ProfessionalService`
  - Articles/guides: `Article`; the tender guide also has `FAQPage`
- `sitemap.xml` lists every page. Update `lastmod` when a page changes, and add new pages to it.
- `robots.txt` allows everything and points to the sitemap.

## Images

The hero photo is served as WebP (`hero-photo.webp`, `hero-photo-sm.webp`) inside a `<picture>` tag, with the `.jpg` files as a fallback for older browsers. `og-image.jpg` stays JPG because social sites expect it.

## Adding a new article or guide

1. Copy `cayman-government-tender-guide.html` and rename it.
2. Change the title, description, canonical, og tags, the article body and the JSON-LD.
3. Add a card for it in the homepage `#news` section.
4. Add it to `sitemap.xml`.

## Things that update themselves

- The deadline countdown on the homepage switches to "now in effect" after 18 September 2026 (JavaScript).
- The footer year.
- Procurement Watch shows the `OPPORTUNITIES` list in the homepage script; empty shows the "where to look" panel.
