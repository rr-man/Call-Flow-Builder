# Changelog — PBXware Call Flow Builder

Versions below cover the work recorded in this build; entries before 0.22 were
not kept in-app and are not reconstructed here.

## [0.42.0]
### Added
- coeo logo in the upper left of the banner, embedded as a data URI so the file
  still has no network dependency. It sits on a white chip: the logo's navy is
  #1C355E, which is 1.18 against the banner and effectively invisible, so the
  chip preserves the supplied colours rather than recolouring the mark.

## [0.41.5]
### Changed
- Draft framing removed for release: the "not production" banner is gone, and
  the title, version chip and file name no longer say draft.
### Fixed
- Moving the credit line into the canvas column broke
  `#cvleft > .panel:last-child`, so the canvas panel lost its `flex:1` and
  collapsed to its 240px minimum instead of filling the window. The panel is
  now targeted by id.

## [0.41.4]
### Changed
- The credit line moved out of the page footer to sit directly under the flow
  canvas, so it stays with the tool rather than reading as page furniture.

## [0.41.3]
### Added
- LinkedIn mark beside each footer credit.

## [0.41.2]
### Added
- Footer credit with LinkedIn links, and the version chip is now a button that
  opens this changelog. The LinkedIn mark is an inline SVG symbol, so the footer
  still renders with no network access.

## [0.41.1]
### Fixed
- The "Nothing built yet" card was a child of `#canvas` and positioned at 50% /
  42% of it. The canvas element is a minimum of 900x520 whatever the window, so
  on a wide screen the card sat well left of centre, and because it was inside
  the canvas it also inherited the zoom transform. It is now an overlay over the
  scroll area, centred by flexbox, immune to canvas size, scroll and zoom.

## [0.41.0]
### Added
- Editable **project name** in the banner. Drives every filename the tool
  writes: `.json`, `.xlsx`, `.png` and `.zip`.
- **Whole workbook** section in the Upload panel: download the consolidated
  template, or save the current flow in the same shape. Both use one writer, so
  the template cannot drift from what the tool produces.
- Agents gained **Bound extension**, which the mapper reads into `agentExt` and
  `agentByExt`. That mapping previously could not survive a round trip.
### Changed
- The workbook now matches a real PBXware export sheet for sheet: 11 sheets in
  export order and column layout. Operation Hours writes the current
  `Days / Time From / Time to / Afterhours Destination` layout instead of the
  legacy one, parsed out of the single schedule field. Caller ID is written as
  headers only, since the builder does not model it.

## [0.40.0]
### Added
- **Conference** as a local destination: palette chip, form, export sheet, CSV
  template and importer. Terminal, and a valid target for a DID or an IVR key.
- Tooltips on every toolbox chip and group label.
### Fixed
- The IVR sheet put `Greeting` at the end. The mapper locates the greeting
  column from the header and reads the twelve option columns immediately after
  it, so **every menu key and every timeout was lost**. Now written in export
  order: `Name | Number | Greeting name | Option 1..# | Timeout | Transcript`.
- Queue agents were written as a comma list, which only worked through a legacy
  path that requires two or more tokens — a **single-agent queue vanished**. Now
  written as a count plus `Members Name N` / `Agent` pairs.
- Zoom and Align stayed right-aligned when the toolbox wraps.

## [0.39.2]
### Changed
- Panel defaults to the left and expanded. An explicit saved choice still wins.

## [0.39.1]
### Changed
- Forms tab hidden. Two things live only there and are unreachable while it is:
  the traced map preview, and the Operation Times schedule field.

## [0.39.0]
### Added
- New, Sample flow and Open now offer **Cancel / Discard / Save first**, with
  Save first as the primary. Open previously replaced the document with no
  prompt at all.

## [0.38.2]
### Added
- Tooltips on every control in the File menu and the canvas-image dialog,
  including state-aware text on the action button.

## [0.38.1]
### Fixed
- Dimming is read from the `dimmed` class rather than computed opacity, which is
  a CSS variable and would silently resolve to `NaN` in some hosts.

## [0.38.0]
### Added
- Export **Context**: "Only this DID" or "Whole flow, dimmed".
### Fixed
- The exporter dropped anything below 0.5 opacity, so a Focus export threw away
  exactly the dimmed context that makes Focus useful.

## [0.37.0]
### Changed
- Clicking a node brings the Inspector forward; dragging one does not. A
  collapsed panel stays collapsed. Clicking bare canvas deselects.

## [0.36.1]
### Changed
- Light is the default theme outright. The operating-system preference is no
  longer consulted.

## [0.36.0]
### Added
- Panel position, Left or Right, in the View menu.

## [0.35.0]
### Added
- Canvas zoom, 40% to 200%, with ctrl/cmd + wheel about the pointer. Fit now
  scales as well as scrolls. PNG export always renders at 100%.

## [0.34.1]
### Fixed
- `nodeSize` was hand-maintained arithmetic that had drifted from the CSS: a
  flat 108 for every non-IVR node, and 5 to 14px short on IVRs. Every layout
  guard was working from wrong numbers. Sizes are now derived from the CSS box
  and then **measured** from the rendered node and cached.
- `ensurePosSafe` numbered each type from zero, so the first node of all eight
  types landed on the same coordinate — 40 overlaps. It now places via
  `freeSpot`.

## [0.34.0]
### Added
- **View** menu with layout guards: snap to grid, warn while dragging, nudge on
  release, push neighbours on grow, report overlaps. First three on by default.
- See-through moved out of the toolbox into the menu.

## [0.33.0]
### Added
- Multi-select export scope. One selection saves a `.png`, more than one a
  `.zip`, with progress. Copy mode is single-pick, since the clipboard holds one
  image.
### Fixed
- The ZIP writer encoded everything through `TextEncoder`, which would have
  corrupted every PNG. It now carries raw bytes and an explicit mime type.

## [0.32.0]
### Added
- Export scope: everything, a single DID, or unrouted. Defaults to the active
  tab and never disturbs the working view.

## [0.31.0]
### Added
- Canvas to PNG. Not a screenshot: the on-screen geometry is read back and
  re-emitted as SVG, then rasterised. Options for theme, background and scale.

## [0.30.0]
### Changed
- Open, Save and Export collapsed into a **File** menu.

## [0.29.0]
### Added
- **Align** horizontal and vertical, laying the flow out by call depth.

## [0.28.0]
### Fixed
- In dark mode Queue and Agent were 2.9 apart on fill and 12.8 on border, so
  neither channel separated them. Queue is now bluer steel, Agent warm taupe:
  16.6 and 35.9.

## [0.27.1]
### Fixed
- The canvas was within 1.02 of white, so white cards and pale nodes had nothing
  to sit against. The empty state became a proper card with a real button.

## [0.27.0]
### Fixed
- Dark mode composited pale node fills over a dark canvas, collapsing every node
  to a muddy mid tone with dark text on it — 1.84 to 3.04. The object families
  now theme, keeping hue and inverting lightness. `SKIN` is untouched, so the
  export is unaffected.

## [0.26.2]
### Fixed
- `--card` never got a dark value, so panels stayed white while text went light.
  Split "text on a themed surface" from "text on a fixed pale card"; 31
  instances corrected.

## [0.26.0]
### Added
- Dark mode, and the panel given a navy header with a teal accent.

## [0.25.1]
### Changed
- One label for the IVR timeout: `t/o` everywhere on the canvas, with a tooltip
  that names the play count it depends on.

## [0.25.0]
### Fixed
- The canvas enforced which destination types are legal; the importers did not.
  A CSV could point a DID at an agent, or make an agent a dial-group member.
  Both now read the same `ACCEPT` table, and refused routes are reported.
