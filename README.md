# debug-frontend

Hands-on practice pages for **Browser Developer Tools for Front-End Developers** — a 10-part learning series.

Each part of the series publishes a visual summary on LinkedIn. This repo is where you actually *run* it. Every card on every sheet has a working minimal case and a click-path: inspect this element, untick that declaration, watch what happens.

**▶ Live pages: <https://shrikanth-h.github.io/debug-frontend/>**

---

## ⚠️ Open these over http(s) — not by double-clicking the file

Downloading a lab and opening it from your `Downloads` folder gives the page a `file://` URL, which the browser treats as a unique **`null` origin**. Several exercises then misbehave in ways that look like bugs but aren't:

| Breaks on `file://`                | Why                                                          |
| ---------------------------------- | ------------------------------------------------------------ |
| CORS demo                          | origin is `null`, and you also get unrelated `file:` security noise |
| Reload modes / Network Size column | there is no HTTP caching to observe                          |
| Preserve log navigation            | Chrome blocks it: *"'file:' URLs are treated as unique security origins"* |
| iframe inspection                  | a `file://` iframe is treated as cross-origin                |

**Use the GitHub Pages links above**, or serve the folder yourself:

```bash
git clone https://github.com/shrikanth-h/debug-frontend.git
cd debug-frontend
python -m http.server 8000
# then open http://localhost:8000/
```

Any static server works — `npx serve`, `php -S localhost:8000`, VS Code's Live Server extension.

---

## The labs

| Part | Lab                                                          | Covers                                                       |
| ---- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 1    | [`part1-devtools-essentials-lab.html`](part1-devtools-essentials-lab.html) | Opening DevTools, inspect, core panels, docking, Command Menu, Console drawer, cross-file search, device toolbar, reload modes, Preserve log, Settings & Ignore List, Issues panel |
| 2    | [`part2-html-dom-lab.html`](part2-html-dom-lab.html)         | DOM vs source, tree navigation, live editing, node reordering, attributes vs properties, `$0`, find by text/CSS/XPath, the Copy submenu, event listeners, DOM breakpoints, shadow DOM & frames, accessibility tree |
| 3    | [`part3-devtools-css-lab.html`](part3-devtools-css-lab.html) | Styles pane, cascade & specificity, inheritance, Computed, box model, Flexbox & Grid inspectors, force element state, CSS variables, media queries, Animations panel, CSS Overview — plus `@layer`, stacking contexts and container queries |
| 4–10 | *coming*                                                     | Console logging · JS breakpoints · Network & API · Storage/sessions/auth · React DevTools · Performance & memory · Tracking, security & a11y |

Each lab is a **single self-contained HTML file**. No build step, no dependencies, nothing to install.

---

## How to work through one

1. Open the lab over http(s).
2. Open DevTools (<kbd>F12</kbd>) and dock it to the side — several sections have panes that get clipped on a short bottom dock.
3. Read the **orientation map** at the top. It shows where the controls used below actually live.
4. Work down the page. Each section has:
   - a **demo** — the thing to inspect
   - **Try this** — a numbered click-path
   - an **Exact path** box — the full menu route, for when a control isn't where you expect
   - an **Answer** — why it matters beyond the mechanics

Where a control is easy to miss, the lab says so explicitly. Two that catch nearly everyone:

- Elements sidebar tabs (**Event Listeners**, **DOM Breakpoints**, **Properties**, **Accessibility**) hide behind a **`»` overflow chevron** on a narrow dock.
- The **Ignore List** pane was called *Blackboxing* until Chrome 106, which is why older articles send you somewhere that no longer exists.

---

## Why practice pages instead of a real website

Production sites make poor teaching material, and there's a concrete example behind this repo.

Chrome's docs say the Styles pane groups rules by cascade layer and offers a layers view. Going looking for that control on a major e-commerce site turns up nothing — because **that site doesn't use `@layer`, so DevTools has nothing to show**. The control is conditional, and so are the grid badge, the flex badge, the container-query block, and most of the rest.

A missing control is usually a statement about the page, not about your browser. These labs guarantee the feature is present, so when something doesn't appear you know it's worth investigating rather than shrugging at.

---

## How these are built

Every interactive claim is verified in a real headless Chromium before publishing — computed styles, paint order via `elementFromPoint`, event registration via the same `DOMDebugger.getEventListeners` API the Event Listeners pane uses.

That check has caught real errors, including a stacking-context demo where three separate properties each created a context, so unticking any one of them changed nothing and the lesson silently failed.

Panel names and menu paths are checked against current Chrome documentation rather than recalled. Known-stale labels that still circulate widely: *Blackboxing* → **Ignore List**, *Fast 3G* → **Fast 4G / Slow 4G / 3G**, and `:visited` is **not** in the Force element state list.

---

## Feedback

Corrections are genuinely welcome — several already landed. If a step doesn't match what your Chrome shows, open an issue with:

- the part and section number
- your Chrome version (`chrome://version`)
- what you saw instead

Chrome's DevTools UI shifts between releases, so drift is expected.

---

## Credits

The `@layer`, stacking-context and container-query sections in Part 3 exist because **[Riad Kilani](https://www.linkedin.com/in/riad-kilani/)** pointed out they were missing from the original post.

---

## Licence

MIT — use these however you like, including in training material. Attribution appreciated but not required.
