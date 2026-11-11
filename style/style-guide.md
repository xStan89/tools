# Style guide

Calm, flat UI. No gradients, glows, or shadows. Yellow is an accent only, never a background behind body text.

Two fixed themes. Each page is built in ONE of them: dark by default, light only when asked for. Never add a theme toggle or follow the system's light/dark setting.

## Colors (CSS variables)
Use the same variable names in both themes, so the rest of the guide applies unchanged.

**Dark (default)**
```css
--bg: #1C1B19;            /* page background */
--surface: #262521;       /* cards */
--surface-hover: #2E2A1E; /* card hover */
--line: #363531;          /* 1px borders, dividers */
--text: #FFFFFF;          /* primary text */
--muted: #A4A4A3;         /* secondary text */
--yellow: #FFD241;        /* primary accent */
--accent: #DEB555;        /* hover border */
--accent-text: #DEB555;   /* small meta text and focus ring */
--badge-bg: #3A3421;
--badge-text: #FFEDB4;
```

**Light**
```css
--bg: #FBFAF7;            /* page background, warm off-white */
--surface: #FFFFFF;       /* cards */
--surface-hover: #FFF8E1; /* card hover */
--line: #E6E4DE;          /* 1px borders, dividers */
--text: #020202;          /* primary text */
--muted: #6B6A66;         /* secondary text */
--yellow: #FFD241;        /* primary accent */
--accent: #DEB555;        /* hover border */
--accent-text: #8A6D1F;   /* small meta text and focus ring (#DEB555 is too faint on white) */
--badge-bg: #FFEDB4;
--badge-text: #020202;
```
In light mode, also set `color-scheme: light`; in dark mode, `color-scheme: dark`.

Brand palette: yellow `#FFD241`, dark yellow `#DEB555`, light yellow `#FFEDB4`, black `#020202`, white `#FFFFFF`. Don't use pure black as a page background.

## Type
Rubik for all interface text (Google Fonts, weights 400/500/600). Hierarchy by size and weight, not color.
- Page title: 22px / 600, letter-spacing -0.3px
- Section label: 13px / 600, UPPERCASE, letter-spacing 1.2px
- Item title: 15px / 500
- Item subtitle: 13px / 400, muted
- Badge: 12px / 400, `--badge-text` on `--badge-bg`, pill
- Meta (e.g. domain): 11px / 400, `--accent-text`

### Indicator type
DM Mono (Google Fonts, weights 400/500) is the one exception to Rubik-only. Use it just for live indicators: figures, counts, percentages, sizes, progress and status lines, logs. Never for titles, labels, body text or buttons.
- Status line / progress label / log: 13px / 400, `--text` (idle or secondary: `--muted`)
- Figure (e.g. `42%`): 13px / 500, `--accent-text`
- Count badge: badge style above, set in DM Mono
- Always `font-variant-numeric: tabular-nums`, so numbers don't jitter as they change
- Progress bar: 8px tall, radius 4px, track `--line`, fill `--yellow`

## Spacing & shape
- Spacing steps: 3, 6, 8, 10, 12, 14, 16, 20, 28, 32, 40, 64px.
- Content max-width 1200px, centered, 32px side padding (20px on mobile).
- Radius: 10px cards, 4px small marks, 999px pills.
- Borders: 1px `--line`; accent underline 2px `--yellow`.

## Components
- **Header:** DeSmog icon + page title, 12px gap, vertically centred. Then a 1px line divider.
  - Icon files: `desmog-sq-big.png` and `desmog-sq-small.png`, kept in the same folder as the page. Layer the big one over the small one, so it stays sharp on high-resolution screens and either file still shows if the other is missing.
  - Size: a 36px square box, with the image scaled to fit (`background-size: contain`), centred, not repeated, no radius. The logo is about twice as wide as it is tall.
  - No yellow square: the icon replaces it.
- **Favicon:** every page puts this in its `<head>`, with `favicon-desmog.png` kept in the same folder as the page:
  ```html
  <link rel="icon" type="image/png" href="favicon-desmog.png">
  ```
- **Section header:** uppercase label + count badge, 12px below it a 2px yellow underline, 14px before content.
- **Card:** surface bg, 1px line border, radius 10px, padding 14px 16px, 10px gap between cards. Contains title, optional subtitle, meta line, and a `→` arrow on the right in muted.
- **Empty state:** 1px dashed line border, radius 10px, 16px padding, centered muted 13px text.

## Interaction
- All transitions 0.15s (border-color, background, opacity, transform only).
- Card hover: bg → `--surface-hover`, border → `--accent`, a 3px `--yellow` strip fades in on the left edge, arrow shifts 3px right and turns `--yellow` (dark) or `--text` (light).
- Focus: 2px `--accent-text` outline, 2px offset.

## Layout
- Equal-width grid columns, `repeat(n, minmax(0, 1fr))`, 28px gap. Order is left→right, top→down as written in the data.
- At ≤760px columns stack into one.

## Don't
Gradients, shadows, glows, yellow backgrounds behind text, a typeface other than Rubik and DM Mono (DM Mono for indicators only), color-coding categories.
