# Building a deck from this template

This repo is the second-edition Guardian deck kit. Three files are load-
bearing and shared across every deck built from it; one file is yours.

- `deck-stage.js` — the `<deck-stage>` web component. **Never edit.**
- `styles.css` — the entire design system: fonts, tokens, materiality,
  chrome, every slide component, all motion keyframes. Extend it only by
  adding new components at the bottom; don't fork per-slide styles into
  the HTML.
- `motion.js` — the choreography engine. **Rarely needs editing.** It
  numbers folios, fills the progress seam, splits `[data-split]` titles
  into masked words, replays `[data-fx]` reveals on every slide visit,
  runs `[data-count]` count-ups, types `.typed` prompts and draws the
  `.ax-line` chart. It choreographs the already-active slide at startup
  (the stage's first `slidechange` fires before this script runs — don't
  "fix" that).
- `index.html` — the deck. **Markup only.** It currently holds one slide
  per pattern with instructive placeholder copy; replace the words, keep
  the grammar, delete what you don't use.

## Non-negotiables

1. **The user's words are sacrosanct.** Copy goes in verbatim. If a line
   reads badly, propose the change and wait — never silently edit. When
   reworking the presentation of an existing deck, prove word-parity with
   a token diff of the visible text, old vs new.
2. **Images dissolve; they are never wiped.** `data-fx="photo"` only.
3. **Vary the slide shapes.** Never run the same boxed-card layout more
   than twice in a row — mix ledgers, diptychs, triptychs, open text
   blocks, conversation rails.
4. **One italic `<em>` word per title** — red on paper slides, yellow on
   ink. It's the deck's punctuation; two is noise.
5. **Verify before declaring done.** Serve locally, step through every
   slide at 1920×1080, screenshot, check for overflow and console errors.
   Cmd-P → Save as PDF must also produce complete slides (print CSS
   forces final animation states — keep new animated elements covered by
   the `@media print` block if you add any).

## The motion grammar

Elements opt in with `data-fx` and an inline `--d` delay:

| attribute | effect |
| --- | --- |
| `data-fx="rise"` | fade up 22px — the workhorse |
| `data-fx="fade"` | plain fade |
| `data-fx="photo"` | photographic dissolve; child `img` settles from 1.04× |
| `data-fx="pop"` | spring scale-in (timeline nodes) |
| `data-fx="spring-up"` | spring rise (speech bubbles, chat) |
| `data-fx="bar"` / `"bar-v"` | rule draws across / down |
| `data-fx="ghost"` | the openers' ghost numeral drift |

Titles take `data-split` (+ optional `data-split-base`, `data-split-step`)
for the masked word-by-word reveal. Figures take `data-count`,
`data-count-suffix`, `data-count-delay`, `data-count-dur`. Typed prompts
are a `.typed` span inside `.prompt-text` with optional `data-typo`
(typed wrong first) and `data-fix` (the correction, which must appear in
the text), plus `data-type-delay`.

Stagger delays by hand, roughly 100–130ms apart, kicker at ~60ms, body
content from ~200ms. Choreography replays automatically on every visit.

Accessibility is free if you stay in the grammar: no JavaScript means
nothing hides, `prefers-reduced-motion` gets a static deck.

## Conventions

- Footers: write `<span class="num">01 / NN</span>`; motion.js renumbers.
- Section openers' ghost numerals (`.chapter-ghost`) match agenda numbers.
- Images go in `images/`; reference as `images/name.jpg`. Replace the
  inline SVG placeholders.
- The deck deploys to GitHub Pages on push to `main`.
- Keep a reverse-chronological changelog in `README.md`, written in the
  deck owner's voice — what was built and why, updated with the work.
