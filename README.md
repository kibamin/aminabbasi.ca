# aminabbasi.ca

Four pages, no build step, no framework, no dependencies. Every page is a single
self-contained file — CSS and JavaScript are inlined, so any page works on its own
whether you open it locally or serve it.

```
index.html   portfolio — summary, work, publications, skills, education, contact
blog.html    blog with an inline reader
lab.html     two interactive ML demos
game.html    مارپله / snakes & ladders
CNAME        your domain
```

The only external requests are the Google Fonts stylesheet and your résumé PDF.

---

## Deploy to GitHub Pages

**1. Create a public repo** named exactly `YOUR-USERNAME.github.io`.

**2. Push these files:**

```bash
cd aminabbasi-site
git init
git add .
git commit -m "Personal site"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/YOUR-USERNAME.github.io.git
git push -u origin main
```

**3. Settings → Pages** → Source: *Deploy from a branch* → `main` / `(root)`. Set Custom domain to `aminabbasi.ca`, then tick Enforce HTTPS once it appears.

**4. DNS** at your registrar:

| Type | Host | Value |
|---|---|---|
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |
| CNAME | `www` | `YOUR-USERNAME.github.io` |

Propagation is usually under an hour.

---

## Before you publish

Search all files for `YOUR-` — there are three placeholder links in `index.html`:

- `https://www.linkedin.com/in/YOUR-LINKEDIN`
- `https://github.com/YOUR-GITHUB`
- `https://scholar.google.com/citations?user=YOUR-ID`

Also check the two arXiv IDs in the publications list resolve (`2605.24008`, `2601.08024`), and swap them for journal DOIs if either has been published since.

**The three blog posts are starter drafts.** I wrote them in your voice on topics from your work, but they are my words, not yours. Read them, rewrite them, or delete them before the site goes live.

---

## Adding a blog post

Open `blog.html` and find the `POSTS` array near the bottom. Copy one object, put the new one at the top:

```js
{
  slug: 'url-friendly-name',
  title: 'Your title',
  date: 'September 2026',
  read: '5 min',
  tag: 'Applied ML',        // creates a new filter button automatically
  excerpt: 'One or two sentences shown on the card.',
  body: '<p>Plain HTML. Use p, h2, ul, blockquote, code.</p>'
}
```

Each post gets its own URL via the hash (`blog.html#url-friendly-name`), so links are shareable and the back button works.

---

## Changing the look

Every colour, radius, and font lives in the `:root` block near the top of each page's
`<style>`, with a matching `[data-theme="dark"]` block below it. Change `--iris` and
`--rose` and the whole page — gradients, buttons, timeline dots, hover states — follows.

Because the pages are self-contained, a token change has to be repeated in each file
you want it to apply to. Find and replace across all four is the quickest way.

The theme choice is stored in `localStorage` and falls back to the visitor's system preference on first visit.

---

## Notes

- Everything respects `prefers-reduced-motion` — animations turn off for visitors who ask for that.
- The lab demos and game are pure canvas and DOM, nothing external.
- Fonts are Sora, Plus Jakarta Sans, JetBrains Mono, and Vazirmatn (for the Persian title), loaded from Google Fonts.
