# The Resilience Capital Lab — website

Static site for The Resilience Capital Lab, at the National Center for Disaster
Preparedness, Columbia Climate School.

## What's here

```
_layouts/default.html    shared shell: <head>, CSS, header and tab bar, hero, footer
index.html               Overview  -> resiliencecapitallab.org/
case-studies/index.html  Case Studies -> /case-studies/
events/index.html        Events -> /events/
publications/index.html  Publications -> /publications/
team/index.html          Team -> /team/
_config.yml              Jekyll settings
404.html                 branded not-found page (standalone)
sitemap.xml, robots.txt  search-engine files
README.md                this file (not published)
```

Each section has its own folder and URL, so any section can be linked to
directly. GitHub Pages builds the site with Jekyll automatically on every
commit: each section page starts with a short front-matter block (`layout`,
`section`, `title`, `description`) and holds only that section's content; the
header, hero and footer come from `_layouts/default.html`. Do not add a
`.nojekyll` file, or the layout will stop being applied. The two NCDP logos are
base64-embedded in the layout. The only external request is to Google Fonts.

## Publishing to GitHub Pages

1. Create a repository (public is required for Pages on a free account —
   a suggested name is `resilience-capital-lab`).
2. Upload the contents of this folder to the repository root, including the
   `_layouts` folder and `_config.yml`. Do not add a `.nojekyll` file.
3. Repository **Settings → Pages**. Under *Build and deployment*, set Source to
   **Deploy from a branch**, branch `main`, folder `/ (root)`. Save.
4. Wait a minute or two, then check `https://<account>.github.io/<repo>/`.

## Pointing a domain at it

Do this in whichever order suits you, but the site should be live on the
`github.io` URL before you add the custom domain.

**On GitHub:** Settings → Pages → *Custom domain*, enter the hostname, save.
This writes a `CNAME` file into the repository. Leave *Enforce HTTPS* unchecked
until the certificate is issued, then turn it on.

**On Cloudflare:** add a `CNAME` record pointing your hostname to
`<account>.github.io`. For an apex domain, use a `CNAME` record on `@` —
Cloudflare's CNAME flattening handles it, so the four GitHub A records aren't
needed.

A note on proxying: GitHub Pages issues its own certificate, and Cloudflare's
orange-cloud proxy can interfere with that validation. Set the record to **DNS
only** (grey cloud) until GitHub reports the certificate as issued, then switch
the proxy on if you want it. If you do proxy, set SSL/TLS mode to **Full
(strict)** — Flexible causes redirect loops with Pages.

## Before it goes public

- `index.html` still contains two bracketed placeholders: the funder and
  partner acknowledgment line, and the Publications list.
- Footer social links are `href="#"` and need real URLs or removal.
- Confirm what CGI stands for in the COP17 dialogue conveners.
- In `index.html`, uncomment the `canonical` and `og:url` tags and fill in the
  domain. If you want the site hidden from search while you test, uncomment the
  `robots` noindex tag — and remember to remove it at launch.
- Add a real social preview image if the Lab has one: save it into the repo and
  add `<meta property="og:image" content="https://YOUR-DOMAIN/social.png">`.
  It has to be a full URL, so this only works once the domain is live.

## Editing later

To change a section, edit its `index.html` in that section's folder. To change
the header, tab bar, hero or footer on every page, edit `_layouts/default.html`.
To add a section, create `new-section/index.html` with the same front matter,
then add a tab link in the layout's `<nav>` and footer, and a `<url>` entry in
`sitemap.xml`. The hero is full height on the Overview and compact on every
other page. NCDP design tokens are the CSS custom properties at the top
(`--crimson`, `--slate`, `--colblue`, `--navy`); changing a color there changes
it everywhere it's used.
