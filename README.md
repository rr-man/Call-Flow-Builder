# PBXware — Master Inbound Call Flow Map

**Version:** 2.2.4 · 2026-07-13 (version link lives in the HTML banner; Coeo logo in the HTML banner)

A single-file, self-contained visual reference for how inbound calls travel
through PBXware: from the provider trunk, through DID processing and
Operation Times gates, to every local destination type — with the branching
destinations (IVR, Ring/Dial Group, Queue/ERG) fully expanded.

## Files

| File | Purpose |
|---|---|
| `pbxware_master_call_flow.html` | Primary deliverable. Opens on a launcher: view the reference map, or upload exports to map your own system. Open in any browser. Works offline, includes zoom in/out/reset controls, a light/dark mode toggle (light by default) and a clickable "Inherit" explainer and hover tooltips across all five parts. |
| `pbxware_master_call_flow.svg` | The raw diagram. Use for embedding in wikis, printing, or further editing. |

| `README.md` | This file. |
| `CHANGELOG.md` | Revision history. |

## Structure of the map

**Part 1 · DID processing spine** — the seven ordered steps every inbound
call passes through: Provider → Trunk → DID Match → Operation Times gate →
CLI Validation & Routing → DID Range rule → Destination + Value. Side
panels show the Operation Times evaluation priority (Open Days → Custom
Destinations → Closed Dates → Default Destination) and where OT is
configured, including the Server/Tenant inheritance chain.

**Part 2 · Downstream local destinations** — the five destination columns a
DID can hand a call to: IVR, Queue, Ring/Dial Group, Extension,
and Conference/Voicemail. The OT gate repeats in front of every object that
has one (DID, IVR, Queue, Dial Group, ERG); Extension/Multi-User,
Conference, and Voicemail have none. Color coding: green = "Local
destinations" billed from the Service Plan; blue = Extension billed per the DID's E.164 incoming price.

**Part 3 · The IVR node, expanded** — the entry sequence (OT gate, Ringing
Type/Preamble, greeting), all twelve selections (0–9, ✱, #) each with its
own Destination Type + value, the Play Greeting replay counter, and the
termination chain: Timeout Destination → Is-Voicemail fork → still no
response → call disconnected.

**Part 4 · The Ring / Dial Group node, expanded** — ring-all flow,
no-answer path (Announce → Default Destination → Is-Voicemail fork), plus
the Enhanced Ring Group (ERG) extras panel.

**Part 5 · The Queue node, expanded** — max-callers/full-redirect check,
the waiting cycle (MOH, position announcements, ring cycle), Exit Digit,
timeout/overflow — plus a Queue vs ERG comparison covering purpose, edition
availability, members, callback, and reporting.

## Key facts encoded in the map

- Operation Times is a **repeating gate**, not a single step. A call can
  clear the DID's OT during business hours and still be diverted by a
  Queue whose own OT is closed. Trace OT at every hop.
- OT exists on: DID, IVR, Queue, Ring/Dial Group, ERG. It does not exist
  on Extension, Conference, or Voicemail (per this deployment).
- `✱` and `#` are ordinary, fully configurable IVR selections — PBXware
  reserves nothing for them.
- The IVR's termination chain: greeting replayed N times → Timeout
  Destination. An unanswered extension falls to its own voicemail box;
  the call disconnects **only if that voicemail is turned off**.
- Ring Groups were renamed **Dial Groups** in v6.5. Business Edition (v6+)
  cannot create new Queues; ERG is used there instead. A destination
  number alone does not reveal whether it is a Queue or an ERG.

## Next phase: data-driven map

The current map is generic. Each part ends with an export checklist listing
the exact fields needed to replace generic nodes with the real system:

- **DIDs** — CSV export (`nr1`, `dest`, `ext`, `did_name` are the key columns)
- **IVRs** — per-selection destination map, Play Greeting N, timeout
  destination + Is-VM flag, OT state
- **Queues / ERGs** — members, strategy, max callers, exit digit,
  timeout/overflow destination, and *which type each object is*
- **Ring/Dial Groups** — members, Default Destination + Is-VM, OT state
- **Extensions** — number + name (labels for the leaves)

With those, the map upgrades to: fully traced multi-level paths per DID,
dead-end and orphan detection, reverse lookup by extension, and
departmental grouping.

## Open items

- PBXware edition and version of the target system (Business /
  Multi-Tenant / Contact Center; v6/7/8) — affects Dial Group vs Ring
  Group naming, ERG availability, and Queue creation.
- Preferred trace depth for the data-driven version: first hop only, or
  full nested tree down to individual extensions.
