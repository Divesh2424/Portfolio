# Divesh — Developer Portfolio

A fast, self-contained personal portfolio. **No build step, no dependencies, no backend.**
The whole site is one `index.html` file, so it deploys to Vercel's free Hobby plan as a static
site with zero configuration. Your résumé and hero photo are embedded, so everything works even
when you open the file directly.

---

## Run it locally

It's static, so any of these work:

```bash
open index.html            # macOS  (start index.html on Windows)

# or serve it (recommended — behaves like production):
npx serve .
# or
python3 -m http.server 5173
```

## "Production verification"

There's no compile step for a static site — what you see locally is what ships. Serve the folder,
then check: no console errors, résumé downloads, the hero photo tilts to your cursor/finger, and the
layout looks right on a phone.

---

## Deploy to Vercel (free Hobby plan)

### Option A — GitHub → Vercel (auto-deploys on push)

1. Push this folder to a new GitHub repo:
   ```bash
   git init && git add . && git commit -m "portfolio"
   git branch -M main
   git remote add origin https://github.com/Divesh2424/portfolio.git
   git push -u origin main
   ```
2. vercel.com → **Add New → Project → Import** your repo.
3. Framework Preset: **Other**. Leave Build Command and Output Directory empty.
4. **Deploy**. Every future `git push` redeploys automatically.

### Option B — Vercel CLI

```bash
npm i -g vercel
vercel          # link/create project, accept defaults
vercel --prod   # ship to production
```

No environment variables needed.

---

## The hero photo (3D tilt)

The hero uses your grey-background studio headshot with a subtle **3D tilt** — it leans and catches
light as the visitor moves their cursor or finger, and sits flat/static under `prefers-reduced-motion`.

The photo is **embedded** in `index.html` (as a data URI) and also included as `portrait.jpg`.
To change it:

- Simplest: replace `portrait.jpg` with a new **3:4 portrait** (e.g. 900×1200), then in `index.html`
  find the hero `<img>` and set its `src` to `"portrait.jpg"` instead of the long `data:` string.
- Or re-embed a new photo as a data URI in that same `src`.

A clean, evenly-lit, front-facing headshot works best here.

---

## Editing your content

Everything lives in `index.html`:

- **Text** (hero, projects, experience, about, contact) — plain HTML in the `<body>`. Search for a
  heading like `ChhotaLink` or `Techennia` and edit inline.
- **Interactive data** — near the bottom, inside `<script>`, see the **EDIT ZONE** comment: `SYS`
  (the "How I think" system map) and `TOOLS` (the skills toolbox). Terminal commands are just below.
- **"Right now" cards** — search for `<!-- EDIT: "currently building" -->` in the About section.

### Swapping your résumé

The PDF is embedded so download works with no extra files. When you update it, replace `resume.pdf`,
then either re-embed it or set `const RESUME_DATA_URI = "/resume.pdf";` in the `<script>` to point at
the static file.

---

## Before you go live — quick checklist

- [ ] Replace the placeholder domain `https://your-project.vercel.app/` with your real Vercel URL in: `<link rel="canonical">`, the Open Graph `og:url`, and `sitemap.xml` / `robots.txt`.
- [x] LinkedIn URL confirmed → `https://linkedin.com/in/divesh2424`.
- [ ] (Optional) Add a social share image at `/og.png` (1200×630). The meta tags already reference it.
- [ ] (Optional) Point project **GitHub** links at the specific repos instead of your profile.

Try the easter egg: press `~` (or the Konami code) for a working terminal — `sudo hire-me`.

---

## What's inside

```
divesh-portfolio/
├── index.html      # the entire site (HTML + CSS + JS, résumé + photo embedded)
├── portrait.jpg    # your hero headshot (also embedded in index.html)
├── resume.pdf      # your résumé (also embedded in index.html)
├── robots.txt
├── sitemap.xml
├── .gitignore
└── README.md
```

Built to be truthful to the résumé, fast, responsive, keyboard-accessible, and to respect
`prefers-reduced-motion`.
