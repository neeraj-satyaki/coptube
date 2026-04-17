# Deep Dive — Case Studies (Real Plants, Real Numbers)

The council cites these when a user asks for precedent, reference installations, or "has anyone actually done this?" All cases are publicly reported.

---

## 1. Hailiang Group — 5th-generation intelligent Cu tube line

**Who:** Zhejiang Hailiang Co., Ltd. (SZSE 002203). Largest Cu pipe exporter in China; global producer with bases in China, USA (Texas), and elsewhere.

**What:** Launched its **5th-generation intelligent cast-and-roll Cu tube line**.

**Reported outcomes (vs. 4th generation):**
- **Yield**: ~91 % → **~93 %**.
- **Energy**: **~300 kWh/t reduction**.
- **Capacity**: **~80 % increase** per line.
- **Labour efficiency**: **×3** — same output with a third of the people.

**Technology lens (inferred):** cast-and-roll route replacing extrusion+draw on the hot end; advanced Level 2 adaptive models; heavy instrumentation; ML-assisted quality prediction; integrated MES.

**Source:** https://news.metal.com/newscontent/101549361/

**Why the council cites this:** benchmark of what is achievable with modern architecture; sets the yield, energy, and labour targets the council uses in greenfield business cases.

---

## 2. Hindalco Industries — Waghodia IGT plant

**Who:** Hindalco Industries (Aditya Birla Group).

**What:** India's first backward-integrated inner-grooved Cu tube (IGT) plant at Waghodia, Gujarat. Plus a 11 500 tpa battery-grade Cu foil facility on the same complex.

**Scale:**
- Phase 1: **25 000 tpa IGT** (start-up).
- Phase 2: expansion to **50 000 tpa IGT**.

**Integration:** backed by Birla Copper smelter at Dahej (~500 kt/yr cathode); Dahej → Waghodia cathode-to-tube chain reduces raw-material risk and captures intermediate margin.

**Significance:** direct response to India's import dependence on ACR-grade IGT; aligned with PLI White Goods scheme for AC components.

**Source:** https://tubepipeindia.com/hindalco-to-establish-indias-first/

---

## 3. Wieland Group — East Alton, IL expansion

**Who:** Wieland Group (Germany — ~400 kt/yr Cu products globally; Ulm-headquartered); Wieland North America operates former Olin Brass and adjacent assets.

**What:** **USD 500 million expansion** announced at East Alton, Illinois (Mar 2025). Additional USD 27 million at Pine Hall, NC (Dec 2024).

**Significance:** US re-industrialisation / nearshoring thesis. Substantial capacity coming online in North America for Cu rolled and tube products.

---

## 4. Gerdau Ouro Branco — Primetals + PSI Metals Melt-shop MES

**Who:** Gerdau Ouro Branco integrated steel mill (Brazil).

**What:** Combined order to **Primetals Technologies + PSI Metals** for Melt-Shop **Manufacturing Execution System (MES)**.

**Pattern:** Primetals for the L2 / automation side, PSI Metals for the MES standard-product side. Illustrates the canonical "buy L2 from the OEM, buy MES from the specialist" playbook.

**Why tube-plant-relevant:** same pattern maps directly to a copper tube plant's L2 + MES architecture.

**Source:** https://www.primetals.com/press-media/news/primetals-technologies-and-psi-metals-receive-order-for-melt-shop-manufacturing-execution-system-mes-from-gerdau-ouro-branco

---

## 5. Jindal Stainless — Primetals Level 2 for AOD converter + SAP BW/4HANA

**Who:** Jindal Stainless (India).

**What, automation side:** **Primetals Level 2 system digitalising know-how** for the AOD (Argon-Oxygen-Decarburisation) converter. The L2 captures multi-decade operator expertise in a mathematical + ML model, allowing consistency and continuous improvement.

**What, enterprise side:** **Adopted SAP BW/4HANA** — first in the Indian manufacturing ecosystem to do so — reporting 10–15× faster query performance.

**Tube-plant lesson:** digitalising process know-how into an L2 is a repeatable pattern; a copper tube plant can apply the same concept to extrusion / pilger / draw schedules.

**Sources:**
- https://www.primetals.com/press-media/news/level-2-system-from-primetals-technologies-digitalizes-know-how-for-jindal-stainless-aod-converter
- https://www.jindalstainless.com/press-releases/jindal-stainless-leads-digital-innovation-in-the-manufacturing-industry-with-adoption-of-bw-4hana/

---

## 6. JSW Salem — Primetals process automation for meltshop

**Who:** JSW Salem Works (India).

**What:** Primetals Technologies L2 / process-automation package for the meltshop.

**Why cite:** shows the Indian-market precedent for Primetals L2 / process control, relevant if an Indian copper-tube producer wants a similar partner for L2.

**Source:** https://www.aist.org/primetals-technologies-to-provide-process-automation-solution

---

## 7. ArcelorMittal — Hot strip mill automation upgrade (Primetals)

**Who:** ArcelorMittal (global steel major).

**What:** Extensive hot-strip-mill automation upgrade by Primetals; L1 and L2 modernisation on an operating brownfield mill.

**Lesson:** brownfield L1/L2 retrofit is routine for the right partner; expect 12–18 months engineering, coordinated shutdown windows, and a clear guarantee of "no net production loss during cut-over" written into the contract.

**Source:** https://www.primetals.com/press-media/news/arcelormittal-chooses-primetals-technologies-for-extensive-hot-strip-mill-automation-upgrade

---

## 8. Jindal Saw — Infor LN ERP across divisions

**Who:** Jindal Saw (India). Ductile iron pipe, large-diameter pipe, seamless pipe divisions.

**What:** **Infor LN (formerly Baan LN)** as the cross-division ERP.

**Why cite:** demonstrates that non-SAP ERPs are a viable choice in metals — particularly where industry-specific functionality (Infor LN's pipe-industry depth) outweighs SAP's breadth.

**Source:** https://www.scribd.com/document/85070175/Case-Study-ERP-JindalSaw

---

## 9. Mueller Industries — North America vertically integrated model

**Who:** Mueller Industries (Collierville, TN). About 15 % of global Cu tube share; only vertically integrated Cu tube + fittings + brass rod producer in North America. Streamline® brand.

**What:** long-standing model of owning the chain — from cathode-adjacent supply through drawn tube through fittings. Explains why Mueller sets the price signal in NA market.

**Sources:**
- https://www.muellerindustries.com/
- https://muellerstreamline.com/
- https://en.wikipedia.org/wiki/Mueller_Industries

**Lesson:** vertical integration is the strategic defence against LME-driven margin compression. Hindalco Waghodia is the Indian answer to the same question.

---

## 10. Digital Twin in metalworking — longitudinal case study (2025 Frontiers)

**Who:** Anonymised metalworking producer (published peer-reviewed).

**What:** DT across turning / milling / welding / material-flow; real-time data integration; longitudinal 5-year evaluation.

**Reported outcomes:**
- **30 %** reduction in material waste.
- **40 %** decrease in reject rate of milled parts.
- **233 %** return on investment over 5 years.

**Specific DT modes used:**
- Milling process optimisation — identifying feed-rate / spindle-speed anomalies; virtual simulation to lower pass depth and increase cooling → 40 % reduction in reject rate.
- Injection-moulding material efficiency — modelling real-time temperature/pressure; 30 % material waste reduction.
- Oil-refinery adjacent case: 15 % energy efficiency improvement, 18 % emissions reduction.

**Why this matters for a tube plant:** the same DT patterns transfer to pilger / draw / inner-grooving with similar or better ROI, given the repetitive, well-instrumented nature of the process.

**Source:** https://www.frontiersin.org/journals/mechanical-engineering/articles/10.3389/fmech.2025.1655565/full

---

## 11. Panagou et al. — Hot rolling mill DT (Italian steel industry)

**What:** used DT to simulate states and conditions, select reliable maintenance-related sensors, and combine real + DT-simulated data in a PdM framework. Cloud-based platform supporting maintenance decisions.

**Why this matters:** direct analogue of what a copper tube plant can do with its pilger main drive bearings, spinner-block drive bearings, and furnace fans — assets that share the rotating-machinery signature and thermal-model structure.

**Sources:**
- https://arxiv.org/html/2509.24443v1
- https://pmc.ncbi.nlm.nih.gov/articles/PMC11057655/

---

## 12. Oldsmar, Florida water plant (2021) — OT cyber incident

**What:** Attacker gained remote access via an authorised remote-access tool and briefly attempted to change chlorine levels in the drinking-water treatment process.

**Why the council cites this:** canonical example cited in IEC 62443 rollouts. Illustrates that the common attacker vector is **authorised remote access** being weakly controlled, not sophisticated zero-days.

**Lesson for a copper tube plant:** jump host in DMZ with MFA and session recording; no standing VPN; named vendor accounts; time-limited approvals.

**Source:** https://www.baculasystems.com/blog/iec-62443-security-standard/

---

## 13. Hailiang Texas base — new North American capacity

**Who:** Hailiang Group.

**What:** Hailiang Texas base for North American Cu tube supply; part of the company's global footprint diversification.

**Why cite:** shows the Chinese-major → North American footprint move, alongside Wieland's East Alton expansion. Combined, they reshape NA supply-side economics for Cu tube.

**Sources:**
- https://www.hailiang.us/
- https://hailiang.us/base/hailiang-texas-base-12.html

---

## 14. Sri City — India's "Cooling City"

**What:** Sri City, Andhra Pradesh — hosts 6 AC manufacturers + 12 AC component manufacturers. A purpose-built cluster for the white-goods ecosystem. Strong policy tailwind via PLI White Goods scheme.

**Why cite:** for users planning an India tube plant, co-location with Sri City (or Sanand / Aurangabad / Neemrana) is a structural advantage, not just a nicety.

**Source:** https://www.pib.gov.in/PressReleasePage.aspx?PRID=2064740

---

## 15. Pattern library — what to extract from these cases

1. **Yield targets** from Hailiang (~93 %) set the modern bar.
2. **Vertical integration** (Mueller, Hindalco) is the enduring structural answer to margin volatility.
3. **Buy L2 from the OEM, MES from the specialist** (Gerdau / Jindal Stainless pattern).
4. **ERP choice is industry-specific, not just vendor-brand** (Jindal Saw on Infor LN).
5. **Digital twin pays back (233 % / 5 yr)** — but only when tied to named use cases with owners and KPIs.
6. **OT cyber incidents are boring, not exotic** — segmentation, identity, and monitored remote access catch 80 % of risk.
7. **Policy matters** — India PLI + state incentives can shift the IRR of a new tube plant by several percentage points; don't leave them on the table.
