---
name: hssb-ops-ui
description: >-
  Applies the Harrisons Sabah internal UI across staff websites: navy ink,
  Harrisons blue, Barlow, 0.4rem controls, working buttons, one filter row,
  and a fast flat layout. Use for HSSB, Harrisons Sabah, sales orders,
  PO shipment, warehouse, upload, history, operations, and other internal tools.
---

# HSSB operations UI

Shared UI for Harrisons Sabah internal websites. Public marketing sites are out of scope. Do not restyle a staff tool as an editorial or marketing page.

Users: sales, warehouse, operations, managers. Priorities, in order: speed, clarity, accuracy, searchability, a calm page, working controls, mobile usability.

## Choose the mode

1. **Ledger.** The job is to pick a branch and read lines. Use the book layout.
2. **Process.** The job is to upload a file, map codes, or review history. Use one column of quiet regions. No branch column and no giant site code.

Both modes share the tokens, type, controls, filter, and release bar below.

## Before editing

1. Read the screen and the stylesheet already in the repo.
2. Reuse an existing component or class before adding one.
3. Change presentation, labels on the screen, and the wiring of controls that are already supposed to act.
4. A visible button, link, or filter must perform its label. Remove a control that does nothing.
5. Leave auth, roles, exports, and calculations as they are. If a working filter or button needs a new query, a new dependency, or a new business rule, stop and ask.

A repo-local rule that forbids logic edits still wins. In that case make the control look right and report that its action could not be wired.

## Page order

Arrange every screen in this order. Leave a region out when the screen has nothing for it.

1. Mast. One title, one sentence of at most 70 characters of measure (70ch).
2. Environment banner, only when the site is not production.
3. One filter row.
4. One result region.
5. Footing, when the result has lines.
6. Release bar.

Region gap is 1.1rem. Put a fifth filter field, notes, and column detail behind a disclosure labelled with what it opens. Lists stay dense. The chrome around them stays quiet: no step numbers, no eyebrow above every block, no card around a table.

## Tokens

Set these on `:root`. Do not add a second action colour.

| Token | Value | Use |
| --- | --- | --- |
| `--ink` | `#10233f` | Text |
| `--paper` | `#ffffff` | Sheet, dialogs, sticky table heads |
| `--desk` | `#f3f7fc` | Page ground |
| `--blue` | `#0a50a3` | The one action and the current selection |
| `--line` | `#d3e2f2` | Idle borders and row rules |
| `--red` | `#c4232b` | Exception only. Never a button fill |
| `--amber` | `#eee6d4` | Environment banner background only |
| `--amber-ink` | `#6b5420` | Environment banner text only |
| `--muted` | `#3d5570` | Labels, secondary text, empty states |
| `--cond` | Barlow Condensed, Arial Narrow, sans-serif | Codes and titles |
| `--text` | Barlow, Segoe UI, sans-serif | Body, tables, forms |

Load Barlow 400/500/600 and Barlow Condensed 500/600, once. Map `--cond` to the condensed face. Root size 15px, line-height 1.4. `color-scheme: light`.

Selected text on a blue fill is white. Secondary text on that fill is `#d6e6f8`. Red is paired with weight or a word.

## Type

- **Ledger site code:** condensed 600, `clamp(4.4rem, 9vw, 6rem)`, line-height 0.78, tracking -0.04em. Below 860px, 3.4rem. Ledger only.
- **Branch name:** condensed 500, `clamp(1.6rem, 3vw, 2.4rem)`, tracking 0.06em, uppercase, once beside the code.
- **Title:** condensed 600, 2rem, tracking -0.03em. Supporting name beside it at 1.05rem / 500.
- **Body:** 15px. Table lines 0.86rem. Banners max 65ch.
- **Column heads:** 0.72rem, 600, tracking 0.04em, uppercase.
- **Field labels:** 0.75rem, muted, not uppercase.
- Amounts and counts use `font-variant-numeric: tabular-nums`.

## Radius

- **0.4rem:** buttons, inputs, selects, thumbs, segmented control, banners, dialogs, drop zone, choice cards.
- **0.75rem:** the sign-in card only. Its buttons stay 0.4rem.
- **0:** table cells, group rows, filter underlines, release-notes link.

## Shared controls

One pattern each. One primary button in a region.

- **Primary button:** `type="submit"` or the existing handler. Blue fill, white text, no border, padding `0.45rem 0.75rem`, radius 0.4rem, min-height 2.6rem. Disabled at opacity 0.55 until the form is valid, and while the action is in flight. The label stays put. Do not swap it for a spinner.
- **Text button:** `type="button"` or a real link. Transparent, blue, underlined, radius 0. Cancel resets the form. A navigation control is an `<a href>`.
- **Current selection:** blue fill, white text, `aria-current="page"`.
- **Segmented control:** white segments, 1px blue border, radius 0.4rem, current segment filled blue. Min height 2.6rem. Clip inner segments square.
- **Short code:** a thumb, min-height 3.1rem, radius 0.4rem. Use for branch codes.
- **Named choice:** a card with a 3px `--line` left edge, radius 0.4rem, padding `0.75rem 0.9rem`. The selected card uses a blue left edge and a white fill. Use for principals and other named options. Do not also use a thumb for the same choice.
- **Field:** 1px `--line` border, radius 0.4rem, padding `0.4rem 0.55rem`, transparent background. Label above.
- **Filter:** one wrapping row under the mast. Each column that can be narrowed gets one control: text, date, or select. Pressing Apply, or changing a select, filters the rows already on screen. Text input waits 300ms after the last key, then filters. Do not request the server on each character. Do not reload the page to hide a row.
- **Table:** full width, collapse, sticky paper heads, `--line` row rules, blue head rule. Numbers right-aligned. The head stays one row. A long list scrolls inside its region. Do not restack rows into cards.
- **Drop zone:** a labelled file input inside a 1px `--line` box, radius 0.4rem, padding `0.9rem`. Choosing a file shows the file name and enables Process. Process submits the existing form.
- **Banner:** 1px line border, radius 0.4rem, padding `0.45rem 0.6rem`. The environment banner uses `--amber` and `--amber-ink` and says which environment it is.
- **Person:** name and role as text beside Sign out. No status dot and no extra badge.
- **Dialog:** paper, 1px line, radius 0.4rem, width `min(32rem, calc(100vw - 2rem))`.
- **Empty:** one muted sentence that names the current filter. Do not invent rows.
- **Loading:** disable the control that started the work. A 2.25rem ring is allowed beside that control. Remove the spin under `prefers-reduced-motion: reduce`.
- **Error:** keep the real message in a banner.
- **Release bar:** fixed to the bottom of the page. Copyright on the left. The version, as a button, on the right. It opens the notes dialog. Underlined blue text, no fill.

Focus: `outline: 2px solid var(--blue); outline-offset: 2px` on `:focus-visible`. Caret is blue. Touch targets are at least 2.6rem.

## Ledger layout

Desktop: `8.75rem` sticky code column and a paper sheet.

- Codes: gap 0.45rem, padding `1.25rem 0.45rem 1rem`. Name, role, and Sign out at the foot.
- Sheet: padding `1.4rem 1.5rem 4.25rem`, gap 1.1rem.
- Mast: code and branch name on one baseline, then the sentence.
- Results: a `15.5rem` group rail and the line list, gap 1rem. Each scrolls inside the sheet.

Below 860px: one column. Codes scroll sideways, min 4.6rem. Mast stacks. Groups scroll sideways, min 9.5rem. The table keeps horizontal scroll.

The giant site code, branch column, group rail, and three-column footing belong to this mode only.

## Process layout

One paper column on the desk, content width `min(72rem, 100%)`, padding `1.4rem 1.5rem 4.25rem`, region gap 1.1rem. No left shadow. Sign-in may show the organisation mark and a small-caps kicker above one paper card of radius 0.75rem. A full-bleed photo is allowed behind that card only.

## Stay fast

- Style with the page stylesheet. Do not add a runtime style engine, a grain overlay, `backdrop-filter`, or `filter: blur`.
- One shadow is allowed, on a dialog only. Working screens stay flat.
- Animate `transform` and `opacity` only, under 200ms. Remove motion under `prefers-reduced-motion: reduce`. Do not animate layout properties and do not listen to scroll to move chrome.
- Load the two font families once. Do not load a second display face.
- Keep off-screen regions unmounted. Do not render every tab's table at once.
- Filter and sort the rows already loaded. Page a list that is longer than one screen through the endpoint the screen already uses.

## Avoid

Gradients, glass, grain, heavy shadows, near-black buttons, extra greens, dashboard widgets, marketing heroes, and a card around every region.

## After a UI change

Report what changed, which files changed, which buttons and filters now run, and that auth, calculations, and dependencies were not changed. For a worked screen, see [examples.md](examples.md).
