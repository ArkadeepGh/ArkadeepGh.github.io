# Setup

## 1. Fill in your details

In `_config.yml`, change:

- `url` → `https://YOUR-USERNAME.github.io`
- `github_username` → your handle
- `email` → your address
- `baseurl` → **leave as `""`** if the repo is named `YOUR-USERNAME.github.io`; set it to `"/blog"` (or whatever the repo is called) otherwise.

Getting `baseurl` wrong is the single most common reason the CSS fails to load.

## 2. Push it

```bash
cd blog
git init
git add .
git commit -m "First commit"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/YOUR-USERNAME.github.io.git
git push -u origin main
```

## 3. Turn on Pages

Repo → **Settings → Pages** → Source: *Deploy from a branch* → Branch: `main`, folder `/ (root)` → Save.

First build takes a couple of minutes. The site lands at `https://YOUR-USERNAME.github.io`.

## Writing a post

Create a file in `_posts/` named `YYYY-MM-DD-some-slug.md`:

```markdown
---
title: "A title with $\\sigma$-algebras in it"
date: 2026-09-20
tags: [linear-algebra]
excerpt: "One sentence shown on the home page."
math: true
---

Body goes here.
```

`math: true` is the default for posts, so you can drop it. The date in the filename must match the date in the front matter, and posts dated in the future won't build unless you pass `--future`.

## Maths

Inline with `$...$`, display with `$$...$$` on its own lines. Numbered equations work via `\begin{equation}...\end{equation}`, and `\label`/`\eqref` cross-references resolve.

Shortcut macros defined in `_includes/mathjax.html`:

| Macro | Renders |
|---|---|
| `\E{X}` | expectation |
| `\Var{X}` | variance |
| `\Cov{X}{Y}` | covariance |
| `\Prob{A}` | probability |
| `\R`, `\N` | ℝ, ℕ |
| `\indep` | independence symbol |
| `\iid`, `\dto`, `\pto` | iid, convergence in distribution / probability |

Add your own to the `macros` block in that file.

## Theorem environments

Wrap Markdown in a div and let the CSS label it:

```html
<div class="theorem" markdown="1">
Statement here, maths allowed.
</div>

<div class="proof" markdown="1">
Argument here. A tombstone □ is appended automatically.
</div>
```

`definition` works the same way. The `markdown="1"` attribute is required — without it kramdown treats the contents as raw HTML and your `$$` won't be processed.

## Previewing locally (optional)

```bash
gem install bundler
bundle install
bundle exec jekyll serve --livereload
```

Then open `http://localhost:4000`. Not required — you can push and let GitHub build it — but it's a much faster loop if you're writing regularly.

## Design notes

Dark mode follows the system setting; both palettes live in the `:root` blocks at the top of `assets/css/style.css`. The text column is capped at roughly 68 characters, which is why long display equations scroll horizontally rather than shrinking.
