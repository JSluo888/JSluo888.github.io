# tianhaoluo.com

Personal website of **Tianhao Luo** — Harvard PhD student in Biomedical Informatics, NSF Graduate
Research Fellow, and startup founder working on AI for science.

Live at **https://tianhaoluo.com**, served by GitHub Pages from the `main` branch of this repository.

## Structure

The site is a single self-contained page. All CSS lives in one `<style>` block in `<head>`, and the
behaviour script in one `<script>` block before `</body>`. There is no build step, no bundler, and no
framework — edit `index.html`, push to `main`, and the change is live.

```
index.html     the entire site: markup, styles, and behaviour
profile.json   schema.org JSON-LD entity graph (mirrors the inline @graph)
llms.txt       markdown profile for AI agents and crawlers
robots.txt     crawler directives; open to all search and AI crawlers
sitemap.xml    sitemap
CNAME          custom domain
*.jpg / *.png  photos, advisor headshots, and institution logos
```

The only external request is Google Fonts (IBM Plex Serif / Sans / Mono).

## Design

The visual system is "Scientific Instrument": the page as a precision-instrument readout. Hairline
rules with tick marks, monospace metadata, tabular numerals, zero border radius, one border weight,
and a single signal colour used only where the page is reporting something — an index, an active
state, a focus ring, the newest record.

Colour, type, and spacing are driven entirely by CSS custom properties in `:root`. **Change the
tokens, not the rules.** Light is defined on bare `:root`; dark is redefined twice, once under
`@media (prefers-color-scheme: dark)` for system-default visitors and once under
`:root[data-theme="dark"]` so the toggle wins in both directions. A tiny inline script in `<head>`
applies the saved preference before first paint, which is what prevents a flash of the wrong theme —
keep it there, and keep it first.

Some deliberate absences: no custom cursor, no typewriter effect, no marquee, no scroll-progress bar,
no card tilt, no infinitely looping animations. These were removed on purpose. Everything that moves
does so because the reader caused it, and all motion is disabled under `prefers-reduced-motion`.

## Editing

**Sections** appear in this order: hero, status strip, about, news, education, research, industry,
ventures, publications, teaching, contact. Section numbering is a CSS counter, and the left-hand
calibration spine reads from the `SECTIONS` array in the behaviour script — if you add or remove a
section, update that array and give the `<section>` an `id`, or the two will disagree.

**Adding a news item** — copy a `.news-item` block to the top of `.news-list`, then move the `is-new`
class off the previous top item onto the new one. Only the most recent entry should carry it.

**Adding images** — resize before committing. Photos should be no more than ~1400px on the long edge,
headshots and logos no more than 200px. Oversized images are the main thing that slows this page down.
On macOS: `sips -Z 1200 -s format jpeg -s formatOptions 82 in.jpg --out out.jpg`.

**Facts live in three places.** If you change a role, date, or affiliation, update `index.html`, the
inline JSON-LD `@graph`, and `llms.txt` together, and mirror the graph into `profile.json`. They are
what search engines and AI assistants read; if they disagree with the page, the page loses authority.

## Publishing

```bash
git add -A
git commit -m "describe the change"
git push
```

GitHub Pages rebuilds automatically — usually live within a minute, plus up to ten minutes of CDN
caching.
