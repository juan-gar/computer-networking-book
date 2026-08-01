# Computer Networks and the Internet — Chapter 1 Study Guide

An interactive, single-page study guide to Chapter 1 of Kurose & Ross,
*Computer Networking: A Top-Down Approach*. Eight sections (1.1 → 1.8), each with a
central idea, summary, key concepts, the formulas worth keeping, and a note on why it
matters in practice.

No build step, no framework, no runtime dependencies. One HTML file plus three fonts.

## Deploy

Live at <https://juan-gar.github.io/computer-networking-book/>.

`.github/workflows/pages.yml` publishes the repo root on every push to `main`, and can
also be run by hand from the Actions tab. It needs **Settings → Pages → Source: GitHub
Actions** set once — the workflow's `GITHUB_TOKEN` is not allowed to create the Pages
site itself. After that, no further setup.

The Open Graph tags in `index.html` carry the absolute Pages URL, since social scrapers
will not resolve relative ones. If the site moves — a different repo, or a custom
domain — update those three tags to match.

## Local preview

```bash
python3 -m http.server 8000
```

Then open `http://localhost:8000`. Opening `index.html` via `file://` mostly works, but
fonts are fetched in CORS mode and some browsers block them on the file protocol — use
the server.

## Contents

```
index.html          the whole guide: markup, styles, content, behaviour
fonts/              Archivo, Newsreader, JetBrains Mono — variable, latin, ~132 KB total
og-image.png        1200×630 social preview
.nojekyll           skip Jekyll processing
.github/workflows/  Pages deploy
```

## Notes

- **Fonts are self-hosted.** No request leaves the origin, so the page renders offline
  and no visitor IP reaches a third party. Variable fonts on the weight axis only —
  one file per family covers every weight used.
- **Theme** defaults to your OS preference, is overridable with the toggle, and persists
  in `localStorage`. An inline script in `<head>` applies it before first paint so a
  stored light theme never flashes dark.
- **Keyboard:** ← / → move between sections.
- Respects `prefers-reduced-motion`; focus rings are visible throughout.

## Licence

Fonts are [SIL OFL 1.1](https://openfontlicense.org) (Archivo, Newsreader, JetBrains
Mono), packaged via [Fontsource](https://fontsource.org). The chapter being summarised
is © Pearson; this is a personal study summary in its own words, not a reproduction.
