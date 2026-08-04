# PRD: PBXware Call Flow Builder — Product Requirements Document

**Version:** 1.0 · 2026-08-04
**Status:** Living document
**Reflects application build:** v0.42.0

---

## 1. Overview

The PBXware Call Flow Builder is a single-file, fully offline web application for **composing** a PBXware call flow. It is the companion to the Call Flow Map Creator and the inverse of it: where the Map Creator reads a configuration export and traces what exists, the Builder lets a technician lay out what *should* exist and then writes the workbook the Map Creator reads.

A technician drags objects onto a canvas — DIDs, IVRs, dial groups, queues, extension ring groups, extensions, voicemail boxes, conference bridges and queue agents — and routes them by dragging a port dot onto a target. Alternatively they import each object type from `.csv`, or open a project saved earlier. Validation runs continuously. When the flow is right, the tool exports it as an `.xlsx` workbook in a real PBXware export's sheet and column layout, as a `.png` of the canvas, or as a `.json` project to resume later.

Everything runs in the browser. Nothing is uploaded, so it is safe on customer data, and it can be deployed as a static page, embedded in Confluence, or opened from a local file.

---

## 2. Goals

1. **Let a flow be designed before it is built.** Give technicians a way to lay out routing for a new customer, or a change to an existing one, and see the shape of it before touching a live PBX.
2. **Make the design reviewable.** Produce a diagram and a workbook that a colleague, a customer or a provisioning engineer can read and check, rather than a description in a ticket.
3. **Catch the routine mistakes at design time.** Missing IVR timeouts, destinations that were never created, loops, duplicate numbers and unreachable objects should be caught while it is still a drawing.
4. **Feed the Map Creator without hand-editing spreadsheets.** The exported workbook must load into the Call Flow Map Creator without adjustment, so a designed flow and a traced flow are the same artifact in two states.

---

## 3. Background and problem

Designing PBXware routing today happens in prose and spreadsheets. A change is described in a ticket, transcribed into a workbook by hand, and only becomes a diagram after it has been built — by exporting the config and running it through the Map Creator. The consequences are ordinary but expensive: a menu key pointing at a number that was never created, an IVR with no timeout so silent callers are dropped, two objects sharing a number, an after-hours path that goes nowhere.

Those are all structural errors, visible in the design if the design is a structure rather than a paragraph. The Builder makes the design a structure.

---

## 4. Target users

- **Provisioning and implementation engineers** laying out a new customer's routing, or a change to an existing one.
- **Support technicians** sketching what a flow should look like before changing it, or reproducing a customer's description to check they have understood it.
- **Senior technicians and team leads** reviewing a proposed flow before it is built.
- **Customers**, indirectly, as the audience for the exported diagram.

---

## 5. Current capabilities (delivered in v0.42.0)

**Composition**

- Nine object types: DID, IVR, dial group, queue, extension ring group, extension, voicemail, conference, agent. Operation Times gates attach to any non-endpoint object.
- Drag from the toolbox to place exactly, or click to drop top-left. Nothing is ever placed on top of something else.
- Routing by dragging a port dot onto a target node, or clicking the dot to arm it and clicking the target. Valid targets stay lit; everything else dims.
- IVR nodes show one row per key with the timeout row always visible, collapsible to routed keys only, and switchable between vertical (ports right) and horizontal (ports below) orientation.
- Legal destinations are enforced from a single rule table: an agent is reachable only from a queue's agent list, a dial group's members must be extensions, and so on.

**Import**

- `.csv` per object type, dropped on a section of the Upload panel or straight onto the canvas. Type is detected from the headers.
- Destinations that do not yet exist are kept as pending and wire themselves when that object appears.
- Destinations of the wrong type are refused and reported. The importer uses the same rule table the canvas enforces, so a file cannot create a route that could not be drawn.
- Full row-by-row import report: added, pending, skipped duplicates, number clashes, refused routes, rejected rows, with the original text viewable.

**Validation**

- Findings recompute on every change: IVRs with no timeout, unresolved destinations, loops, OT gates with no closed path, duplicate numbers across types, objects with no number, routing objects nothing reaches, endpoints off every published route, and optionally overlapping nodes.
- A status chip in the toolbox summarises; the strip lists each finding with the objects named.

**Layout**

- Align by call depth, horizontally or vertically. Never changes routing.
- Layout guards: snap to a 22px grid, warn while dragging over an occupied area, nudge a colliding node to the nearest free gap, push neighbours aside when a node grows, and report any overlap that remains.
- Zoom 40–200%, Ctrl/Cmd + wheel about the pointer, and a Fit that scales and scrolls to the current view.
- Canvas tabs per DID with Focus (dim what this DID does not reach) and Filter (hide it). Positions are shared, so switching tabs never moves anything.

**Output**

- `.json` project: objects, wiring, positions, notes, panel and view state, theme.
- `.xlsx` workbook: eleven sheets in a real export's order, column layout and cell formats.
- `.png` of the canvas: scope (whole flow, one DID, or unrouted), context (only that DID, or whole flow dimmed), theme, background and 1–3× scale. Multiple scopes produce a `.zip`.
- Consolidated `.xlsx` template with a Read me and one worked example per sheet, written by the same code path as the export so the two cannot diverge.

**Interface**

- Light and dark themes, light by default because it matches the exported map.
- Panel left or right, collapsible to a rail, with Upload, Inspector and Notes tabs.
- Every confirmation drawn in-page, because Chrome suppresses native dialogs in a cross-origin iframe.
- New, Sample flow and Open all offer Cancel / Discard / **Save first**.

---

## 6. Functional requirements

1. Compose all nine object types and the OT gate, with routing enforced against a single legality table shared by the canvas and the importers.
2. Import each object type from `.csv` with type detection, pending destinations, refused illegal routes and a per-row report.
3. Validate continuously and report findings naming the objects involved.
4. Export `.xlsx` in the exact sheet and column layout the current Call Flow Map Creator reads.
5. Export the canvas as `.png` at selectable scope, context, theme, background and scale.
6. Save and reopen the whole project as `.json` with layout and view state intact.
7. Provide a consolidated `.xlsx` template and per-type `.csv` templates, generated by the application.
8. Operate with no network access and no server, from a single HTML file.

---

## 7. Non-functional requirements

1. **One file, no dependencies.** No CDN, no external image, no font download. The coeo logo is embedded as a data URI for this reason.
2. **Offline and private.** No customer data leaves the browser.
3. **Iframe-safe.** No native dialogs, and a clipboard path for the diagram where downloads are blocked.
4. **Legible.** Every text/background pair to clear WCAG AA for normal text in both themes; the weakest pair measured is 4.6:1.
5. **Layout from measurement, not arithmetic.** Node sizes are read back from the rendered DOM and cached, so the layout guards cannot drift from the CSS.
6. **Reduced-motion respected** for the progress bar and pulse animations.

---

## 8. Architecture and constraints

- Single HTML file: markup, CSS, and one script block. State lives in one `DOC` object; the canvas and the object forms are two editors over it.
- The trace and render engine is lifted unchanged from `pbxware_master_call_flow.html` and is present only so this file runs standalone. On merge it becomes the host application's own code and the block disappears.
- `SKIN.did` deliberately diverges: teal here, navy in the Map Creator. Recorded in a comment; a merge must decide which wins.
- The `.xlsx` writer builds Open Packaging XML by hand and a store-method ZIP, with no compression library. The same ZIP writer carries binary entries for the multi-image `.png` export.
- The `.png` export is a redraw, not a screenshot: the on-screen geometry is read back and re-emitted as SVG, then rasterised. No browser API rasterises live HTML, and the `foreignObject` route is blocked in Chrome and Safari.

---

## 9. Deployment modes

1. **Local file.** Open the HTML directly. Everything works, including downloads.
2. **Static hosting** (GitHub Pages). Same.
3. **Confluence iframe / HTML macro.** Downloads are restricted by the browser; use Copy canvas image. Native dialogs are suppressed, which is why none are used.

---

## 10. Out of scope (current release)

- Reading `.xlsx`. The workbook is write-only; import is `.csv`.
- Writing to PBXware. The Builder produces documents, not configuration.
- Caller ID modelling. The sheet is written with headers only.
- Multi-select and edge alignment. Align works on the whole flow.
- Undo. A prerequisite for any bulk apply, including an assistant.
- AI assistance. The panel tab exists and is disabled.

---

## 11. Roadmap

1. **Operation Times editing.** Currently unreachable — see §13. Make ⏱ open the gate in the Inspector, or unhide the Forms view.
2. **`.xlsx` import.** Close the round trip so a filled template can be loaded, not just written. Needs a ZIP reader plus inflate; feasible in the browser via `DecompressionStream`.
3. **Undo stack.** Prerequisite for anything that changes many objects at once.
4. **Multi-select and edge alignment.** Shift-click and box-select, then align and distribute.
5. **Handover document.** Markdown of DIDs and their routes, IVR key tables, OT schedules, findings and notes — the artifact provisioning actually needs.
6. **Merge into the Map Creator**, so composing and tracing are two modes of one tool.
7. **PBXware API.** The shared long-term goal with the Map Creator: read and eventually write configuration directly.

---

## 12. Success metrics

1. A designed flow exports and loads into the Call Flow Map Creator with no manual editing of the workbook.
2. Findings catch the routine structural errors — missing timeout, unbuilt destination, duplicate number, unreachable object — before a flow is built.
3. A technician can produce a reviewable diagram of a proposed flow in minutes without a spreadsheet.
4. The file keeps working offline and inside Confluence with no per-deployment adjustment.

---

## 13. Risks and open questions

1. **Operation Times cannot currently be edited.** Hiding the Forms view removed the only surface for a gate's schedule and after-hours destination. The gate can still be added and removed, so a flow can carry a gate whose schedule is neither visible nor editable. **This should be closed before wide use.**
2. **Column order in two sheets is load-bearing and fails silently.** The Map Creator locates the IVR greeting column from the header and reads the options immediately after it; a queue with one agent is dropped unless the pair columns are used. Both are now correct and commented, but neither error announces itself.
3. **Version skew against the Map Creator.** The workbook layout is aligned to v2.45.0. An earlier copy of the mapper reads three sheets differently. Any change to either side needs checking against the other.
4. **Two artifacts for one diagram** if the flowchart is embedded in the app as SVG as well as kept as Mermaid source.
5. **Rendered output is not verifiable in the build environment.** Text metrics and CSS variables do not resolve headlessly, so PNG geometry and colour fidelity need a human check in a real browser.
6. **`SKIN` divergence** between the two tools is deliberate but unresolved.

---

## 14. Build snapshot

**Application:** `pbxware_call_flow_builder.html` — v0.42.0, single file, ~232 KB
**Aligned to:** Call Flow Map Creator v2.45.0
**Object types:** 9 plus Operation Times gates
**Export sheets:** 11
**Templates:** 1 consolidated `.xlsx`, 8 per-type `.csv`
**Test suite:** 21 headless jsdom scripts, all passing
