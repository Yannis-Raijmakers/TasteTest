# TasteTest

A training ground for your eye for interface design. Pick one of 200 challenges and work through four timed rounds, one hour in total. You design in Figma; this site gives you the brief, runs the clock and keeps your two versions next to each other.

1. **Design** (20 min, in Figma): a brief and an empty frame. No references, no AI. Hand in the frame when the clock stops.
2. **Study** (10 min, on the site): search for screens that solve the same problem, pin the strong ones and write down 3 patterns, 3 do's and 3 don'ts.
3. **Redesign** (20 min, in Figma): the same brief again, with what you just saw. Hand in the new frame.
4. **Review** (10 min, on the site): check both versions against eight principles. The site shows what you held on to, where you got better and what still needs work.

The idea: AI can generate a hundred screens in a minute, but someone still has to judge which one is good. That judgement is trained by designing, looking closely, and designing again.

## Challenges

200 briefs in 20 kinds of screens, across four types:

- **Mobile app**: checkout, onboarding, sign in, empty and error states, detail screens, home screens, search and lists, settings.
- **Website**: landing hero, pricing, shop and listing pages, web forms.
- **Web app**: data tables, dashboards, calendars and booking, inbox and detail.
- **Component**: cards, navigation, dialogs, form controls.

The start page offers one challenge a day (the same for everyone) and a library you can filter and search.

## Handing in a frame

The site has no drawing tool. In the design rounds it only shows the timer, the brief and how to hand in:

- In Figma, select your frame and copy it as PNG: ⇧⌘C (Ctrl+Shift+C on Windows).
- Go back to the TasteTest tab and paste: ⌘V.
- Or export the frame as PNG and drop or choose the file.

The clock runs on real time, so it keeps counting while you are in Figma. The remaining time shows in the tab title and a short sound plays when a round ends.

## Reference search

In Study the site searches design-inspiration sites and shows the image results in the page, so you can pin them. This runs on a free [Google Programmable Search Engine](https://programmablesearchengine.google.com/), which works on a static site.

To use your own engine:

1. Create a search engine and list the sites to search (up to 50), for example `dribbble.com`, `behance.net`, `mobbin.com`, `pinterest.com`, `figma.com`, `land-book.com`, `lapa.ninja`, `godly.website`, `pageflows.com`, `refero.design`, `collectui.com`.
2. Turn on **Image search**.
3. Copy the **Search engine ID** into `SEARCH_CX` at the top of the script in `index.html`. The ID is public by design.

If the ID is empty or Google's script is blocked, Study falls back to links that open the same search on Dribbble, Behance, Pinterest and Google Images. Screens you copy there can be pasted into the page as references.

The site does not host screenshots. Results are thumbnails served by Google that link to their source; pinned references are saved as links in your own browser.

## Progress

Every review ticks eight principles for the first version and for the redesign. Each principle belongs to a skill: hierarchy, layout, typography, colour, copy, states, interaction or accessibility. From that the start page shows:

- **You hold on to**: skills that were already there in your first versions.
- **You got better at**: skills your first versions improved on over time, or that your redesigns added.
- **Still to work on**: skills that are still missing after the redesign.

Plus a chart per session and a bar per skill. It is a self-review: there is no AI judging your work.

## Run and host

The site is a single static file, `index.html`, plus its icons (`favicon.svg`, `favicon.ico`, `apple-touch-icon.png`). No build step, no backend. Open it in a browser, or put the folder on any static host such as GitHub Pages, Netlify, Vercel or Cloudflare Pages.

```bash
python3 -m http.server 4174
```

Sessions, notes and the log are stored in the browser's `localStorage`; handed-in frames and pasted references in IndexedDB. Nothing is uploaded.

Because the data lives in one browser, the Log section has **Export my data** and **Import data**. Export saves all finished sessions with their frames as one JSON file; import adds such a file to what is already there, so you can move to another browser or keep a backup.

## Structure

Everything lives in `index.html`:

- `KINDS`: the 20 kinds of screens, each with search suggestions and eight review principles.
- `BRIEFS`: ten briefs per kind.
- `Search`: the in-page reference search.
- `renderHome`, `renderRound`, `renderResult`: the views. `progHTML` computes the progress overview from the log.
