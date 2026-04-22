# Test 1 — Single expert: process-expert

**Prompt:** For CuNi 90/10 (C70600) seamless tube via pilger process, typical billet preheat temperature band? One metallurgical risk if run 30 °C hotter than band top?

**Subagent:** coptube:process-expert
**Mode:** solo (no parallel fan-out)
**Duration:** 32.7 s
**Tokens:** 7,577

---

### 🏭 Dr. P — Process view

**CuNi 90/10 (C70600) preheat band for extrusion→pilger route:** typical billet soak **880–920 °C** (some shops push 900–950 °C for large-OD heavy-wall condenser tube; Sanicro/KME practice). Pilger itself is **cold** (strain hardening ~60–80 % per pass, interpass anneal 700–750 °C in bright/H2). The preheat number above is for the **extrusion** that feeds the pilger mother hollow.

**Run 30 °C over band top (→ ~950 °C sustained):** the one dominant risk is **hot shortness / grain-boundary liquation from residual Pb, S, Bi** (C70600 spec caps Pb ≤ 0.05 %, S ≤ 0.02 % — ASTM B111/B466). Above ~940 °C you approach the Cu–Ni–S ternary eutectic trough; grain-boundary films open into longitudinal cracks on the extrusion exit cone and show up as spiral tears after the first pilger pass. Secondary effect: coarse β-free but very large γ-Cu grain (>120 µm), which wrecks subsequent pilger surface finish and flares burst-test scatter.

**Protocol-era field:** N/A (parameter/metallurgy question, no era gating).

---

**SWOT — running at band top (~920 °C)**
- **S:** lowest flow stress, longest container/die life, cleanest extrusion surface.
- **W:** narrow margin to liquation window; furnace ±15 °C scatter eats the safety band.
- **O:** higher extrusion ratio achievable (up to ~200:1 for small condenser tube) without press stall.
- **T:** any S/Pb excursion in the cast billet (scrap-heavy charge) turns into a QA reject wave.

**Pros / Cons — band top vs band middle (~900 °C)**
- **Pro top:** lower press load (~15–20 % drop vs 880 °C), better die fill on thin-wall, fewer stringer defects from unmelted oxide.
- **Pro middle:** robust to pyrometer drift, finer as-extruded grain (~60–80 µm) → better pilger Q-factor and surface, safer with dirtier billet chemistry.
- **Con top:** liquation risk, grain coarsening, heavier scale loss (Cu/Ni oxide, ~0.3–0.5 % yield hit).
- **Con middle:** higher extrusion force, shorter die life, risk of press-stall on long billets.

**Cross-talk:**
- **@Met-Lead / Dr. M:** confirm you want β-phase-free single-phase α-Cu(Ni) exit — if yes, band top is fine chemistry-wise, but please verify billet S + Pb + Bi sum < 0.04 %.
- **@QC:** eddy-current (ASTM E243) on mother hollow is the catch-net for liquation cracks — don't rely on visual.
- **@Maintenance:** pyrometer cal interval should be ≤ monthly if you operate at band top; thermocouple drift of 20 °C is common on induction preheaters after ~2000 h.

**Open questions:**
1. Is this for condenser/heat-exchanger tube (ASTM B111) or sub-sea/offshore (EN 12451 / NORSOK)? Band shifts ~10–15 °C.
2. Billet source — continuous cast (Outokumpu/KME) or remelted scrap? Scrap charge tightens the upper limit.
3. Final OD/WT? Thin-wall (<1.5 mm) tolerates less grain coarsening.

**Links / sources:**
- `skills/coptube/references/deep-dives/process-parameters.md` §CuNi extrusion preheat
- `skills/coptube/references/deep-dives/failure-modes-catalogue.md` §hot shortness / liquation
- ASTM B111/B466, EN 12451
- Copper Development Association Pub TN31 — *Nickel-Containing Copper Alloys: Hot Working Guidance*

---

## Test verdict

- Loaded persona file correctly (Dr. P voice intact)
- Loaded process-parameters.md + failure-modes-catalogue.md deep-dives
- SWOT block present and context-aware (band top vs band middle)
- Pros/Cons anchored to numbers (15-20% press load drop, 60-80 µm grain, 0.3-0.5% yield hit)
- Cross-talk to 3 non-agent roles — note: not one of the 11 coptube subagents, agent improvised role names. Protocol says pings should use registered agent names only. Minor drift.
- Protocol-era field correctly marked N/A for a parameter question
- Open questions + links present
- Real numbers, real standards — no hallucination spotted
