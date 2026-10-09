# portfolio

Personal site for **Oniyide Opeyemi** ([@opesco23](https://github.com/opesco23)) — developer working in JavaScript, Python and HTML, building browser extensions and CLI tools.

Live content lives in the pages; this README covers what it is, where the data came from, and how to run it.

## What's here

| Path | What it is |
| --- | --- |
| `index.html` | Home — hero, about, connect links, featured projects, stack |
| `projects.html` | All 8 public repositories |
| `contact.html` | Contact channels |
| `icons/` | Favicon set, generated from the GitHub avatar |
| `favicon.ico` | Multi-size icon (16/32/48/64) |
| `site.webmanifest` | PWA manifest |
| `_next/static/` | Compiled CSS, JS chunks and webfonts |

Static HTML — no build step. Three pages, 2.1 MB total.

## Running it locally

```bash
python3 -m http.server 8000
```

Then open <http://localhost:8000>.

Serve from the **repository root**, not from inside a subfolder. The pages reference assets with absolute paths like `/_next/static/...`, so opening `index.html` directly off the filesystem (`file://`) will render unstyled.

## Where the data came from

Everything on this site is derived from real GitHub data for `opesco23`, fetched from the public API — not invented:

- **Project cards** — the 8 public repos. Descriptions are summaries written from each repo's README.
- **Stack section** — languages measured from the repos by bytes: JavaScript 58%, Python 28%, HTML 9%, CSS 5%. Chrome Extension / Manifest V3 / Node.js / GitHub Actions / unittest all appear in project READMEs.
- **Star count (5)** — the sum across all repos.
- **Location** — Lagos, Nigeria.

**About `focus-block` and `git-analyzer`** — the two highlighted projects, picked for being the most substantial and most distinctive of the set.

## Provenance

This site started as a static mirror of a third-party Next.js portfolio, captured with HTTrack and then repopulated. Two consequences worth knowing:

**The styling and layout are not mine.** The Tailwind CSS, the `_next/` chunk directory, and the overall design all come from that original site. Treat this repo as a fork of someone else's front end with different content in it.

**Interactivity is mostly gone, by design.** The original had a command palette, collapsible sections, and animated counters — all Next.js client components driven by React hydration. Those don't survive being served as static files, so the sections they lived in were removed rather than left broken. What remains is a static page plus one working feature: the dark/light toggle, which is a small self-contained script (`data-theme-fallback`) that drives the `dark` class directly and does not depend on hydration. It persists your choice in `localStorage` under `vite-ui-theme`.

If you want more interactivity back, it needs rebuilding against this content — the original component source isn't here.

## Editing

The pages are large single files, and most content lives in two places in each: the visible markup, **and** a Next.js RSC payload in `<script>` blocks that React would re-render from. If you edit visible text and it snaps back on reload, the payload needs the same edit. There's no build step to regenerate it.

Search `__next_f.push` to find the payload.

## Contact

- GitHub — [@opesco23](https://github.com/opesco23)
- X — [@opeyemi42035925](https://x.com/opeyemi42035925)
- Email — opeyemioniyide2006@gmail.com
