# Deep Dive — Process Parameters, Set-points, Tolerances

Working numbers the council cites when a specific value is asked for. All ranges are industrially reported; any individual plant should verify against its own OEM specs and customer standards before acting.

---

## 1. Melting and Casting

| Parameter | Typical value / range | Source / note |
|---|---|---|
| Cathode purity (feedstock) | ≥ 99.95 % Cu (LME Grade A) | ASTM B115, BS EN 1978 |
| Melt temperature | 1 200–1 300 °C in shaft/reverberatory furnace | chinatialloy.com process note |
| Deoxidiser | Cu-P master alloy, 13–15 % P, ~1.8–1.9 kg per t Cu | rubycopper.vn process |
| Casting rate (shaft furnace) | ~1 t/h (small) to 8 t/h (large) | industry typical |
| Mother-tube cast dimensions | ~90 mm OD × 23.5 mm wall (horizontal CC) | rubycopper.vn |
| Mother-tube length | up to 19 m, ~890 kg per log | rubycopper.vn |
| Billet diameter (extrusion route) | 7″ (178 mm) common; 12″ (305 mm) for heavy | machinetools.com Schloemann listings |
| Billet preheat | 1 535 °F / ~835 °C | copper.org "How Do They Do That" |
| Oxygen content, OFC (up-cast) | < 10 ppm | ccmcoppermouldtube.com up-draw description |

## 2. Extrusion

| Parameter | Typical value / range | Source / note |
|---|---|---|
| Hot extrusion temperature window | 600–1 000 °C (Cu); above dynamic recrystallisation | deringerney.com; Wikipedia extrusion |
| Billet charge temperature, practice | 700–850 °C; 835 °C typical for ACR | copper.org; Frontiers FEM study |
| Extrusion pressure | 100–1 500 MPa direct; 10–15 kbar hydrostatic (research) | Ferro-Tic; US3774431A patent |
| Extrusion ratio (Cu tube) | typical 40–100; can exceed 1 000 for small refrigeration tube | Ohio Univ thesis |
| Extrusion speed | 30–300 m/min (rod / heavy); up to 15 m/s (hydrostatic research) | Ohio Univ; US3774431A |
| Tube-out-of-press length | typically 25–90 m (mother tube) | SMS group, copper.org |
| Exit OD after extrusion | ~70 mm (ACR mother tube); up to 250 mm (industrial) | copper.org |
| Eccentricity requirement (mother tube) | ≤ 5 % preferred, ≤ 10 % acceptable | industry standard; thefabricator.com on ECT |
| Press tonnage families | 1 500 / 2 500 / 4 000 / 5 500 / 7 000 US tons | NME, Schloemann catalogue |
| Dummy-block shell (copper oxide) | ~3–5 % of billet, recycled to refining | copper.org |

## 3. Cold Pilger Rolling

| Parameter | Typical value / range | Source / note |
|---|---|---|
| Cross-section reduction per pass | up to 90 % for Cu; 75–80 % stainless; 70 % Ti alloys | thefabricator.com; Total Materia |
| Tube OD range (capacity) | 8–230 mm OD; 0.5–30 mm wall | Semantic Scholar mandrel paper |
| Typical Cu tube deformation strength | ~400 N/mm² (up to 1 500 N/mm² for alloys) | thefabricator.com |
| Surface roughness achievable | Ra < 0.02 µin (special) / typically Ra < 0.5 µm | thefabricator.com; ultrasonic processing paper |
| Saddle reciprocation | mechanical crank drive, forward + return stroke both form | SMS cold pilger description |
| Output rate (mother tube stage) | 12–18 m/min | rubycopper.vn |

## 4. Cold Drawing

| Parameter | Typical value / range | Source / note |
|---|---|---|
| Reduction per pass | 15–35 % per cold draw pass | pilgermilltechnologies.com |
| Die angle (fixed plug) | 28–32° total included; plug 20–24° | thefabricator.com cold drawing |
| Bearing length | 10–15 % of die diameter | thefabricator.com |
| Combined-draw (linear) speed | 40–50 m/min | rubycopper.vn |
| Spinner-block finish-draw speed | up to 1 000 m/min | rubycopper.vn |
| Smallest practical finish OD | ~4 mm | rubycopper.vn |
| Straight-drawing max OD | ~42 mm (output of straight-tube draw machine) | rubycopper.vn |
| Anneal between passes | typically after 60–80 % total reduction | industry practice |
| Lubricant viscosity | 8 000 – 100 000+ SUS depending on alloy and wall | thefabricator.com |

## 5. Annealing

| Parameter | Typical value / range | Source / note |
|---|---|---|
| Intermediate anneal temperature (Cu) | 400–600 °C | ASM Handbook; process practice |
| Final anneal temperature (soft temper) | 500–700 °C | ASTM B280 guidance, OEM recipes |
| Bell-type furnace max temperature | up to 1 100 °C (for carbon steel, etc.) | Therelek; Moran |
| Roller-hearth bright anneal for Cu tubes | max 950 °C typical | Nianda |
| Protective atmosphere | 100 % H₂ or N₂-H₂ mix; dew point tightly controlled | Beijing Holland; Tenova HPH |
| Target grain size after final anneal | 0.015 – 0.050 mm (ACR tube typical) | ASTM E112, ASTM B280 |

## 6. Inner-Grooving

| Parameter | Typical value / range | Source / note |
|---|---|---|
| Grooving head speed | up to 49 000 rpm (SMS VNVG 2000) | SMS copper tube plants |
| Line speed | up to 100 m/min | SMS |
| Inner-groove tube OD range | 5.0 – 12.7 mm (MetTube IGT range) | mettube.com |
| Inner-groove wall thickness | 0.24 – 0.55 mm (MetTube IGT range) | mettube.com |

## 7. Product Standards and Finished-Tube Tolerances (ACR focus)

### ASTM B280 — Seamless Copper Tube for ACR Field Service (C10200 / C12000 / C12200)

- Material: ≥ 99.9 % Cu + Ag; P 0.015 – 0.040 %.
- Oxygen max: 10 ppm for deoxidised (UNS C12200).
- Temper: H58 (hard drawn) for straights; O60 (soft annealed) for coils — bright annealed after coiling.
- Interior cleanliness residue limit: 0.0035 g/ft² (0.038 g/m²) both for soft coils and straight lengths.
- End closure: capped / plugged / crimped after dehydration.
- Designated by **actual OD** (not nominal pipe size).
- Yield strength, annealed: 5 100 psi (~35 MPa).

Source: ASTM B280-20, https://store.astm.org/b0280-20.html ; Winland Metal — https://winlandmetal.com/standard/astm-b280-acr-copper-tube ; Engineering Toolbox — https://www.engineeringtoolbox.com/copper-tube-astm-280-d_1084.html

### Other tube / pipe standards

| Standard | Scope | Source |
|---|---|---|
| ASTM B42 | Seamless Cu pipe, standard sizes (1/8″–12″) | copper.org |
| ASTM B68 | Seamless Cu tube, bright annealed — refrigeration, fuel-oil, gasoline | copper.org |
| ASTM B75 | Seamless Cu tube, general engineering (round, square, rectangular) | copper.org |
| ASTM B88 | Plumbing tube, Types K / L / M / DWV (designated by nominal size) | copper.org |
| ASTM B251 | General requirements, wrought seamless Cu & Cu-alloy tube | copper.org |
| EN 1057 | Plumbing Cu tube (EU) | EN |
| EN 12735-1 / -2 | ACR seamless Cu tube (EU) | EN |
| JIS H3300 | Seamless Cu and Cu-alloy tube (Japan) | JIS |

Copper.org reference: https://www.copper.org/applications/plumbing/techref/tpf_stds/tube_pipe_stds.html and the Copper Tube Handbook https://www.copper.org/publications/pub_list/pdf/copper_tube_handbook.pdf

### Typical Type-K/L/M wall thicknesses (US plumbing, ASTM B88)

| Nominal | Type K | Type L | Type M | Source |
|---|---|---|---|---|
| ½″ | 0.049″ | 0.040″ | 0.028″ | ASTM B88 |
| ¾″ | 0.065″ | 0.045″ | 0.032″ | ASTM B88 |
| 1″ | 0.065″ | 0.050″ | 0.035″ | ASTM B88 |

(European designations: Type X / Y / Z per EN 1057.)

### Dimensional tolerances commonly quoted by ACR tube producers

- OD tolerance: ±0.05 mm (small OD); ASTM tables specify per OD band.
- Wall thickness: ±10 % typical; ±8 % for premium.
- Straightness: 2 mm per 1 m for straight tube.
- Eccentricity: ≤ 10 % (finished); tightened below for premium heat-exchanger tube.
- Surface residue: ≤ 0.0035 g/ft² ≈ 0.038 g/m² (ASTM B280 interior).

## 8. Non-Destructive Testing (ECT) Parameters

| Parameter | Typical value / practice | Source |
|---|---|---|
| Through-coil frequency | 100 Hz – 1 MHz, tuned to wall | Foerster application notes; thefabricator.com |
| Encircling coil, test speed | up to 120 m/min for LWC | thefabricator.com |
| Rotating probe, RPM | 3 000–6 000 rpm typical | thefabricator.com |
| Calibration standard | tube with EDM notches, typ. 10 % / 5 % wall | ASTM E243 |
| Guide vibration tolerance | ~< 0.1 mm radial for thin-wall Cu | thefabricator.com |
| Acceptance | per ASTM E243, ISO 9303 or customer-specific | ASTM / ISO |

## 9. Benchmarks — modern vs. legacy lines

| KPI | Modern (cast-and-roll, e.g., Hailiang 5th-gen) | Legacy (extrusion + multi-draw) | Source |
|---|---|---|---|
| Finished-tube yield from cathode | ~93 % | 85–91 % | Hailiang / industry |
| Specific energy | ~1 200–1 500 kWh/t | 1 500–1 800 kWh/t | Hailiang 5th-gen reports –300 kWh/t |
| Labour per t | 1× (modern baseline) | ~3× higher | Hailiang |
| Changeover time | < 30 min on inner-groove | 60–120 min | SMS VNVG |
| Typical OEE target | 85 %+ | 60–75 % | industry rule of thumb |

Hailiang 5th-generation source: https://news.metal.com/newscontent/101549361/
