# TasteTest

A daily exercise to train your eye for interface design. One challenge, four timed rounds, one hour in total:

1. **Design** (20 min): a brief and a blank canvas. No references, no AI.
2. **Study** (10 min): four sketched reference screens. Write down 3 patterns, 3 do's and 3 don'ts.
3. **Compare** (10 min): put your notes next to an analysis of eight observations and tick the ones you spotted yourself.
4. **Redesign** (20 min): the same screen again, with what you just learned. Afterwards both versions sit side by side.

The idea: AI can generate a hundred screens in a minute, but someone still has to judge which one is good. That judgement is trained by designing, looking closely, and designing again.

## Designing

In the design rounds you choose where you work:

- **Sketch here**: a built-in drawing area with pen, shapes, text, fill, move and eraser.
- **Design in Figma**: work in Figma and bring your frame in by pasting it as a PNG (⇧⌘C in Figma, ⌘V on the page), or by choosing or dropping an image.

## Run and host

The site is a single static file, `index.html`. No build step, no backend. Open it in a browser, or put the folder on any static host such as GitHub Pages, Netlify, Vercel or Cloudflare Pages.

```bash
python3 -m http.server 4174
```

Sessions, notes and the log are stored in the browser's `localStorage`.

## Structure

Everything lives in `index.html`:

- `BUILTIN`: the five built-in challenges with reference screens and observations.
- `BLOCK` and `phone()`: the building blocks that draw a reference screen from a short list.
- `mountBoard()`: the drawing area. `mountSource()`: the Figma mode.
