# HMTc New Chat Handoff — April 13, 2026

## For the Next Claude Conversation

Karen Pendergrass (CEO, Paleo Foundation) needs to produce corrected
Standards Briefing JSON files for all 23 HMTc product categories,
starting with Category 1 (Infant and Child Foods).

This document summarizes all methodology decisions made on April 13, 2026.
These are SETTLED. Do not re-derive, re-debate, or second-guess them.

---

## THE METHODOLOGY (v5.0 — Dual-Percentile Model)

### How clean-platform limits are set

```
Limit_clean = round_by_range( min( P90_clean, Regulatory_Anchor, 2×M ) )
```

P90_clean = 90th percentile of the clean platform's market occurrence
distribution. Approximately 90% of clean-platform products pass.

### How contaminated-platform limits are set (affected metals only)

Use the **confidence ladder** — whichever tier produces data, in order:

**Tier 1 (Full Data):** P10 directly from a qualifying dataset.
**Tier 2 (Derived):** P10 estimated from platform shift ratio × clean distribution.
**Tier 3 (Bounded):** min( Regulatory_Floor × 0.75, 2 × Limit_clean )
**Tier 4 (No Data):** HELD TO CLEAN — same limit as clean row.

Then:
```
raw = min( P10_or_derived_or_bounded, Regulatory_Anchor, 2×M )
Limit_dirty = round_by_range( raw )
Limit_dirty = max( Limit_dirty, Limit_clean )   ← clean floor rule
```

### Contaminated rows on unaffected metals
Limit = Limit_clean (same value as clean row)

### Final gate (all rows)
```
Limit_published = min( Limit, Regulatory_Floor )
```

### Rounding — SINGLE OPERATION, LAST STEP

Standard rounding to nearest by magnitude range. Applied ONCE at the
very end after all constraints. No intermediate rounding anywhere.
All calculations use raw decimals until this final step.

| Range | Round to nearest |
|---|---|
| Under 100 ppb | 1 |
| 100–999 ppb | 10 |
| 1,000–9,999 ppb | 100 |
| 10,000+ ppb | 1,000 |

Direction: standard rounding (0.5 rounds up). NOT always down.

**The old 18-value publication ladder is RETIRED.** Any integer is a
valid published limit (below 100 ppb). Any multiple of 10 is valid
(100–999 ppb). Etc.

### What was eliminated
- T (tolerance factor) — replaced by P10 / confidence ladder
- VME (Visible Margin Exception) — no longer needed
- CC_clean × (1+T) — replaced by independent dirty-platform data
- The two-step rounding (rounding table + ladder snap) — replaced by
  single round_by_range
- The 18-value publication increment ladder — replaced by range-based
  standard rounding

### Percentile threshold parameters (adjustable per category)

| Parameter | Default | Range |
|---|---|---|
| P_clean | 90th percentile | 85th–95th |
| P_dirty | 10th percentile | 5th–15th |

Category-level. Documented in Build Summary but never in published docs.

---

## THE JSON STRUCTURE

The attached JSON file (heavy-metal-tested-certified...copy.json) shows
the **structure** of the Standards Briefing output. The **values and
categories are NOT correct** — they were produced in March before the
methodology was corrected.

### What must change in the JSON:

1. **16 rows, not 10.** Every contamination platform split must be a
   separate row. No slash notation ("100/125*"). The Expanded Subcategory
   List from Category1_Step_0_Output_LOCKED.md defines the exact 16 rows.

2. **All limit values must be recalculated.** No previously calculated
   limits (including Lead) should be treated as final. The methodology
   changed significantly on April 13, 2026 — the old publication ladder
   was retired, T was eliminated, rounding rules changed, and the
   contaminated-platform formula was replaced. All values across all 8
   metals must be derived fresh using the v5.0 dual-percentile model
   with the confidence ladder and simplified rounding.

3. **Per-metal standards table columns must be:**
   - Category (subcategory name)
   - HMTc Std (ppb)
   - EU / EEA Regulation Reference (single column)
   - US FDA Reference (single column)
   - Notes

4. **Notes column must discuss what is routinely achieved** in that
   subcategory. Examples:
   - "Dairy-based infant formula powder routinely tests at 2–4 ppb Pb.
     Achievable with current sourcing."
   - "Rice-based baby cereals typically test 5–15 ppb Pb. The top 10%
     of rice cereal products achieve levels at or below 10 ppb through
     low-Pb varietal selection and sourcing controls."

   Notes must NOT contain: formula math, percentile values (P90, P10),
   confidence tags (PROVISIONAL, HELD TO CLEAN, DERIVED, BOUNDED), or
   any notation allowing reverse-engineering.

5. **All other values (iAs, Hg, Cd, Cr, Ni, Sn, Al) must be
   recalculated** using the dual-percentile model with the confidence
   ladder and simplified rounding. The March values are inaccurate.

---

## DOCUMENTS TO LOAD AS PROJECT KNOWLEDGE

Upload all of these into the new chat's project:

### Updated protocols (from the April 13 zip):
- HMTc_Step_Zero_Protocol_v1_3.md
- HMTc_Step_One_Protocol_v1_5.md
- HMTc_Step_Two_Protocol_v1_2.md
- HMTc_Step_Three_Protocol_v1_2.md
- HMTc_Clean_Benchmark_Policy.md (v3.0)
- HMTc_Methodology_Reference_v5_0.md
- HMTc_Governing_Principles.md (v1.1)
- SKILL_v5_0.md

### Unchanged documents (from the original project):
- Category1_Step_0_Output_LOCKED.md
- Category1_Pre_Build_Deliverables_1-5.md
- Comprehensive_Testing_Category_Taxonomy_for_the_HMTc_Program.pdf
- HMTc_Lot_Testing_Schedule.pdf
- March_17th_HMTc_Program_Governance_Policy.pdf

### The template JSON:
- heavy-metal-tested-certified...copy.json (structural reference only)

---

## WHAT TO ASK THE NEW CHAT

"I need to produce a corrected Standards Briefing JSON for Category 1
(Infant and Child Foods) using the updated v5.0 dual-percentile
methodology. Read all the protocol documents in the project first. The
attached JSON shows the output structure but the values are wrong —
recalculate everything using the new methodology. The verified Lead
values are in the handoff document. For all other metals, source
occurrence data via web search and apply the formula."

---

## CONFIRMED CORRECTIONS (check every build)

1. Pb BMDL01 for nephrotoxicity: 0.63 µg/kg bw/day (NOT 0.50)
2. JECFA Al PTWI = 2 mg/kg bw/week. EFSA Al TWI = 1 mg/kg bw/week.
3. EFSA MeHg TWI = 1.3 µg/kg bw/week. The 4.0 value is inorganic Hg.
4. Prop 65 Lead = MADL 0.5 µg/day (reproductive). NOT NSRL 15 µg/day.
5. ASTM F963 §4.3.5 — Ni and Sn are NOT among the 8 soluble elements.
6. FDA CTZ covers Lead ONLY. Cd, iAs, Hg NOT finalized as of April 2026.
7. FDA CTZ dry infant cereals: 20 ppb (NOT 10).
8. FDA CTZ does NOT apply to infant formula.
9. Cd floors from EU (Reg. 2023/915), not FDA.
10. EU 2024/1987 Ni for liquid formula (§3.6.13.3): 100 ppb, no soy split.
11. EFSA Ni TDI is 13 µg/kg bw/day (2020 update). Not 2.8.

---

## KEY CONTEXT

- Authors: K. Pendergrass (CEO), K. Eyer, D. Aleru
- NEVER "Victor Eyer" or "Oluwatobi Aleru"
- Metal order: Pb → iAs → Sn → Ni → Cd → Cr → Al → Hg
- The Standards Briefing is the published product
- Formula math is NEVER exposed in published documents
- Anti-circumvention makes 6 moves; Move 6 uses dual-percentile framing
- The generator at https://reportify-mu.vercel.app/standards-generator.html
  renders the JSON into a formatted document (password-protected)

---

## WHAT NOT TO DO IN THE NEW CHAT

- Do not re-derive the expanded subcategory list. It's locked. 16 rows.
- Do not re-debate the clean benchmark principle. Settled.
- Do not use the old 18-value ladder. Retired.
- Do not use T, VME, or CC_clean × (1+T). Eliminated.
- Do not round twice. One rounding operation, final step.
- Do not treat the March JSON values as correct. They are structural
  templates only.
- Do not add approval gates. The pipeline runs end-to-end.
