# Deep Dive — Standards the Council Cites

A working reference for engineers, tender writers and test planners. Each entry lists the standard, what it covers, why it matters in a copper tube plant, and the source.

---

## 1. Product standards — copper tube & pipe

### 1.1 North American (ASTM)

| Standard | Scope | Why it matters |
|---|---|---|
| **ASTM B42** | Seamless Cu pipe, standard sizes 1/8″–12″ | Plumbing, boiler feed, refrigeration. Allows C10200/C10300/C10800/C12000/C12200. |
| **ASTM B68** | Seamless Cu tube, bright annealed | Refrigeration, fuel-oil, gasoline. Interior surface essentially clean. O50 / O60 tempers. |
| **ASTM B75** | Seamless Cu tube, general engineering (round, square, rectangular) | Broad industrial. H55/H58/H80/O60/O50 tempers. |
| **ASTM B88** | Seamless Cu water tube — Types K, L, M, DWV | US plumbing. Designation is nominal size (not OD). |
| **ASTM B224** | Classification of Coppers | Reference for UNS codes. |
| **ASTM B251** | General requirements, wrought seamless Cu & Cu-alloy tube | Governs tolerances, testing, inspection for many B-series tube standards. |
| **ASTM B280** | Seamless Cu tube for ACR field service | THE standard for air-conditioning & refrigeration. C10200/C12000/C12200. Oxygen ≤10 ppm. Cleanliness ≤0.0035 g/ft². Capped/plugged. |
| **ASTM B819** | Seamless Cu tube for medical gas systems | Medical gas; C12200 only; stricter cleanliness. |
| **ASTM E112** | Standard test methods for determining average grain size | Cited in acceptance; 0.015–0.050 mm for ACR final anneal. |
| **ASTM E243** | Standard practice for electromagnetic (eddy-current) examination of Cu & Cu-alloy tubes | Acceptance basis for ECT. |
| **ASTM B577** | Detection of cuprous oxide | Hydrogen embrittlement avoidance. |

Copper Development Association master reference:
- https://www.copper.org/applications/plumbing/techref/tpf_stds/tube_pipe_stds.html
- Copper Tube Handbook: https://www.copper.org/publications/pub_list/pdf/copper_tube_handbook.pdf
- ASTM B280-20 specification: https://store.astm.org/b0280-20.html

### 1.2 European (EN)

| Standard | Scope |
|---|---|
| **EN 1057** | Seamless, round Cu tube for water and gas in plumbing/HVAC |
| **EN 12449** | Seamless round Cu & Cu-alloy tube for general purposes |
| **EN 12735-1** | Seamless Cu tube for ACR — standards for field use |
| **EN 12735-2** | Seamless Cu tube for ACR — standards for equipment |
| **EN 13348** | Seamless Cu tube for medical gases |
| **EN 13349** | Pre-insulated Cu tube |

### 1.3 Japanese (JIS)

| Standard | Scope |
|---|---|
| **JIS H3300** | Copper and copper alloy seamless pipes and tubes |
| **JIS H3250** | Copper and copper alloy rods and bars |

### 1.4 Other

| Standard | Scope |
|---|---|
| **ISO 1337** | Wrought Cu — basic tolerances |
| **ISO 9303** | Seamless and welded steel tubes — full peripheral ultrasonic / ET |
| **AS 1432** | Australia — Cu tube for plumbing |
| **BS 2871** | UK (older) — Cu tube, largely superseded by EN 1057 |

## 2. Automation programming and execution

### 2.1 IEC 61131-3 — PLC Programming Languages

Defines five standard languages:
- **Ladder (LD)** — boolean logic, classical electricians' favourite.
- **Function Block Diagram (FBD)** — data-flow-oriented.
- **Structured Text (ST)** — Pascal-like, most flexible.
- **Instruction List (IL)** — assembly-style; deprecated.
- **Sequential Function Chart (SFC)** — state-machine-oriented.

Nearly every PLC platform in a copper tube plant is IEC 61131-3 compliant (Siemens SCL is their flavour of ST; Rockwell Studio 5000 supports ST, LD, FBD, SFC).

### 2.2 IEC 61499 — Distributed Automation (emerging)

Function-block model for distributed control across networked controllers. Worth watching for next-generation multi-vendor cells; not yet standard in metals plants.

## 3. Functional Safety

### 3.1 IEC 61508 — Functional safety, base standard
Umbrella safety integrity level (SIL) standard; derived standards below.

### 3.2 IEC 62061 — Machinery functional safety — electrical/electronic/programmable electronic control
Machinery-specific derivative of 61508.

### 3.3 ISO 13849 — Safety of machinery — safety-related parts of control systems
The more commonly used standard on machine safety in Europe. Performance Levels a–e and Categories 1–4.

Typical copper tube mill: the main safety PLC handles the whole line's safety circuit at PL d, Cat 3 (or higher for presses). Press-specific interlocks often PL e, Cat 4.

### 3.4 ISO 13855 — Positioning of safeguards
Where a light curtain has to be, given reaction time + hand speed; essential for press safety.

### 3.5 ISO 12100 — Safety of machinery — general principles
The risk assessment mother-standard; feeds the others.

## 4. OT Cybersecurity

### 4.1 ISA/IEC 62443 — the OT cybersecurity bible

Four sub-series:
- **62443-1-x** — General concepts, terms, models.
- **62443-2-x** — Asset-owner policies/procedures (CSMS).
- **62443-3-x** — System security (risk assessment, zones/conduits, foundational requirements).
- **62443-4-x** — Component security (vendor product security lifecycle).

Key concepts:
- **Zone and conduit** segmentation (Purdue model aligned).
- **Security Levels SL 1 → SL 4** of increasing adversary capability.
- **Seven Foundational Requirements:** IAC, Use Control, System Integrity, Data Confidentiality, Restricted Data Flow, Timely Response to Events, Resource Availability.

Sources:
- https://www.isa.org/standards-and-publications/isa-standards/isa-iec-62443-series-of-standards
- https://www.baculasystems.com/blog/iec-62443-security-standard/
- https://www.fortinet.com/resources/cyberglossary/iec-62443
- https://www.txone.com/blog/how-to-construct-the-cornerstone-of-ot-cybersecurity-using-isa-iec-62443/
- https://www.dragos.com/blog/isa-iec-62443-concepts
- https://www.rockwellautomation.com/en-gb/company/news/blogs/iec-62443-security-guide.html
- https://industrialcyber.co/features/the-essential-guide-to-the-iec-62443-industrial-cybersecurity-standards/

### 4.2 Complementary cyber frameworks
- **NIST SP 800-82 Rev. 3** — Guide to OT Security.
- **NIST Cybersecurity Framework (CSF) 2.0** — Identify / Protect / Detect / Respond / Recover / Govern.
- **NERC-CIP** — US electric utilities (not tube plants, but often cited).
- **ISO/IEC 27001** — IT-side ISMS; applies to corporate layer.

## 5. Enterprise-to-shop integration

### 5.1 ISA-95 / IEC 62264 — Enterprise-Control System Integration

The contract between L4 ERP and L3 MES.
- **Part 1** — terminology, object models.
- **Part 2** — object model attributes.
- **Part 3** — activity models of manufacturing operations.
- **Part 4** — object models for operations management information exchange.
- **Part 5** — business-to-manufacturing transactions.

**B2MML** — XML schema implementation of ISA-95 object models; widely used in ERP↔MES integrations.

### 5.2 ISA-88 / IEC 61512 — Batch control
Physical and procedural model hierarchy: Enterprise / Site / Area / Process Cell / Unit / Equipment Module / Control Module. Even in non-batch tube processing, the equipment model is the right backbone for HMI, MES data, and digital twin topics.

## 6. NDT and inspection

- **ASTM E243** — Electromagnetic (eddy-current) examination of Cu / Cu-alloy tubes (already in §1.1 but worth repeating in the NDT list).
- **ASTM E309** — Eddy-current examination of steel tube with magnetic saturation.
- **ISO 9303** — UT / ET of seamless and welded steel tube; principles transferable.
- **ASTM E2491** — Practice for evaluating performance characteristics of phased-array UT.
- **ASTM E1316** — Terminology for NDT.
- **ISO 9712** — NDT personnel qualification.
- **SNT-TC-1A** (ASNT) — NDT personnel qualification (US).

## 7. Quality and management

- **ISO 9001** — Quality Management Systems (QMS).
- **ISO 14001** — Environmental Management Systems.
- **ISO 45001** — Occupational Health and Safety.
- **IATF 16949** — QMS for automotive suppliers (relevant if the tube plant serves auto HVAC).
- **ISO 50001** — Energy Management Systems (relevant for kWh/t programs).

## 8. Protocols and network

- **IEC 61158 / IEC 61784** — Fieldbus families (PROFINET IO, EtherNet/IP, EtherCAT, Modbus TCP).
- **OPC UA (IEC 62541)** — industrial semantic interoperability.
- **MQTT v5 (ISO/IEC 20922)** — lightweight pub/sub transport.
- **Sparkplug B** — Eclipse Foundation specification on top of MQTT.
- **TSN (Time-Sensitive Networking, IEEE 802.1 family)** — for deterministic Ethernet in future lines.

## 9. Commonly mis-applied or under-applied standards

- **GAMP 5** — not mandatory outside pharma, but its V-model and risk-based validation thinking translate well to metals automation.
- **ISA-18.2** — alarm management (lifecycle, rationalisation, shelving). Under-applied; most brownfield tube plants have 10× too many alarms.
- **ISA-101** — HMI design. Under-applied; most operator screens look like 1995.
- **IEC 62682** — machinery-safety alarms; works in concert with ISA-18.2.

## 10. How the council uses these standards

- **Dr. P** — product (ASTM B280 / EN 12735) + NDT (ASTM E243) + grain size (ASTM E112).
- **Arch** — ISA-95, ISA-88, IEC 62264, OPC UA, IEC 62443.
- **Quinn** — IEC 61131-3, IEC 61508, ISO 13849, ISA-18.2, ISA-101, IEC 62443, GAMP 5.
- **Dev** — IEC 61131-3 language choice, OPC UA companion specs, Sparkplug B payload format.
- **Mgr** — ISO 9001 / 14001 / 45001, IATF 16949, ISO 50001 for project deliverables and contract clauses.
- **Cyber** — IEC 62443 at every level, NIST 800-82 / CSF 2.0 for corporate alignment.
- **Ops** — ISO 55000 (asset management), ISO 50001 (energy), and reliability references.
