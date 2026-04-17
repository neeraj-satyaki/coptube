# copper-tube-automation-experts — Skill README

A seven-expert council skill for Claude covering copper tube manufacturing and the complete automation/IT stack around it (sensors, drives, PLC, SCADA, Level 2, MES, ERP, historian, IIoT, digital twin, OT cybersecurity, reliability).

## What's inside

```
copper-tube-automation-experts/
├── SKILL.md                              # triggers + council orchestration
├── README.md                             # this file
└── references/
    ├── 01-process-expert.md              # 🏭 Dr. P — PhD process & automation engineer
    ├── 02-software-architect.md          # 🏗️ Arch — senior software architect
    ├── 03-qa-tester.md                   # 🧪 Quinn — QA / validation engineer
    ├── 04-developer.md                   # 💻 Dev — industrial developer
    ├── 05-manager.md                     # 📋 Mgr — dual-hat program manager
    ├── 06-cybersecurity-expert.md        # 🛡️ Cyber — OT cybersecurity specialist
    ├── 07-operations-expert.md           # 🔧 Ops — plant operations & reliability
    ├── industry-research.md              # sourced map of the industry with links
    └── deep-dives/
        ├── process-parameters.md         # temperatures, tolerances, ASTM specs
        ├── commissioning-playbook.md     # FAT / SAT / HAT playbook with gates
        ├── failure-modes-catalogue.md    # defects & troubleshooting
        ├── india-context.md              # PLI, clusters, Indian producers
        ├── digital-twin-iiot.md          # OPC UA vs Sparkplug, UNS, DT cases
        ├── standards-deep-dive.md        # ASTM / EN / JIS / IEC / ISA / ISO
        ├── capex-benchmarks.md           # CAPEX & OPEX with real numbers
        ├── vendor-deep-dives.md          # per-vendor product families
        └── case-studies.md               # real plants with real numbers
```

## What it does

When the user asks anything about copper tube processes, equipment, or the automation / IT / reliability stack around a tube mill, Claude assembles a seven-voice answer:

- 🏭 **Dr. P** — process physics, metallurgy, equipment
- 🏗️ **Arch** — ISA-95 architecture, protocols, PLC/SCADA/MES/ERP integration
- 🧪 **Quinn** — FAT/SAT/HAT, traceability, acceptance criteria
- 💻 **Dev** — PLC / HMI / L2 / MES code structure, real snippets
- 📋 **Mgr** — schedule, budget, vendor strategy, commissioning, contracts
- 🛡️ **Cyber** — IEC 62443 zones, identity, OT monitoring
- 🔧 **Ops** — OEE, PdM, spares, operator behaviour, energy per tonne

…followed by a **⚖️ Council consensus** block with a reconciled recommendation and next actions.

Deep-dive files are loaded on-demand based on the question — e.g., a cost question pulls in `capex-benchmarks.md`, a troubleshooting question pulls in `failure-modes-catalogue.md`, an India-specific question pulls in `india-context.md`, and so on.

## How to install as a Claude skill (.skill file)

1. Upload the `copper-tube-automation-experts.skill` file in Claude (Settings → Capabilities → Skills → Upload).
2. Or in Claude Code / Cowork, drop the folder into your skill directory.
3. Ask a tube-mill or automation question. The skill should trigger automatically; if not, nudge it with "use the copper tube automation experts" or "give me the council view on…".

## How to invoke without installing

Paste `SKILL.md` plus the seven persona files (plus any relevant deep-dive files) into a Project or a long system prompt. Claude will behave as the council for every message in that context.

## Example prompts

- "Design the Level 2 stack for a 30 kt/yr inner-grooved ACR copper tube line in Gujarat. Primary vendors, integration contracts, acceptance criteria."
- "We have a Schloemann 5500-ton extrusion press from the 1980s. Retrofit plan for PLC + Level 2 + MES that minimises downtime."
- "Our eddy-current on the LWC line has 12 % false-reject rate. Council, tell me how to debug."
- "What FAT evidence should I demand from the OEM for a cold pilger mill upgrade?"
- "Budget and schedule bands for a greenfield 40 kt/yr copper tube plant with full ISA-95 stack."
- "Design an OT cybersecurity architecture per IEC 62443 for an Indian brownfield copper tube plant with Siemens PLCs and a Windows 7 HMI legacy."
- "What predictive-maintenance wins should I target first on a mid-age copper tube plant, and how do I tie them into a digital twin?"
- "Walk me through how to apply for the PLI White Goods scheme for a new IGT plant in Sanand."

## Style the skill enforces

- Each expert's section is short (3–8 lines), in that expert's voice.
- Specific vendors, model families, standards and numbers — no generic "an automation system".
- Every vendor, standard or number is cross-referenced into `industry-research.md` or the relevant deep-dive file.
- Consensus block is always present — even if experts disagree.

## Notes on scope

- Works for adjacent non-ferrous tube (brass, cupronickel, aluminium) because the equipment and automation stack overlap heavily.
- Does NOT replace a real FEED study, FAT or vendor evaluation — it produces working-engineer guidance, not a binding deliverable.
- Uses only public, sourced information. No proprietary vendor brochures.

## Customising

- Add an eighth expert? Drop a new file in `references/` (e.g., `08-metallurgist-deep.md`) and reference it from `SKILL.md`.
- Narrow the domain (e.g., ACR only)? Edit the description frontmatter in `SKILL.md` and the trigger list.
- Add your own plant data? Put it in a separate file under `references/` and tell the skill to read it alongside `industry-research.md`.
