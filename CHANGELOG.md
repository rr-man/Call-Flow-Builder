# Changelog — PBXware Master Inbound Call Flow Map

All notable changes to the call flow map. Dates are 2026-07-13 unless noted;
the map was developed iteratively in a single working session.

## [2.2.4] — 2026-07-13
- Theme-adaptive logo done properly: instead of a CSS filter, a real
  light-on-dark variant of the lockup (white circles and wordmark,
  brightened blue "e") is embedded and swapped in when dark mode is on.
  Light mode keeps the original navy lockup on its white pill.

## [2.2.3] — 2026-07-13
- The banner logo now adapts to the theme: light mode keeps the navy
  lockup on its white pill; dark mode drops the pill and inverts the
  artwork (hue-preserving) so it reads as a light lockup directly on the
  dark banner.

## [2.2.2] — 2026-07-13
- Banner logo replaced with the full Coeo "Business Connectivity"
  lockup; sized up slightly to keep the tagline legible.

## [2.2.1] — 2026-07-13
- Expanded view now uses the full screen and auto-fits the map to the
  window on open (Reset returns to the fitted size).
- Horizontal / Vertical layout switching and the dark/light theme toggle
  are available inside the expanded view; in dark mode the expanded map
  re-themes with the same hue-preserving inversion as the reference map.

## [2.2.0] — 2026-07-13
### Added
- The generated map now sits under a named **"Call Map"** section header.
- **Expand** button on every generated map: opens the map full-screen in
  an overlay with its own Zoom in / Zoom out / Reset, **Download SVG**,
  and Close controls.
### Fixed
- The version link previously pointed at CHANGELOG.md as a separate
  file, which showed nothing when the HTML travels alone. The changelog
  is now embedded in the app: clicking the version (banner or footer)
  opens it in an in-app overlay.

## [2.1.2] — 2026-07-13
- The light/dark mode toggle moved into the banner, so it is available
  on the landing screen, the reference map, and the upload/mapper view
  alike; the duplicate button in the map toolbar removed.

## [2.1.1] — 2026-07-13
- Footer restructured: the "Created by Ron Mangune" credit moved to its
  own smaller line below the footer's main row, centred, separated by a
  hairline, with a smaller LinkedIn mark.

## [2.1.0] — 2026-07-13
### Added
- **Map per IVR.** The upload view now lists every IVR in the workbook
  alongside the DIDs; picking one traces that IVR as the root — its
  options → terminating destinations only.
- **Horizontal / Vertical layout toggle** on every generated map. The
  vertical layout narrows boxes and re-routes connectors top-down;
  spacing in both modes guarantees no overlapping nodes or labels.
- **Footer** across all views with version link, and "Created by Ron
  Mangune" with the LinkedIn mark linking to his profile — also shown at
  the bottom of the landing screen's left card.
### Changed
- Responsive layout: the landing cards stack on narrow windows, the
  reference-map canvas scales to the window width, and paddings tighten
  under 900px.

## [2.0.0] — 2026-07-13
### Added — the mapper is now data-driven
- The upload view reads a **PBXware .xlsx export directly in the browser**
  (ZIP + DecompressionStream + DOMParser — no libraries, still one
  offline file). Sheets read: DID routing, IVR, Dial Group, ERG,
  Extension, Voicemail, Operation Hours.
- Every DID in the workbook is listed; picking one traces and draws its
  complete call map: **DID → Operation Times (if enabled) → IVR → every
  configured option → the terminating destination** (extension,
  voicemail, dial-group members, ERG member, directory).
- Findings are reported beside the map, not drawn as nodes: IVRs with no
  Timeout Destination, options whose target matches no object in the
  workbook, and options that route back into a menu already on the path.

### Scope
Only **configured** routes are drawn. An unset option or unset timeout is
the absence of a destination, so it gets no node — it is listed as a
finding instead. An IVR is expanded once; later references to it are
shown as a dashed "shown above" node rather than duplicating the subtree.

### Verified against
New Age Elder Care export — 6 DIDs, 21 IVRs, 4 dial groups, 29 ERGs,
32 extensions. DID 8474033053 traces to 48 terminating destinations.

## [1.3.0] — 2026-07-13
### Added
- **Landing screen.** The HTML now opens on a launcher with two paths:
  "View the call map" (the reference diagram, unchanged) and "Map my
  system from a file". A Home button in the banner returns to it.
- **Upload view.** Drag-and-drop or browse for PBXware CSV exports.
  Files are parsed in the browser — nothing leaves the machine.
  A DID export (detected by an `nr1` column) renders a routing table of
  every DID to its first-hop destination, and flags DIDs with no
  destination set as dead ends. Non-DID files are reported rather than
  silently ignored.
- Guidance panel listing what to export per object type and what each
  additional export unlocks.
- `sample_dids.csv` added so the upload path can be tried immediately.

### Note
The upload view currently traces the **first hop only**. Following DIDs
onward into IVR digit maps, queue members and timeout destinations is the
next step, and needs those exports.

## [1.2.0] — 2026-07-13
- Tooltips added to Parts 4 and 5, completing coverage across the whole
  map (19 in total). Part 4: Ring All, Announce sound, group Default
  Destination, and the ERG panel. Part 5: Max Callers, The Wait, Exit
  Digit, Members vs Agents, and Timeout/Overflow. Same rule as Parts 1-3
  — each adds a constraint, an example, or a failure mode not visible on
  the canvas; nothing restates what is already printed.

## [1.1.11] — 2026-07-13
- Text selection is now visible. Added explicit ::selection styling
  (amber highlight on dark text) for the page and for SVG text, with a
  separate rule for dark mode so the canvas inversion filter does not
  wash the highlight out. Selection explicitly enabled on the canvas.

## [1.1.10] — 2026-07-13
- Part 3: destination-types panel lowered so its vertical middle aligns
  with the keypad's — the "any" arrow from the selections into the panel
  is now a single straight horizontal line instead of an elbow.

## [1.1.9] — 2026-07-13
- Fixed the "no" branch in the Part 3 termination. The 1.1.8 cascade had
  shifted its elbow turn-point inconsistently, leaving the arrow running
  backwards — up from the diamond's bottom tip instead of down. It now
  drops from the bottom tip into the centre of the Extension rings box.

## [1.1.8] — 2026-07-13
- Part 3: the selections column (header, keypad, note, Invalid and
  Timeout Selection) lowered so the keypad's vertical middle aligns with
  the Greeting box — the "key" arrow is now a single straight horizontal
  line rather than an elbow. Termination, the ✱/# panel and the export
  panel shifted down to clear it; Parts 4 and 5 cascaded; canvas extended.

## [1.1.7] — 2026-07-13
- Part 3: the "key" arrow from Greeting plays now elbows up and points
  into the vertical middle of the keypad's left edge, instead of running
  flat off the side of the Greeting box toward empty space.

## [1.1.6] — 2026-07-13
- "Extension rings" subtitle changed from "operator / receptionist" to
  "deskphone · softphone · mobile app" — it describes the devices that
  ring, not an assumed role. Applied in both places it appears (Part 3
  termination and Part 4 Dial Group).

## [1.1.5] — 2026-07-13
- Tooltips added to Part 3, following the same rule as Parts 1 and 2 —
  only where they add something the canvas cannot show. Eight in total:
  Greeting (the two timeouts), Play Greeting (the counter and its
  consequences), Selection ✱, Selection #, Invalid Selection (its replay
  burns the counter), Timeout Selection (silence vs wrong key), Timeout
  Destination (the invisible field where calls vanish), and the
  Is-Voicemail flag (the full fall-through to disconnect).
  No tooltips on the plain digit keys or the destination-type chips —
  those are self-evident.

## [1.1.4] — 2026-07-13
- Part 1 tooltips pruned to match Part 2. Removed the Provider tooltip
  (the box already states it) and the OT Gate tooltip (the priority
  ladder panel sits directly beside it and says the same thing).
  Trimmed Trunk, DID Match, CLI, Range and Destination to their unique
  content; dropped the billing footnote from Destination, consistent
  with its removal from the legend.

## [1.1.3] — 2026-07-13
- Part 2 tooltips pruned. Removed the three OT-gate tooltips (they
  repeated each other, the Part 1 OT panel, and the legend gotcha).
  Trimmed the five node tooltips: dropped billing lines (billing was
  removed from the legend in 1.1.1) and "→ expanded in Part N" lines
  (already printed on the map as labels). Each tooltip now carries only
  what is not visible elsewhere.

## [1.1.2] — 2026-07-13
- Legend rebuilt as two bounded columns with a divider: swatches and
  their (now wrapped) descriptions on the left, the gotcha note on the
  right. The amber and green lines had been running ~570px wide and
  colliding with the gotcha column, and the gotcha's last lines were
  falling outside the box after it was tightened in 1.1.1.

## [1.1.1] — 2026-07-13
- Legend trimmed: removed the "✻ Billing only" footnote and the
  "Red dashed / Amber dashed" line, plus the now-orphaned ✻ marker on
  the Extension node. Legend box tightened to fit. The billing detail
  remains available in the Extension and Destination tooltips.

## [1.1.0] — 2026-07-13
### Corrected
- **Extension recoloured green.** It had been blue, which implied it was
  not a local destination. It is one — Extension is an internal DID
  destination exactly like IVR, Queue, Conference and Voicemail. The
  colour channel had been overloaded to carry a *billing* distinction.
- Billing difference moved to a secondary "✻" marker on the Extension
  node and a legend footnote: IVR/Queue/Conference/VM bill as "Local
  destinations" from the Service Plan; an Extension bills per the DID's
  E.164 incoming price. Same routing category, different invoice line.
- Extension and Part 1 Destination tooltips reworded to lead with the
  routing fact and demote billing to a footnote.

## [1.0.24] — 2026-07-13
- Tooltips added to Part 2: all five destination nodes (IVR, Queue,
  Ring/Dial Group, Extension, Conference/Voicemail) and the three OT
  gates. Each explains the object, its billing treatment, and where it
  is expanded; the OT gate tips call out the double-divert behaviour.
  Reuses the amber tooltip engine introduced in 1.0.8.

## [1.0.23] — 2026-07-13
- Light mode is now the default on load. The page no longer follows the
  OS colour-scheme preference; dark mode is opt-in via the toolbar button.

## [1.0.22] — 2026-07-13
- Part 2: horizontal distribution bus trimmed from x=1055 to x=1035 —
  it had overshot the Conference/Voicemail drop point by 20px, leaving a
  loose line hanging past the last column.

## [1.0.21] — 2026-07-13
- Light/dark mode added to the HTML. Toggle button in the toolbar; the
  page follows the OS colour-scheme preference on first load. Dark mode
  uses a hue-preserving inversion filter on the canvas, so the diagram
  re-themes without duplicating the SVG palette. The banner logo keeps
  its white pill and is unaffected.

## [1.0.20] — 2026-07-13
- Coeo logo relocated from the SVG canvas into the HTML banner, above
  the zoom toolbar, on a white pill so the navy artwork stays legible on
  the dark header. Diagram title/subtitle returned to the left margin.

## [1.0.19] — 2026-07-13
- Coeo logo moved to the upper-left; title and subtitle shifted right
  beside it.

## [1.0.18] — 2026-07-13
- Coeo logo added to the top-right of the title block (embedded, no
  external file needed).
- Version/date link removed from the diagram subtitle; the clickable
  version now lives only in the HTML banner.
- Part 3: "Configured as Selection 0…9 / ✱ / #" note re-wrapped onto
  three lines so it no longer runs into the destination-types panel.

## [1.0.17] — 2026-07-13
- Termination: red-drop label reworded from "VM off + no response" to
  "VM off / Call Hang up".

## [1.0.16] — 2026-07-13
- Voicemail box vertically centered on the "yes" arrow from the
  Is-Voicemail diamond; Extension rings and disconnect re-spaced below
  it with even gaps, the no-path, up-arrow, and red drop re-spanned to
  match.

## [1.0.15] — 2026-07-13
- Is-Voicemail branches set to conventional flowchart form: "yes" runs
  straight from the diamond's right-most tip into the Voicemail box;
  "no" drops from the bottom tip and elbows right into Extension rings.

## [1.0.14] — 2026-07-13
- Is-Voicemail branches made fully independent: "yes" now exits the
  diamond's upper-right edge, "no" the lower-right edge — previously
  both launched from the right vertex and overlapped for their first
  22px. Labels sit above their own arrows, clear of each other.

## [1.0.13] — 2026-07-13
- Termination: yes/no branches from the Is-Voicemail diamond redrawn as
  orthogonal elbows (the yes path had degraded into a flat squiggle);
  outcome labels moved from the far right to sit directly beside their
  arrows.

## [1.0.12] — 2026-07-13
- Termination column: yes-arrow into the Voicemail box smoothed to a
  single sweep; Extension box lowered for a proper gap, giving the
  upward "no answer" arrow (34px) and the red "VM off" drop (36px)
  standard lengths; no-curve and labels repositioned to match.

## [1.0.11] — 2026-07-13
- Part 3 termination re-spaced: header sits just below the section
  divider; main row (Greeting replayed → Timeout Destination →
  Is-Voicemail diamond) aligned on one axis; Voicemail / Extension /
  disconnect stacked with even 28px gaps; yes/no curves and the two
  vertical outcome arrows cleaned up with labels beside them.

## [1.0.10] — 2026-07-13
- Part 3 termination: disconnect box relocated directly below "Extension
  rings", aligned to the Voicemail/Extension column, fed by a straight
  red drop labeled "VM off + no response". Part 3 panels and Parts 4/5
  cascaded down to make room.

## [1.0.9] — 2026-07-13
- Part 3 termination logic corrected: Voicemail box is a true terminal
  (no path to disconnect). Is-Voicemail = No → extension rings → if
  unanswered, the call falls to that extension's voicemail box (new
  upward arrow). The call disconnects only when the extension's
  voicemail is turned off; disconnect node reworded accordingly.

## [1.0.8] — 2026-07-13
- Part 1 tooltips restyled: native browser titles replaced with custom
  scripted tooltips matching the OT gate panel (amber #fffdf7 fill,
  #e0a800 border), bold heading line, cursor-following placement clamped
  to the canvas edge. Requires script: works in the HTML and in the SVG
  opened directly; static image embeds fall back to no tooltip.

## [1.0.7] — 2026-07-13
- Hover tooltips added to all seven Part 1 stages (Provider, Trunk, DID
  Match, OT Gate, CLI, Range, Destination) using native SVG titles —
  each explains the stage with examples; cursor shows help pointer.

## [1.0.6] — 2026-07-13
- "Inherit" in the OT config panel is now clickable: it toggles an
  explanation callout (three OT states; Inherit re-applies the
  Server/Tenant rules; historical on/off-only note). Click the callout
  to close. First interactive element on the map.

## [1.0.5] — 2026-07-13
- "Where Operation Times is configured" panel: the Inherit arrow moved
  from the left edge to the horizontal center of the rows.

## [1.0.4] — 2026-07-13
- Arrowhead added to the Part 1 Destination → Part 2 pointer (stops just
  above the bus so the marker doesn't overlap it).

## [1.0.3] — 2026-07-13
- Part 1: the Destination → Part 2 feed line restyled to match the
  drill-down pointers (purple dashed) with an "expanded in Part 2 ↓"
  label, consistent with the Part 3/4/5 pointers.

## [1.0.2] — 2026-07-13
- Part 2: "Extension / Multi-User" node simplified to "Extension";
  legend and OT config panel wording updated to match.

## [1.0.1] — 2026-07-13
- Version stamp made clickable in both the SVG subtitle and the HTML
  header; it links to this CHANGELOG.md.
- Changelog completed with previously undocumented fixes (see additions
  under 0.6 and 0.9 below).

## [1.0] — 2026-07-13

First complete release. Version stamp added to the diagram subtitle and the
HTML header. README and CHANGELOG introduced.

### Content
- Removed all vendor-name references; restriction facts retained and
  reworded neutrally.

---

## Pre-release iterations (0.x)

### [0.9] — Layout polish
- Uniform ~28–30px arrows across all five parts (spine, columns, and all
  expansion flows); dependent elements reflowed.
- Part 1 spine rebuilt with even stage spacing; closed the oversized gap
  left by the fax-stage removal; stage labels vertically centered and
  renumbered 1–7 with no gaps (labels 4 and 6 lifted clear of the side
  boxes that were painting over them).
- Termination cluster in Part 3 shifted down so the section divider runs
  full width unobstructed (twice — the upward-fanning Voicemail box
  collides whenever Part 3 spacing changes).
- Drill-down arrow from the IVR digit map to Part 3 straightened and
  stopped at the divider; Part 2 legend moved right to clear its path.
- Divider added between the title block and Part 1; section framing
  (accent bars) added and subsequently removed by request.
- Inherit arrow inside the Part 1 "where OT is configured" panel
  lengthened; panel rows re-spaced to give the inheritance cascade a
  visible run.
- Overlap fixes: drill-down connector no longer routes through the Part 2
  legend; "nests"/"replay ×N"/invalid-loop annotations lifted off the
  curves they sat on; over-long legend line shortened to clear the gotcha
  column; Part 2 divider trimmed while the OT config panel extended past
  it (later restored to full width).
- Part 3 invalid-key loop-back rerouted as a clean orthogonal path into
  PLAY GREETING, and the disconnect-node curves replaced with labeled
  elbow arrows (both elements removed in a later revision — see 0.6).

### [0.8] — Part 5: Queue + ERG comparison
- Added Part 5: full queue flow (OT gate, max-callers check with
  full-redirect, waiting cycle with MOH and position announcements, Exit
  Digit, ring cycle, timeout/overflow).
- Queue vs ERG comparison panel: purpose, edition availability, members,
  callback, reporting, and shared features.
- Export checklist per Queue/ERG, including "record which type it is".

### [0.7] — Part 4: Ring / Dial Group
- Added Part 4: ring-all flow, no-answer path (Announce → Default
  Destination → Is-Voicemail fork), ERG extras panel, export checklist.
- Pointer labels added under the Part 2 Queue and Ring Group columns.

### [0.6] — Content corrections
- Removed all fax content (Auto Fax Detection stage in Part 1, Fax-to-Email
  destination chip in Part 3); spine stages renumbered.
- Removed the IVR-digit-map → Queue "nests" arrow in Part 2.
- Removed the invalid-key-press chain and its loop-back from the Part 3
  termination row (the Invalid Selection config field remains in the
  selections column).
- Removed the replay loop arrow (Play Greeting → Greeting plays); the
  replay behavior remains documented in the Play Greeting box text.
- Counted and removed all vendor-name occurrences on request (finalized
  in 1.0); Conference/Voicemail "no OT" placeholder removed in favor of a
  clean arrow.

### [0.5] — Operation Times accuracy pass
- Verified OT per object against documentation: present on DID, IVR,
  Queue, Ring/Dial Group, ERG; absent on Conference and Voicemail.
- Extension OT (opt-in via Enhanced Services) shown as a dashed
  conditional gate, then removed entirely per the deployment's convention;
  legend and config panel updated to match.
- Conference/Voicemail "no OT" placeholder later removed in favor of a
  clean arrow, with the fact retained in the legend.

### [0.4] — Format change
- Delivered as a single self-contained HTML file (inline SVG, offline,
  zoom in/out/reset toolbar); SVG retained alongside.

### [0.3] — Part 3: IVR expansion
- Added the IVR detail section: entry sequence, all selections 0–9 plus
  ✱ and # (each individually mapped), destination-type panel, Play
  Greeting replay counter, and the termination chain ending in disconnect.
- Clarified ✱/# as ordinary configurable selections; noted the distinct
  feature codes (✱304xxx greeting recording, ✱401/✱402 OT override).

### [0.2] — Operation Times as a repeating gate
- Reworked OT from a single spine step into a gate at every hop.
- Added the OT priority ladder panel (Open Days → Custom Destinations →
  Closed Dates → Default Destination, with the Is-Voicemail flag).
- Added the "where OT is configured" panel with Server/Tenant inheritance.
- Documented the double-divert gotcha (DID open, Queue closed).

### [0.1] — Initial map
- Generic DID → local destination flow: Provider → Trunk → DID match →
  processing checks → Destination + Value, fanning out to IVR, Queue,
  Ring Group, Extension/Multi-User, Conference, Voicemail.
- Billing distinction encoded: green "Local destinations" billed from the
  Service Plan vs blue Extension/Multi-User billed per the DID's E.164
  incoming price.
