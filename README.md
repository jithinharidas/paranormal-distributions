# Paranormal Distributions

Personal blog and portfolio of Jithin K Haridas.  
Built with Hugo. Hosted on GitHub Pages.

---

## Setup (first time)

**1. Install Hugo**
```bash
# macOS
brew install hugo

# Windows (via Chocolatey)
choco install hugo-extended

# Verify
hugo version
```

**2. Clone your repo**
```bash
git clone https://github.com/jithinharidas/paranormal-distributions.git
cd paranormal-distributions
```

**3. Preview locally**
```bash
hugo server -D
# Open http://localhost:1313
```

---

## Writing a new post

```bash
hugo new posts/your-post-title.md
```

This creates `content/posts/your-post-title.md` with front matter pre-filled.

Open the file and edit:
```yaml
---
title: "Your Post Title"
date: 2026-04-20
categories: ["Analytics"]   # Analytics / Engineering / Career / Statistics
tags: ["sql", "attribution"]
description: "One line summary shown on the homepage."
draft: false                 # Change to false when ready to publish
---

Your content here in Markdown.
```

---

## Deploy to GitHub Pages

```bash
# Build the site
hugo

# This generates the /public folder
# Commit everything (source + public)
git add .
git commit -m "new post: your post title"
git push
```

> **GitHub Pages setup**: In your repo Settings → Pages → set source to `main` branch, `/docs` folder.  
> Rename `public/` to `docs/` or configure Hugo to output to `docs/`:  
> Add `publishDir = "docs"` to `hugo.toml`

---

## Custom domain (GoDaddy)

**In your repo:**
1. Create a file `docs/CNAME` containing just your domain:
   ```
   paranormaldistributions.com
   ```

**In GoDaddy DNS settings:**
Add these records:

| Type  | Name | Value                  |
|-------|------|------------------------|
| A     | @    | 185.199.108.153        |
| A     | @    | 185.199.109.153        |
| A     | @    | 185.199.110.153        |
| A     | @    | 185.199.111.153        |
| CNAME | www  | jithinharidas.github.io |

Wait 10–30 minutes for DNS to propagate. GitHub will auto-provision HTTPS.

---

## Project structure

```
paranormal-distributions/
├── content/
│   ├── posts/          ← your blog posts (markdown)
│   └── about.md        ← about page trigger
├── layouts/
│   ├── _default/       ← base, list, single templates
│   ├── about/          ← about page layout
│   └── index.html      ← homepage
├── static/
│   └── css/main.css    ← all styles
├── archetypes/
│   └── posts.md        ← new post template
└── hugo.toml           ← site config
```

---

## Updating content

| Task | File to edit |
|---|---|
| Bio / description | `hugo.toml` → `params.description` |
| Social links | `hugo.toml` → `params.*` |
| Skills | `layouts/about/single.html` → skills section |
| Projects | `layouts/about/single.html` → projects section |
| Site title | `hugo.toml` → `title` |
