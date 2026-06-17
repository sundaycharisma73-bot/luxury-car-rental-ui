# Setup Guide — Luxury Car Rental UI

This repository contains a static website built with plain HTML and CSS. Use this guide to set up the project locally, run a development server, and deploy to common static hosting providers.

## 1. Prerequisites

- Git
- A modern web browser
- (Optional) Node.js and npx if you want to use `http-server` for a local server
- (Optional) Python 3 for running a simple local server

## 2. Clone the repository

```bash
git clone https://github.com/sundaycharisma73-bot/luxury-car-rental-ui.git
cd luxury-car-rental-ui
```

## 3. Run locally

Because this is a static HTML/CSS site there is no build step required. You can open `index.html` directly in your browser, but a local static server is recommended for a more realistic environment.

- With Node (http-server):

```bash
npx http-server -c-1
# Open http://localhost:8080
```

- With Python 3:

```bash
python3 -m http.server 8000
# Open http://localhost:8000
```

- With VS Code Live Server extension: right-click `index.html` → "Open with Live Server"

## 4. Environment variables (optional)

Static sites typically don't require server-side environment variables. If you reference third-party keys (maps, analytics) client-side, do not commit secret keys to the repository. Use the hosting service's environment settings or a server-side proxy for secrets.

See `.env.example` for example keys used purely for documentation.

## 5. Deployment

Below are recommended ways to deploy a static HTML/CSS site.

- GitHub Pages (recommended for GitHub-hosted repos)
  - Option A — Use a GitHub Action (this repo includes a workflow at `.github/workflows/deploy-gh-pages.yml`): push to the default branch (usually `main`) and the workflow will publish your site.
  - Option B — In repository settings → Pages, set the source to the `gh-pages` branch or `main`/`docs` folder if you prefer a branch-less setup.

- Netlify
  - Create a site from Git → GitHub, choose this repo, set the build command to (none) and publish directory to `/` or `public` depending on how you want to organize the repo. If you rely on a build step, provide the command and the build output directory.

- Vercel
  - Connect the repo in Vercel dashboard, add any environment variables, and deploy. For a pure static site Vercel will serve HTML and assets directly.

- Docker (optional)

Example Dockerfile to serve the built static site with nginx:

```dockerfile
FROM nginx:stable-alpine
COPY . /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

Build and run:

```bash
docker build -t luxury-car-ui .
docker run -p 8080:80 luxury-car-ui
```

## 6. Custom domain

To use a custom domain with GitHub Pages, add a `CNAME` file to the repository (root or `public` folder that's published) containing your domain and configure DNS for your domain provider (CNAME or A records per GitHub Pages docs). For Netlify/Vercel, follow their dashboard instructions to add a custom domain and configure DNS.

## 7. CI / Automatic deploy

This repository includes a GitHub Actions workflow that uploads the repo files to GitHub Pages whenever `main` is pushed. You can adjust the branch or add additional steps if you have a build process in the future.

## 8. Troubleshooting

- 404 after deploy: confirm the publish directory contains `index.html` at its root.
- Assets not loading: check paths are relative or ensure the hosting service preserves the directory structure.
- Custom domain issues: ensure DNS is propagated and configured per provider instructions.

## 9. Contributing

- Fork the repo and open a pull request for changes.
- Keep HTML/CSS and assets organized in folders (e.g., `assets/, css/, img/`).

## 10. Support

Open an issue in this repository for questions or problems.
