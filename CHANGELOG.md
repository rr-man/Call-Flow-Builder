# Changelog — PBXware Call Flow Builder

Versions below cover the work recorded in this build; entries before 0.22 were
not kept in-app and are not reconstructed here.

## [0.110.0] - 2026-09-01
### Changed
- **The Expand button pops all the time now.** The ⤢ button wears the loud
  amber in its normal state too, not just while the view is expanded — the
  same treatment either way, with the short pulse still marking the moment
  the full-window view engages.

## [0.109.0] - 2026-09-01
### Changed
- **The Exit button pops while the view is expanded.** In the full-window
  work area the ⤢ button now turns solid amber with a short pulse as it
  engages, so the way back out is findable at a glance (the pulse respects
  the system's reduced-motion setting). It returns to its quiet style on
  exit.

## [0.108.0] - 2026-09-01
### Changed
- **Expand also folds the side panel.** Filling the window with the work area
  now collapses the Upload/Inspector/Notes/AI panel to its rail so the canvas
  really gets the whole window — and Exit puts the panel back the way it was.
  A panel you had collapsed beforehand stays collapsed, and the rail's Panel
  button still opens it inside the expanded view.

## [0.107.0] - 2026-09-01
### Changed
- **The theme switch is an icon at the far right.** The Dark/Light button
  moves past the title and version to the banner's outer edge and shows just
  the moon/sun glyph — the tooltip and a screen-reader label still say what it
  does. In the left group, Canvas/Forms now sits to the right of New (File,
  View, New, Canvas/Forms).

## [0.106.0] - 2026-09-01
### Fixed
- **Only one banner menu opens at a time.** Clicking File while the View menu
  was open (or the reverse) left both panels showing on top of each other;
  opening either now closes the other first.

## [0.105.0] - 2026-09-01
### Fixed
- **The File and View menus no longer open off-screen.** With the buttons on
  the left (0.104.0), both dropdowns still hung from their button's right
  edge and ran past the window's left border. A menu now anchors to whichever
  side keeps it on screen: left edge while its group sits on the left, right
  edge when the side toggle moves the group right.

## [0.104.0] - 2026-09-01
### Changed
- **The banner buttons are regrouped.** Left of the name: **File**, then
  **View**, then Canvas/Forms, then New. Right of the name, beside the title
  and version: **Sample flow** — now on an amber-outlined field so it stands
  out — and the **Dark/Light** switch, with the version chip outermost. The
  side toggle and the pinned logo behave as before.

## [0.103.0] - 2026-09-01
### Changed
- **The empty name field now reads "Project Name"** instead of "Name this
  flow" — plainer about what the centred banner field is.

## [0.102.0] - 2026-09-01
### Changed
- **The logo is pinned to the far left.** The coeo mark no longer moves with
  the side toggle: it holds the banner's left corner in both layouts, while
  **Buttons on the right** now swaps just the buttons and the title/version
  block — those two still never share a side.

## [0.101.0] - 2026-09-01
### Changed
- **The buttons sit on the left now, and the ends of the top bar can swap.**
  Canvas/Forms, Dark, New, Sample flow, View and File move to the left of the
  banner by default, with the logo and version on the right and the project
  name still centred between them. A new View option — **Buttons on the
  right** — swaps the two ends in one click; the logo/version block always
  takes the opposite side, and the choice is saved with the project.

## [0.100.0] - 2026-09-01
### Changed
- **The project name is centred in the banner.** The headline name now sits in
  the middle of the top bar — the logo and tool title on the left, the controls
  on the right — with the text centred in its field. Same click-to-rename
  field, amber edge and tab-title behaviour as 0.99.0.

## [0.99.0] - 2026-09-01
### Changed
- **The project name is the headline now.** The name moves to the front of the
  banner, right after the logo, set large with its amber edge — the tool's own
  title steps back to a small label over the version chip. The browser tab
  carries the name too, so a flow can be found among open tabs. Same
  click-to-rename field, same dashed hint while unnamed.

## [0.98.0] - 2026-09-01
### Added
- **An Operation Hours filter.** The View menu gains **Only Operation Hours**:
  the canvas keeps just the DIDs and local destinations that carry a ⏱ gate —
  the after-hours picture on its own, across every type. It changes the view
  only (export, findings and the traced map still see the whole flow), it is
  saved with the project, and turning it on with no gates in the flow explains
  itself instead of blanking the canvas.

## [0.97.0] - 2026-09-01
### Added
- **Operation Times are editable on the canvas — the oldest open item.** The ⏱
  badge now opens an editor instead of blind-toggling the gate: **Open Days
  rows** exactly like the PBX's own screen — day chips plus time-from/-to, with
  as many windows as the line needs (say 08:00–23:59 weekdays plus a 00:00–02:00
  night window) — and the **after-hours destination** picked from the flow's own
  destinations, with the voicemail flag. Removing a gate moved into the editor,
  behind a confirmation. Existing gates migrate their old one-line schedule into
  the first row automatically, and the ⏱ tooltip now shows the hours at a
  glance.
- **The workbook carries every window.** The Operation Hours sheet writes one
  row per open window (number, type and after-hours destination repeated) — the
  multi-row form the template's Read me always sanctioned; single-window gates
  export byte-identically to before.
### Fixed
- **A gate created by wiring the closed port can now be a voicemail gate** — it
  used to be written with a dead `vm` key instead of `isVm`, so the voicemail
  flag silently never applied to wire-created gates.

## [0.96.0] - 2026-08-31
### Changed
- **DID numbers take E.164 and 10-digit dialing everywhere, stored one way.**
  The CSV import always stripped punctuation, but the inspector form stored
  whatever was typed — a `+13125550100` entered by hand could never match, route
  or push, silently. Both paths now normalise to the same digit-only form, so
  `+1 (312) 555-0100`, `13125550100` and `3125550100` are one number; the same
  number in two spellings dedupes on import instead of duplicating; the template
  ships an E.164 example row; and import now caps a DID at 15 digits (the push
  limit) with a clear reason instead of accepting numbers that could never be
  pushed.
### Added
- **A finding when local numbers are mixed lengths.** Every local destination —
  extensions, voicemail, conferences, IVRs, dial groups, queues, ERGs — must
  share one number length (a PBXware tenant has a single fixed ext_length);
  **agents are exempt**. Mixed lengths now raise a finding that groups the flow
  by length and names the odd ones out with jump links. The sample flow was
  brought into line (the practice-briefing conference is now 6400).

## [0.95.0] - 2026-08-31
### Fixed
- **The Align (Row / Column) buttons show when they are usable.** They looked
  identical whether or not anything was selected, so with an empty or
  single-node selection a click only produced a hint that was easy to miss —
  reading as "alignment does not work". The buttons now grey out until two or
  more nodes are selected and light the moment a box-drag or Shift-click makes a
  real selection. The behaviour itself was verified working end to end through
  real event paths: three Shift-clicks then Row put all three on one row (grid
  positions 22/242/462), Column mirrored, the marquee selected all twenty sample
  nodes, and zero errors were raised.

## [0.94.0] - 2026-08-31
### Changed
- **The layout buttons are named what they are: Orientation.** ⇄ Horizontal and
  ⇅ Vertical re-lay the whole flow by call stage — they never aligned anything —
  so the group label now says Orientation.
### Added
- **A real Align, for the selection.** Select two or more nodes (box-drag or
  Shift-click), then **Row** makes their vertical positions the same — one row —
  and **Column** makes their horizontal positions the same — one column. The
  anchor is the topmost / leftmost node, snapped to the grid; nodes that would
  collide on the new line are packed apart in grid steps with their order kept,
  so an overlap is impossible and everything stays on the same lattice as
  dragging. Routing is never touched. With fewer than two nodes selected the
  buttons explain how to select instead of doing nothing.

## [0.93.0] - 2026-08-31
### Fixed
- **Align now snaps to the grid.** Aligned nodes used to land on arbitrary
  pixel positions even with the View menu's snap guard on, so an aligned node
  and a hand-dragged one lived on different lattices and never quite lined up.
  Align's final placement now goes through the same snap as dragging (guard
  honoured — with snap off it stays plain rounding), and a snapped neighbour
  that rounds too close is bumped along in grid steps, so spacing keeps a
  readable floor and an overlap stays impossible whatever the rounding. Proven
  on the sample flow and a 56-node dense flow in both directions: every node on
  the 22px grid, zero overlaps, the four call-stage columns intact — and the
  sample flow is verified working under all the recent changes, in the real DOM.

## [0.92.0] - 2026-08-31
### Changed
- **After the test upload, continue in batches or go full auto.** The review
  gate now offers three ways forward. **Upload next batch** sends just the next
  tier — ① extensions, then ② ring groups/ERGs, then ③ IVRs, then ④ DIDs — and
  pauses again after each with "*batch* updated — N created and verified", so a
  big flow lands one confirmed section at a time until everything is complete.
  **Upload all remaining — auto** sends everything still waiting in one go;
  refusals are collected rather than fatal, and the run ends with a report that
  names **what was NOT uploaded** — every refused object with the PBX's own
  reason (duplicates called out as such), anything created but not visible on
  re-read, plus the standing never-attempted items (duplicates already on the
  PBX, types the API cannot create). **Stop here** still keeps what has been
  verified and sends nothing more. Every batch is verified against a fresh read
  of the PBX before the next is offered.
- The test runner now awaits asynchronous tests — a rejected async expectation
  fails the run instead of passing silently — and the harness can lift `async`
  functions, so the live-run machinery itself (`pbxRunOps`, batch collection) is
  under test for the first time.

## [0.91.0] - 2026-08-31
### Changed
- **The upload order is now tiered, and DIDs go truly last.** A push (and its
  test upload) follows the sequence a call depends on: **① extensions** first
  (agents and conference bridges belong to this tier, but the PBXware API has no
  add action for them, so they are skipped, not reordered) → **② ring groups and
  ERGs** (queues likewise API-less) → **③ IVRs** → **④ DIDs last**. DIDs used to
  sit third — harmless while IVRs could not be pushed, but wrong the day they
  can. The order is now shown in the dialog above the plan, the emitted script's
  header says the same, and the suite asserts each tier precedes the next with
  DIDs pinned to the final slot.

## [0.90.0] - 2026-08-31
### Changed
- **A live push is now canary-first, with a review gate before the rest.** The
  run starts by creating exactly **one of each selected type — a test extension,
  a test group, a test DID — in dependency order**, then re-reads the PBX and
  verifies each actually landed. Anything not visible on re-read (or a list that
  cannot be re-read) stops the run with nothing else sent. When the test upload
  verifies, the dialog **pauses on a review section** — what was created and
  verified, and what is still waiting, per type with numbers — and asks:
  **Create the rest** or **Stop here** (keeping only the test objects). Only the
  operator's click sends the remainder. A selection of one-per-type skips the
  review; there is nothing left to ask about.
- **Duplicates alarm by name and are never pushed.** Objects already on the PBX
  now appear in a loud **“Needs attention — already on the PBX”** block naming
  every number per type (and the preflight warn names them too) instead of a
  bare count. Behaviour is unchanged — they were never pushed — but now they
  demand a look. A collision the PBX only reveals at create time (“number
  reserved by…”) is likewise classified **Duplicate on the PBX — needs
  attention**, with what to do about it, rather than a raw error string.
- **The digit-length check always answers.** It already validated every local
  type's numbers (extensions, dial groups, IVRs, ERGs — DIDs exempt as full
  numbers) against the tenant's real `ext_length`; but when the tenant was never
  resolved it said nothing. It now reports a visible warning — “digit length
  could not be verified — run Test connection” — so pass, fail, or
  cannot-verify, there is always a verdict.

## [0.89.0] - 2026-08-31
### Changed
- **The Standalone and MLT buttons light up while their PBX is the target.** In
  both the Fetch and Push dialogs, the button whose host the Server fields point
  at now shows a lit state (navy fill with a ring), and it follows the fields
  live — click MLT and it lights, retype the host by hand and both dim. Matched
  on the host alone, so editing the tenant does not un-light it. Which box you
  are about to talk to is now readable at a glance.

## [0.88.0] - 2026-08-31
### Changed
- **The canvas has a real dark palette.** The per-type node colours (tinted
  destination rows, key rows, swatches, wire tints, the View menu's type chips)
  were light-theme pastels injected inline, so dark mode drew pale `#e4f5f7`-style
  rows glaring inside dark nodes. A dark counterpart table now mirrors the dark
  theme's own family tokens — dark fills a step off the node colour, luminous
  inks, wire accents that stay visible on the dark canvas — and the canvas reads
  whichever table matches the live theme, including a dark PNG export. Every
  dark ink-on-fill pair measures ≥8:1 and every wire accent ≥3:1 on the canvas
  (`tests/contrast.test.js` now computes both tables); light mode is untouched,
  byte for byte the same colours as before.

## [0.87.0] - 2026-08-31
### Added
- **Conference CSV import, completed.** The importer spec for conferences existed
  but was never wired in: no upload section, no sample link, and a template whose
  `number,name` header nothing could recognise — so `conference_template.csv`
  could not import anywhere. The Upload panel now has a Conferences section with
  a drop zone and template link, the sample carries a distinctive
  `conference_number` header the type-sniffer detects, and the shipped template
  was regenerated from the app.
### Fixed
- **A failed direct-route Test connection explains itself again.** `pbxProbe` —
  the diagnostic that tells "blocked by CORS" from "unreachable" from mixed
  content, each with its fix — was left uncalled by the push rework, so a
  direct-route failure said only "Not connected". Both Test connections now run
  it when the direct route fails and append its finding.
- **Dead code removed:** `pbxCurlTest` (the copy-a-CORS-check button's helper,
  feature removed in 0.80.0) and `pbxRedact` (nothing displays a URL carrying a
  key any more). With `pbxProbe` wired, both fetch sites CLAUDE.md invariant 1
  documents are live again, and the suite's five recorded defects are all closed.
### Added
- **Contrast is now computed, not promised.** `tests/contrast.test.js` derives
  every normal-text pairing from the CSS tokens in both themes and asserts WCAG
  AA; the true weakest pair is 4.76:1. The headless click-through also proves the
  project library round-trip (save → read back) when an IndexedDB shim is present.

## [0.86.0] - 2026-08-31
### Fixed
- **The emitted push script now declares the server id it actually sends, and
  refuses to hide an unresolved tenant.** `pbxServerId()` is the single source of
  the `server=` value — the resolved internal id on a multi-tenant PBX, never the
  tenant code — used by both the live push and the emitted `.sh`. The script's
  `SERVER=` line and header used to show the typed code (or blank) while every
  request sent something else; they now agree, and when a multi-tenant code was
  never resolved the emitter writes a loud warning and drops the bad `server=`
  rather than sending the code, which PBXware only answers with "invalid server id".
- **A multi-tenant PBX whose host name contains "pbx" is no longer mislabelled
  "Standalone".** The banner and status now decide standalone vs multi-tenant from
  the tenant field, not the host name, so a typed tenant code is always shown as a
  tenant.
- **ERG and Queue CSVs are no longer misread as IVR.** `sniffKind` treated a
  `timeout` column as an IVR tell, but queues and ERGs carry one too, so dropping a
  queue or ERG file onto the canvas detected it as an IVR. IVR is now told by its
  key columns, and the more specific queue/ERG tells are checked first.
### Added
- **A verification harness so a run is provably checked.** `node tests/run.js` now
  also covers the templates (the twelve-sheet workbook and its load-bearing IVR /
  Queues columns, a drift check against the shipped `.xlsx`, and every `.csv`
  against the importer), the project library (a saved record can never hold a key),
  and the `server=` API shape. `tests/live_verify.sh` checks the real API read-only
  on both a standalone and a multi-tenant PBX — tenant resolve, `ext_length`, and
  every readable type — with an opt-in single-create write smoke. `docs/VERIFY.md`
  is the one-page guide.

## [0.85.0] - 2026-08-31
### Added
- **A project library — saved projects, offline, in the browser.** File ▸ Project
  library keeps named projects in the browser (IndexedDB), so you no longer have to
  download, name and reopen loose `.json` files by hand. Save the current flow under
  a name; reopen, rename, duplicate or delete any saved project; and a **Last
  session** entry autosaves the current flow as you work, so a reload or crash
  loses nothing. It is offline and browser-local — no server, never shared between
  machines — so **File ▸ Save `.json` stays the portable, permanent copy** and the
  way to move a project to another computer. A saved record is exactly what
  `docForSave()` writes, so it can never hold an API key. Where a browser blocks
  local storage (a Confluence frame, a private window) the library says so and
  Save/Open `.json` works exactly as before.

## [0.84.0] - 2026-08-20
### Added
- **A QA layer over Fetch and Push, so a run is provably checked.** Fetch now
  shows a **Fetch QA** block after reading: per type it names the rows the parser
  dropped, duplicate numbers in the reply, records with no name, and any route
  that points at a number nowhere in the fetch or the flow — the silent data loss
  is silent no longer, and the read-nothing types (voicemail, conference, queue,
  agent) are listed with their reason. Push now leads its plan with a
  **preflight verdict**: a ✓/!/✗ line for every check — connected, tenant
  resolved, capability per type, **digit length against the tenant's real
  `ext_length`**, existing objects (reviewed, never edited), and **route
  correctness** (every destination must already be on the PBX or be created in the
  same run, extensions → ring groups → DIDs last) — each failure carrying its fix.
  A hard ✗ disables the Create button on top of the existing per-type guardrail.
  All the checks are pure functions with headless tests on both a standalone and a
  multi-tenant fixture, and a new `diagrams/pbxware_pbx_sync_flowchart.mermaid`
  shows the Fetch (read) and Push (write) paths side by side.

## [0.83.0] - 2026-08-20
### Changed
- **A type the push cannot create now says whose problem that is.** "The API
  refused this — no add action, or the key is not permitted" covered two
  different situations with two different owners, and sent people to the wrong
  one. The capability list now keeps the PBX's own words: when the refusal is
  `Selected action not allowed` it says the action exists and this key's
  whitelist does not include it, and names where an admin grants it (Settings ▸
  Admin Settings ▸ API). Any other refusal is quoted verbatim instead of
  paraphrased. Which limit gets named matters as much as the wording: an IVR or
  an ERG cannot be built into a flat request whatever the key says, so those rows
  lead with that and state outright that granting the action would not help —
  rather than sending someone to an admin to widen a key that was never the
  problem.
- **The extension payload is re-confirmed against the live test PBX, and the way
  it was confirmed is now written down.** All seven required defaults were
  checked without creating anything: sent against an extension number that
  already exists, so a payload that validates fails on "number 100 is reserved"
  rather than making an extension, while dropping any one field answers
  `Required field '<name>' is missing`. None of the seven is optional.
- **Recorded the trap in `pbxware.ext.configuration`.** It returns the *stored*
  shape, where `ua`, `secret`, both call limits and `voicemail` sit nested under
  `options` — but `ext.add` takes the whole set flat and maps them itself.
  Rewriting the flat defaults to match a `configuration` reply looks like a
  correction and breaks every create, so the code now says so where someone
  would try it.
- Probing the standalone test PBX also established what its key may actually do:
  the five list actions plus `ext.add` and `ext.configuration`. `did.add`,
  `ring_group.add`, `tenant.list`, `queue.list` and every `.edit` come back
  `Selected action not allowed`, so DIDs and ring groups are wired but not
  pushable with that key until an admin widens it. The dialog has always probed
  this per connection; what changed is that it now explains the answer.

## [0.82.0] - 2026-08-20
### Added
- **The push works out what actually needs pushing, and pushes what you tick.**
  Test connection now builds a plan for the whole flow instead of counting
  extensions: it asks the API which types this key may create, reads back what
  the tenant already has for each of them, and reports every object in one list —
  with a checkbox each for the ones it can create, and everything that would not
  be created accounted for beside them. Extensions, DIDs and ring groups are
  wired; which of them a given key may actually use is probed, never assumed. Tick and untick
  across types, then Push sends exactly the ticks, extensions first, then the
  groups that ring them, then the numbers that point at either — a DID cannot be
  aimed at a destination the same run has not created yet.
- **Nothing is created blind.** A type whose list action the key cannot read is
  reported as unchecked and is not offered, because with nothing to compare
  against every object in the flow looks new and a push would duplicate what is
  already on the PBX. The same refusal covers a number shared with another object
  and a DID that appears twice.
- **Types that can never be pushed now say so.** Queues, agents, conferences,
  voicemail and operation-times gates are named in the dialog with the reason —
  no add action in the API, or no editable surface here yet — rather than being
  quietly missing. IVRs and ERGs sit in between: the API would take them, but
  their keymap and member list are nested and no flat request for them has been
  confirmed, so they are counted and named and no request is invented.
- **The two emitters have buttons again.** Request URLs `.txt` and Script `.sh`
  write out the ticked requests, aimed straight at the PBX and never through the
  proxy, with no network involved. On the `file://` route, where the reply to a
  request that did take effect may be unreadable, that is still the honest path —
  and for a type whose parameters are unconfirmed it is how you run one by hand
  before pushing many.
- **Checked against real replies from the test PBX, not just the docs.** The
  destination a DID is given now uses PBXware's own wording, which is
  inconsistent on purpose to nobody: a live `did.list` reply carries "Extension"
  singular beside "Queues" and "Conferences" plural, and sending the tidy form
  lands the DID on no destination at all. A ring group now also carries
  `last_dest_vm`, present in every real row and absent from this builder's
  fields, derived from whether its final destination is one of the flow's own
  mailboxes — wrong either way sends the overflow somewhere that never answers.
- **A DID whose trunk is a name rather than an id is flagged before the run.**
  Every trunk in a real reply is a numeric id; the builder's trunk field is free
  text people fill in with a name. That is a warning on the plan and not a
  refusal — it may well be accepted — but the run stops on the first request the
  PBX rejects, and hearing about it beforehand is worth more than afterwards.
### Changed
- **Extensions are the only type whose request set is confirmed against a live
  PBX.** DIDs and ring groups are marked *unconfirmed* on their row and in the
  confirmation prompt: the parameter names come from what the matching list
  action returns, not from a create that worked. A wrong guess stops the run on
  the first request rather than half way through.
- The credentials `.csv` covers extensions only, since nothing else has a
  generated secret, and the progress line, the confirmation and the emitted
  script now all name the tally the same way — "2 extensions, 1 DID" — so the
  three cannot disagree about what a run is about to do.

## [0.81.0] - 2026-08-19
### Added
- **Voice AI agents, associated to a client.** The AI panel tab is now live. Each
  voice AI agent belongs to a client — the same client a DID names in its tenant
  field — and the tab lists only the selected client's agents, so you see just the
  ones that client has access to. Pick a client, add or remove its agents, and it
  all travels in the project `.json` (which never carries a key). The client list
  is drawn from the DIDs plus any client already on an agent; the sample flow now
  ships two agents for Bridgeway. The app already defaults to light mode.

## [0.80.0] - 2026-08-19
### Changed
- **Push to PBXware, reworked to match Fetch, with real guardrails.** The dialog
  now has the same target controls as Fetch — **Standalone** and **MLT** buttons,
  the tenant-name banner, and one **Test connection** that confirms the tenant and
  reads the existing extensions in a single step (on a multi-tenant PBX the tenant
  code is resolved to the internal `server=` id, exactly as Fetch does).
- **New "What can be pushed" test.** Test connection probes each type's add action
  and reports what this key and tenant will actually accept — Extensions, DIDs,
  ring groups, ERGs and IVRs each marked can-create or refused. On the test PBXes
  only extension creation is allowed; the rest have no add action for these keys.
- **Guardrails against an accidental push.** Nothing writes unless the connection
  tested clean, the capability check says extensions are creatable, and there is
  something new to create — and then an explicit confirmation names the count and
  the exact tenant before anything is sent. The server-side proxy is also
  read-only by default, so a push is refused until writes are deliberately turned
  on, and the dialog says so plainly.
- **Simplified.** Removed the CORS-test button, the phone-type (ua) mapping, the
  paste/assume-empty inputs and the emit-URLs/shell-script section — a create
  needs none of them. Push now creates extensions only (the one write the API
  allows) and never edits or deletes. Each new extension is created with a
  generated, policy-compliant SIP secret and PIN, offered as a one-time
  credentials download after the push so a handset can register.

## [0.79.0] - 2026-08-19
### Fixed
- **A standalone PBX is named as one, not "tenant 1".** A host with *pbx* in its
  name is a single standalone phone PBX, not a multi-tenant system, so the
  connection banner now reads **Standalone PBX** with the host beneath it and a
  handset glyph — where it used to mislabel it *tenant 1 · tenant 1*. A real
  multi-tenant sub-tenant still shows its name, code and server id with a building
  glyph. The connection status line matches the same wording.

## [0.78.0] - 2026-08-19
### Changed
- **The sub-tenant name now shows in a tinted banner, not a small line.** When a
  tenant is resolved — or the moment MLT is picked — its name is drawn in an
  accent-tinted banner under the Connection heading (a building glyph, the name
  in bold, and *tenant 202 · server 169* beneath), so which tenant a fetch will
  read from is unmissable. The small connection line beside Test connection now
  carries only the route/host. The banner hides on a single-tenant PBX and when
  Standalone is picked.

## [0.77.0] - 2026-08-19
### Changed
- **The MLT button names the sub-tenant the moment it is picked.** Clicking MLT
  now shows *tenant 202 — Rons Tenant* in the connection line straight away,
  rather than only once the test has resolved it. A successful test then re-states
  it with the internal `server=` id it mapped to.

## [0.76.0] - 2026-08-19
### Added
- **One-click test server buttons in the Fetch dialog: Standalone and MLT.** The
  old single **Defaults** button is now two. **Standalone** fills the single-tenant
  test box (tst-pbx-01) and **MLT** fills the multi-tenant one (tst-mlt-01,
  tenant 202 — Rons Tenant); both test the connection straight away. MLT also
  clears the API-key field, so when the page is served by the proxy the right key
  is supplied server-side by host — nothing to paste to try a multi-tenant fetch.

## [0.75.0] - 2026-08-19
### Added
- **Fetch works against a multi-tenant PBX, by tenant code.** On a multi-tenant
  PBXware the API's `server=` wants the tenant's internal id, not the tenant code
  an operator knows it by — `server=202` is rejected where `server=169` works.
  Test connection now reads `pbxware.tenant.list` first, maps the code you type
  to the internal id, and shows the sub-tenant's name before anything is read
  (e.g. *tenant 202 — Rons Tenant*); every subsequent fetch sends the resolved
  id. If the key is not allowed `tenant.list`, or the code is not found, it falls
  back to sending exactly what you typed, so a single-tenant PBX is unchanged.
  Confirmed on the test multi-tenant box: extensions, DIDs, ring groups, ERGs and
  IVRs fetch; conferences, voicemail, queues and agents have no read action there
  either, the same as on a standalone PBX.

## [0.74.0] - 2026-08-19
### Fixed
- **IVR key rows show their port dot again when destination names are on.** With
  names shown, each menu key renders as the wider `krow2` row, but the dot's
  size, border and fill were only styled for the plain key row — so the dot was
  there and draggable but invisible, and a wire appeared to leave from nothing.
  The dot now draws on every key row, including the timeout, and keeps its green
  fill when the key is routed. The port itself never changed; only its styling
  was missing.

## [0.73.0] - 2026-08-19
### Added
- **Select several nodes and move them together.** Drag a box on empty canvas to
  rubber-band everything it touches, or Shift/Ctrl/Cmd-click node headers to add
  and remove them from the selection. Dragging any selected node then moves the
  whole group, keeping their relative spacing and snapping to the grid. A plain
  click or Esc clears the selection; clicking a single selected node drops back
  to just that one. The box only ever picks up nodes that are actually on the
  canvas, so a hidden or filtered destination is never scooped into a move you
  cannot see.

## [0.72.0] - 2026-08-19
### Fixed
- **The footer credits line up.** The "Created by" and "Contributor" labels were
  baseline-aligned and sat slightly off the LinkedIn mark and the name beside
  them; each credit is now a centred row, so the label, the logo and the name
  share one line.

## [0.71.0] - 2026-08-19
### Changed
- **Align now columns by call stage, not traced depth.** The layout bands a node
  by its type — DID, then IVR, then ring group / dial group / queue, then the
  endpoints (extension, agent, conference, voicemail) — so the columns always
  read in the order a call travels, however the flow was wired. Before, a DID
  that dialled an ERG or an extension directly dropped that destination into a
  shallow column beside the IVRs; now it sits in its own stage's column. An
  unrouted destination lands in its type's column beside its kind, rather than
  being parked off on its own. The sample flow loads straight into this shape.

## [0.70.0] - 2026-08-19
### Added
- **The canvas image export has a Tidy option.** Alongside Context, Theme,
  Background and Size, the PNG dialog now offers **As placed** (the default —
  export the nodes exactly where you put them), **Tidy ⇄** and **Tidy ⇅**. Tidy
  lays the flow out by call depth for that one image and then puts the canvas
  back exactly as it was, so you get a clean pipeline picture without disturbing
  a layout you have arranged by hand. It applies to every scope in the export,
  including a whole-flow .zip and copy-to-clipboard.

## [0.69.0] - 2026-08-19
### Changed
- **Align now lays the flow out as a clean pipeline instead of stacked columns.**
  The layout keeps its call-depth bands — DID, then IVR, then ring group / dial
  group / queue, then the extensions, agents, conferences and mailboxes they
  reach — but within each band it now orders nodes by where their wires go
  (barycentre crossing reduction) and then slides each node toward the centre of
  what it connects to. A straight chain draws as one straight line, and on a busy
  flow the crossing wires drop by roughly two thirds. Nothing about routing
  changes — only positions — and Horizontal and Vertical both use it.

## [0.68.0] - 2026-08-18
### Changed
- **Each type group in the Fetch checklist has a header checkbox.** Click it to
  select or clear that whole type — Extensions, DIDs, and so on — in one move,
  with an indeterminate (–) state when only some of its rows are ticked. It
  stays in step with the individual row checkboxes both ways, and toggles only
  the rows the current filter shows. The per-group all/none links remain as a
  secondary.

## [0.67.0] - 2026-08-18
### Changed
- **The Fetch window now curates a selection across every destination type
  before importing.** A **Fetch all** button reads every fetchable type in one
  pass (single-type buttons still work and accumulate), and the preview becomes
  one checklist grouped by type with per-group and global select-all/none. A
  filter row narrows it — a search box over number and name, and **All / New /
  Changes** chips — so large sets can be picked without ticking each row.
  Importing opens a **consolidated review**: a per-type summary of what will be
  created and updated, confirmed before anything lands, and the selected objects
  are imported endpoints-first (extensions, dial groups, ERGs, then IVRs, then
  DIDs) so routing resolves as it arrives. Nothing is ever deleted.

## [0.66.0] - 2026-08-18
### Added
- **View ▸ Hide unrouted destinations.** A new checkbox in the Routing view
  section drops every object nothing routes to from the canvas — the same set
  the Unrouted tab isolates, hidden instead of shown. DIDs are sources and are
  never hidden. It is a canvas view only: the export, the findings and the
  traced map still see every object. The choice is saved with the project.

## [0.65.0] - 2026-08-18
### Added
- **Fetch now covers DIDs, IVRs, dial groups and ERGs — not just extensions —
  and flags the types that cannot be fetched at all.** The Fetch dialog offers a
  button per fetchable type; each reads its list action through the proxy and
  merges by number with the same tick-to-select, create/update, never-delete
  contract as the extensions import. DID destinations, IVR key maps, ring-group
  members and ERG members come across mapped to this builder's fields — a PBX
  ERG's full member list and strategy are preserved on the object even though the
  builder's ERG form edits a single ringing extension, so nothing is lost.
  Voicemail, conferences, queues and agents are shown **flagged as not
  fetchable** rather than omitted: the PBXware API — legacy `index.php` and the
  v2 REST API alike — has no read action for those four, confirmed against
  Bicom's own collection and by probing the live server, so they can only be
  added by hand. Verified against a live tenant: 67 extensions, 15 DIDs, 16
  IVRs, 31 dial groups, 2 ERGs.

## [0.64.0] - 2026-08-18
### Changed
- **Save/export consolidated into the File menu.** The blank-template download,
  which only lived in the Upload panel, is now a File-menu item beside Export
  `.xlsx`, and the duplicate "This flow" workbook button — the same action as
  Export — is removed from the Upload panel. The panel's workbook card becomes a
  focused "Blank template" card for the download-fill-import path, and points at
  File ▸ Export for saving the current flow.

## [0.63.0] - 2026-08-18
### Changed
- **The Push dialog now matches the Fetch dialog.** Its target section is a
  single Host field with the same one-click **Defaults** button and a Tenant
  field — the https/http toggle and the tenant **Resolve** button are gone, since
  the proxy handles the scheme and `tenant.list` is refused to a read/write-scoped
  key anyway. **Test connection now probes with `pbxware.ext.list`**, the action
  such a key is actually allowed, instead of `tenant.list`; a scoped key that can
  push was previously stuck at "not connected", so live push never unlocked. Like
  Fetch, it prefers the same-origin proxy and reports how many extensions the key
  can read.

## [0.62.0] - 2026-08-18
### Added
- **Fetch from PBXware.** A new File-menu entry reads objects from a tenant and
  merges them into the flow, the reverse of the push. It matches by number: new
  numbers are created, existing ones have their non-empty fields updated, and
  nothing is ever deleted — the same safe contract as the CSV importers. The
  preview lists every fetched object with a checkbox, plus Select all / None, so
  only the ticked rows are imported; rows that already match are shown greyed and
  cannot be ticked. It runs through the same-origin proxy when the app is served
  by one, so the API key stays on the server and there is no CORS to negotiate.
  **Extensions only for now**, because a scoped API key typically permits
  `pbxware.ext.list` and little else; DIDs, IVRs, dial groups and ERGs are wired
  to slot into the same fetcher registry the moment the key is granted their read
  permissions, each validated through `ACCEPT` before it lands. Verified against a
  live tenant of 67 extensions.
- **Fetch dialog gained Server, Tenant and API-key fields** with a one-click
  **Defaults** button for the test server. Filled fields drive the read through
  the same-origin proxy, which accepts them as host/key overrides of its own
  `.env` and reuses its resolve-IP pin when the host matches — so the firewalled
  public name still reaches the internal address. Blank key means "use the
  server's stored key." The key is held for the tab only, never saved.
- **A same-origin proxy makes both the live read and the live push work without
  CORS.** When the app is served by `cfbuilder-serve`, `/pbx-api` on the page's
  own origin relays to the PBX with the API key injected server-side, so the
  browser never holds the key and there is no cross-origin request to be
  blocked — this is what lets a live push, not just a fetch, run from an ordinary
  browser tab. It accepts the dialog's host/key fields as overrides of its
  `.env`, reusing a resolve-IP pin when the host matches so a firewalled public
  name still reaches the internal address, and it refuses write actions unless
  it was started with `CFB_ALLOW_WRITE=1`.

## [0.61.0] - 2026-08-17
### Added
- **Push extensions to PBXware.** File ▸ Push to PBXware builds the
  `pbxware.ext.add` and `pbxware.ext.edit` requests for the extensions in the
  flow, against a host and tenant you set. It reads what `pbxware.ext.list`
  already holds and shows what it would create, what it would update and what it
  would leave alone, before anything is sent. Extensions the PBX has that this
  flow does not describe are listed and never touched — there is no delete.
- **The requests can always be emitted, with no network at all.** Copy the URLs,
  or download a shell script that reads the key from `$APIKEY` and never contains
  it. That path matters because the API answers a plain GET and sends no CORS
  header, so a page opened from disk or embedded in Confluence can send a request
  and still not be allowed to read the reply. Live push is offered only once a
  test connection proves the reply is readable, and the test says which of the two
  it found — reachable but unreadable, or not reachable — rather than guessing.
- **The API key is typed, or read from a `.env` you pick or drag onto the dialog.**
  Either way it is held in memory for the tab only and never written into the
  project file: Save `.json` and both embed hand-offs now go through one function
  that strips it. A `.env` may also carry `PBXWARE_HOST` and `PBXWARE_TENANT`, so
  the whole target arrives in one go, and the dialog names the file the key came
  from — a stale `.env` otherwise looks identical to a fresh one, and pushing to
  the wrong tenant is the mistake that causes. A file carrying no
  `PBXWARE_API_KEY` changes nothing at all, so dropping the wrong file cannot
  clear a key that is already working. A page cannot read a file path by itself,
  so handing the file over is one deliberate click per session — that buys not
  retyping the key, not invisibility.
- **Generated SIP secrets and PINs, outbound only.** `ext.add` needs both, and
  neither belongs in a project file that gets emailed or carried across tabs in a
  URL, so they are generated per tab and offered as a credentials `.csv`.
  Reloading forgets them, which makes that file the only copy. An edit never
  sends them: rotating the secret of a handset that is already registered would
  take a working phone off the air.
- **When a live push is blocked, the dialog now names the fix.** The API sends no
  CORS header, so a page opened from disk cannot read a reply even though the
  request reached the PBX and took effect. Two ways out, and the dialog says both:
  serve this file from the PBX host, which makes the page same-origin so the rule
  never applies and nothing needs configuring, or add
  `Access-Control-Allow-Origin: *` to the reply for `/index.php` — these are
  simple GETs, so there is no preflight to handle, just that one header. **Copy
  CORS test** hands you a `curl` command that shows whether the header is there,
  and the connection test now recognises and confirms the same-origin case.


### Notes
- Queues, agents and conferences have no add or edit action in the PBXware API,
  so they are never pushed and stay in the workbook. Seven of the ten object
  types here have write actions; extensions are the first to be wired up, as a
  proof of the path.
- A failed request stops the run. Nothing after it is attempted, and the PBX's
  own error text is shown rather than a guess at what it meant — the API reports
  failure as an `error` key inside an HTTP 200, so the body is what gets checked.

## [0.60.0] - 2026-08-04
### Fixed
- **A duplicate landed on top of the original.** The copy took the original's
  coordinates verbatim, so both sat on the same pixel \u2014 the new one invisible
  beneath the old, and an overlap reported that nobody caused. It now goes to the
  first free space to the right, wrapping to the next row down, which keeps a
  copy beside the thing it was copied from, level with it while there is room on
  that row.
- **Duplicate never redrew the canvas.** It refreshed the panel and stopped, so
  the copy was not on screen until something else triggered a draw. The copy is
  now selected, scrolled to and flashed, the same treatment the duplicate-number
  links use.
- A duplicated DID has no number, since one cannot be guessed. The flash now says
  so \u2014 *"Give it a number"* \u2014 rather than leaving a finding to explain it.

## [0.59.3]
### Fixed
- **Licences past the second were silently cut off.** The row could not wrap and
  the value column was 106px; five chips are 256px, so 150px of it simply
  vanished. Worse than an ellipsis, because a clipped chip still looks like a
  whole chip \u2014 which is why it went unnoticed.
- The row now wraps, and an extension widens to 230px at Full detail.
  **Widening alone changed nothing**: at both 190px and 230px the line counts
  were 1, 1, 2, 2, 3. Taking 1px off the chip margin is what moved them to
  1, 1, 1, 2, 2 \u2014 so three licences now sit on one line and five on two.
- The height estimate wraps the chips exactly as the CSS does, so the layout
  guards work from the real height rather than assuming one line.

## [0.59.2]
### Fixed
- **Mobile was invisible and the deeper licences appeared to shout over it.**
  The ramp tinted each chip's fill, and the palest step came out `#eef4fb`,
  byte-identical to `--blue-l`, which is the extension node's own background \u2014
  so the first chip had a contrast of 1.00 against the surface it sat on and the
  second only 1.10. I had measured the ramp against white and against the dark
  canvas, but never against the node it actually renders on.
- The ranking now lives in the **border**. A line only has to be seen, not to
  carry text, so it can range much wider than a fill while one ink stays legible
  on every chip. Every border clears 1.53 to 7.30 against the node in light and
  1.97 to 6.59 in dark, adjacent steps are 52 to 62 apart in RGB, and the ink
  reads 10.91 on every chip instead of sliding from 9.86 down to 5.58.

## [0.59.1]
### Fixed
- The extension detail was unreachable. I recommended it "at Full detail behind
  the i button", then built only the Full detail half \u2014 so a single node had no
  way to show it and switching the whole canvas was the only route. Extensions
  now carry an **i** button, in the header rather than a control strip: a strip
  costs 30px and extensions are the type there are most of. No **S**, because
  "number only" means nothing for an endpoint.
- The sample's extensions had no department, handset or licence, so turning the
  feature on showed four nodes reading *not set*. They now carry realistic
  values, including a softphone and a handset with no licence.

## [0.59.0]
### Added
- **Extensions show their phone and licences at Full detail**: department when
  set, the handset, and a chip per S-NET Connect licence.
- Licence chips use five tints of the extension's own blue, in licence order, so
  the colour carries the same meaning as the position. Five separate hues was
  the obvious idea and the measurements ruled it out \u2014 every candidate sat
  within 31 to 62 of a colour already meaning DID, ERG or queue. A single-hue
  ramp with one text colour failed too: the middle step read 3.15 on white and
  2.74 on dark ink. Light tints clear AA at every step, 9.86 down to 5.58.
- Dark mode gets its own ramp rather than reusing the light one, which measured
  11 to 12 against the dark surface and would have glowed. Every dark step also
  clears AA, 8.65 down to 4.65.
- The handset is a two-state chip \u2014 desk phone or software client \u2014 matched on
  the words people type rather than a list of vendors. Anything unrecognised is
  treated as a handset.
### Note
- Colour is never the only signal: every chip keeps its full name, because a
  9px blue ramp is exactly what a colour-blind reader cannot separate.

## [0.58.0]
### Added
- **Duplicate local destination number** is now visible on the canvas, not only
  in the findings. Both objects get a red edge stripe and their number in red,
  plus the warning icon naming what they clash with. A stripe rather than an
  outline, because the selection ring is also 2px and the two together read as
  one thick smear.
- The finding is renamed to **Duplicate local destination number** and each
  object is a link that selects it, scrolls it into view and flashes it \u2014
  un-hiding its type and switching to the All tab first if need be.
### Fixed
- The check missed **conferences and agents** entirely, and only compared across
  types \u2014 so two queues both on 4001 went unreported. It now covers all eight
  local destination types and same-type clashes.

## [0.57.1]
### Changed
- The project name is now the loudest thing in the banner: wider, 14px bold on a
  lighter field with an amber edge, and the tool's own title stepped back to
  make room for it. The name decides what every file is called, and the fixed
  product name does not change.
- While it is unnamed the field is outlined in dashed amber and reads *Name this
  flow*, so it is obvious before a download turns up called `call_flow`.
- Placeholder text is white at 72%. The lower alphas looked right but measured
  3.25 against the field, below AA.

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
