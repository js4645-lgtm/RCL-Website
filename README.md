# The Resilience Capital Lab — website

Static site for The Resilience Capital Lab, at the National Center for Disaster
Preparedness, Columbia Climate School.

## What's here

```
index.html    the entire site — HTML, CSS, JS, and logo assets in one file
404.html      branded not-found page
.nojekyll     tells GitHub Pages to serve files as-is
robots.txt    allows indexing; edit the Sitemap line once the domain is set
README.md     this file
```

There is no build step, no dependencies, and no server-side code. The two NCDP
logos are base64-embedded, so the page renders correctly even when opened from
a local file. The only external request is to Google Fonts for Roboto, Roboto
Serif, and Roboto Mono.

## Publishing to GitHub Pages

1. Create a repository (public is required for Pages on a free account —
   a suggested name is `resilience-capital-lab`).
2. Upload the contents of this folder to the repository root. Include the
   dotfile `.nojekyll`; if you use drag-and-drop in the browser, confirm it
   made it, since some file pickers hide dotfiles.
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

Everything is in `index.html`. The tab behavior is the short script at the
bottom of the file. NCDP design tokens are the CSS custom properties at the top
(`--crimson`, `--slate`, `--colblue`, `--navy`); changing a color there changes
it everywhere it's used.
