# Design system — Sports MiniBoards

The style layer for `sports-miniboards.com`. Craft decisions (hierarchy, interaction, accessibility, motion) come from the `design-better` skill; every *visual* value comes from this file.

Tokens live in `css/style.css` under `:root`. Change a value there, not in a rule.

## Colour

| Token | Value | Role | Contrast |
|---|---|---|---|
| `--bg` | `#0a1f2c` | Page background | — |
| `--bg-card` | `#16344a` | Raised region: cards, strips | 1.30:1 on `--bg` |
| `--bg-elev` | `#1a3a52` | Control surface, chips | 1.42:1 on `--bg` |
| `--text` | `#e8eef3` | Body copy | **14.4:1** on `--bg` |
| `--muted` | `#94a8b8` | Secondary copy, nav | **6.9:1** on `--bg` |
| `--gold` | `#f0b323` | Accent, primary action, active nav | **9.0:1** on `--bg` |
| `--accent` | `#4ea3ff` | Links | **6.4:1** on `--bg` |
| `--rule` | `#2a4d67` | Hairline divider | decorative |
| `--rule-strong` | `#4a7796` | Component boundary (card edges) | **3.5:1** on `--bg` |
| `--on-gold` | `#11293a` | Text on a gold fill | **8.0:1** |

Rules:
- Body text never drops below 4.5:1. UI component boundaries never drop below 3:1.
- Colour is never the only signal — every coloured state also carries a label.
- Gold is reserved for the primary action, active nav state, and section headings. If everything is gold, nothing is.

## Spacing

`--space-1` 4px · `--space-2` 8px · `--space-3` 12px · `--space-4` 16px · `--space-5` 24px · `--space-6` 32px · `--space-7` 48px · `--space-8` 72px

Every margin, padding, and gap is one of these. Nothing is off-scale. Related items sit one step apart; unrelated groups sit two or more steps apart (Law of Proximity).

## Type

`--text-xs` 0.78 · `--text-sm` 0.875 · `--text-base` 1 · `--text-md` 1.1 · `--text-lg` 1.3 · `--text-xl` 1.6 · `--text-2xl` 1.9 (rem)

One scale, no exceptions. Body is `--text-base` at 1.55 line-height. Headlines use `text-wrap: balance`; prose uses `text-wrap: pretty`. Prose is capped at `--prose` (65ch) so no line runs long. Numeric columns use `font-variant-numeric: tabular-nums`.

## Radii

`--radius-sm` 4px · `--radius-md` 8px · `--radius-lg` 12px

## Focus

`--focus-ring` 2px solid `--gold`, `--focus-offset` 3px.

Never set `outline: none` without a `:focus-visible` replacement of at least this size. The ring is gold so it reads against both the page and the card surfaces.

## Motion

`--dur-micro` 120ms (hover, toggle) · `--dur-standard` 220ms (menu, card lift) · `--ease-out` `cubic-bezier(0, 0, 0.2, 1)`

Motion eases out on entry. Transition `transform` and `opacity`; colour transitions are permitted because they never trigger layout. `prefers-reduced-motion: reduce` drops every transition and every transform while keeping the feedback signal.

## Components

| Component | Rules |
|---|---|
| `.btn` | Primary action. Gold fill, `--on-gold` text, 44px minimum height. One per view. |
| `.btn--quiet` | Secondary action. Transparent fill, gold text, `--rule-strong` border. |
| `.card` | Raised region. `--bg-card` fill, `--rule-strong` border, `--radius-md`. 16:9 media block on top. |
| `.facts` | Key/value spec list. Gold key column at a fixed 170px so values align. |
| `.feature` | Image + copy row. Alternate `.reverse` so the page doesn't read as a stack of identical rows. |
| `.feature-sm` | Same, with the media capped at 330px for secondary features. |
| `.feature-mini` | Compact strip for secondary points. Bordered card, small image left. |
| `.strip` | Full-width callout band, gold left rule. |
| `.skip-link` | Off-screen until focused, then gold and visible. |

## Do

- One primary action per view, visually dominant.
- Keep the measure at 50–75 characters.
- Reach for the tokens instead of literals.
- Give every interactive element a visible focus ring and a 24×24px minimum target (44×44 on touch).
- Keep the header nav inside five items.
- Mark the current page in the nav.

## Don't

- Don't introduce a hex value, a font size, or a pixel value that isn't a token.
- Don't animate width, height, top, or left.
- Don't remove a focus ring without a replacement.
- Don't use gold for anything other than the three roles above.
- Don't ship a page with no primary action.
