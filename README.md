# Highwater — writing site

A fast, owned, static publication. You write Markdown; it builds clean long-form
pages. Free hosting on GitHub Pages, pointed at **hw-p.com**.

---

## Writing a new post

1. In `src/pages/essays/`, add a new file, e.g. `0003-my-title.md`.
2. Start it with this block (the "frontmatter"):

   ```
   ---
   layout: ../../layouts/Essay.astro
   title: My Title
   dek: One line that sits under the title.
   date: 2026-08-15
   ---
   ```

3. Write the body below the second `---` in normal Markdown.
4. Save/commit. The site rebuilds and publishes itself.

Notes:
- Posts sort newest-first by `date`, and the homepage numbers them automatically.
- Add `draft: true` to the frontmatter to keep a post hidden from the homepage.
- The two starter posts in `essays/` are examples. Replace them with your own.

---

## First-time deploy (about 15 minutes, all in the browser)

**1. Put the code on GitHub**
- Create a free account at github.com if you don't have one.
- Click **New repository**, name it `highwater-site`, keep it Public, create it.
- On the repo page: **Add file → Upload files**, drag in everything from this
  folder (keep the folder structure), and commit to the `main` branch.

**2. Turn on Pages**
- Repo **Settings → Pages**.
- Under **Build and deployment → Source**, choose **GitHub Actions**.
- The included workflow builds and deploys on every commit. First run takes a
  couple minutes; watch it under the repo's **Actions** tab. When it's green,
  your site is live at `https://<your-username>.github.io/...` (a temporary URL).

**3. Attach hw-p.com**
- Still in **Settings → Pages**, under **Custom domain**, enter `hw-p.com`, Save.

**4. DNS at Squarespace (this is the only place email could break — don't touch MX)**
- Go to your Squarespace **Domains → hw-p.com → DNS**.
- **Leave every MX, SPF, DKIM, DMARC / TXT email record exactly as is.** Those
  are your Workspace email. Do not delete them.
- **Remove** any preset/parking records Squarespace points at its own servers:
  the default `@` **A** records and any `@` or `www` record aimed at Squarespace
  parking. (These conflict with GitHub.)
- **Add four A records**, Host `@`, pointing to GitHub Pages:
  ```
  185.199.108.153
  185.199.109.153
  185.199.110.153
  185.199.111.153
  ```
- **Add one CNAME record**, Host `www`, value `<your-username>.github.io`
  (use your real GitHub username; keep the trailing dot if the form requires one).

**5. Finish**
- Back in **Settings → Pages**, wait for the domain check to pass (minutes to a
  few hours), then tick **Enforce HTTPS**.
- `https://hw-p.com` now serves your site.

---

## Preview locally (optional)

If you have Node installed:

```
npm install
npm run dev      # live preview at http://localhost:4321
npm run build    # production build into dist/
```

You do **not** need Node to publish — GitHub builds it for you.
