# APE-system Next.js → GitHub Pages Deployment

This repository (`qanglee-a11y.github.io`) hosts the GitHub Pages site for the
[APE-system](https://github.com/qanglee-a11y/APE-system) Next.js project.

## How it works

A GitHub Actions workflow (`.github/workflows/deploy.yml`) automatically:

1. Checks out the `APE-system` repository
2. Installs dependencies (`npm ci`)
3. Builds the Next.js project as a static export (`npm run build`)
4. Deploys the generated `out/` directory to GitHub Pages

The site is available at: **https://qanglee-a11y.github.io/**

## Triggering a deployment

The workflow runs automatically on every push to the `main` branch of this
repository.  You can also trigger it manually from the **Actions** tab on
GitHub (*Run workflow*).

## Required secrets

Before the workflow can check out `APE-system`, you must create a **Personal
Access Token (PAT)** with `repo` scope and add it as a repository secret named
`PAT_TOKEN`:

1. Go to **GitHub → Settings → Developer settings → Personal access tokens**
2. Generate a new token (classic) with the `repo` scope
3. In *this* repository go to **Settings → Secrets and variables → Actions**
4. Create a new secret called `PAT_TOKEN` and paste the token value

## Required configuration in APE-system

For a Next.js project to export as a static site suitable for GitHub Pages,
the `APE-system` repo's `next.config.js` (or `next.config.ts`) must include:

```js
/** @type {import('next').NextConfig} */
const nextConfig = {
  output: 'export',
  // If the site is NOT served at the root domain (e.g. a sub-path like
  // /APE-system), set basePath and assetPrefix accordingly:
  // basePath: '/APE-system',
  // assetPrefix: '/APE-system/',
};

module.exports = nextConfig;
```

> **Note:** When using `output: 'export'`, Next.js writes the static files to
> the `out/` directory.  Image optimisation (`next/image`) and other
> server-side features are not supported in static export mode.