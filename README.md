# Guardian deck template

Skeleton for HTML slide decks in the Guardian editorial style. Use as a starting point: spin a new repo from this template, edit `index.html`, drop images in `images/`, push to `main`, and GitHub Pages serves the result.

## Starting a new deck

In Claude Code, in an empty folder, say:

> "Set up a new deck from my template, call it `xyz`."

Claude will clone the template into the folder via `gh repo create --template`, push the first commit, and hand back the live URL once Pages has built. No terminal needed.

## What's in here

- `index.html` — six reference slides (cover, section opener, content, three-card row, image-only, quote). Replace the placeholder copy. Copy and adapt the slide patterns for new slides.
- `styles.css` — Guardian fonts (loaded from `assets.guim.co.uk`), design tokens (`--paper`, `--ink`, `--guardian-blue`, `--news-red`, `--guardian-yellow`, `--eco-green`), and base components.
- `deck-stage.js` — the `<deck-stage>` web component. Handles keyboard navigation (←/→, PageUp/PageDown, Space, Home/End, R, number keys), auto-scaling to viewport, tap zones on mobile, idle-fading overlay, and print rules that lay one slide per page at 1920×1080 for Cmd-P → Save as PDF.
- `.github/workflows/pages.yml` — GitHub Actions workflow that deploys to Pages on every push to `main`. Has concurrency control so a newer push cancels an in-flight build rather than queuing behind it.
- `images/` — drop PNGs and JPGs here. Reference them as `images/filename.png`.

## Working in the deck

Open `index.html` in a browser to preview. Arrow keys / space to navigate, R to reset, Cmd-P → Save as PDF for one-slide-per-page export at 1920×1080.

When you want a more elaborate component than the six examples — animated chart, two-column callout, worksheet sheet, chevron flow, table — the [awayday repo](https://github.com/peter-guillam123/awayday) has working implementations of all of those. Lift the pattern from there.

## Notes

- **Fonts** load from `assets.guim.co.uk`. The deck only renders correctly online. The CSS falls back to Georgia / Helvetica system fonts if the CDN is unreachable, but the visual is noticeably different. If you're presenting somewhere with patchy wifi, self-hosting the four `.woff2` files is a 10-minute job.
- **Slide page numbers** are auto-filled by the inline JS at the bottom of `index.html`. Don't manually write `"03 / 12"` — write `"03 / NN"` or any placeholder; the JS rewrites it on load with the actual position and total.
- **Animations replay** on every slide arrival, including when you navigate backwards, via the `slidechange` event listener. When you add new animated elements, append their selector to the `querySelectorAll(...)` list in the inline `<script>`.
- **The `.slide-title em`** rule gives the italic word in any paper-slide title the editorial red colour. The same pattern in `.section-opener h1 em` gives section openers their yellow italic. One italic word per title is the deck convention.
