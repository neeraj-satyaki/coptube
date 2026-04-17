# Deep Dive — Failure Modes & Defects Catalogue

Troubleshooting reference for copper tube and tube-mill problems. Each entry: what it looks like, where it came from, how to detect it, how to fix it. The council cites this file whenever the user asks "what went wrong" or "how do I stop this."

---

## 1. Dimensional & geometric defects

### 1.1 Eccentricity — OD and ID not concentric
- **Looks like:** one side of the tube wall thicker than the other; varies around the circumference.
- **Root causes (in order of frequency):**
  1. Piercer mis-alignment at extrusion press.
  2. Mandrel tilt or off-centre floating plug in draw pass.
  3. Worn or mismatched die/plug geometry.
  4. Non-uniform billet temperature at press (off-centre induction heating).
  5. Non-uniform cooling after extrusion.
- **Detection:** inline ultrasonic 4-channel wall gauge (MAC Echomac FD), laser diameter + ultrasonic wall pair, offline micrometer on sectioned ring.
- **Fix:** re-align piercer/mandrel; die-tilt drawing technique (Semantic Scholar neutron-diffraction study); re-profile induction heater; verify billet residence-time distribution.
- **Source:** https://www.mac-ndt.com/blogs/press-room/eccentricity-inspection ; https://www.sciencedirect.com/science/article/abs/pii/S0264127516307791

### 1.2 Wall thickness variation along length
- **Root causes:** mandrel drift during pilger / draw, drive-speed pulsation, plug wear, lubrication film collapse on a fast pass, coiler back-tension irregularity.
- **Detection:** continuous ultrasonic or isotope wall gauge post-draw; statistical out-of-control flag on SPC chart.
- **Fix:** plug replacement schedule; review tension setpoints in Level 2; check spinner-block synchronisation.

### 1.3 Out-of-round (ovality)
- **Root causes:** uneven coil support during winding, poor straightener calibration, heavy LWC with insufficient internal support, coil handling by crane pad.
- **Detection:** laser OD gauge in two orthogonal planes; offline 3-point mic.
- **Fix:** re-set straightener rolls; enforce "no lifting by bare slings" in handling SOP.

### 1.4 Bow / straightness deviation
- **Root causes:** uneven cooling after extrusion/anneal, straightener worn, residual stress asymmetry.
- **Tolerance benchmark:** ≤ 2 mm per 1 m for ACR straight tube; tighter for heat-exchanger tube.
- **Fix:** straightener re-calibration; longer controlled-cooling section post-anneal.

### 1.5 Twist / spiral marking
- **Root causes:** rotating mandrel slip in pilger, asymmetric draw die set-up, guide-roll crown mismatch.
- **Fix:** replace/repack mandrel head bearings; check die-holder concentricity.

---

## 2. Surface defects (outside diameter)

### 2.1 Scratches
- **Root causes:** worn or damaged guide rolls, chipped die inlet, contamination in the draw lubricant, damaged straightener pads, hook/lifter contact post-finish anneal.
- **Fix:** inspect all contact surfaces regularly; polish/replace rolls; filter lubricant; review handling path.

### 2.2 Die lines
- **Root causes:** die wear, broken bearing-surface polish, particulates in lubricant, inadequate lubrication.
- **Fix:** shorten die-change interval; improve filtration to 5–10 µm; re-polish die; confirm drawing speed vs. lubricant regime.

### 2.3 Scale / oxidation marks
- **Root causes:** furnace atmosphere upset (dew point too high, H₂ purity drop), leak into anneal cover, post-anneal exposure to moist air.
- **Fix:** dew-point sensor verification; atmosphere-gas purity audit; inspect bell / roller-hearth seals.
- **Source:** Beijing Holland bell anneal documentation.

### 2.4 Pits / inclusions
- **Root causes:** cathode contamination (Pb, Bi, S), dross carry-over from melt, oxide inclusion in cast mother tube, particulate in the extrusion container.
- **Detection:** ECT encircling coil (Foerster, BKN, Cangxin); rotating ECT for small discrete pits.
- **Fix:** cathode QA tighten (LME Grade A compliance); improve skimming; mould level control in casting; scrap discipline in melt.
- **Source:** https://www.mac-ndt.com/blogs/press-room/eccentricity-inspection and MAC inclusion articles.

### 2.5 Roping / orange peel
- **Root causes:** large / inhomogeneous grain after anneal; over-annealing; severe strain path.
- **Fix:** tighten anneal temperature/time; consider intermediate anneal frequency; confirm cold-work % before final anneal.

---

## 3. Surface defects (inside diameter)

### 3.1 Ant-nest corrosion (formicary corrosion)
- **Looks like:** fine tunnelled corrosion on ID, leading to diametric cracks at bends; red-brown / dull-black cuprous oxide films.
- **Root cause:** simultaneous presence of moisture, oxygen, and a short-chain carboxylic acid (formic / acetic) — common in refrigeration with polyol-ester oils and contaminated interiors.
- **Detection:** failure cross-section shows pit tunnels with fine longitudinal cracks bridging pitted regions.
- **Fix at producer level:** meet ASTM B280 interior cleanliness (≤ 0.0035 g/ft²), dehydrate, cap. At user level: material selection (OFC vs DHP), ester-oil specification, nitrogen purge during brazing.
- **Source:** https://www.researchgate.net/publication/259521758_Failure_analysis_of_copper_tube_used_in_a_refrigerating_plant ; phosphorus effect studies.

### 3.2 Inner-groove tooth damage
- **Root causes:** floating-ball misalignment, mandrel spindle vibration, coolant contamination, speed mismatch between grooving head and line speed.
- **Detection:** sample-cut and microscopy; optical bore-scope at sampling station.
- **Fix:** re-centre ball; spindle bearing replacement; tighten coolant filtration; verify Level 2 speed coordination.

### 3.3 ID cleanliness failures
- **Root causes:** draw-lubricant carry-over, incomplete dehydration, moisture ingress post-anneal.
- **Detection:** ASTM B280 residue test (gravimetric).
- **Fix:** improve dewatering; verify cap / plug / crimp before packaging.

---

## 4. Metallurgical defects

### 4.1 Chevron / centreline cracks
- **Root causes:** over-severe cold draw pass on inhomogeneous mother tube; billet discontinuity propagated through extrusion.
- **Detection:** longitudinal sectioning + etching; ultrasonic at finished stage.
- **Fix:** reduce pass reduction; pre-screen cast mother tubes; verify billet conditioning.

### 4.2 Grain-size drift
- **Target:** 0.015–0.050 mm for ACR per ASTM B280 and customer specs.
- **Root causes:** anneal temperature drift; residence-time variability; atmosphere excursion.
- **Detection:** offline grain-size per ASTM E112 (sample per coil).
- **Fix:** thermocouple calibration; Level 2 recipe lock; atmosphere monitoring.
- **Source:** OCI Group metallurgical article.

### 4.3 Freeze-split / longitudinal split
- **Applies:** installed plumbing systems; rarely producer defect.
- **Looks like:** fish-mouth split on elbows; outward bulging.
- **Distinguish from:** manufacturing split, which typically exhibits clean fractography with no outward bulging.
- **Source:** https://ocig.com/ocig-institute/water-claims-copper-pipes-and-what-can-go-wrong/

### 4.4 Stress-corrosion cracking (SCC)
- **Conditions:** tensile stress + corrosive environment + susceptible microstructure (typically brass rather than pure Cu, but possible in Cu-Zn fittings).
- **Fix:** post-forming stress-relief anneal; environment control.

---

## 5. Automation / control failures

### 5.1 Level 2 model divergence after a coil stop
- **Symptom:** next coil sees wildly wrong roll-force or temperature prediction.
- **Root cause:** post-calc path skipped when operator aborted; adaptive gain captured spurious actuals.
- **Fix:** in the model code, bound adaptation per cycle; always run post-calc on any coil that reached position X; trap abnormal terminations.

### 5.2 Phantom cycle on PLC restart
- **Symptom:** a motor starts briefly after power return with no operator command.
- **Root cause:** retentive bit left set after E-stop; no clear-down logic in startup OB.
- **Fix:** always-reset logic in the startup block for every equipment FB's "active" bit; unit tests covering the restart case.

### 5.3 MES timezone bug around DST
- **Symptom:** night shift's coils appear in the wrong day in OEE reports.
- **Root cause:** mixing local time and UTC across L1 / L2 / L3.
- **Fix:** store UTC everywhere, display local time only at the edge; unit test the DST transition.

### 5.4 Historian tag rename breaks analytics silently
- **Symptom:** KPI dashboards flatline at the old value.
- **Fix:** tag renames go through a change-control board; analytics layer uses aliases that route to the current tag; monitor for "staleness" (no updates for X minutes).

### 5.5 Drive-pair speed imbalance (tension pull)
- **Symptom:** tube loops or snaps between stands / draw passes.
- **Root cause:** encoder drift, drive gain mismatch after service, missed sync signal.
- **Fix:** encoder calibration schedule; gain sync test at SAT + each shutdown restart; master/slave tension control with overspeed trip.

### 5.6 ECT high false-reject rate
- **Symptom:** > 10 % reject rate, most rejects downstream re-inspection passes.
- **Root cause:** probe centring off, guide vibration, calibration notch depth drift, frequency not tuned to wall.
- **Fix:** verify guide concentricity < 0.1 mm; re-calibrate against EDM-notch standard per shift; retune frequency per product code.
- **Source:** https://www.thefabricator.com/tubepipejournal/article/testingmeasuring/eddy-current-testing-strategies-for-copper-tube

---

## 6. Equipment mechanical failures (by asset class)

### 6.1 Extrusion press
- Container liner wear → eccentricity, seizure risk. Replace on wear-band threshold.
- Stem seal failure → hydraulic leak, slow cycle. Seal kit on 3–6 month cycle.
- Piercer misalignment → eccentricity + mother-tube wall variation. Laser alignment quarterly.
- Hydraulic oil contamination → valve sticking, erratic pressure. Quarterly oil analysis; 10-µm filtration.
- Heater-band failure → localised cold spot in billet; blotch on mother tube. IR thermography quarterly.

### 6.2 Cold pilger mill
- Mandrel wear / breakage → wall variation, tube scrap. Hardness check; replace at cycle-count threshold.
- Crank-drive bearing failure → vibration, main drive trip. Vibration PdM on main drive.
- Die wear → OD variation, surface lines. Die-change on wear indicator.
- Lubrication clogging → scoring. Filter-change and sampling schedule.

### 6.3 Draw bench / spinner block
- Die scoring → surface lines. Daily die inspection.
- Plug drift → wall variation. Plug-change cycle by coil count.
- Chuck slip → tail-end of coil lost. Chuck pressure sensor + alarm.
- Winder bearing → vibration → coil distortion. Vibration PdM.

### 6.4 Anneal furnace (bell / roller-hearth)
- Heating element burn-out → cold zone → grain-size drift. Redundant thermocouples; element-resistance monitoring.
- Atmosphere excursion → oxidation on tube surface. Dew-point + O₂ trim control.
- Thermocouple drift → process drift. Annual calibration.
- Fan motor bearing → hot spot / atmosphere distortion. Vibration PdM.

### 6.5 Inner-grooving line
- Spindle bearing → surface finish degrades. Vibration + temperature trending.
- Floating-ball positioning → groove depth variation. Regular sampling, offline microscope.
- Cooling blockage → overheating, premature tool wear. Flow-switch on coolant.

### 6.6 Coiler & packaging
- Winder motor → coil not formed. Drive fault capture.
- Wire-feed (strapping) → pack-out stops. Wire-stock sensor.
- Label printer → shipping error. Redundant barcode verify.

---

## 7. How to use this catalogue during an incident

1. Freeze the data window: last 15 min of all L1/L2/L3 tags around the event.
2. Categorise: dimensional / surface / metallurgical / automation / mechanical.
3. Map to this catalogue; list top 3 candidate root causes.
4. Apply a structured RCA method — 5-Whys or fishbone — with the shift team.
5. Capture: what changed in the last 24 h (recipe, operator, raw material lot, maintenance work, software release). Change is where 80 % of incidents live.
6. Close with a corrective action in the CMMS linked to a PM task.
