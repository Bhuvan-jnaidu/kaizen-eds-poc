# Kaizen EDS POC — Adobe blocks + Kaizen theme

Adobe's **aem-block-collection** (all blocks, JS untouched / OOTB) with a single
**Kaizen global theme** layered on via CSS.

## What was added (only 3 things)
1. `styles/kaizen-theme.css` — remaps the boilerplate's design tokens (colors,
   fonts, type scale, buttons) to Kaizen values, so every Adobe block inherits
   the Kaizen look. Includes the NVIDIA Sans `@font-face`.
2. `fonts/NVIDIASansVF_NALA_W_Wght.woff2` — the NVIDIA Sans variable font.
3. `head.html` — one extra `<link>` loading `kaizen-theme.css` after `styles.css`.

**No block JS or block CSS was modified.** When Adobe updates a block, drop in
their new version — the Kaizen look still applies.

## Run it locally
```sh
npm install
npm install -g @adobe/aem-cli
aem up          # serves http://localhost:3000
```
Then set a mountpoint in `fstab.yaml` (Google Drive or AEM) for content.

## Deploy
Push to your POC branch, add the AEM Code Sync GitHub/GitLab app, and preview via
`https://<branch>--<repo>--<owner>.aem.page/`.

## Optional: use REAL Kaizen tokens (not just fallbacks)
`kaizen-theme.css` uses `var(--kaizen-token, nvidia-fallback)`. To drive it with
Kaizen's actual tokens:
```sh
npm i @kui/foundations-css
```
then import its `dist/base/variables.css` (+ theme) before `kaizen-theme.css`.

## Lighthouse
No React, no per-block rewrites — keeps the 100/100/100/100 target intact.
