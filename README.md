QA Portfolio — Uday Prakash Patel

This repository contains a static portfolio website (index.html) for Uday Prakash Patel (QA Testing Specialist).
This README explains, step-by-step, how to publish this site using GitHub Pages.

Quick checklist (before you start)

You have a GitHub account.

index.html is in the repository root (or in /docs if you prefer that option).

You know your GitHub repo name (or will create one now).

Option A — Deploy using GitHub web UI (fast, no CLI required)

Create a new repository

Go to GitHub → click New repository.

Repository name: e.g. qa-portfolio (or your-username.github.io for a user site).

Choose Public (recommended for Pages). Click Create repository.

Upload files

In your new repo, click Add file → Upload files.

Drag & drop index.html (and any other files: assets, css, README etc).

Commit the changes (Add a commit message → Commit changes).

Enable GitHub Pages

Go to the repo Settings → Pages (or Settings → Pages).

Under Source, select:

Branch: main (or master)

Folder: / (root) — or /docs if you uploaded files to /docs.

Click Save.

After publishing, GitHub will show the site URL (e.g. https://your-username.github.io/your-repo/). Use that to view the live site.

Option B — Deploy from your local machine (recommended if you use Git)

Create a new GitHub repo (use web UI as above, do not initialize with README if you plan to push an existing local repo).

Open terminal in your project folder (the folder that contains index.html) and run:

# initialize (if not already a git repo)
git init

# add files
git add .

# initial commit
git commit -m "Initial commit: portfolio site"

# set main branch (optional)
git branch -M main

# add remote (use HTTPS or SSH)
# HTTPS:
git remote add origin https://github.com/<your-username>/<your-repo>.git
# OR SSH (if you have SSH keys configured):
git remote add origin git@github.com:<your-username>/<your-repo>.git

# push to GitHub
git push -u origin main


Enable GitHub Pages

On GitHub, go to Settings → Pages.

Select main branch and root (/) (or /docs).

Save and then open the provided URL to view the site.

Option C — Project page vs User/Organization page (naming)

User/Organization site: Repository name must be <your-username>.github.io. The site will be available at https://<your-username>.github.io/ and must be published from the main branch root.

Project site: Any repository name — the URL will be https://<your-username>.github.io/<repo-name>/.

Option D — Upload via ZIP (GitHub web UI)

If you have a ZIP of your site:

Unzip locally.

Use the Upload files button in GitHub repo UI to upload all extracted files.

Commit and enable Pages as above.

Test site locally (quick check)

From your project folder run:

# Python 3 simple server
python3 -m http.server 8000

# Then open:
http://localhost:8000


(Or use VS Code Live Server extension.)

Deploy to gh-pages branch (alternative method)

If you prefer publishing from gh-pages branch (common for static sites):

# from project root
git add .
git commit -m "Publish to gh-pages"
git push origin `git subtree split --prefix . main`:gh-pages --force


Or use gh-pages npm package or ghp-import for build workflows. (If you want, I can add a gh-pages workflow file.)

(Optional) Automatic deploy with GitHub Actions — example

Place the following file at .github/workflows/deploy-pages.yml to automatically publish when you push to main. This example uses the GitHub Pages official actions pattern.

name: Deploy to GitHub Pages
on:
  push:
    branches:
      - main

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      # If you had a build step (e.g. static site generator), run it here.
      # - name: Build
      #   run: npm ci && npm run build

      - name: Upload artifact to Pages
        uses: actions/upload-pages-artifact@v1
        with:
          path: .   # path to files to publish; change to ./dist if you build to dist

      - name: Deploy to GitHub Pages
        uses: actions/deploy-pages@v1


Note: that workflow publishes the repository contents (or a build output) to GitHub Pages automatically whenever you push to main. If you want, I can add this workflow file to your repo/ZIP.

Custom domain (optional)

To use a custom domain (e.g. www.uday.com):

In your repo root, create a file named CNAME containing the domain, for example:

www.yourdomain.com


In your domain registrar, configure DNS:

For apex/root domain (yourdomain.com): create A or ALIAS records per your registrar (check GitHub docs or registrar help).

For www.yourdomain.com: create a CNAME to your-username.github.io.

In GitHub repository Settings → Pages, add the custom domain.

GitHub will provision HTTPS for that domain (if DNS is correct). If you run into certificate issues, double-check DNS records and that the CNAME file matches exactly.

If you want, I can create the CNAME file content and show example DNS records for your registrar (I will need your domain registrar name).

Common troubleshooting & checks

Blank page / 404 — Ensure index.html exists at the publish root (repo root or /docs) and is named exactly index.html.

Wrong branch selected — Verify Pages source is set to main (or gh-pages, or /docs) in Settings → Pages.

404 after changing settings — Refresh the Pages settings section to see the published URL. (GitHub will list the URL there.)

Custom domain errors — Ensure DNS records are pointing correctly and the repo contains the correct CNAME file.

Site not public — If repository is private, Pages may still work for your account type; making it public is the simplest way to ensure wide access.

Recommended commit workflow

git add .

git commit -m "Update: improved cover letter toggle + animations"

git push origin main

If you use the GitHub Actions workflow above, each push to main will redeploy.

Where I can help next

I can add the GitHub Actions workflow into your zip/repo now.

I can update the README.md inside your zip with this full content (and re-create the ZIP).

I can create a ready-made CNAME file if you tell me your custom domain.

Short summary

Easiest: upload files via GitHub UI, enable Pages from main root.

Preferred if you use Git: push to main and enable Pages.

Want automation? Add the Actions workflow file above.
