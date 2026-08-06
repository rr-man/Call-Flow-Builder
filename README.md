# PBXware — Call Flow Builder

**Version:** 0.57.0 · 2026-08-04 (version chip in the HTML banner opens the changelog; coeo logo in the banner)

A single-file, self-contained tool for **composing** a PBXware call flow rather
than reading one. The Call Flow Map Creator takes a configuration export and
traces it; this reverses the arrow — you build the flow on a canvas, or import
it from CSV, and the tool writes the workbook the Map Creator reads.

## Files

| File | Purpose |
|---|---|
| `pbxware_call_flow_builder.html` | Primary deliverable. Open in any browser. Works offline, no install, no server. |
| `pbxware_call_flow_builder_flowchart.mermaid` | How a flow is composed, checked and exported. Paste into a Confluence Mermaid macro, or render at mermaid.live. |
| `templates/PBXware_call_flow_template.xlsx` | Consolidated workbook: a sheet per object type, in real export column order, with a Read me and one worked example each. |
| `templates/*.csv` | One template per object type, for loading a single type at a time. |
| `README.md` | This file. |
| `CHANGELOG.md` | Revision history. Identical to the in-app log; both come from one source in the HTML. |
| `PRD_PBXware_Call_Flow_Builder.md` | Product requirements. |

## What it does

**Compose.** Drag DIDs, IVRs, dial groups, queues, ERGs, extensions, mailboxes,
conferences and agents onto a canvas, then route them by dragging a port dot
onto a target. An IVR shows a row per key with the timeout always visible,
because a missing timeout is the most common misconfiguration. IVRs, ring
groups and queues also carry a standing **Closed** port: wiring it creates the
after-hours gate itself.

**Import.** Drop a `.csv` for any object type, or straight onto the canvas.
Destinations that do not exist yet are kept as pending and wire themselves the
moment that object appears. Destinations of the wrong type are refused and
reported — the importer reads the same rule table the canvas enforces, so a file
cannot create a route you could not draw.

**Check.** Findings run on every change: IVRs with no timeout, destinations that
were never built, loops, Operation Times gates with no closed path, duplicate
numbers across types, and routing objects nothing reaches.

**Export.**

| Output | Contents |
|---|---|
| `.json` | The project itself: objects, wiring, positions, notes, panel and view state. |
| `.xlsx` | Eleven sheets in a real PBXware export's column order and cell formats. |
| `.png` | The canvas, per DID or whole flow, with theme, background, context and scale options. |
| Template `.xlsx` | The consolidated template, written by the same code path as the export. |

## Embedding in Confluence (or any page)

The tool works inside an `<iframe>` (Confluence's iframe / HTML macro, a wiki, a
portal). Two things behave differently when framed, both by the browser rather
than by choice:

- **Silent downloads are blocked by the frame's sandbox.** So when framed, every
  download opens a small dialog of routes that survive it, best first: a direct
  save link, open in a new tab, copy the contents (text formats), and **Open the
  full app**, which opens the tool in its own tab **with the current project
  carried over** — via browser storage when available, encoded in the URL when
  not — where nothing blocks the save. **Copy canvas image** also works framed,
  for the diagram itself.
- **Native dialogs are suppressed.** Every confirmation in the app is drawn
  in-page for this reason. If you see a stock browser dialog anywhere, that is a
  bug.

If you control the embed, the cleaner fix is to allow it at the source. On a raw
iframe, add:

    <iframe src="…" sandbox="allow-scripts allow-same-origin allow-downloads allow-popups">

Confluence's own macros set their sandbox themselves; where that cannot be
changed, the in-app routes above are the answer.

## Interface notes

- **Toolbox** — drag a chip to place it exactly, or click to drop one top-left.
- **View menu** — layout guards (snap to grid, warn while dragging, nudge on
  release, push neighbours on grow, report overlaps), see-through destinations,
  and panel position left or right.
- **File menu** — open and save `.json`, export `.xlsx`, save or copy the canvas
  image.
- **Zoom** — 40% to 200%, or Ctrl/Cmd with the wheel about the pointer. **Fit**
  scales and scrolls to whatever the current tab shows.
- **Destinations** — how much a DID or an IVR says about where its routes go:
  nothing, number only, **number and name (default)**, or full detail. A DID
  places it on its routes-to and closed rows; an IVR on its key rows, widening
  from 120px to 150px or 230px as the step needs. Horizontal IVR keys are 34px
  columns, so they take the colour and no text. Full detail adds a summary
  block. This drives every port row on every type — a dial group reads
  `rings Extension 1001 Reception desk`, and a queue's timeout and after-hours
  row name what they reach. On a DID, IVR, dial group, queue or ring group,
  **S** gives the number-only view and **i** full detail for that node alone;
  clicking a lit button follows the menu again.
- **Destination colour** — how a destination's own colour appears on the node:
  none, **tinted (default)**, left stripe, or a swatch. **Colour the wires** is a
  separate toggle, on by default. Note the palette holds six colours for nine
  types — `ivr`, `dg` and `vm` share a green — so colour is a hint and the label
  stays precise. After-hours wires keep their amber either way.
- **Routing view** — a checkbox per routing type (IVR, dial group, queue, ERG,
  voicemail, conference, agent) controlling what the canvas draws. DIDs and
  extensions are always shown: they are the two ends of every route. Hidden
  types are removed rather than faded, nothing moves, and a chip on the canvas
  says how many are hidden. A type the flow has none of is greyed out and reads
  *none* rather than being unticked, so the list shows what the flow contains
  without claiming anything is hidden; a switch turns that off. It changes the
  picture only — the export, the findings and the traced map still see
  everything.
- **Inspector fields** — one field per row with the label beside it (default),
  or two across. At 340px, three across left 78px of text room and truncated
  both a phone model and an email address.
- **SMS marker** — how a DID says it takes SMS: not shown, a pill in the
  subtitle, **its own row (default)**, or an edge stripe with a header badge.
  Only the row costs height. Note SMS travels in the project file and the CSV,
  not the workbook — a real DID routing sheet has no column for it.
- **Auto-fit** — on by default: the flow rescales itself (up to 175%) when the
  window or embed resizes, the panel folds or moves, Expand toggles, or the DID
  tab changes. Zooming by hand switches it off, visibly, in the View menu.
- **Align** — lays every node out by call depth, horizontally or vertically.
  Never changes routing.
- **Canvas tabs** — All, one per DID, and Unrouted. **Focus** dims what the
  chosen DID does not reach; **Filter** hides it. Neither moves a node:
  positions are shared across tabs.
- **Expand** fills the window with the work area.

## Column layouts that are load-bearing

The exported workbook matches a real PBXware export, and two sheets are easy to
get wrong:

- **IVR** — `Name | Number | Greeting name | Option 1…Option # | Timeout |
  Greeting Transcript`. The Map Creator finds the greeting column from the
  header and reads the twelve option columns **immediately after it**. Move the
  greeting and every menu key and the timeout are lost, silently.
- **Queues** — the `Agents` column is a **count**; the members follow as
  `Members Name N` / `Agent` pairs from column E. A single agent still needs the
  pair columns: a lone comma value falls through a legacy path that drops it.

## Open items

- **Operation Times cannot be edited.** The Forms view is hidden, and an OT gate
  is only selectable from its object list — on the canvas it is a badge, not a
  node. The ⏱ button still adds and removes gates, but the schedule and
  after-hours destination cannot currently be set or read. Fix is either to
  unhide Forms, or to make ⏱ open the gate in the Inspector.
- **No `.xlsx` import.** The workbook is write-only; the importer reads `.csv`.
  Reading `.xlsx` in the browser needs a ZIP reader and an inflate step.
- **Caller ID is not modelled**, so that sheet is written with headers only and
  is dropped by a round trip through the builder.
- **Merge with the Map Creator.** The trace and render engine is lifted from
  `pbxware_master_call_flow.html` and is present only so this file runs
  standalone. `SKIN.did` is deliberately teal here where the mapper uses navy;
  if the two are merged, decide which side wins rather than letting one
  overwrite the other.
