# TasteTest

A static, single-file web app that trains design taste: one UI challenge a day in four timed rounds (Design 20 min, Study 10, Compare 10, Redesign 20). Built as a portfolio piece for Yannis, so it must stay hostable as a plain static site.

Inspired by a "Design training camp" concept from an Instagram post by a UX designer; this is an original implementation, not a copy of that project's code, name or assets.

## Constraints

- One file: `index.html` holds all HTML, CSS and JS. No build step, no framework, no backend, no dependencies beyond Google Fonts.
- All state is in `localStorage` under the key `tastetest.v1`; before/after thumbnails per finished session are under `tastetest.v1.shot.<sessionId>` (only the latest 30 are kept).
- The UI is in English.
- Reference screens are drawn by the app from data. Do not add real app screenshots or real brand names (copyright).

## How the code is organised (in order, inside the one `<script>`)

- `ROUNDS`, `NOTES`, `BUILTIN`: round definitions and the five challenges. A challenge has `title`, `context`, `intro`, four `refs` and eight `obs` (observations).
- `BLOCK` + `phone(ref)`: a tiny DSL. A reference screen is a list of blocks like `['row', title, sub, right]` or `['btn', label, kind]`; `phone()` renders them into a phone frame. To add a challenge, add an entry to `BUILTIN` using these blocks.
- Drawing: shapes are vector objects (`k`: `p` pen, `r` rect, `e` ellipse, `l` line, `t` text) on a 360×720 logical canvas. `mountBoard()` owns tools, undo/redo and hit-testing.
- Figma mode: `mountSource()` lets the user paste, drop or pick an image of their Figma frame; `fitImage()` normalises it onto the same 1:2 paper so before/after compare like for like.
- Timer, views (`renderHome`, `renderRound`, `renderResult`), dialog, log storage, PNG export, and one delegated click handler on `#view`.

## Design system

- Tokens are CSS custom properties on `:root`, with a dark set under `prefers-color-scheme: dark`. Style through tokens only.
- The reference screens and the artboard use the `--shot-*` tokens and stay light in both themes on purpose, like screenshots.
- Type: Bricolage Grotesque (display, timer), Instrument Sans (body), DM Mono (labels).
- Signature elements: the large stopwatch on round screens, the 60-minute routine drawn to scale on the home page, and the yellow highlighter mark on observations the user spotted.

## Working on it

- Preview: `python3 -m http.server 4174` and open http://localhost:4174.
- After editing, at least syntax-check the script and walk through all four rounds once, in both sketch and Figma mode.
- Earlier versions ran as a Claude artifact with account storage, an AI coach and a Figma connector. Those were removed to make it a normal site; bringing AI feedback back would need a backend holding an API key.
