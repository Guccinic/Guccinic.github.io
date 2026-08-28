# Nicole Cevallos — research site

Static site. No build step, no dependencies. Every file is plain HTML/CSS and works
when opened directly in a browser or served from GitHub Pages.

```
index.html          Profile, research outputs, about, contact
capture-once.html   The working paper, wrapped in site navigation
style.css           Design system for index.html
sitenav.css         Navigation bar only (the paper keeps its own inline styles)
assets/             Put poster.pdf and any figures here
```

---

## 1 · Fill in the placeholders

Search `index.html` for these and replace:

| Placeholder | Where | What to put |
|---|---|---|
| `REPLACE@EXAMPLE.COM` | Contact section, twice | Your email |
| `REPLACE-USERNAME` | Contact section, twice | Your GitHub username |
| `Add your profile URL` | Contact section | LinkedIn URL, or delete the row |

Then export the poster from PowerPoint as PDF and save it to `assets/poster.pdf`.
(In PowerPoint: File → Export → PDF. Keep the 36×24 page size.)

---

## 2 · Publish to GitHub Pages

**One-time setup.** Create a repository named exactly:

```
YOUR-USERNAME.github.io
```

That exact name is what makes it publish at the root domain rather than a subpath.

Then, from inside this folder:

```bash
git init
git add .
git commit -m "Research site: profile, working paper, poster"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/YOUR-USERNAME.github.io.git
git push -u origin main
```

In the repo on GitHub: **Settings → Pages → Source → Deploy from a branch → `main` / `root`**.

Live within a minute or two at:

```
https://YOUR-USERNAME.github.io
```

**Every update after that** is three commands:

```bash
git add .
git commit -m "what changed"
git push
```

---

## 3 · Point the poster QR at the site

Once the site is live, regenerate the QR so it points at your own domain instead of
the artifact link:

```bash
python3 -c "import segno; segno.make('https://YOUR-USERNAME.github.io', error='h').save('qr_research.png', scale=22, border=2, dark='#16264F', light='white')"
```

Replace `qr_research.png` next to the poster script and rebuild. A QR pointing at your
own site is better than one pointing at a platform link — you control where it goes,
and you can change the destination later without reprinting.

---

## 4 · Get a DOI (recommended before you present)

A DOI makes the paper citable and permanent. Free, and takes about fifteen minutes.

**Zenodo** — https://zenodo.org — run by CERN. Upload the paper as PDF, choose
"Publication → Working paper", add authors and a description, publish. You get a DOI
immediately.

**OSF** — https://osf.io — better if you plan to add data and materials later.

Once issued, put the DOI in the `#doi` note in `index.html` and on the poster.

---

## 5 · Custom domain (optional, later)

Buy a domain, then:

1. Create a file named `CNAME` in this folder containing only your domain, e.g. `nicolecevallos.com`
2. At your registrar, add these DNS records:
   - `A` records for `@` → `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - `CNAME` for `www` → `YOUR-USERNAME.github.io`
3. In repo Settings → Pages, enter the domain and tick **Enforce HTTPS**

---

## Notes

- The site is fully static, so it costs nothing and cannot break at runtime.
- Both pages respond to system dark mode.
- The working paper keeps the design it was written with; only a nav bar was added
  around it, so editing the paper never touches the site styles.
- Everything marked "planned" or "pending" on the index is labeled honestly. Update the
  status chips (`chip live`, `chip draft`, `chip soon`) as things ship.
