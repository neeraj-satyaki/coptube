# Deep Dive — Vendor Deep-Dives

Working technical cribsheet per major vendor the council recommends. Use this when a user asks "which Primetals product specifically" or "what would an SMS bid look like."

---

## 1. Line OEMs (copper tube and pipe)

### 1.1 SMS group (Germany)
- **Copper-tube portfolio:** extrusion presses (Schloemann heritage), cold pilger mills, drawing benches, spinner-block finish draw, **directube®** cast-and-roll line, **VNVG 2000** inner-grooving (grooving head up to 49 000 rpm, line speed up to 100 m/min), bull blocks, jumbo coilers, pickling/cleaning lines.
- **Automation brand:** **X-Pact®** (L1 + L2 for hot and cold processing lines).
- **Reference links:**
  - https://www.sms-group.com/plants/copper-tube-lines
  - https://www.sms-group.com/plants/extrusion-presses-for-heavy-metals
  - https://www.sms-group.com/plants/cold-pilger-mill
  - https://www.sms-group.com/services/process-automation-for-hot-flat-rolling-mills-for-steel-and-copper
- **When to pick SMS:** full-line modern ACR plants, high-end IGT lines, greenfield in Europe/India/US. Very strong L1+L2 bundle, decades of copper experience.
- **Watch-outs:** premium pricing; long lead times on critical components; ensure you negotiate interfaces for non-SMS MES / ERP up-front.

### 1.2 Danieli Breda (Italy)
- **Portfolio:** direct and indirect extrusion presses for Cu, brass, Cu-Ni, Al. Inline piercer integration. Strong in heavy-section / industrial tube.
- **Reference:** https://www.danieli.com/en/products/products-processes-and-technologies/extrusion-presses-non-ferrous-extrusion-plants_26_46.htm
- **When to pick Danieli:** heavy-wall, industrial-tube (not ACR) focus; when the rest of the plant is also a Danieli ecosystem.

### 1.3 Primetals Technologies (UK/Japan; MHI JV)
- **Portfolio:** cold & foil rolling mills for non-ferrous; strong L1/L2 process automation (X-Pact-style); MES in partnership with PSI Metals.
- **Notable:** pioneers of physics-based + ML-based Level 2 models; autonomous-operation roadmap.
- **References:**
  - https://www.primetals.com/portfolio/technology-packages
  - https://www.primetals.com/en/portfolio/solutions/cold-rolling/
  - https://www.primetals.com/en/autonomous-operation/
- **When to pick Primetals:** when the plant includes a cold-rolling/strip line alongside tube; or when you specifically want a best-in-class L2 with self-learning models and deep metals domain expertise.

### 1.4 Outokumpu (Finland) — historic but important
- **Historical role:** pioneered the **Cast-and-Roll** tube process at Pori pilot plant (1987), which reshaped modern ACR tube economics.
- **Current state:** the copper-tube IP largely transferred through Luvata / Mitsubishi Materials / SMS; Outokumpu itself is now a stainless-steel major.
- **Reference context:** https://entrepreneurindia.co/public/index.php/project-details/inner-grooved-copper-tube-manufacturing-plant-detailed-project-report

### 1.5 Senbo Machinery (China), TED Machine (China), SuperbMelt (China)
- Turnkey Cu pipe lines (cast-and-roll, combined drawing, spinner block, straightening).
- Two-roller cold pilger mills (TED LG models).
- Hollow-tube forming for Cu / Al / precious metals (SuperbMelt).
- **When to pick:** cost-sensitive Asian / MENA greenfield; retrofit of Chinese base. Verify engineering depth for critical components (especially pilger dies and finishing lines).
- **References:**
  - https://www.tube-rolling-mill.com/pipe-and-tube-line/copper-pipe-and-tube-line-machine/straight-copper-pipe-and-tube-line.html
  - https://www.tedmetal.com/pilger-mill/cold-pilger-mill/two-rollers-cold-pilger-mill-for-ferrous-and.html
  - https://www.superbmelt.com/hollow-tube-forming-machine/

## 2. Furnaces and heating

### 2.1 Tenova LOI Thermprocess (Germany)
- Bell-type HPH® annealing; furnace-side automation.
- https://tenova.com/technologies/bell-type-annealing-furnace-wire-rod

### 2.2 Ajax TOCCO Magnethermic (US)
- Induction bright-annealing for Cu tubes; billet heaters for extrusion presses.
- https://www.ajaxtocco.com/blog/bright-annealing-induction-furnace

### 2.3 IAS / Inductotherm / EFD Induction
- Billet preheat ahead of extrusion (IAS, part of SMS family).
- Inline induction anneal (EFD).

### 2.4 Therelek / JR Furnace / Thorson (India)
- Indian bell/top-hood/induction/brazing furnaces; growing player for domestic retrofits.
- https://www.therelek.com/products/bell-furnace/bell-annealing-furnace/
- https://www.jrfurnace.net/bell-type-annealing-furnace-for-wire-rod-coils-strips/
- https://www.thorsonindustries.com/industrial-furnace.html

### 2.5 Beijing Holland / Nanjing Nianda / Hangzhou Suntech (China)
- Vacuum bell anneal (Beijing Holland), roller-hearth bright anneal up to 950 °C (Nianda), bell heating-hood anneal (Suntech).

## 3. NDT / ECT / inspection

### 3.1 Foerster (Germany)
- Gold-standard through-coil and rotating-probe ET for seamless tube. Referenced in most tube OEM FAT specs.

### 3.2 Olympus / Evident, UniWest, ETher NDE, OKOndt, Rohmann, Tecscan
- Comprehensive ET / UT instrument catalogues.
- Directory: https://ndtsupply.com/eddy-current-instruments/

### 3.3 Magnetic Analysis Corp (MAC, US)
- **Echomac® FD 4-channel** ultrasonic eccentricity tester — widely used post-extrusion on drawing lines.
- https://www.mac-ndt.com/blogs/press-room/eccentricity-inspection

### 3.4 Shanghai Cangxin, BKN (China)
- Encircling-coil ECT systems for Cu tube; MFL, rotating ET, UT.
- https://www.cangxingroup.com/Copper-tubes/copper-tube-eddy-current-testing
- https://www.bkneddy.com/eddy-current-testing-equipment/

### 3.5 Intertek, ATS, Z-Check, R-CON NDT
- Third-party ET services; distributors; equipment sourcing.

## 4. PLC / DCS / SCADA / HMI

### 4.1 Siemens
- **S7-1500 / S7-1500F** — modern PLC for new builds; the default for European-built SMS / Danieli / Primetals lines.
- **PCS 7 / PCS neo** — process DCS for larger integrated plants.
- **TIA Portal** — unified engineering workbench.
- **WinCC Unified / WinCC Comfort / WinCC OA** — HMI / SCADA families.
- **SINAMICS** drives (S120, G120) — with current-signature analysis onboard.
- **Safety Integrated** — SIL/PL-rated libraries for S7-1500F.
- **Scalance** — industrial managed switches; core of OT network design.
- **References:**
  - https://www.siemens.com/global/en/products/automation/process-control/simatic-pcs-7.html
  - https://www.siemens.com/global/en/products/automation/process-control/simatic-pcs-7/plant-operation.html
  - https://www.siemens.com/global/en/products/automation/process-control/simatic-pcs-7/plant-automation-engineering.html
  - https://www.siemens.com/global/en/products/automation/process-control/simatic-pcs-7/plant-device-management.html

### 4.2 Rockwell Automation
- **ControlLogix 5580 / 5570, CompactLogix 5380** — PLC for new builds.
- **GuardLogix** — safety PLC.
- **Studio 5000 Logix Designer** — engineering tool.
- **FactoryTalk View SE / ME** — HMI / SCADA.
- **FactoryTalk Historian** — on top of OSIsoft PI.
- **PlantPAx** — Rockwell DCS for process integration.
- **PowerFlex** drives — with predictive-maintenance features.
- **References:**
  - https://www.rockwellautomation.com/en-us/products/hardware/programmable-controllers.html
  - https://www.rockwellautomation.com/en-gb/company/news/blogs/iec-62443-security-guide.html

### 4.3 Schneider Electric
- **Modicon M580, M340** — PLC.
- **Control Expert (Unity Pro)** — engineering.
- **EcoStruxure Foxboro DCS** — process DCS (historically IA / I/A Series heritage).
- **Altivar** drives.
- **EcoStruxure Machine Expert** — machine-level engineering.
- Common in French / India installations and hybrid process-discrete environments.

### 4.4 ABB
- **AC800M** controller + **Ability System 800xA** DCS — frequently bundled with ABB drives and Level 2.
- **Roll@xA** — metals-processing library on 800xA.
- **ABB Ability MOM4Metals** — manufacturing operations management.
- **ABB drives:** ACS880 (process drive), ACS580, ABB Ability Smart Sensor for motors.
- **References:**
  - https://new.abb.com/metals
  - https://new.abb.com/control-systems/industry-specific-solutions/metals
  - https://new.abb.com/cpm/industry-specific-solutions/metals
  - https://www.abb.com/global/en/company/stories/metals-industry-decarbonization

### 4.5 COPA-DATA
- **zenon** SCADA / HMI with multi-PLC driver support; widely used in metals plants that run a mixed Siemens + Rockwell floor.
- https://www.copadata.com/en/industries/smart-factory/

### 4.6 Inductive Automation
- **Ignition** — SCADA + Gateway Network + MQTT Engine + lightweight MES (OEE, Track&Trace, SPC modules).
- Popular with mid-size producers who want to avoid WinCC / FactoryTalk licensing lock-in and prefer a flat per-server licence.
- Common edge / MQTT gateway, often used to back-fill a UNS on existing plants.

### 4.7 Beckhoff
- **TwinCAT 3** on industrial PC with EtherCAT field bus. Increasingly seen on high-speed inspection lines and motion-critical cells.

## 5. Level 2 process control

### 5.1 Primetals X-Pact for rolling (reference architecture)
- Physics-based models (roll force, temperature, flatness, AGC) with self-learning adaptation after each coil.
- Runs on redundant industrial PCs; talks to PLC over PROFINET or EtherNet/IP and to MES over OPC UA.
- Jindal Stainless AOD L2 case: https://www.primetals.com/press-media/news/level-2-system-from-primetals-technologies-digitalizes-know-how-for-jindal-stainless-aod-converter
- ArcelorMittal hot-strip mill automation upgrade: https://www.primetals.com/press-media/news/arcelormittal-chooses-primetals-technologies-for-extensive-hot-strip-mill-automation-upgrade

### 5.2 SMS X-Pact® for copper and steel
- Similar concept; deeply integrated with SMS mechanical and electrical packages. https://www.sms-group.com/services/process-automation-for-hot-flat-rolling-mills-for-steel-and-copper

### 5.3 ABB Roll@xA on 800xA
- L1+L2 libraries for metal-processing lines; tightly coupled to ABB drives for closed-loop control.

### 5.4 Ingeteam, Russula
- L1+L2 for rolling and metal processing; competitive in mid-size / emerging-market projects.
- https://www.ingeteam.com/en-us/sectors/steel-metals/p15_29_169_0/level-1-and-2-automation.aspx
- https://www.russula.com/solutions/rolling-mills/automation

## 6. MES for metals

### 6.1 PSI Metals
- Metals-specialist, standard product, frequent partner of Primetals. Orders from Gerdau, etc.
- https://www.psi.de/en/blog/psi-blog/post/meet-smartness-the-future-of-production-management-systems-in-the-metals-industry/
- Gerdau Ouro Branco melt-shop MES with Primetals: https://www.primetals.com/press-media/news/primetals-technologies-and-psi-metals-receive-order-for-melt-shop-manufacturing-execution-system-mes-from-gerdau-ouro-branco

### 6.2 SAP Digital Manufacturing (DM / DMC / MII)
- Connects shop floor to S/4HANA. BADIs and extensions for metals.
- https://www.sap.com/products/scm/manufacturing.html

### 6.3 Siemens Opcenter Execution
- Process and discrete MES variants; good integration with Siemens PCS 7 / TIA ecosystem.

### 6.4 Rockwell FactoryTalk ProductionCentre
- MES in the FactoryTalk stack.

### 6.5 ABB MOM4Metals
- ABB's metals-MES layer on Ability.

## 7. ERP for metals

### 7.1 SAP S/4HANA
- Dominant in large groups. SAP Mill Products industry solution covers metals, paper, packaging, building materials.
- https://www.sap.com/industries/mill-products.html
- Jindal Stainless BW/4HANA adoption: https://www.jindalstainless.com/press-releases/jindal-stainless-leads-digital-innovation-in-the-manufacturing-industry-with-adoption-of-bw-4hana/

### 7.2 Oracle
- Oracle EBS / Fusion Cloud ERP; presence in large Indian and global metals groups.

### 7.3 Infor LN
- Used by Jindal Saw across ductile iron, large-diameter pipe, seamless pipe divisions.
- https://www.scribd.com/document/85070175/Case-Study-ERP-JindalSaw

### 7.4 Microsoft Dynamics 365 F&O
- Used by some mid-market metals companies, especially in North America.

### 7.5 Kingdee
- Dominant in Chinese metals groups.

## 8. Historian / analytics

- **AVEVA PI System** (+ PI AF) — de-facto standard in metals.
- **GE Proficy Historian** — legacy incumbent at some sites.
- **InfluxDB + Grafana** — modern, open-source-leaning stack for greenfields.
- **Seeq, TrendMiner** — process-specific analytics on top of historians.
- **Snowflake, Databricks** — data-lake / warehouse for advanced analytics.

## 9. OT cybersecurity vendors

- **Claroty** — OT asset discovery and passive monitoring.
- **Nozomi Networks** — similar; partners with ABB.
- **Dragos** — strong threat-intel pedigree, ICS-specific.
- **Tenable OT (Tenable.ot)** — vuln management + passive monitoring.
- **TXOne, Trend Micro** — endpoint for OT.
- **Kaspersky KICS** — ICS-specific endpoint (geopolitical sensitivity in some markets).
- **Fortinet, Cisco, Hirschmann, Siemens Scalance** — industrial firewalls / managed switches.

## 10. Putting a tender shortlist together — pragmatic heuristics

- **Greenfield modern ACR plant, premium quality, EU / India / US:** SMS group (prime) + Primetals or in-house L2 + PSI Metals or SAP DM (MES) + SAP S/4HANA (ERP) + AVEVA PI (historian) + Claroty/Nozomi (OT cyber).
- **Cost-driven greenfield, Asia / MENA:** Senbo or TED (prime) + Siemens S7-1500 + Ignition (SCADA/MES-lite) + SAP S/4HANA Public Cloud + InfluxDB/Grafana historian + Tenable.ot for cyber.
- **Brownfield retrofit, Indian mid-tier:** keep existing PLC where supported, add OPC UA gateway, Ignition (SCADA), PSI Metals-lite or custom MES-on-Ignition, SAP Business One or S/4HANA Cloud, Nozomi for passive OT monitoring.
- **Inner-grooving cell add-on:** SMS VNVG 2000 or equivalent, with its L2 tying into the plant historian and MES via OPC UA.

Always negotiate interfaces first: who owns the OPC UA server, who owns the B2MML schema for L3↔L4, who has the cyber-baseline responsibility, and how much of the code the plant owns after year 2.
