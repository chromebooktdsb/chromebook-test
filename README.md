## Purpose

This application was created to assist IT Support staff with Chromebook diagnostics and hardware verification.

It provides a centralized interface for testing device components and collecting troubleshooting information before repair or deployment.


## Features

- Hardware diagnostics
- Device information
- Display testing
- Keyboard testing
- Touchpad testing
- Audio testing
- Camera testing
- Network information
- Screenshot support
- File upload support

## Changes made from the original export

1. **Minified the 5 app scripts** (terser, compress + mangle). Combined size
   dropped from 99 KB to 56 KB raw (43% smaller); ~22.6 KB to ~15.5 KB gzipped
   (31% smaller over the wire). No behavior changes — same code, just compressed.

2. **Added `defer` to every `<script>` tag**, including the React/ReactDOM CDN
   tags. Previously all 5 scripts loaded render-blocking and sequentially; now
   they download in parallel while the page keeps parsing, and execute in
   order once parsing finishes.

3. **Rebuilt `favicon.png`.** The file in the original export wasn't actually
   an image — it was ~1MB of `react-dom.development.js` source text saved
   with a `.png` extension (almost certainly a mixup from whatever export step
   produced the upload). I regenerated a real 256×256 PNG (4.8 KB) from the
   app's own icon artwork (the SVG already embedded in your `index.html`
   `<template id="__bundler_thumbnail">`), so the site has a working favicon
   again. **If you have a different intended favicon design, swap this file
   out before deploying** — this is a functional placeholder, not necessarily
   your final branding.

## Deploying — GitHub Pages

```bash
cd chromebook-test-tool
git init
git add .
git commit -m "Chromebook test tool: minified assets, deferred scripts, fixed favicon"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-repo>.git
git push -u origin main
```

Then in the repo on GitHub: **Settings → Pages → Deploy from a branch → main
/ (root)**. Your site will be live at
`https://<your-username>.github.io/<your-repo>/`.

If you're pushing into an **existing** repo/branch and want to overwrite
whatever's there (be sure this is what you want — it discards remote history
on that branch):

```bash
git push --force origin main
```

## Notes

- This is a static site — no build step, no `node_modules` to commit (see
  `.gitignore`).
- The two extra files from your earlier upload (`e8851639-...js` and
  `dd8d3f9e-...js`) aren't included here — neither is referenced by
  `index.html`. `dd8d3f9e-...js` was a byte-for-byte duplicate of
  `audio_right.mp3`, and `e8851639-...js` was the unminified React dev
  source (not what the page actually loads — it loads React from the CDN).
