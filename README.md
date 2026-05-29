# Tech Gloria — Website

The official marketing website for **Tech Gloria**, a custom software solutions company. It's a single-page static site hosted on GitHub Pages at [techgloria.com](https://techgloria.com).

## Tech Stack

- **HTML5** — single-page site ([`index.html`](index.html))
- **Tailwind CSS 2.2.19** — loaded via CDN (no build step)
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
├── img/              # Images (logo, favicon)
│   ├── logo.png
│   └── favicon.ico
├── css/              # (currently empty — styling is via Tailwind CDN)
└── js/               # (currently empty — scripts are inline in index.html)
```

## Running Locally

No build tools or dependencies are required. Either:

- **Open directly:** double-click `index.html` to open it in a browser, or
- **Serve it** (recommended, so relative paths and the form behave like production):

  ```bash
  # Python 3
  python -m http.server 8000

  # or Node
  npx serve .
  ```

  Then visit <http://localhost:8000>.

## Contact Form

The contact form submits to [Web3Forms](https://web3forms.com) via AJAX (`fetch`), showing inline success/error messages without a page reload. If JavaScript is disabled, it falls back to a standard form POST.

Configuration lives in the form markup in [`index.html`](index.html):

- `access_key` — the Web3Forms access key that routes submissions to the destination inbox.
- The **destination email** is configured in the Web3Forms dashboard, not in this repo.

To change where submissions go, update the destination email in the Web3Forms dashboard. To use a different form/account, replace the `access_key` value.

## Deployment

The site deploys automatically via **GitHub Pages** from the `main` branch. To publish changes:

```bash
git add .
git commit -m "Your message"
git push
```

GitHub Pages rebuilds within a minute or two. The custom domain is set by the [`CNAME`](CNAME) file.

## SEO

- Meta tags, Open Graph, and Twitter Card tags are in the `<head>` of [`index.html`](index.html).
- Schema.org `Organization` structured data (JSON-LD) is included for rich results.
- [`robots.txt`](robots.txt) and [`sitemap.xml`](sitemap.xml) help search engines crawl the site. Update `sitemap.xml`'s `lastmod` date when content changes.
