---
name: hmtc-standards
description: "Build Heavy Metal Tested & Certified (HMTc) standards documents (.docx) for the Paleo Foundation. Use whenever asked to create HMTc standards, per-metal documents, Standards Briefings, or factual audits. Triggers: 'HMTc', 'heavy metal standards', 'Paleo Foundation standards', 'standards briefing', metal names (Pb/As/Hg/Cd/Cr/Ni/Sn/Al) in certification context, product categories (infant foods, cosmetics, cleaning, supplements, toys, pet foods, etc.), 'build the next category', 'start [category]', anti-circumvention language, or regulatory value audits. Covers the full workflow: consolidated Standards Briefing with 8 per-metal sections, master summary table, factual audit, and rebuild. Always use this skill for HMTc work even if the request seems simple."
---

# HMTc Standards Document Builder — v5.0

## Overview

This skill builds publication-ready HMTc standards for the Paleo Foundation's
Heavy Metal Tested & Certified program. Each product category produces ONE
consolidated Standards Briefing containing all 8 metals, a master summary
table, and all supporting sections.

The 8 metals: Lead (Pb), Arsenic (iAs), Mercury (Hg), Cadmium (Cd),
Chromium (Cr), Nickel (Ni), Tin (Sn), Aluminum (Al).

**Authors: K. Pendergrass (CEO), K. Eyer, D. Aleru.**
**NEVER use "Victor Eyer" or "Oluwatobi Aleru."**

## Before Starting Any Build

Read these project knowledge documents in order:

0. **`HMTc_Governing_Principles.md`** — READ FIRST. The five objectives
   that govern every decision: drive down contamination, protect consumers,
   protect brands, legal defensibility, scalable to 23 categories. Apply
   at every step.

1. **`HMTc_Step_Zero_Protocol_v1.3.md`** — Subcategory expansion AND all
   data sourcing: Expanded Subcategory List, Contamination Platform Map,
   Regulatory Floor Table (with Watch Items), Clean Platform Data Package
   (P90 via web search), Contaminated Platform Data Package (P10 via web
   search). No formula application. No slash notation.

2. **`HMTc_Step_One_Protocol_v1.5.md`** — Limit determination. Consumes
   all five Step 0 outputs. Dual-percentile formula: clean rows use P90,
   contaminated rows use P10. Clean floor rule. Direct ladder snap. No T,
   no VME. Produces the Master Limit Table.

3. **`HMTc_Step_Two_Protocol_v1.2.md`** — Document generation: from
   locked Master Limit Table to Standards Briefing. Page sequence,
   per-metal section structure, Notes column rules, formatting specs.

4. **`HMTc_Step_Three_Protocol_v1.2.md`** — Validation, 11-step factual
   audit, rebuild cycle, and 9 pre-publication gates. Nothing ships
   without passing all 9 gates.

5. **`HMTc_Methodology_Reference_v5.0.md`** — Technical reference:
   dual-percentile formula, contamination platform protocol, regulatory
   anchors and confirmed corrections, speciation triggers, regulatory
   floor values, audit protocol details, publication presentation rules,
   document architecture and formatting.

6. **`HMTc_Clean_Benchmark_Policy.md`** — Policy rationale, settled
   decisions, rejected objections, dual-percentile design rationale,
   and the 6-move anti-circumvention argumentative structure.

Also read the `docx` skill at `/mnt/skills/public/docx/SKILL.md` for
docx-js best practices when generating .docx files.

## Pipeline (4 steps, no human gates)

**Step 0** — Data sourcing (per Step Zero Protocol):
Produces: Expanded Subcategory List, Contamination Platform Map,
Regulatory Floor Table, Clean Platform Data Package, Contaminated
Platform Data Package.
All via web search at runtime. No formula application.
Outputs pass programmatic validation, then pipeline proceeds.

**Step 1** — Limit determination (per Step One Protocol):
Consumes all five Step 0 outputs. Two formula variants:
- Clean/Unsplit: `Limit = L_down( min( P90_clean, Regulatory_Anchor, 2×M ) )`
- Contaminated (affected metals): `Limit = L_down( min( P10_dirty, Regulatory_Anchor, 2×M ) )` then `max(Limit, Limit_clean)`
Computation order: clean/unsplit first → contaminated → clean floor rule
→ 2×M verification pass → regulatory floor check.
Produces Master Limit Table.
Outputs pass programmatic validation, then pipeline proceeds.

**Step 2** — Document generation (per Step Two Protocol):
Build the Standards Briefing from the locked Master Limit Table.
One document, all 8 metals, master summary table. No computation.
Pure formatting and presentation.

**Step 3** — Validation and delivery (per Step Three Protocol):
3A: Structural validation (programmatic)
3B: 11-step hallucination-resistant factual audit (programmatic)
3C: Full rebuild with corrections (not partial patches)
Re-run 3A and 3B on the rebuilt document
3D: 9 pre-publication gates — all must PASS
3E: Final delivery with Build Summary

## Critical Rules

1. **Never expose formula math in published documents.** No percentile
   values, M values, rounding calculations, or internal tags in Notes.
2. **One row per expanded subcategory.** Every contamination platform split
   gets its own row. No slash notation. The Expanded Subcategory List from
   Step 0 defines the exact rows for every table.
3. **Master summary table required** in every briefing (all subcategories
   × 8 metals).
4. **Published values use the primary increment ladder only:**
   1, 2, 3, 5, 10, 15, 20, 25, 50, 100, 200, 500, 1000, 1300, 1500,
   2000, 5000, 10000
5. **Limits set by clean benchmark, not contaminated platform.** Do not
   loosen to accommodate. Do not raise achievability concerns. Read the
   Clean Benchmark Policy — these are settled decisions.
6. **Anti-Circumvention makes 6 moves.** Move 6 is the clean benchmark
   principle with dual-percentile framing. All 6 mandatory in every
   Standards Briefing.
7. **Never fabricate citations.** If you don't have a real source, say so.
8. **Regulatory Floor is the absolute ceiling.** Checked last. Overrides
   everything.
9. **The Standards Briefing is the published product.** Per-metal working
   files are internal only and are never published.
10. **Metal order in document:** Pb → iAs → Sn → Ni → Cd → Cr → Al → Hg
11. **Every decision must serve all 5 governing principles.** If a decision
    serves one principle but undermines another, flag the conflict.
12. **Occurrence data selection is mechanized.** Clean platform: Path A
    (P90 of clean distribution) or Path B (5× LOQ). Contaminated platform:
    Path A (P10 of contaminated distribution) or Path B (HELD TO CLEAN).
    No third path. No expert judgment.
13. **No document ships without passing all 9 pre-publication gates.**
14. **The audit is 11 steps, not 9.** Steps 10 (formula compliance including
    clean floor rule) and 11 (regulatory floor compliance) are mandatory.
15. **No approval gates.** The pipeline runs end-to-end. Validation is
    programmatic. If a step fails, the pipeline stops with a specific
    error — it does not pause for human input.
16. **Clean floor rule.** The contaminated platform limit never falls below
    the paired clean platform limit for the same metal. If P10_dirty rounds
    below Limit_clean, set Limit_dirty = Limit_clean.
17. **No separate contaminated limit without data.** If contaminated platform
    occurrence data does not exist (Path B), the contaminated row is HELD
    TO CLEAN — it receives the same limit as the clean row.

## Confirmed Corrections (check every build)

1. Pb BMDL01 for nephrotoxicity: 0.63 µg/kg bw/day (NOT 0.50)
2. JECFA Al PTWI = 2 mg/kg bw/week. EFSA Al TWI = 1 mg/kg bw/week. Distinct.
3. EFSA MeHg TWI = 1.3 µg/kg bw/week. The 4.0 value is inorganic Hg.
4. Prop 65 Lead = MADL 0.5 µg/day (reproductive). NOT NSRL 15 µg/day (cancer).
5. ASTM F963 §4.3.5 — Ni and Sn are NOT among the 8 soluble elements.
6. FDA CTZ covers Lead ONLY. Cd, iAs, Hg are NOT finalized as of April 2026.
7. FDA CTZ dry infant cereals: 20 ppb (NOT 10).
8. FDA CTZ does NOT apply to infant formula.
9. Cd floors for infant foods come from EU (Reg. 2023/915), not FDA.
10. EU 2024/1987 Ni for liquid formula (§3.6.13.3): 100 ppb, no soy/non-soy
    distinction. Soy split only exists for powder (§3.6.13.1 vs §3.6.13.2).
11. EFSA Ni TDI is 13 µg/kg bw/day (2020 update). Not the 2015 value of
    2.8 µg/kg bw/day.

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 4.1 | April 2026 | Added mechanized CC selection (Rule 12), 9 gates requirement (Rule 13). |
| 4.2 | April 2026 | Removed all "Wait for approval" gates. Required for Inngest compatibility. |
| 4.3 | April 2026 | Rewrote Pipeline Summary to reflect corrected architecture. |
| 5.0 | April 2026 | **Dual-percentile model.** Replaced T, VME, CC×(1+T), and two-step rounding with: P90 for clean, P10 for dirty, clean floor rule, direct ladder snap, HELD TO CLEAN for missing dirty data. Updated all rules. Added Rules 16 (clean floor) and 17 (no limit without data). Updated reading list versions. Updated Pipeline Summary formula variants. Updated Move 6 to dual-percentile framing. |
