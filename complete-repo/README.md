# HMTc Program — Standards Generation System

## What This Is

The **Heavy Metal Tested & Certified (HMTc) Program** is a voluntary certification program operated by the **Paleo Foundation** (CEO: Karen Pendergrass). It sets parts-per-billion (ppb) limits for 8 heavy metals across 23 consumer product categories.

The 8 metals: **Lead (Pb), Arsenic (iAs), Mercury (Hg), Cadmium (Cd), Chromium (Cr), Nickel (Ni), Tin (Sn), Aluminum (Al).**

This repository contains the complete specification and reference documents needed to build the **standards generation system** — an automated pipeline that produces per-category Standards Briefing documents.

---

## START HERE

If you are a new collaborator, read these two documents first:

1. **`HMTc_New_Chat_Handoff_April_13.md`** — Everything decided on April 13, 2026: the formula, the rounding, the confidence ladder, verified Lead values, what's settled, what's eliminated, and exact instructions for producing corrected output.

2. **`HMTc_Pipeline_Failure_Modes_and_Critique.md`** — What went wrong in previous iterations and why. Prevents you from repeating solved problems.

Then read the protocol documents in the order listed below.

---

## Repository Contents

### The Handoff (read first)

| File | Purpose |
|------|---------|
| `HMTc_New_Chat_Handoff_April_13.md` | Complete summary of the April 13 methodology redesign. The formula, rounding rules, confidence ladder, verified Pb values, and instructions for new conversations. **Start here.** |

### Core Protocol Documents (read in this order)

| # | File | Version | Purpose |
|---|------|---------|---------|
| 0 | `HMTc_Governing_Principles.md` | v1.1 | The 5 non-negotiable principles. Includes the two-percentile-mechanisms clarification. |
| 1 | `HMTc_Step_Zero_Protocol_v1_3.md` | v1.3 | Data sourcing: subcategory expansion, regulatory floors, clean platform data (P90), contaminated platform data (P10), confidence ladder tiers |
| 2 | `HMTc_Step_One_Protocol_v1_5.md` | v1.5 | Limit determination: dual-percentile formula, clean floor rule, simplified rounding, 2×M check |
| 3 | `HMTc_Step_Two_Protocol_v1_2.md` | v1.2 | Document generation: Master Limit Table → Standards Briefing (.docx or JSON) |
| 4 | `HMTc_Step_Three_Protocol_v1_2.md` | v1.2 | Validation: 11-step factual audit, rebuild cycle, 9 pre-publication gates |
| 5 | `HMTc_Methodology_Reference_v5_0.md` | v5.0 | Technical reference: complete formula spec, regulatory anchors, confirmed corrections, audit protocol, formatting |
| 6 | `HMTc_Clean_Benchmark_Policy.md` | v3.0 | Policy rationale, dual-percentile design, anti-circumvention 6-move structure |

### Skill File

| File | Purpose |
|------|---------|
| `SKILL_v5_0.md` | Claude instruction set for building standards. Load as SKILL.md in a Claude project. |

### Category 1 Working Files

| File | Purpose |
|------|---------|
| `Category1_Step_0_Output_LOCKED.md` | Locked Step 0 output — 16 expanded subcategories, contamination platform map, regulatory floor table |
| `Category1_Pre_Build_Deliverables_1-5.md` | Pre-build deliverables for Category 1 |
| `Category1_Sample_Output_INACCURATE.json` | **VALUES ARE WRONG.** March output using old methodology. Use for JSON structure reference only. |

### System Documents

| File | Purpose |
|------|---------|
| `HMTc_Master_Handoff.md` | RETIRED. Historical context only. The April 13 handoff supersedes this. |
| `HMTc_Pipeline_Failure_Modes_and_Critique.md` | Documented failure modes from previous iterations. Still relevant — read this. |
| `HMTc_Pre_Build_Protocol_v2_0_RETIRED.md` | RETIRED. Content absorbed into Step Zero. |

### PDFs

| File | Purpose |
|------|---------|
| `Comprehensive_Testing_Category_Taxonomy_for_the_HMTc_Program.pdf` | All 23 product categories and their testing taxonomy |
| `HMTc_Lot_Testing_Schedule.pdf` | Lot testing schedule (needs minor updates — see handoff) |
| `March_17th_HMTc_Program_Governance_Policy_...pdf` | Governance policy (needs minor updates — see handoff) |

---

## The Formula (v5.0 — Dual-Percentile Model)

### Clean / unsplit rows:
```
raw = min( P90_clean, Regulatory_Anchor, 2×M )
Limit = round_by_range( raw )
```

### Contaminated rows (affected metals):
```
raw = min( best_available_dirty_estimate, Regulatory_Anchor, 2×M )
Limit = max( round_by_range(raw), Limit_clean )
```

Where `best_available_dirty_estimate` comes from the confidence ladder:
- **Tier 1:** P10 from qualifying dataset
- **Tier 2:** P10 derived from platform shift ratio
- **Tier 3:** min( Regulatory_Floor × 0.75, 2 × Limit_clean )
- **Tier 4:** HELD TO CLEAN (= Limit_clean)

### Final gate (all rows):
```
Limit_published = min( Limit, Regulatory_Floor )
```

### Rounding (single operation, final step):

| Range | Round to nearest |
|---|---|
| Under 100 ppb | 1 |
| 100–999 ppb | 10 |
| 1,000–9,999 ppb | 100 |
| 10,000+ ppb | 1,000 |

Standard rounding (nearest, 0.5 up). Applied ONCE. No old ladder.

---

## Standards Generator

A password-protected Standards Briefing generator is live at:

> **https://reportify-mu.vercel.app/standards-generator.html**

Request the password from Karen. This tool takes JSON input and renders formatted Standards Briefing documents.

**Sample JSON (`Category1_Sample_Output_INACCURATE.json`):**
This JSON file is included in the repo so you can load it into the standards generator and see what the output is *supposed to look like structurally.* The generator will render a full Standards Briefing from it. **The limit values in this file are wrong** — they were produced in March before the methodology was corrected. The other 7 metals besides Pb were never validated. Later iterations using the Inngest pipeline produced better numbers but broke the document structure (missing sections, wrong formatting, incomplete references).

**What this March file gets RIGHT (use as your structural reference):**
- Table of Contents present and correct
- Statement of Purpose present and correct
- Anti-Circumvention & Integrity section present with all 6 moves
- Notes column discusses achievability for each subcategory
- Separate EU/EEA and US FDA reference columns in per-metal tables
- Product Categories visual layout correct
- Per-metal sections in correct order with all 6 subsections each
- Toxicology sections, non-compliant product tables, and remediation tables all present
- References section present

**What this March file gets WRONG (must be corrected in new output):**
- The ppb limit values are inaccurate across all metals
- Only 10 rows instead of 16 (contamination platform splits not fully expanded)
- Slash notation still present in master summary ("100/125*", "500/600*")
- References section is incomplete — the Inngest pipeline was not returning research papers properly
- Some Notes column text is generic rather than citing specific occurrence data

The corrected output must have 16 rows (per Category1_Step_0_Output_LOCKED.md), accurate values from the v5.0 dual-percentile methodology, no slash notation, and complete references.

---

## Limit Values

**All values must be recalculated under the v5.0 dual-percentile methodology before publication.** No previously calculated limits (including Lead) should be treated as final. The methodology changed significantly on April 13, 2026 — the old publication ladder was retired, the tolerance factor (T) was eliminated, rounding rules changed from always-down to standard rounding, and the contaminated-platform formula was replaced entirely. Any values produced under the previous methodology (v4.x) must be re-derived.

---

## What's Eliminated (do not use)

| Eliminated | Replaced by |
|---|---|
| T (tolerance factor, 0.33) | P10 of contaminated platform / confidence ladder |
| VME (Visible Margin Exception) | Not needed — dirty limits are independently derived |
| CC_clean × (1+T) | P10_dirty or derived estimate |
| 18-value publication ladder | Range-based standard rounding |
| Two-step rounding (table + ladder snap) | Single round_by_range operation |
| Rounding always down | Standard rounding (nearest) |

---

## Known Failure Modes (from previous iterations)

Read `HMTc_Pipeline_Failure_Modes_and_Critique.md` for details:
- **"Polished confidence covering skipped math"** — Output looks professional but formulas weren't executed
- **Regulatory floor treated as default** — Limits should be derived from formula, not defaulted to regulatory maximums
- **Web search returning empty data silently** — Caused fallback to defaults across the board
- **Context loss between sessions** — Previous fixes re-discovered and re-broken
- **Double round-down compounding** — The old ladder + rounding table compressed values far below formula intent

---

## Confirmed Corrections (check every build)

1. Pb BMDL01 for nephrotoxicity: **0.63** µg/kg bw/day (NOT 0.50)
2. JECFA Al PTWI = 2 mg/kg bw/week. EFSA Al TWI = 1 mg/kg bw/week. Distinct.
3. EFSA MeHg TWI = **1.3** µg/kg bw/week. The 4.0 value is inorganic Hg.
4. Prop 65 Lead = MADL **0.5** µg/day (reproductive). NOT NSRL 15 µg/day.
5. ASTM F963 §4.3.5 — Ni and Sn are NOT among the 8 soluble elements.
6. FDA CTZ covers **Lead ONLY**. Cd, iAs, Hg NOT finalized as of April 2026.
7. FDA CTZ dry infant cereals: **20 ppb** (NOT 10).
8. FDA CTZ does NOT apply to infant formula.
9. Cd floors from **EU (Reg. 2023/915)**, not FDA.
10. EU 2024/1987 Ni for liquid formula (§3.6.13.3): **100 ppb**, no soy split.
11. EFSA Ni TDI is **13** µg/kg bw/day (2020 update). Not 2.8.

---

## Authors

- **K. Pendergrass** (CEO, Paleo Foundation)
- **K. Eyer**
- **D. Aleru**

**NEVER use "Victor Eyer" or "Oluwatobi Aleru" — those are hallucinated names.**
