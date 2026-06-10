# Coffee &amp; Canines Collective — Website

The public website for **The CCC: Coffee &amp; Canines Collective**, a California Nonprofit
Public Benefit Corporation in Fresno, CA. A faithful static port of the original Google Sites
design (same content, fonts, colors, images, and layout) — plain HTML/CSS, no build step —
intended to be served at **https://coffeeandcaninescollective.org** via GitHub Pages.

## Structure

```
.
├── index.html               # Home ("Coming Soon to Fresno, CA")
├── the-mission.html         # The Mission
├── menus.html               # Menus (Human Provisions | Canine Nutrition)
├── the-pack.html            # The Pack (team)
├── the-collective.html      # The Collective (partnerships + interest form)
├── 404.html                 # Not-found page
├── css/styles.css           # Theme: blush/terracotta/brown, Caveat + Montserrat
├── js/site.js               # Header scroll behavior + mobile nav
├── assets/                  # All original site images (downloaded from Google Sites)
├── sitemap.xml  robots.txt  # Search-engine plumbing
└── CNAME  .nojekyll         # GitHub Pages: custom domain + no Jekyll
```

All paths are **relative**, so the site renders correctly when you open `index.html`
directly in a browser (no server needed). For a local server:
`python3 -m http.server 8000` then visit http://localhost:8000.

## Editing

Text lives directly in each `.html` file. Shared styling is `css/styles.css`.
The partnership form on The Collective page is the original embedded Google Form —
replies still go to the same spreadsheet/inbox.

## Deploying — GitHub organization + GitHub Pages (free)

1. **Create a free GitHub organization** (https://github.com/organizations/plan) so the
   repo and site are independent of any personal account. The org name never appears on
   the live site once the custom domain is set.
2. **Push this folder** to a repo in the org:
   ```bash
   git init -b main && git add . && git commit -m "CCC website"
   git remote add origin https://github.com/<ORG>/website.git
   git push -u origin main
   ```
3. **Enable Pages**: repo → Settings → Pages → Deploy from branch → `main` / root.
   The custom domain auto-fills from the `CNAME` file. Check **Enforce HTTPS** once DNS works.
4. **GoDaddy DNS** — first **delete the existing domain forwarding to Google Sites**
   (this is what currently 301-redirects the domain). Then add:
   - Four `A` records on `@`: `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - `CNAME` record `www` → `<ORG>.github.io`
5. **Google Search Console** (fixes the original indexing problem):
   add property `coffeeandcaninescollective.org`, verify via DNS TXT record, submit
   `https://coffeeandcaninescollective.org/sitemap.xml`, then *URL Inspection → Request
   indexing* on the homepage.

DNS propagation can take minutes to ~24 h. After that, Google indexes the site normally —
unlike `sites.google.com` pages.
