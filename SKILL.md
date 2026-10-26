---
name: hssb-ops-ui
description: >-
  Applies Harrisons Sabah (HSSB) internal operations UI: navy ink, Harrisons
  blue, Barlow, 0.4rem controls, a dense ledger, and one pattern per control.
  Use when designing, restyling, reviewing, or building screens for HSSB,
  Harrisons Sabah, sales, warehouse, operations, or other internal staff tools.
---

# HSSB operations UI

Internal tools for Harrisons Sabah staff. The screen is a working ledger: desk ground, paper sheet, navy ink, one blue for action and selection. Public marketing sites are out of scope. Do not restyle these tools as an editorial or marketing page.

Users: sales, warehouse, operations, managers. Priorities, in order: speed, clarity, accuracy, searchability, mobile usability, minimal clicks.

## Before editing

1. Read the screen and the stylesheet already in the repo.
2. Reuse an existing component or class before adding one.
3. Change presentation only: markup, class names, layout, copy on the screen, and styles.
4. Leave queries, auth, roles, filters, exports, and calculations as they are.
5. If the visual change needs new data, a new dependency, or a logic change, stop and ask.

A repo-local rule that forbids logic edits still wins.

## Tokens

Set these on `:root`. Do not introduce a second palette.

| Token | Value | Use |
| --- | --- | --- |
| `--ink` | `#10233f` | Text, rules that must read as ink |
| `--paper` | `#ffffff` | Sheet, cards, sticky table heads |
| `--desk` | `#f3f7fc` | Page ground behind the sheet |
| `--blue` | `#0a50a3` | Primary action, current selection, focus, caret |
| `--line` | `#d3e2f2` | Idle borders and row rules |
| `--red` | `#c4232b` | Exception only (overdue, short). Never a button fill |
| `--muted` | `#3d5570` | Secondary text, labels, empty states |
| `--cond` | Barlow Condensed, Arial Narrow, sans-serif | Codes, titles, branch names |
| `--text` | Barlow, Segoe UI, sans-serif | Body, tables, forms |

Load Barlow 400/500/600 and Barlow Condensed 500/600. Map `--cond` to the condensed face, not the body face. Root size 15px, line-height 1.4. `color-scheme: light`.

Blue is the only chromatic action colour. Red marks an exception and is paired with weight or a word, never colour alone. Selected rows and the current group invert to blue with white text. Secondary text on that fill is `#d6e6f8`.

## Type

- **Site code:** condensed 600, `clamp(4.4rem, 9vw, 6rem)`, line-height 0.78, tracking -0.04em. Below 860px, 3.4rem. Ledger screens only.
- **Branch name:** condensed 500, `clamp(1.6rem, 3vw, 2.4rem)`, tracking 0.06em, uppercase, once beside the code.
- **Chapter title:** condensed 600, 2rem, tracking -0.03em. Supporting name beside it at 1.05rem / 500.
- **Body:** 15px. Order lines 0.86rem. Notes and banners max 65ch. Mast sentence max 70ch.
- **Column heads:** 0.72rem, 600, tracking 0.04em, uppercase.
- **Field labels:** 0.75rem, muted, not uppercase.
- Amounts, counts, and footings use `font-variant-numeric: tabular-nums`.

## Radius

- **0.4rem:** buttons, inputs, selects, branch thumbs, the segmented control, banners, dialogs, and the export action.
- **0.75rem:** the sign-in card only. Its buttons stay 0.4rem.
- **0:** group rows, tables, column-filter underlines, and text links such as release notes.

## Layout

Use the book layout on branch ledgers. Other internal tools keep the tokens, type, radius, and controls, and use the layout the task needs.

Desktop ledger: `8.75rem` sticky fore-edge and a paper sheet.

- Fore-edge: site-code thumbs, gap 0.45rem, padding `1.25rem 0.45rem 1rem`. Sign-out, name, and role sit at the foot.
- Sheet: padding `1.4rem 1.5rem 4.25rem`, region gap 1.1rem, left shadow `-12px 0 28px -18px rgba(20, 20, 20, 0.55)`.
- Mast: code and branch name on one baseline, then a sentence under a line rule.
- Spread: `15.5rem` group rail plus the line list, gap 1rem. Both scroll inside the sheet.

Spacing rhythm: 0.2rem label-to-control, 0.35rem tight, 0.45rem row and thumb gap, 0.85rem under a mast rule, 1rem rail-to-list, 1.1rem between regions, 1.25rem between mast columns.

Below 860px: one column. Thumbs scroll sideways (min 4.6rem). Sheet shadow drops, inset 1rem. Mast stacks. Group rail scrolls sideways (min 9.5rem). Tables keep horizontal scroll. Do not restack columns into cards.

## One pattern each

Match these. Do not add a second button, table, search, filter, dialog, empty, or loading style.

- **Primary button:** blue fill, white text, no border, padding `0.45rem 0.35rem`, radius 0.4rem. Disabled at opacity 0.55.
- **Current selection:** blue fill, white text (`aria-current="page"` on thumbs, groups, and segmented links).
- **Segmented control:** white segments, 1px blue border, radius 0.4rem, current segment filled blue. Min height 2.6rem. Clip the inner segments square so the outer radius stays one shape.
- **Text button:** transparent, blue, underlined, radius 0, for low-priority actions.
- **Field:** 1px `--line` border, radius 0.4rem, padding `0.4rem 0.55rem`, transparent background. Label above in muted 0.75rem.
- **Table:** full width, collapse, sticky paper heads, `--line` row rules, head rule in blue. Numbers right-aligned. Square corners.
- **Group row:** ruled row, square, code in condensed type, name in muted. Current row filled blue.
- **Banner:** 1px line border, radius 0.4rem, padding `0.45rem 0.6rem`.
- **Dialog:** paper, 1px line, radius 0.4rem, width `min(32rem, calc(100vw - 2rem))`, shadow `0 18px 40px -24px rgba(16, 35, 63, 0.55)`, backdrop `rgba(16, 35, 63, 0.45)`.
- **Empty:** muted text that states what the screen is showing. Do not invent rows.
- **Loading:** a fixed quiet veil and a 2.25rem ring, 3px `--line` with a blue top, spinning. Do not change when loading starts. Remove the spin under reduced motion.
- **Error:** keep the real message. Improve layout only. Do not hide or rewrite technical errors into vague copy.
- **Release notes:** a bar fixed to the bottom of the sheet (`left: 8.75rem` on wide screens, `left: 0` below 860px). Copyright on the left. The release-notes control, shown as the version, on the right. Underlined blue text, no fill.

Focus: `outline: 2px solid var(--blue); outline-offset: 2px` on `:focus-visible`. Caret is blue.

## Behaviour

- Keep operational facts visible. Put secondary detail behind disclosure.
- Status keeps its existing meaning and label. Do not add statuses.
- Exceptions (late dates, shortages, failures) are red plus weight or text.
- Motion is limited to a short chapter change. Remove it under `prefers-reduced-motion: reduce`.
- Touch targets stay at least 2.6rem on controls people tap.
- Keyboard access, visible focus, labels, and screen-reader text stay in place. Do not swap a label for an icon alone.

## Keep local to the product

Do not copy these onto a tool that is not a branch ledger: the monumental site code, the fore-edge of branch thumbs, the item-group / sales-group flip, and the three-column order footing.

## Avoid

Gradients, glass, heavy shadows, huge decorative headings, dashboard widgets, marketing heroes, extra card chrome, and random colours. The sign-in cover may use a full-bleed photo behind a single paper card. Working screens stay flat.

## After a UI change

Report what changed, which files changed, and that data, auth, business logic, API behaviour, and dependencies were not changed.
