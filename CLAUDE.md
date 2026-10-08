# TasteTest

A static, single-file web app that trains design taste: a library of 200 UI challenges, each done in four timed rounds (Design 20 min, Study 10, Redesign 20, Review 10). The designing happens in Figma. The site gives the brief, runs the clock, takes in the frame as an image, searches comparable screens online and shows what the user held on to, got better at and still misses. Built as a portfolio piece for Yannis, so it must stay hostable as a plain static site.

Inspired by a "Design training camp" concept from an Instagram post by a UX designer; this is an original implementation, not a copy of that project's code, name or assets.

## Constraints

- One file: `index.html` holds all HTML, CSS and JS. No build step, no framework, no backend. The only external loads are Google Fonts and, in the Study round, Google's Programmable Search script (`cse.google.com/cse.js`).
- The only other files the site serves are the icons next to it: `favicon.svg` (the source: navy tile, cream circle, pink dot), `favicon.ico` (16, 32 and 48 px) and `apple-touch-icon.png` (180 px, square corners because iOS rounds them). They are linked with relative paths so the site also works from a sub-folder.
- There is no drawing tool on the site, on purpose: design rounds show only the timer, the brief and how to hand in. Do not bring the sketch board back.
- State is in `localStorage` under the key `tastetest.v2` (session, log, pick, sound). Images are Blobs in IndexedDB: database `tastetest`, store `img`, keys `<sessionId>.0` (first version), `<sessionId>.1` (redesign) and `<sessionId>.r.<refId>` (pasted references). Frames of the latest 60 sessions are kept; the log is kept in full. The old `tastetest.v1` data of the sketch-era version is left alone.
- The UI is in English.
- The site hosts no screenshots of real products, and none may be added to the repo (copyright). Study shows Google's image results (thumbnails served by Google, linking to the source); pinned references are saved as URLs in the visitor's own browser. Do not hide Google's branding or paging in the results.
- Feedback is a self-review against a checklist. There is no AI coach; bringing one back would need a backend holding an API key.

## How the code is organised (in order, inside the one `<script>`)

- `SEARCH_CX`: the ID of the Programmable Search Engine (public by design, owned by Yannis's Google account, image search on, limited to design-inspiration sites). Empty means Study falls back to outbound search links.
- `ROUNDS`, `NOTES`, `SKILLS` (eight skills), `TYPES` (mobile, web, dash, comp: name, Figma frame size, aspect ratio).
- `KINDS`: 20 families of screens. A kind has `type`, `name`, three search suggestions `q` and eight `checks`, each `[skill, principle, how to check it in your own frame]`. The checks drive Review and Progress.
- `BRIEFS`: ten `[title, context]` per kind. A challenge id is `<kind>-<position>`, so only ever append to a list. To add a kind, add it to both `KINDS` and `BRIEFS`.
- State, `ORDER` (one fixed shuffle for the daily challenge and the library order), `todays()`, `streak()`.
- Images: `DB` (IndexedDB with an in-memory fallback), `urlOf`, `hydrate()` (views are strings; `img[data-key]` is filled in afterwards), `normalise()` (keeps the frame's own proportions, white under transparency).
- Timer: counts on the wall clock via `session.runAt`, so it keeps going while the user is in Figma and survives a reload. `Chime` schedules the end-of-round sound on the audio clock. The remaining time is mirrored in `document.title`.
- `Search`: loads Google's element with `parsetags: 'explicit'`, renders a `searchresults-only` element with `overlayResults: false`, and draws the image results itself in the `ready` callback so they can be pinned.
- Views: `renderHome` (hero, routine, library via `libParts`, progress via `progHTML`, log), `renderRound` with `ROUND_BODY`, `renderResult`. Then dialog, PNG export, and delegated handlers on `#view` and the dialog.
- Review maths: `stOf()` turns the two ticks of a principle into `held`, `gain`, `lost` or `open`; `tally()` counts them; `trioHTML()` shows them as held on to, got better at and still to work on.

## Design system

- Tokens are CSS custom properties on `:root`. Style through tokens only. There is one theme, built on a four-colour brand palette used roughly 60/25/10/5: `--prussian-blue` #000223 (ground), `--white` #ffffff (type), `--deep-pink` #ff44b4 (accent: actions, focus, overtime), `--banana-cream` #ffee71 (highlights). The semantic tokens (`--paper`, `--ink`, `--accent`, `--mark`, ...) point at these.
- Contrast: text on pink or cream is always navy (`--accent-ink`, `--mark-ink`); white on pink is only 3.1:1 and white on cream 1.2:1.
- Handed-in frames and the search results panel are "paper": they use the `--shot-*` tokens and stay light on purpose, like screenshots.
- Review and Progress use one colour code everywhere: cream means it was there from the first version, pink means the redesign added it. Text next to those marks stays in the text tokens.
- Type: Helvetica (headers, timer; system stack `Helvetica Neue, Helvetica, Arial`, not loaded from Google Fonts), JetBrains Mono (body text and labels, Google Fonts).
- Signature elements: the large stopwatch on round screens, the 60-minute routine drawn to scale on the home page with a cream "In Figma" tag on the two design rounds, and the yellow highlighter mark on principles the user held from the first version.

## Working on it

- Preview: `python3 -m http.server 4174` and open http://localhost:4174.
- After editing, at least syntax-check the script and walk through all four rounds once: paste a PNG in Design and in Redesign, search and pin in Study, tick both versions in Review. Do it for a mobile challenge and for a desktop or component one, and look at Progress with a few sessions in the log.
- Earlier versions had a built-in sketch board with app-drawn reference screens, and before that ran as a Claude artifact with account storage, an AI coach and a Figma connector. All of that was removed.
