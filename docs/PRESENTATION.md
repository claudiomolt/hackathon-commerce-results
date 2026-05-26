# Presentation internals

This project is a single-file static HTML presentation deployed on Vercel.

## Public URLs

- Production: https://hackathon-commerce-results.vercel.app
- GitHub: https://github.com/claudiomolt/hackathon-commerce-results

## Main file

- `index.html` contains the full deck: CSS, data, slide templates and navigation logic.
- `data/projects.json` mirrors the project/ranking data from `index.html` so another IDE or agent can inspect/edit the dataset without reverse-engineering the HTML.

At the moment, the browser renders from the inline `projects` array inside `index.html`. If you edit `data/projects.json`, also update the inline array in `index.html` or refactor the page to load JSON dynamically.

## Rendering flow

1. `projects` array defines all project data and ranking.
2. `stats` derives high-level metrics from `projects`:
   - total projects
   - projects with public demo
   - projects with live pitch
   - projects without pitch
   - detectable tests count
   - accessible repo count
3. `slide(body, water)` wraps each slide with shared header/footer.
4. `slides.push(...)` creates the deck slides as HTML strings.
5. `deck.innerHTML = slides.join('')` injects them into `<div id="deck">`.
6. `show(index)` toggles `.slide.active`, updates dots, counter and progress bar.

## Important bug note

Do **not** create a global function named `top()`.

Browsers expose `window.top` as a non-redeclarable global. A previous version used `function top()` and Chromium threw:

```text
Identifier 'top' has already been declared
```

That prevented `deck.innerHTML` from running, so the page showed only nav arrows and no slides.

Use names like `renderTop()` / `renderFoot()` instead.

## Controls

- Keyboard:
  - `ArrowRight`, `PageDown`, `Space`: next slide
  - `ArrowLeft`, `PageUp`, `Backspace`: previous slide
  - `F`: browser fullscreen
- Mobile:
  - swipe horizontal
  - bottom arrow buttons
  - invisible side tap zones
- URL hash:
  - `#1`, `#2`, etc. deep-link to slide number.

## Slide list

1. Cover: Commerce results
2. Judging methodology: 3 judges / 3 perspectives
3. Tournament stats / data curiosities
4. Podium winners
5. Winner detail: Cursats
6. Second place: QRWapu
7. Third place: Zaploop
8. Strong mention: wapufy
9. Full ranking table
10. Final reading / takeaways

## Design system

Uses La Crypta brand assets from the official public branding repo:

- Logo: `https://github.com/lacrypta/branding/raw/main/title/512-transparent.png`
- Favicon: `https://github.com/lacrypta/branding/raw/main/iso/128-transparent.png`
- Fonts:
  - Blatant Bold
  - Standerd SemiBold

Main color tokens are in `:root` inside `index.html`.

## Local development

```bash
npm start
# opens a static server, usually at http://localhost:3000 or shown by npx serve
```

Alternative with Python:

```bash
python3 -m http.server 4177
# http://127.0.0.1:4177
```

## Verification

Recommended before deploy:

```bash
node - <<'NODE'
const fs=require('fs');
const js=fs.readFileSync('index.html','utf8').match(/<script>([\s\S]*)<\/script>/)[1];
new Function(js);
console.log('JS parses OK');
NODE
```

For visual/runtime verification, open the production URL in Chromium or any browser and confirm:

- the first slide shows `RESULTADOS FINALES / COMMERCE`
- the footer shows `01 / 10`
- arrows/swipe move between slides
- no console error about `top`

## Deployment

The project is linked to Vercel in `.vercel/project.json`.

Deploy manually:

```bash
vercel deploy --prod
```

Current production alias:

```text
https://hackathon-commerce-results.vercel.app
```
