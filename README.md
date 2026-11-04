# AiNex Documentation

This repository contains the AiNex VitePress documentation site. The
documentation source files are Markdown files under `docs/docs/`.

## Local development

Install dependencies and start the local documentation server:

```bash
npm ci
npm run docs:dev
```

Build the production site and stage the artifacts:

```bash
npm run docs:build
npm run docs:stage-main
```

The staged production files are generated in `projects/AiNex/en/latest/`.
During staging, raster images are converted to WebP and page references are
updated to match.

## Feedback widget configuration

The Chat button is mounted by `docs/.vitepress/theme/Layout.vue`. Its form is in
`docs/.vitepress/theme/FeedbackWidget.vue`; its styles in
`docs/.vitepress/theme/custom.css` match the AiDoggy template. Feedback is labelled
`AiNex docs`; the version is taken from the final segment of the site's `base`.

The default endpoint is `https://www.hiwonder.net/english-course-feedback`.
To override it, copy `docs/.env.example` to `docs/.env.local`, change
`VITE_FEEDBACK_API_URL`, then restart the dev server or rebuild the site.
The endpoint must accept multipart POST fields and `images[]`, and return JSON
with `code: 1` or `code: 200` on success. For requests from another origin,
the API server must allow the documentation site's origin through CORS.

Run `npm run docs:dev` to preview. For publishing, run `npm run docs:build`
and `npm run docs:stage-main` before deploying the generated `projects/` files.

## GitHub Pages deployment

The build artifacts under `projects/` are committed to the repository. Open
**Settings > Pages**, select **Deploy from a branch**, and choose **main** and
**/(root)**. Do not bind a custom domain.

The GitHub Pages direct URL is:

```text
https://hiwonder-docs.github.io/AiNex-vite/projects/AiNex/en/latest/
```

The public-facing URL (via the baota Nginx reverse proxy) is:

```text
https://wiki-test.hiwonder.com/projects/AiNex/en/latest/
```
