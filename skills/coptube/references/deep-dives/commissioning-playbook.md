# Deep Dive — Commissioning Playbook (FAT → SAT → HAT → Handover)

The council cites this file when the user's question is about acceptance testing, commissioning sequencing, or punch-list management. Numbers and gate structures are calibrated to tube-mill / metals-automation projects.

---

## Why this matters

Industry studies repeatedly show that a defect caught at FAT costs roughly **1/10×** of the same defect at SAT, and **1/100×** of the same defect found in production. Skipping or rushing FAT is the single most expensive decision on a capital project. Reference: https://oxmaint.com/industries/manufacturing-plant/equipment-commissioning-checklist-installation-fat-sat-acceptance

## Stage map

```
 Award   Design  FAT     SAT    HAT /       Performance   Handover   End of
 ▼       ▼       ▼       ▼      Hot start   Run (72 h)    ▼          Warranty
[─────Engineering────][───Build───][──Ship/install──][─Commissioning─][─Run─][─Warranty─]
                       │           │                │                │
                       │           │                │                └─ Punch list close
                       │           │                └─ Guarantee KPIs
                       │           └─ Wiring, loop checks, motions
                       └─ Simulated operation at OEM premises
```

---

## 1. FAT — Factory Acceptance Test (at OEM / integrator)

### 1a. Entry gate (must be done BEFORE FAT begins)

- URS / FDS signed off by owner.
- Traceability matrix (URS ↔ FDS ↔ test case) baselined.
- FAT protocol written by OEM, reviewed by owner, approved in writing.
- All documents available: P&ID, SLD, layout, cable schedule, I/O list, HMI screen list, alarm list, interlock matrix, pass-schedule tables, safety-circuit drawing, CE/UL certificates.
- Code and configuration under version control; baseline tagged as "FAT1 candidate."
- Required simulators ready (PLCSIM Advanced, Studio 5000 Emulate, or physical process simulator).

### 1b. FAT test blocks (generic, adapted for a copper tube line)

| # | Block | What is verified | Typical evidence |
|---|---|---|---|
| F-01 | Documentation & physical inventory | BOM vs. PO; nameplates; certificates; manuals | Signed checklist, photos |
| F-02 | Mechanical as-built | Dimensions, alignment, cleanliness | Dimensional sheet, photos |
| F-03 | Electrical as-built | Wiring per drawing, grounding, labelling, spare cores | Cable-continuity log, megger tests |
| F-04 | Safety circuit | E-stops, guards, light curtains, interlocks, Cat 3/4 per ISO 13849 | Safety loop-check sheet, TÜV-witnessed where applicable |
| F-05 | Power-on | Voltage/phase, PLC boot, HMI boot, drive boot, no fault | Power-on log |
| F-06 | I/O loop check (hard) | Every I/O point forced and observed in HMI | Signed I/O list |
| F-07 | Device function | Drives commissioned, encoders scaled, valves stroked, pyrometers calibrated | Per-device test sheet |
| F-08 | Sequence & recipe | Each operating mode (Manual / Auto / Simulation) on emulator | Recorded run logs |
| F-09 | L2 models (where in scope) | Pass-schedule calc on a reference coil, post-calc adaptation | Model input/output records |
| F-10 | HMI completeness | Screens, navigation, alarms, trends, user roles | Walk-through log, screenshots |
| F-11 | Alarms & interlocks | Every alarm fired, priority checked, acknowledgement logged | Alarm test log |
| F-12 | MES message round-trip (if in scope) | Order download, production confirmation, quality upload | Captured JSON / IDoc |
| F-13 | ERP message round-trip (if in scope) | BAPI_PRODORDCONF_CREATE_TT / IDoc LOIPRO | SAP transport / screen |
| F-14 | Cybersecurity baseline | Hardening checklist, credentials, patch level, Nmap scan | Scan report, hardening sign-off |
| F-15 | Backup & restore | Image backup; restore to spare; tested OK | Backup media + log |
| F-16 | Performance test on simulator | Scan time, response time, deterministic cycle at peak load | Wireshark + PLC stats |
| F-17 | Failure-mode test | Injected failures: drive trip, sensor fault, network drop | Recovery log |
| F-18 | Punch list review | All non-conformances categorised A / B / C | Signed punch list |

### 1c. Punch-list categorisation

- **Category A** — Must be closed before equipment ships. No exceptions.
- **Category B** — Must be closed before SAT sign-off.
- **Category C** — Minor; resolved during warranty, tracked in the CMMS / Oxmaint from day 1.

Reference: https://oxmaint.com/industries/manufacturing-plant/equipment-commissioning-checklist-installation-fat-sat-acceptance

### 1d. Common FAT mistakes

- Running on a sample of the line, not the whole line. Find all interfaces.
- Sending only engineers. Send the future shift supervisor and one operator too.
- Squeezing a multimillion-dollar FAT into a week to meet a shipping date — classic false economy.
- Not testing restart-from-power-failure. That is how real plants break.
- Not bringing the customer's production recipes / samples — test on generic material, surprised in production.

Sources: https://www.dxpe.com/what-is-factory-acceptance-test-protocol-purpose/ ; https://carelabz.com/what-factory-acceptance-testing-how-fat-done/ ; https://www.csidesigns.com/blog/articles/how-to-get-the-most-out-of-your-next-factory-acceptance-test ; https://safetyculture.com/checklists/factory-acceptance-test

---

## 2. SAT — Site Acceptance Test (at the plant, cold)

### 2a. Entry gate

- Equipment physically installed, anchored, levelled.
- Utilities connected: power, compressed air, water, N₂/H₂ where applicable.
- Earth-continuity verified to the plant's main earth bar.
- Documentation updated with any FAT-era changes.
- Safety file updated; LOTO (lock-out / tag-out) procedure in place.
- Commissioning team on site with authority to stop.

### 2b. SAT blocks

| # | Block | What is verified |
|---|---|---|
| S-01 | Civil and mechanical installation | Levelling ≤ 0.3 mm over 1 m, alignment per OEM |
| S-02 | Laser shaft alignment for coupled rotating equipment | Parallel < 0.05 mm, angular < 0.05 mm/m (re-check after 500 h) |
| S-03 | Electrical supply | Voltage ±10 %, phase sequence, earth continuity, cable sizing |
| S-04 | E-stop and safety circuit | Full loop test, timing < ISO 13849 target |
| S-05 | Loop check with instrumentation | Each analogue point calibrated to engineering units |
| S-06 | Drive re-commission on real motors | Auto-tune under no-load and low-load |
| S-07 | No-load sequences | All modes run with empty line |
| S-08 | Network integration | Plant OT VLAN, NTP, historian tags arriving, MES queue |
| S-09 | OT cybersecurity on site | Segmentation verified, passive monitoring picks up the new assets |
| S-10 | Operator training | Minimum hours per role; assessment signed |
| S-11 | SAT punch list | Close all Category B items from FAT; new items logged |

### 2c. Typical SAT duration

- A major new copper tube line: 2–4 months SAT.
- A bolt-on piece of equipment (e.g., new inner-grooving line on an existing plant): 2–6 weeks.
- A Level 2 retrofit (software-only): 2–4 weeks.

Reference alignment tolerances and checklist shape: https://oxmaint.com/industries/manufacturing-plant/equipment-commissioning-checklist-installation-fat-sat-acceptance ; https://jsbwcrane.com/factory-acceptance-test-fat-and-site-acceptance-test-sat-checklist/

---

## 3. HAT — Hot Acceptance Test / Hot Commissioning

The moment real copper goes through the line.

### 3a. Entry gate

- SAT sign-off.
- First-run materials delivered and inspected.
- Operations team trained; OEM commissioning engineers on site.
- Utilities stable; consumables stocked; spares A-class present.
- Emergency response plan briefed.

### 3b. HAT sequence

1. **First billet / first mother tube** — minimal speed, short run, data recorded at 10–100 ms on all critical tags.
2. **First full-length pass** — confirm OD, wall, eccentricity within ±20 % of guarantee just to prove physics works.
3. **Recipe walk** — run each product code once. Capture Level 2 pre-calc vs. actuals.
4. **Ramp to nameplate** — speed up to full line rate over several shifts; record stability, vibration, temperature, energy.
5. **First customer-acceptable coil** — passes ECT, dimensional, visual, cleanliness.

### 3c. 72-hour Performance Run (the contractually critical part)

- Run at nameplate tonnage for 72 hours with agreed recipes and material.
- Measure against **guarantee curves** from the contract:
  - Capacity (t/day)
  - Yield (%)
  - Energy (kWh/t)
  - Quality (OD, wall, eccentricity, ECT pass rate, surface)
- Acceptance is pass/fail per contract; re-runs per contract.
- All data archived, signed by both parties.

### 3d. Common HAT failure modes

- Level 2 model drifts after a coil stop because post-calc path skipped.
- Operator HMI alarm flood — not calibrated for realistic operation.
- Pyrometer misreads because optics fouled during shipment.
- MES order not closed because weight rounding mismatched the scale.
- ECT false-reject rate > 10 % — probe centring not set on real tube.

---

## 4. Handover and Warranty

### 4a. Handover dossier (before final payment)

- As-built drawings (mechanical, electrical, P&ID, SLD).
- Code and configuration archive (PLC, HMI, L2, MES, drive parameter files) — in version control.
- Parameter and recipe tables.
- Spare-parts list with lead times; minimum stock list.
- Operating manuals and maintenance manuals in local language.
- Training records.
- Punch-list sign-off.
- Cybersecurity baseline documents.
- Backup media and restore procedure tested on site.

### 4b. Warranty period management

- Typical warranty: 12–24 months from HAT.
- Defect classification and response time in contract (e.g., critical: 4 h on site).
- Change-control board for all modifications during warranty so OEM cannot disclaim.
- End-of-warranty walkdown: full re-inspection, final punch list closure, maintenance contract handover.

---

## 5. A practical FAT / SAT document kit (what to demand from OEM)

1. Master test plan (MTP).
2. Per-system test protocols (mechanical, electrical, safety, control, L2, MES interface, cyber).
3. I/O and signal list with calibration sheets.
4. Alarm and interlock matrix.
5. Safety loop test protocol per ISO 13849.
6. Cycle-time and performance test protocol.
7. Failure-injection test protocol.
8. Punch-list template with severity rules.
9. Training plan with per-role hours.
10. Handover dossier template.

These protect both parties and make it impossible to argue later about "what the test was supposed to show."
