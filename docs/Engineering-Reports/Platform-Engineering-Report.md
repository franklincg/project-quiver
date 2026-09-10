---
title: Platform Engineering Report
description: Decision register tracing Project Quiver design decisions from PT1 through the Dev Kit
---

# Project Quiver Platform Engineering Report

> Work-in-progress for task T-09. Upstream assignment is pending acceptance of the M0 sample in issue #256. This branch is prework only; no upstream PR should be opened before assignment.

## Source index

- [PT1 Engineering Report](./PT1-Engineering-Report.md) — PT1 mission envelope, communication choices, structural requirements, propulsion/power baseline, and payload architecture.
- [PT2 Engineering Report](./PT2-Engineering-Report.md) — PT2 FC/GNSS configuration, selected propulsion and battery, PCB/SSR changes, and updated operating requirements.
- [PT3 Engineering Report](./PT3-Engineering-Report.md) — PT3 structural changes, distributed PCB architecture, FC selection, redundant navigation/altimetry, payload interfaces, and serviceability changes.
- [Dev-Kit Engineering Report](./Dev-Kit-Engineering-Report.md) — PT3-to-Dev-Kit deltas including structural weight testing, weatherproofing, electronics revisions, sensors, software, and transport configuration.
- [PT3 flight-controller setup information note](../../task-grant-bounty/pt3/flight-controller/0002-flight-controller-setup/information-note.md) — ESC DroneCAN setup and validated telemetry configuration.
- [Task T-09 / issue #256](https://github.com/Arrow-air/project-quiver/issues/256) — decision-register schema, milestones, review rules, and acceptance criteria.

## Decision register

| ID | Phase | Decision | Replaced | Why | Evidence | Status |
|---|---|---|---|---|---|---|
| D-001 | PT1 | Set a 25 kg maximum mission load and size designated maximum thrust at about 45–50 kg. | New | The report ties the 45–50 kg thrust target to the safety margin around the 25 kg mission load. | [PT1 report](./PT1-Engineering-Report.md) | Standing through PT2/PT3 mission-envelope work. |
| D-002 | PT1 | Use CAN bus for signal communication where applicable instead of relying on traditional non-differential PWM links. | Traditional PWM-style signal links for those functions | PT1 states CAN was chosen to avoid electromagnetic interference that PWM may be subject to. | [PT1 report](./PT1-Engineering-Report.md) | Standing; expanded in later prototypes. |
| D-003 | PT1 | Build the structural frame around commercially available/off-the-shelf or easily manufacturable components. | New | The structural requirement connects this choice to rapid assembly and ease of replacement while retaining a lightweight, strong frame. | [PT1 §2.2](./PT1-Engineering-Report.md) | Standing design principle. |
| D-004 | PT2 | Select the Tattu 14S HV 30000 mAh Smart Battery. | Earlier battery baseline / generic 12S–14S requirement | PT2 cites the integrated BMS and efficient mechanical integration; the pack uses a specialized Molex connector with a safety latch. | [PT2 report](./PT2-Engineering-Report.md) | Standing into later Quiver configurations. |
| D-005 | PT2 | Use the Mateksys AP DroneCAN M10Q-3100 GNSS, with the Mateksys M9N-G4-3100 identified as the replacement source. | M10Q-3100 when unavailable | PT2 records that the M10Q-3100 was no longer produced and explicitly names the M9N-G4-3100 as the substitute. | [PT2 GNSS](./PT2-Engineering-Report.md) | M10Q superseded for sourcing; M9N persists as backup in PT3/Dev-Kit. |
| D-006 | PT3 | Replace PT2’s single centralized custom-PCB approach with four custom boards: Battery PCB, Main PCB, FC PCB, and Attachment Interface PCB. | PT2 single centralized PCB | The distributed architecture lets each board be optimized for its role, reduces interdependencies, simplifies maintenance, and improves troubleshooting/upgrades. | [PT3 electronics integration](./PT3-Engineering-Report.md) | Standing architecture; revised in Dev-Kit. |
| D-007 | PT3 | Select Pix32 V6 as the baseline flight controller. | Mateksys H743-SLIM V3 used in PT2 | After comparing candidate FCs, PT3 says Pix32 V6 balanced performance and affordability for prototyping while preserving an upgrade path to Pixhawk 6X or Cube Orange. | [PT3 FC selection](./PT3-Engineering-Report.md) | Standing in Dev-Kit. |
| D-008 | PT3 | Use a dual-RTK-capable primary GNSS arrangement with a Mateksys M9N-G4-3100 backup. | PT2 initial/single GNSS configuration | PT3 adds redundancy: F9P-based DroneCAN hardware is primary, while the M9N is retained as a backup the autopilot can promote if the primary fails. | [PT3 navigation](./PT3-Engineering-Report.md) | Standing in Dev-Kit. |
| D-009 | PT3 | Accommodate both Ainstein US-D1 radar and Benewake TF03-180 LiDAR for altitude sensing. | PT1 radar-only / PT2 LiDAR-only progression | Radar provides reliable long-range readings through fog/dust/rain, while LiDAR provides higher-resolution short-range measurements for hovering and terrain following. | [PT3 altimetry](./PT3-Engineering-Report.md) | Standing; mount revised in Dev-Kit. |
| D-010 | Dev Kit | Keep the upper-airframe thickness reductions, but restore/retain the lower frame and battery-bay parts at their original thicknesses. | Proposal to thin both upper and lower airframe parts | With ~7 kg payload, the thinned lower frame produced strong oscillations and the flight was aborted; the final configuration therefore keeps only the upper reductions. | [Dev-Kit weight reduction study](./Dev-Kit-Engineering-Report.md) | Standing Dev-Kit configuration. |

## Phase narrative

To be developed after the M1 decision register is complete and accepted. The narrative will be derived from the register rather than written independently, preserving traceability from each phase-level statement back to its source.
