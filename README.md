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

The compiled stylesheet ([`css/styles.css`](css/styles.css)) is committed, so to just **view** the site you don't need to build anything — open `index.html` directly, or serve it (recommended, so absolute paths like `/css/styles.css` and the form behave like production):

```bash
# Python 3
python -m http.server 8000

# or Node
npx serve .
```

Then visit <http://localhost:8000>.

## Styling (Tailwind build)

Styles are written with Tailwind utility classes in the HTML, plus custom CSS in [`src/input.css`](src/input.css). The Tailwind CLI compiles these into a minified, purged [`css/styles.css`](css/styles.css).

**If you change any markup or `src/input.css`, rebuild the stylesheet** (otherwise newly used utility classes won't exist in the compiled CSS):

```bash
npm install        # once, to install the Tailwind CLI
npm run build      # compile css/styles.css (minified)
npm run watch      # or: rebuild automatically while editing
```

Commit the regenerated `css/styles.css` along with your changes.

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
