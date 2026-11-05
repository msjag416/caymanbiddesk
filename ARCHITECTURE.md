# Cayman Bid Desk: how the site works

A plain static website. No build step, no framework, no database. GitHub Pages serves the files exactly as they are in this repo at www.caymanbiddesk.com (set by the `CNAME` file).

## Pages

| File | What it is |
|---|---|
| `index.html` | Homepage: services overview, audit and inspection readiness checker, Procurement Watch, Regulatory Watch, guides, About (founder bio), FAQ, contact form |
| `compliance-support.html` | Service page for CIMA compliance teams: three packages, how it works, FAQ |
| `tender-support.html` | Service page for tender bidders: three packages, how it works, FAQ |
| `cayman-government-tender-guide.html` | Guide: how to respond to a Cayman Islands Government tender |
| `cima-aml-audit-independence.html` | Analysis: who can audit your AML programme under the new CIMA rule |
| `privacy.html`, `terms.html` | Legal pages |
| `cima-aml-audit-checklist.pdf` | Free one-page download, linked from the homepage, the CIMA article and the compliance page |
| `sample-cima-evidence-tracker.pdf` | Sample deliverable (fictional entity), linked from the compliance page |
| `sample-tender-compliance-matrix.pdf` | Sample deliverable (fictional tender), linked from the tender page |

Each page has its own CSS inside a `<style>` tag in its `<head>`, and its own small script at the bottom.

## Email address

The address is never written out in the HTML, so spam bots can't scrape it. Each page rebuilds it in the browser from two pieces:

```
var USER = ['con','tact'].join('');
var HOST = ['caymanbid','desk','.com'].join('');
```

To change the address, edit those two lines on every HTML page. Links marked `data-mailto` become `mailto:` links. Forms marked `data-mailform` send through formsubmit.co to the same address.

## SEO pieces

- Each page has a `<title>`, a meta description (keep under 155 characters), a canonical link and Open Graph tags.
- Structured data (JSON-LD, near the bottom of each page):
  - Homepage: `FAQPage` (must match the visible FAQ), `ProfessionalService`, and `Service` for the two divisions
  - Every page except the homepage: `BreadcrumbList` (Home > page)
  - Articles/guides: `Article`; the tender guide also has `FAQPage`
  - Service pages: `Service` and `FAQPage`
  - The homepage `ProfessionalService` block names JoAnne Gomez as founder
- `sitemap.xml` lists every page. Update `lastmod` when a page changes, and add new pages to it.
- `robots.txt` allows everything and points to the sitemap.

## Images

The hero photo is served as WebP (`hero-photo.webp`, `hero-photo-sm.webp`) inside a `<picture>` tag, with the `.jpg` files as a fallback for older browsers. `og-image.jpg` stays JPG because social sites expect it.

## Adding a new article or guide

1. Copy `cayman-government-tender-guide.html` and rename it.
2. Change the title, description, canonical, og tags, the article body and the JSON-LD.
3. Add a card for it in the homepage `#news` section.
4. Add it to `sitemap.xml`.

## Founder photo

The About section shows `joanne-gomez.webp`, with `joanne-gomez.jpg` as the fallback (both 480x480). To change the photo, replace both files with the same names.

## Package prices

Each package on the service pages shows "Fixed fee, quoted in writing". To show a price, edit the `pack-fee` line for that package.

## Type wave (homepage)

Right under the hero there's a dark band with two rows of very large words (inspired by onepagelove.com/typewave). As the visitor scrolls, the top row slides left and the bottom row slides right. The words live in the `rowA` and `rowB` lines of the "Type wave" script near the bottom of `index.html`; edit those to change them. Classes: `o` = outlined word, `t` = teal, `g` = gold. The band is hidden from screen readers and stays still for visitors who've turned off motion in their device settings. To remove it, delete the `<div class="wave">` block, the `TYPE WAVE` CSS and the "Type wave" script.

## Living dot grid (homepage hero)

The hero background is a grid of small square dots drawn by a short script ("Living dot grid" near the bottom of `index.html`), inspired by onepagelove.com/builders-table. On a computer, dots near the mouse grow and glow teal. On phones, a soft glow drifts slowly across the grid instead. It only runs while the hero is on screen, and it stays still for visitors who've turned off motion. `GAP` sets the dot spacing and `REACH` sets how wide the glow is. To remove it, delete that script; the hero falls back to plain navy.

## Things that update themselves

- The footer year.
- Procurement Watch: the "where to look" panel is written directly in the HTML so all search engines can read it. If the `OPPORTUNITIES` list in the homepage script has entries, the script replaces the panel with those cards.
