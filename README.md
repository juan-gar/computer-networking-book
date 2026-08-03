# Computer Networking — A Top-Down Approach Study Guides

Interactive, single-page study guides to Kurose & Ross, *Computer Networking: A
Top-Down Approach*. One page per chapter, eight sections each, every section with a
central idea, summary, key concepts, the formulas worth keeping, and a note on why it
matters in practice.

No build step, no framework, no runtime dependencies. One HTML file per chapter plus
the shared fonts.

| | Chapter | Sections |
|---|---|---|
| 1 | [Computer Networks and the Internet](https://juan-gar.github.io/computer-networking-book/ch1/) | 1.1 → 1.8 |
| 2 | [Application Layer](https://juan-gar.github.io/computer-networking-book/ch2/) | 2.1 → 2.8 |

## Deploy

Live at <https://juan-gar.github.io/computer-networking-book/>.

`.github/workflows/pages.yml` publishes the repo root on every push to `main`, and can
also be run by hand from the Actions tab. It needs **Settings → Pages → Source: GitHub
Actions** set once — the workflow's `GITHUB_TOKEN` is not allowed to create the Pages
site itself. After that, no further setup.

The Open Graph tags in each `index.html` carry absolute Pages URLs, since social
scrapers will not resolve relative ones. If the site moves — a different repo, or a
custom domain — update them to match.

## Local preview

```bash
python3 -m http.server 8000
```

Then open `http://localhost:8000`. Opening the files via `file://` mostly works, but
fonts are fetched in CORS mode and some browsers block them on the file protocol — use
the server.

## Contents

```
index.html          contents page: the chapter list
ch1/index.html      Chapter 1 — the whole guide: markup, styles, content, behaviour
ch1/og-image.png    1200×630 social preview for Chapter 1
ch2/                Chapter 2, same shape
fonts/              Archivo, Newsreader, JetBrains Mono — variable, latin
og-image.png        1200×630 social preview for the contents page
og-source.html      the markup that image is rendered from
.nojekyll           skip Jekyll processing
.github/workflows/  Pages deploy
```

Fonts live at the root and are shared by every page: Archivo and JetBrains Mono are
byte-identical across chapters, so one copy serves all. Chapter 1 uses Newsreader on
the weight axis, Chapter 2 the optical-size axis with a true italic — both are present,
and each page declares only what it uses.

### Regenerating the contents-page og-image

`og-source.html` is the source for the root `og-image.png`. With the local server
running, screenshot it at exactly 1200×630 — for example with Playwright:

```js
const p = await browser.newPage({ viewport: { width: 1200, height: 630 } });
await p.goto('http://localhost:8000/og-source.html', { waitUntil: 'networkidle' });
await p.evaluate(() => document.fonts.ready);
await p.screenshot({ path: 'og-image.png' });
```

## Adding a chapter

Drop it in as `chN/index.html`, point its font references at `../fonts/`, give it the
same `cn-theme` localStorage key so the theme carries across pages, add a
`.chapter-switch` nav to its masthead, and add a card to the root `index.html`.

## Notes

- **Fonts are self-hosted.** No request leaves the origin, so the pages render offline
  and no visitor IP reaches a third party. Variable fonts, latin subset.
- **Theme** defaults to your OS preference, is overridable with the toggle, and persists
  in `localStorage` under `cn-theme` — shared by all pages, so the choice follows you
  from chapter to chapter. An inline script in `<head>` applies it before first paint so
  a stored light theme never flashes dark.
- **Keyboard:** ← / → move between sections within a chapter.
- Respects `prefers-reduced-motion`; focus rings are visible throughout.

## Licence

Fonts are [SIL OFL 1.1](https://openfontlicense.org) (Archivo, Newsreader, JetBrains
Mono), packaged via [Fontsource](https://fontsource.org). The chapters being summarised
are © Pearson; these are personal study summaries in their own words, not a
reproduction.
