# Tech Gloria — Website

The official marketing website for **Tech Gloria**, a custom software solutions company. It's a single-page static site hosted on GitHub Pages at [techgloria.com](https://techgloria.com).

## Tech Stack

- **HTML5** — single-page site ([`index.html`](index.html))
- **Tailwind CSS 4** — compiled to a minified, purged stylesheet ([`css/styles.css`](css/styles.css)) via the Tailwind CLI
- **Web3Forms** — handles contact form submissions without a backend
- **GitHub Pages** — static hosting with a custom domain

## Project Structure

```text
.
├── index.html        # The entire site (markup + inline scripts)
├── 404.html          # Custom not-found page (served by GitHub Pages)
├── CNAME             # Custom domain for GitHub Pages (techgloria.com)
├── robots.txt        # Search engine crawl rules
├── sitemap.xml       # Sitemap for SEO
├── package.json      # Build scripts + Tailwind CLI dependency
├── src/
│   └── input.css     # Tailwind entry point + custom CSS (edit this, not styles.css)
├── css/
│   └── styles.css    # Compiled, minified stylesheet (generated — commit it)
├── img/              # Images (logo, favicon)
│   ├── logo.png
│   └── favicon.ico
└── js/               # (currently empty — scripts are inline in index.html)
```

## Running Locally

Install dependencies once, then start the dev server:

```bash
npm install        # once
npm run dev        # serves at http://localhost:8000 with live reload
```

`npm run dev` runs two things together: the Tailwind CLI in watch mode (recompiling `css/styles.css` on every change) and [`live-server`](https://www.npmjs.com/package/live-server), which serves the site and auto-refreshes the browser when files change. Open <http://localhost:8000>.

> **Note:** serve the site (don't just double-click `index.html`). The pages use absolute asset paths like `/css/styles.css`, which only resolve when served from a document root — under the `file://` protocol they point at your drive root and the page renders unstyled.

The compiled stylesheet is committed, so if you only want to **view** the site without Node, any static server works (e.g. `python -m http.server 8000` or `npx serve .`).

## Styling (Tailwind build)

Styles are written with Tailwind utility classes in the HTML, plus custom CSS in [`src/input.css`](src/input.css). The Tailwind CLI compiles these into [`css/styles.css`](css/styles.css).

```bash
npm run dev        # watch + live-reload server (development)
npm run watch      # watch + recompile only (no server)
npm run build      # one-off minified production build
```

**Before committing, run `npm run build`** so the committed `css/styles.css` is the minified production build (the watch/dev tasks emit an unminified stylesheet). Commit the regenerated `css/styles.css` alongside your changes — otherwise newly used utility classes won't exist in the deployed CSS.

## Contact Form

The contact form submits to [Web3Forms](https://web3forms.com) via AJAX (`fetch`), showing inline success/error messages without a page reload. If JavaScript is disabled, it falls back to a standard form POST.

Configuration lives in the form markup in [`index.html`](index.html):

- `access_key` — the Web3Forms access key that routes submissions to the destination inbox.
- The **destination email** is configured in the Web3Forms dashboard, not in this repo.

To change where submissions go, update the destination email in the Web3Forms dashboard. To use a different form/account, replace the `access_key` value.

## Deployment

The site deploys automatically via **GitHub Pages** from the `main` branch — it serves the committed static files as-is (there is no CI build step, so the compiled `css/styles.css` must be committed). To publish changes:

```bash
npm run build      # if you changed markup or src/input.css
git add .
git commit -m "Your message"
git push
```

GitHub Pages rebuilds within a minute or two. The custom domain is set by the [`CNAME`](CNAME) file.

## SEO

- Meta tags, Open Graph, and Twitter Card tags are in the `<head>` of [`index.html`](index.html).
- Schema.org `Organization` structured data (JSON-LD) is included for rich results.
- [`robots.txt`](robots.txt) and [`sitemap.xml`](sitemap.xml) help search engines crawl the site. Update `sitemap.xml`'s `lastmod` date when content changes.
