<!-- prettier-ignore -->
<div align="center">

<img src="icons/icon-192.png" alt="" align="center" height="96" />

# portfolio

*static developer portfolio for a JavaScript and Python engineer building browser extensions and CLI tools*

[![Vercel](https://img.shields.io/badge/Deploy-Vercel-black?style=flat-square&logo=vercel&logoColor=white)](https://vercel.com/new)
[![License](https://img.shields.io/badge/License-MIT-blue?style=flat-square)](LICENSE)
[![GitHub stars](https://img.shields.io/github/stars/Opesco23/portfolio?style=flat-square&labelColor=blue)](https://github.com/Opesco23/portfolio/stargazers)

[View live](#deploy-to-vercel) &nbsp;•&nbsp; [Features](#what-it-includes) &nbsp;•&nbsp; [Deploy](#deploy-to-vercel) &nbsp;•&nbsp; [Local setup](#run-locally) &nbsp;•&nbsp; [Editing](#editing-content) &nbsp;•&nbsp; [Provenance](#provenance)

</div>

Personal site for **Oniyide Opeyemi** ([@opesco23](https://github.com/opesco23)), based in Lagos, Nigeria. Three static pages, 2.1 MB, no build step and no runtime dependencies.

## Deploy to Vercel

The fastest route. Static HTML, so Vercel needs no framework preset and no build command.

**From the dashboard**

1. Sign in at [vercel.com](https://vercel.com) with your GitHub account
2. **Add New → Project**, then import `Opesco23/portfolio`
3. Vercel auto-detects **Other** as the framework — leave every field as-is:
   - Build Command: leave empty
   - Output Directory: leave empty
   - Install Command: leave empty
4. **Deploy**

You get a live URL at `https://portfolio-<hash>.vercel.app`. To claim the clean subdomain, go to **Project Settings → Domains → Add**, enter `portfolio.vercel.app`, and follow the DNS instructions.

**From the CLI**

```bash
npm i -g vercel
vercel link
vercel deploy --prod
```

> [!IMPORTANT]
> Deploy from the **repository root**, not from inside a subfolder. The pages load assets from absolute paths like `/_next/static/...`, so serving from a nested directory breaks styling.

**Custom domain**

Point any registrar at Vercel:

| Record | Name | Value |
| --- | --- | --- |
| `A` | `@` | `76.76.21.21` |
| `CNAME` | `www` | `cname.vercel-dns.com` |

Vercel provisions the TLS certificate automatically once DNS resolves.

## GitHub Pages as an alternative

Works too, but requires one change first. GitHub Pages serves this repo from `opesco23.github.io/portfolio` — a subpath — while the pages assume they sit at the domain root. Rewrite the absolute asset paths to be relative:

```bash
# preview the effect without committing
grep -c '/_next/' index.html

# then, in index.html, projects.html and contact.html:
#   /_next/  ->  ../_next/
```

Then enable it under **Settings → Pages → Deploy from a branch → `main` → `/root`**. Because this repo is a user site rather than a project site, publishing from `/root` of `main` serves it at the repository path.

> [!TIP]
> Vercel needs no such edit because a project deploy is already served from the root of its own subdomain. For a portfolio, that's the reason to prefer it.

## What it includes

- **Home** — hero with location and GitHub star count, a short about section, contact links, four featured projects, and a stack breakdown
- **Projects** — all eight public repositories with descriptions and language tags
- **Contact** — direct channels rather than a form, since static hosting has no backend to receive one
- **Dark and light mode** — persists to `localStorage`
- **Favicon set** — `favicon.ico` plus eight PNG sizes, generated from the GitHub avatar
- **Progressive web manifest** — installable to a home screen

## Stack

Measured across the eight public repositories by bytes, not asserted:

| Language | Share |
| --- | --- |
| JavaScript | 58% |
| Python | 28% |
| HTML | 9% |
| CSS | 5% |

Everything else on the stack section — Chrome Extension, Manifest V3, Node.js, Git, GitHub Actions, unittest — appears in project READMEs.

## Run locally

```bash
python3 -m http.server 8000
```

Open <http://localhost:8000>.

Serve from the repository root and over `http://`. Opening `index.html` directly off the filesystem will render unstyled, because absolute asset paths will not resolve.

## Editing content

> [!WARNING]
> Each page holds its content in **two** places: the visible markup, and a Next.js RSC payload in `<script>` blocks that React re-renders from. Edit both or your change will revert on reload. There is no build step to regenerate the payload.

Search for `__next_f.push` to locate it. Editing the payload by hand is safe for text and URLs; structural edits are not, since the format is positional.

To retarget an external link, search the filename — a GitHub repo URL appears in the markup, the payload, and sometimes a JS chunk:

```bash
grep -rn 'github.com/opesco23' --include=*.html --include=*.js .
```

## Where the data came from

Everything here derives from the public GitHub API for `opesco23` rather than being written from memory:

- **Project cards** — the eight public repositories, with descriptions summarised from each README
- **Stack** — language bytes measured per repository
- **Star count** — the sum across all repositories
- **Featured projects** — `focus-block` and `git-analyzer`, the two most substantial and distinctive

## Provenance

This began as a static mirror of a third-party Next.js portfolio, captured with HTTrack and repopulated with the content above. Two things follow from that, and they are worth stating plainly rather than discovering later.

**The design is not original.** The Tailwind stylesheet, the `_next/` directory, and the overall layout all descend from the original site. Consider this repository a fork of someone else's front end carrying different content.

**Interactivity is deliberately minimal.** The original shipped a command palette, collapsible sections, and animated counters — all React client components that depend on hydration. Those do not survive being served as static files, so the sections holding them were removed rather than left broken.

What remains is static HTML plus one working feature: the theme toggle, a small self-contained script marked `data-theme-fallback` that drives the `dark` class directly and needs no hydration. It reads and writes `localStorage` under `vite-ui-theme`.

Restoring further interactivity means rebuilding it against this content — the original component source is not in this repository.

## Contributing

Issues and pull requests are welcome. See [CONTRIBUTING.md](CONTRIBUTING.md), and please read [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md) first.

## License

[MIT](LICENSE) © 2026 Oniyide Opeyemi
