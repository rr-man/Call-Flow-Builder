# Changelog — PBXware Call Flow Builder

Versions below cover the work recorded in this build; entries before 0.22 were
not kept in-app and are not reconstructed here.

## [0.57.0]
### Added
- **Grey out empty types**, on by default, in the Routing view. A type the flow
  has none of is dimmed, reads *none* and cannot be ticked, so the list shows
  what the flow actually contains. Unticking them instead would have made the
  summary claim things were hidden when nothing was, and the first object you
  added of that type would never have appeared. The switch turns it off for
  anyone who wants the full list regardless.
- A type that is deliberately hidden is never dimmed, even when empty, so it can
  always be ticked back on.

## [0.56.0]
### Added
- **Routing view** in the View menu: a checkbox per routing type \u2014 IVR, dial
  group, queue, ERG, voicemail, conference and agent \u2014 with the object's own
  colour and how many of them exist, plus All and None. DIDs and extensions are
  not listed: they are the two ends of every route.
- Hidden types are removed from the drawing rather than faded, since Focus
  already fades and two kinds of dimming cannot be told apart. Nothing moves, so
  ticking a box back restores the picture exactly.
- The setting saves with the project, and whenever anything is hidden a chip
  appears on the canvas saying so, listing what and restoring everything in one
  click. Without it a shared file could show half a flow and look complete.
- Hiding a queue greys the Agent row, which explains that its agents would have
  nothing visible to hang from.
### Note
- This changes the picture only. The export, the findings and the traced map all
  still see every object.

## [0.55.0]
### Changed
- **S-NET Connect takes more than one licence**: Mobile, Office, Business,
  Agent and Supervisor, as a two-column checkbox grid with a count in the label.
- The value is stored as a list and written to the workbook as `Office; Agent`,
  read back the same way. A value that is not one of the five \u2014 anything typed
  in before, or an unfamiliar import \u2014 is kept and shown as a greyed entry
  rather than dropped, so an import cannot silently lose it.
## [0.54.0]
### Changed
- **Inspector fields are one per row**, with the label beside the input. The
  panel is 340px, so three across left 78px of text room and cut off both a
  phone model and an email address. Labels now line up into a column, and the
  form is about a third shorter than stacking the labels above would be.
### Added
- **Inspector fields** in the View menu, offering **Two across** for anyone who
  wants the shorter form. A long value is still truncated there, which is why it
  is not the default. One class on the form container drives both shapes, so no
  form markup changed \u2014 pick lists, checkboxes and the IVR key grid keep their
  own arrangements.

## [0.53.0]
### Added
- **Department, Phone type (UAD) and S-NET Connect** on an extension: three
  fields in the Inspector, importable from CSV under the usual aliases, in the
  CSV template, and written as trailing columns on the Extension sheet. That
  sheet is read by position and stops at MAC, so the extra columns travel
  without disturbing the Map Creator \u2014 verified by round trip.

## [0.52.0]
### Added
- **SMS marker** in the View menu: a pill in the subtitle, **its own row (the
  default)**, an edge stripe with a header badge, or not shown at all. Teal
  throughout, so it cannot be mistaken for an Operation Times gate or for
  something broken. Only the row option costs height, and the estimate accounts
  for it, so the layout guards stay accurate.

## [0.51.0]
### Added
- **SMS on a DID** \u2014 a checkbox in the Inspector, shown on the node beside the
  tenant and trunk, importable from an `sms` column (`yes`, `y`, `true`, `1`).
### Changed
- **Tenant and trunk are no longer editable in the Inspector.** Both are still
  held, still imported and still written to the DID routing sheet, so a round
  trip is unchanged \u2014 but a DID created in the builder can no longer be given a
  trunk, and PBXware needs one.
### Note
- A real DID routing sheet has no SMS column, so the flag travels in the project
  file and the CSV, not the workbook.

## [0.50.1]
### Changed
- The sample flow now covers two destination types it never reached: a **DID
  straight to a dial group** with no menu in front of it, and a **conference
  bridge**, published on its own line and on a menu key so the same object is
  reached two ways. The queue also gained the timeout it was missing, which was
  showing red in the detail view.

## [0.50.0]
### Added
- **The destination scale now drives every port row on every type**, not just
  DIDs and IVR keys. A dial group reads `rings Extension 1001 Reception desk`,
  a queue's timeout and a ring group's extension name what they reach, and the
  after-hours row names its target wherever a gate exists.
- **Dial groups, queues and ring groups get the S and i buttons** and a full
  detail block: what it rings or how many agents, the strategy, the timeout and
  the after-hours path, each reddened when unset.
- They widen from 190px to 230px at the name and detail steps, where a list of
  names needs the room, and stay at 190px below that.
### Changed
- A port keeps its own word: a ring group reads `rings 1001`, not `\u2192 1001`.
  Only a DID's routes-to uses the bare arrow, and only the after-hours row uses
  the clock \u2014 the duplicated "after hours" tail is gone, since the clock
  already says it.

## [0.49.4]
### Changed
- On an IVR the **closed** row now sits below the keys rather than above them.
  It is the after-hours fallback, so showing it first read as though it came
  first. Every other type is unchanged \u2014 their closed row was already last.

## [0.49.3]
### Changed
- **S now means "number only", not "nothing".** Stripping the destination out
  entirely left the node saying where none of its keys go, which is the thing it
  exists to show. It also puts the node at 150px rather than 120px, where the
  control strip fits on one line without wrapping. The View menu keeps a true
  **Nothing** step for anyone who wants bare labels.

## [0.49.2]
### Fixed
- In simple view the IVR's collapse button sat outside the node. The control
  strip needs 150px for five buttons and simple view is 120px wide; it fitted
  before only because there were three. The strip now wraps, so it cannot
  overflow at any width, zoom or font size, and the gap and padding are tighter
  so the wider views still keep it on one line. The height estimate knows when
  it wraps, so the layout guards stay accurate.

## [0.49.1]
### Added
- **S for simple** on the IVR and the DID, beside the existing **i**. S strips
  that node back to bare labels whatever the View menu says; i gives it full
  detail. Clicking a lit button clears the override, so the node follows the
  menu again \u2014 previously a second click on **i** silently meant "simple",
  which was the wrong thing for the only button available to say it.

## [0.49.0]
### Changed
- **One destination scale for both node types.** The setting now says how *much*
  to show rather than *where*: **Nothing / Number only / Number and name (the
  default) / Full detail**. Each type places it where it fits \u2014 a DID on its
  routes-to and closed rows, an IVR on its key rows \u2014 and the closed row is
  included whenever a gate exists instead of being a mode of its own.
- **IVR key rows now carry their destination**, tinted by the same Destination
  colour setting. A vertical IVR widens only as far as the step needs: 120px
  bare, 150px for numbers, 230px with names. Horizontal keys are 34px columns,
  so they take the colour and no text at any step.
- **Full detail adds an IVR summary**: keys used, timeout (red when unset, since
  silent callers drop), and the after-hours path.
- The per-node **i** override now works on IVRs as well as DIDs.
- Changing the scale now tidies any overlaps it causes. Every node changes size
  because of a global switch rather than anything the person did, so the app
  clears up after itself instead of leaving collisions on the canvas.
- Projects saved with the old five modes are migrated: `row`, `both` and `line`
  all become **Number and name**; `off` and `detail` map straight across.

## [0.48.1]
### Changed
- Defaults now show the routing rather than hiding it: DID destinations **On
  both rows**, destination colour **Tinted**, and **Colour the wires** on. All
  three still switch off in the View menu, and a project saved with different
  settings keeps them.

## [0.48.0]
### Added
- **Destination colour** in the View menu: no colour, **tinted (the default)**,
  left stripe, or a swatch of the destination node. Applies wherever a DID shows
  its destination \u2014 the port rows, the destination line and the detail block.
- **Colour the wires**, a toggle: each wire takes its destination's colour
  instead of one grey. Off by default. Arrowheads are minted per colour, since
  a marker cannot reliably inherit its line's stroke. After-hours wires keep
  their amber, because that colour means something and a destination hint must
  not overwrite it.
### Note
- The palette holds six colours for nine types: `ivr`, `dg` and `vm` share one
  green. Colour is a hint, not an identifier \u2014 the label stays precise. Giving
  them distinct colours would disagree with the Map Creator's own output.

## [0.47.1]
### Changed
- "Destination and hours" now writes into the port rows rather than adding two
  pills above them. The pills were inset 16px against the rows' 12px, so they
  never lined up; those rows already mean "routes to" and "closed", so putting
  the destination in them removes a duplicate instead of aligning one. It also
  costs no height, which matters now auto-fit rescales for taller nodes.
  Renamed to **On both rows**. An unresolvable destination reddens the label.

## [0.47.0]
### Added
- **DID destinations on the node.** A DID said its number, tenant and trunk but
  never where it went \u2014 the wire was the only answer, which does not scale to
  forty DIDs. **View \u203a DID destinations** offers five modes: nothing, a
  destination line, on the routes-to row, **full detail (the default)**, or
  destination plus after-hours. Full detail shows the first hop, the
  after-hours path, the hours and how many objects the DID reaches.
- Per node, an **i** button overrides the menu either way, so one DID can be
  opened up on an otherwise quiet canvas, or closed on a detailed one.
- An unrouted DID, a destination that does not exist, a gate with no closed
  path and a DID reaching nothing all show in red.

## [0.46.0]
### Added
- **Timeout destinations on queues and ERGs**: a `t/o` port on the node, a field
  in the Inspector, importable from CSV, carried through renumbering, and shown
  in the traced preview. The ERG sheet gains a trailing Timeout column the
  mapper ignores. The Queues sheet deliberately does not: the mapper reads
  member pairs from column E to the end of the row, so a trailing cell comes
  back as a phantom agent \u2014 caught by round-trip. A queue's timeout travels in
  the project file and the CSV instead.
### Changed
- The dial group's no-answer port is labelled `t/o` like every other timeout;
  it was always PBXware's Last Destination.

## [0.45.0]
### Fixed
- IVRs showed **two `t/o` rows** for the one timeout port: `portsFor` emitted it
  as a big-port row while the key grid rendered its own. It is a key port now,
  so only the grid row remains \u2014 still always visible.
### Added
- **A standing Closed port on IVRs, ring groups and queues.** Wiring it is how
  an after-hours path is made: the Operation Times gate is created by the wire
  itself. Clearing the wire removes a gate that holds nothing else, so an
  accidental connection fully undoes; a gate carrying a schedule survives.
  Other types still show Closed once a \u23f1 gate exists, as before.

## [0.44.0]
### Added
- **Auto-fit.** The workspace now rescales itself to the space it has: resize
  the window or the Confluence iframe, fold or move the panel, toggle Expand,
  or switch DID tab, and the flow refits \u2014 up to 175%, so a small flow on a
  large screen does not balloon. Zooming by hand is a takeover and switches it
  off, visibly, in the View menu; ticking it back on or pressing Fit resumes.
  The choice is saved with the project.

## [0.43.0]
### Added
- Downloads now work from inside an embed. A sandboxed iframe (Confluence's
  macro) is allowed to swallow programmatic downloads silently, and nothing in
  the page can override that. Framed, every download now opens a dialog of
  routes that survive it: a direct save link, open in a new tab, copy the
  contents for text formats, and **Open the full app**, which hands the whole
  project to a top-level tab \u2014 via storage when available, in the URL itself
  when not \u2014 where nothing blocks the save.
### Changed
- Project adoption is one function shared by Open, the embed hand-off and the
  URL restore, so all three normalise a file the same way.

## [0.42.1]\n### Fixed\n- `safeName` left non-ASCII characters in filenames, so a project called\n  "Bridgeway Dental \u2014 main line" produced a file with an em dash in its name.\n  The download attribute is handed straight to the operating system, and a name\n  it will not accept fails silently. Names are now normalised to ASCII, with\n  dashes folded to hyphens, and a name that reduces to nothing falls back to\n  `call_flow` instead of to a bare separator.\n\n## [0.42.0]
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
