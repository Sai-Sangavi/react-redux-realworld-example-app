# UI guidelines

These rules are generated from this system's design choices (direction **edit**,
palette **Rose quartz**); they hold for every screen. Tokens are referred to by name; their values
live in `tokens.css`.

## Colour

- Every colour is a semantic token: surfaces (`--color-bg`, `--color-surface`,
  `--color-surface-subtle`), text (`--color-fg`, `--color-fg-muted`, `--color-fg-faint`), the brand
  (`--color-primary`, with `--color-on-primary` on it), borders and the status roles. A literal
  colour in a screen breaks dark mode, which swaps only the tokens.
- Status is a role, never a hue: success, warning, danger and info each come as a strong colour, a
  text colour and a soft fill (`--color-danger`, `--color-danger-text`, `--color-danger-soft`).
  Status text goes on its own soft fill, the pairing that is contrast-checked.
- Light and dark are both supported: `tokens.css` follows the system setting and
  `[data-theme="light"]` / `[data-theme="dark"]` pin one. Test a screen in both.
- Charts use `--color-viz-1` to `--color-viz-6` in order, with `--color-on-viz-n` for a label on a
  series; a sixth series is the limit, beyond it group the rest as "Other".

## Typography

- Headings use Fraunces, body copy Inter, code and ids Fira Code (`--font-family-heading`,
  `--font-family-body`, `--font-family-mono`). The fonts are vendored under `fonts/`; until the
  files are added the declared fallback stack renders.
- Sizes come from the eight-step scale `--font-size-xs` to `--font-size-4xl`: page titles
  `--font-size-3xl`, section headings `--font-size-2xl` or `--font-size-xl`, body `--font-size-md`,
  captions `--font-size-sm`. Skip no more than one step between a title and the text under it.
- Weights are `--font-weight-regular` for text, `--font-weight-medium` for labels and
  `--font-weight-heading` for headings; line height is `--line-height-normal` for text and
  `--line-height-tight` for headings.

## Icons

The icon set is **Duotone** (Phosphor-style, soft filled shapes), drawn at 20px with a 1.75px stroke: sizes come from `--icon-size-sm`, `--icon-size-md` and `--icon-size-lg`, never a literal.

- Draw an icon with `<svg class="icon"><use href="#i-name"/></svg>` from the sprite in `icons.svg`; it takes the colour of the text around it, so an icon is never given a colour of its own.
- The starter glyphs are `home`, `kanban`, `check`, `cal`, `user`, `users`, `bell`, `search`, `sliders`, `plus`, `filter`, `flag`, `clock`, `tag`, `msg`, `trash`. A screen that needs another asks for a design-system change; it does not draw one-off icons or use emoji.
- An icon-only control (`.btn-icon`) carries an `aria-label` and a tooltip, and only a conventional glyph (search, plus, close, settings) stands without a visible label.
- A decorative icon next to text is `aria-hidden`; a status is never shown by an icon alone, it is paired with text or a `.badge`.
- Licence: Glyph geometry authored for bnts-arc. Style follows Phosphor (MIT); no Phosphor paths are copied.

## Layout kit

- The shell is **sidebar app shell** (left navigation, header, content); `app-shell.html` is the
  frame and a screen designs only the content inside it. A screen never restyles the shell.
- A screen picks one page template from `layout-templates.html` (this system's default is
  **empty states**: first-use and no-results pages with one clear action), chooses its columns and states, and stays inside
  it. A needed new template is a design-system change, reviewed once.
- Widths and rhythm come from tokens: `.container` follows `--container-sm` to `--container-xl`,
  the page edge is `--page-gutter`, vertical sections sit `--section-gap` apart and related items
  `--density-gap`. Content never grows past `--container-xl`.
- Spacing uses `--space-1` to `--space-10` only. Breakpoints are `--breakpoint-sm` to
  `--breakpoint-xl` (documented values: a media query cannot read a custom property); the shell
  collapses its navigation below 820px behind a menu button.
- Compose pages from the page kit (`.page`, `.page-header`, `.toolbar`, `.page-body`) and the
  layout helpers (`.stack`, `.cluster`, `.grid`, `.split`); do not write a screen's own flex or
  grid rules where one of these does the job.

## Density

- The density is **spacious** (44 px controls, 56 px rows): controls take `--control-height-md`, table and list rows take `--density-row-height`, cards and panels pad with `--density-padding` and sit `--density-gap` apart. Pick sizes (`.btn-sm`, `.btn-lg`) for hierarchy, never to fix a layout, so the density stays one decision.

## Motion

- Motion is **subtle**: transitions use `--motion-duration-fast`, `--motion-duration-base` or `--motion-duration-slow` with `--motion-easing-standard`, and only on colour, shadow and position. Every animation is switched off under `prefers-reduced-motion`, so none carries information on its own.

## Accessibility

- Text and its background meet WCAG AA in both modes (4.5:1 for text, 3:1 for graphics and the
  focus ring): the pairs above are checked when the system is generated, so use a token pair as
  named and do not tint text or surfaces by hand.
- Focus is always visible: `:focus-visible` draws a ring of `--focus-ring-width` in
  `--color-primary`; do not remove it. A touch target is at least `--control-height-md` tall
  except in dense tables, where the whole row is the target.
- Information never rests on colour alone: a status pairs its colour with text or an icon, and an
  error message sits next to the field that caused it (`.field-error`).

## Content voice

- Considered, editorial copy: full sentences, sentence-case headings, no jargon.
- Sentence case for headings, buttons and labels. A button says the action ("Save changes",
  "Create board"), never "OK" or "Submit"; a destructive one names what goes ("Delete 3 items").
- An empty state says what belongs here and offers the one action that fills it; an error says
  what went wrong in the person's terms and what to try, and never blames them.

<!-- arc:additions (everything below this line is kept on regeneration) -->

## Product navigation and sections

The product is a board-based task tracker. The main navigation in `app-shell.html` has four sections, in this order, and a screen uses these labels and nothing else:

- **Overview** (`home`): the landing summary of work across boards; it comes first because it is where a session starts.
- **Boards** (`kanban`): the list of boards and each board's columns and cards; it is the core of the product, so it is the default `aria-current="page"` section.
- **My tasks** (`check`): every task assigned to the signed-in person across boards, so personal work is one click away.
- **Settings** (`sliders`): account, workspace and notification preferences; it is last because it is visited least.
- The header holds only Search (`search`), Alerts (`bell`) and the avatar; these are global actions, so they never move into the sidebar and no screen adds a fifth section or header icon without a design-system change.
- A page inside a section (one board, one task) is reached from that section's page, not from the sidebar, and its `.page-header` title names it while the sidebar keeps the parent section marked current, so the person never loses their place.
- Task attributes reuse the starter glyphs with fixed meanings: `user` assignee, `clock` due date, `flag` priority, `tag` label, `msg` comments; a glyph keeps one meaning so it reads at a glance.

## Imagery and illustration

- The product is text-and-data led: a screen needs no photography, and none is used as decoration, because photos compete with card content on a board.
- Illustration appears only in empty states (the default template), one per page, drawn flat in `--color-primary-soft` and `--color-primary` with `--color-border` outlines, so it stays on palette and works in dark mode.
- An empty-state illustration is about 160px wide, centred above the heading, with an empty `alt` because the heading and action carry the meaning.
- Avatars are circles (`--radius-full`) at `--control-height-sm` in lists and cards and `--control-height-md` in headers; they show a photo when one exists and otherwise two-letter initials on `--color-primary-soft` in `--color-primary-text`, so a missing photo never leaves a gap.
- A stack of avatars on a card shows at most three, then a "+N" count, because more overflows the card.
- Any photo (avatar, workspace logo, a card cover if a board offers one) is cropped with `object-fit: cover` to a fixed ratio: 1:1 for people and logos, 16:9 for card covers, so grids stay aligned.
- Image placeholders are a `--color-surface-subtle` block at the final ratio with a `--border-width` `--color-border` edge, so layout does not jump when the image loads.
- Every meaningful image has descriptive `alt` text; a decorative one has `alt=""`.

## Brand wording and content voice

- The product name is written as "Product" in the shell until it is named; use the name exactly as it appears in `app-shell.html`, never abbreviated, so the brand stays consistent.
- Use the product's own nouns: **board**, **column**, **card** for a task on a board, **task** when it is in a person's list. Do not mix in "project", "ticket" or "item", because one word per concept keeps the interface learnable.
- Address the person as "you" and the team as "your team"; avoid "we" except in help and error text where the product speaks, so the voice stays calm and not chatty.
- Empty states follow a fixed shape: a sentence-case heading saying what belongs here ("No boards yet"), one line of explanation, and one primary button naming the action ("Create board"); the line explains the benefit, because first-use pages should invite rather than instruct.
- Dates read as "Today", "Tomorrow" or "12 Mar"; a past due date adds "overdue" in `--color-danger-text` on `--color-danger-soft`, so urgency is stated in words and not colour alone.
- Counts use numerals and a unit ("3 tasks", "1 task"); never "(s)", because correct plurals read as careful.
- Confirmations are short and in the past tense ("Board created"); toasts do not exclaim, since the editorial tone favours restraint over celebration.
