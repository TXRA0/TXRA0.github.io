# Screeps Combat Lab

A Jekyll blog starter for publishing Screeps combat engineering guides, bot-design notes, research logs, and battle reports. It uses the [Minimal Mistakes](https://github.com/mmistakes/minimal-mistakes) theme through its GitHub Pages remote-theme setup.

## 1. Create the GitHub repository

1. Create a new **public** repository named `screeps-combat-lab` under your GitHub account.
2. In `_config.yml`, replace every `YOUR-USERNAME` with your GitHub username.
3. Keep `baseurl: "/screeps-combat-lab"` for a project repository named `screeps-combat-lab`.
4. From this folder, initialise Git and push the files to your new, empty repository:

   ```bash
   git init -b main
   git add .
   git commit -m "Initial Screeps Combat Lab site"
   git remote add origin https://github.com/YOUR-USERNAME/screeps-combat-lab.git
   git push -u origin main
   ```

   You can also upload the files through GitHub's web interface, keeping the folder structure intact.

If instead you name the repository exactly `YOUR-USERNAME.github.io`, set `baseurl: ""` in `_config.yml` and update `url` to `https://YOUR-USERNAME.github.io`.

## 2. Enable GitHub Pages

1. Open the repository's **Settings → Pages**.
2. Under **Build and deployment**, select **GitHub Actions** as the source.
3. Open the **Actions** tab and check that **Build and deploy site** runs after your first push to `main`.
4. When the workflow succeeds, the site will be available at `https://YOUR-USERNAME.github.io/screeps-combat-lab/`.

The workflow in `.github/workflows/pages.yml` builds the Jekyll site and deploys the generated `_site` directory using GitHub's Pages Actions.

## 3. Publish a post

Create a Markdown file in `_posts/` with this filename pattern:

`YYYY-MM-DD-your-post-title.md`

Start with YAML front matter:

```yaml
---
title: "Your article title"
date: 2026-10-30 12:00:00 +0000
categories:
  - guides
tags:
  - screeps
  - combat-ai
excerpt: "A one-sentence summary for archive pages."
---
```

Then write the article in Markdown. `POST_TEMPLATE.md` contains a suggested structure for guides and research articles. Copy it when starting a new post, and remove the template comments/placeholders before publishing.

Available section categories are `guides`, `bot-design`, `research`, and `battle-reports`. A post can belong to more than one category.

## 4. Preview locally (optional)

You'll need Git, Ruby, and Bundler installed. From the repository folder:

```bash
bundle install
bundle exec jekyll serve --baseurl ""
```

Open the local URL printed by Jekyll. The empty local `baseurl` keeps the preview at the root; the GitHub Actions workflow supplies the correct project path during deployment. To build without starting the local server:

```bash
bundle exec jekyll build
```

## 5. Main files to edit

| File | Purpose |
|---|---|
| `_config.yml` | Site title, URL, author details, theme, and plugins |
| `_data/navigation.yml` | Top navigation links |
| `index.html` | Homepage introduction and latest posts |
| `about.md` | About page |
| `guides/`, `bot-design/`, `research/`, `battle-reports/` | Section landing pages |
| `_posts/` | Published articles |
| `POST_TEMPLATE.md` | Suggested article structure |
| `assets/css/main.scss` | Small theme style customisations |
| `.github/workflows/pages.yml` | Automatic GitHub Pages deployment |

## Editorial suggestion

For technical credibility, make each substantial post answer: what problem was being solved, what assumptions applied, what changed, how it was tested, what the evidence showed, and what limitations remain. Label pseudocode clearly and include the Screeps API or game-version context when relevant.

## Theme and deployment references

- [Minimal Mistakes quick-start guide](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/)
- [Minimal Mistakes configuration](https://mmistakes.github.io/minimal-mistakes/docs/configuration/)
- [GitHub Pages: Create a site with Jekyll](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll)
