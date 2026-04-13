# HMTc Step Two Protocol
## Document Generation: From Master Limit Table to Standards Briefing
### Version 1.2 — April 2026
### Prepared by K. Pendergrass (CEO), K. Eyer, D. Aleru

---

**Governing document: `HMTc_Governing_Principles.md` — read first, apply at every step.**

---

## What This Document Is

This protocol governs Step 2 of every HMTc standards build: generating the
consolidated Standards Briefing from the locked outputs of Steps 0 and 1.

Step 2 takes two locked inputs:
1. The **Expanded Subcategory List** from Step 0 (the rows)
2. The **Master Limit Table** from Step 1 (the values)

And produces one output:
- The **Standards Briefing** — a single .docx document containing all 8
  metals, the master summary table, anti-circumvention section, and all
  supporting content

The Standards Briefing is the published product. It is the document that
goes to manufacturers, regulators, retailers, and the public. Per-metal
working files are internal only and are never published.

**No value in the Standards Briefing may differ from the Master Limit
Table.** The document generation process is a formatting and presentation
step, not a computation step. Every number was locked in Step 1.

---

## When This Protocol Runs

Step 2 runs after the Master Limit Table is locked and validated in Step 1.
It produces the Standards Briefing, which then proceeds to validation and
audit (Step 3).

---

## Input Verification

Before generating any content, the pipeline verifies:

- The Expanded Subcategory List is locked (Step 0 validation passed)
- The Master Limit Table is locked (Step 1 validation passed)
- Every cell in the Master Limit Table has a value (no blanks)
- Every value is on the publication increment ladder
- The Clean Platform Data Package (Step 0F) and Contaminated Platform
  Data Package (Step 0G) are available for confidence tags and Notes
  column content

If any input is missing or invalid, the pipeline fails with a specific
error identifying the missing input.

---

## The Standards Briefing — Page Sequence

The Briefing has exactly this structure, in this order:

1. **Cover Page**
2. **Table of Contents**
3. **Statement of Purpose**
4. **Anti-Circumvention & Integrity**
5. **Product Categories** (visual card layout)
6. **Terms and Abbreviations**
7. **HMTc Approved Standards — All Metals** (master summary table +
   analytical methods + speciation triggers + LOQ + lab accreditation)
8–15. **Per-metal sections** in order: Pb → iAs → Sn → Ni → Cd → Cr → Al → Hg
16. **References** (consolidated, two-column, IEEE-style)

No sections may be added, removed, or reordered.

---

## Section-by-Section Generation Rules

### Cover Page

Required elements:
- Title: "HMTc Standards Briefing: [Category Name]"
- Subtitle: "Heavy Metal Tested & Certified Program"
- Authors: "K. Pendergrass (CEO), K. Eyer, D. Aleru"
- Citation line: "Paleo Foundation, [Month Year]"
- Category list (the base categories covered)
- Taxonomy version: "Built against HMTc Taxonomy v[X], dated [date]"

**NEVER use "Victor Eyer" or "Oluwatobi Aleru."**

### Statement of Purpose

Must reference:
- The Clean Benchmark Standard by name
- The 8-metal panel (Pb, iAs, Hg, Cd, Cr, Ni, Sn, Al)
- The target population for this category
- The exposure pathway
- The concentration-based measurement basis (ppb, as-sold)

Must NOT contain:
- Formula math or variable names
- Percentile values (P90, P10), M values
- Any notation that would allow reverse-engineering of inputs

### Anti-Circumvention & Integrity

This section must make ALL 6 argumentative moves. No move may be omitted
or collapsed. The reference text in `HMTc_Clean_Benchmark_Policy.md`
(Part 6) is approved and may be adapted per category, but all 6 moves
must be present and complete.

**Move 1:** State the concentration-based unit basis (ppb, as-sold)
**Move 2:** Close the serving-size loophole
**Move 3:** Explain why this is dangerous for the target population
**Move 4:** Categorically disqualify serving-based thresholds
**Move 5:** State the measurement basis (powders as sold, liquids after
reconstitution per label instructions)
**Move 6:** State the clean benchmark principle using the dual-percentile
framing (all 4 sub-points: name the problem, state the design principle
with 90/10 language, state the effect, make the categorical statement)

Move 3 must be adapted for the specific target population of the category
being built. Infant and child foods emphasize variable intake, weight-
proportional exposure, and developing organ systems. Adult categories
emphasize chronic cumulative exposure and bioaccumulation.

### Product Categories (Visual Card Layout)

A visual presentation of the expanded subcategory list. Each subcategory
is presented as a card showing:
- Subcategory name
- Variant type (if applicable: clean benchmark, contamination platform)
- Affected metals (for contamination platform variants)

### Terms and Abbreviations

Standard terms required in every briefing:
- ppb (µg/kg or µg/L)
- ML (Maximum Level)
- LOQ (Limit of Quantification)
- ICP-MS, ICP-OES, GFAAS, CVAAS (analytical methods as applicable)
- iAs (inorganic arsenic)
- MeHg (methylmercury)
- Cr(VI) (hexavalent chromium)
- Any category-specific terms

**Do not define CC (clean counterpart) or any formula terminology in
published documents.** The clean benchmark principle is explained in
Move 6 using plain language, not technical notation.

### HMTc Approved Standards — All Metals (Master Summary Table)

This is the master summary table. It reproduces the Master Limit Table
exactly. Every cell must match. No value may be recalculated.

**Format:**

| # | Subcategory | Pb | iAs | Sn | Ni | Cd | Cr | Al | Hg |
|---|-----------|-----|-----|-----|-----|-----|-----|-----|-----|

Note: Metal order in the table headers follows the document metal order:
Pb → iAs → Sn → Ni → Cd → Cr → Al → Hg.

**Header text (required):** "All values in ppb (µg/kg or µg/L) as sold
(powders) or after reconstitution per label instructions
(liquids/concentrates)."

**Below the table, include:**
- Analytical methods for each metal (with method references)
- Speciation triggers (from Methodology Reference Section 3.3)
- LOQ requirements
- Lab accreditation requirements (ISO/IEC 17025)

### Per-Metal Sections (8 sections, one per metal)

Each section contains exactly these subsections, in this order:

**1. Title:** "[Metal Name] ([Symbol]) Standards"

**2. Scope/measurement paragraph** (italicized label):
One paragraph stating what this metal section covers, the measurement
basis, the analytical method, and the speciation requirement (if any).

**3. Standards table** (5 columns):

| Category | HMTc Std (ppb) | EU Regulation / Reference | US FDA / CPSC Reference | Notes |

- **Category column:** Uses the exact expanded subcategory names from
  the locked Expanded Subcategory List, in the exact order.
- **HMTc Std column:** Uses the exact values from the locked Master
  Limit Table column for this metal. Integer values only.
- **EU Regulation / Reference column:** The applicable EU regulation
  with section number, or "—" if none exists.
- **US FDA / CPSC Reference column:** The applicable US regulation
  with section number, or "—" if none exists.
- **Notes column:** See Notes Column Rules below.

**4. Toxicology and Margin of Safety:**

Compressed continuous prose — NO subsection headings (no H2s, no H3s).
Target: 150–270 words of body text plus a closing callout statement.

Structure:
1. Bold lead-in statement (1–2 sentences identifying core population risk)
2. Two to three short paragraphs covering:
   a. Key toxicological property and primary regulatory reference value
   b. Why the target population faces disproportionate risk
   c. One concrete exposure calculation using HMTc limits (from the locked
      Master Limit Table) to demonstrate margin of safety
3. Closing callout statement: "This underscores why HMTc [metal] limits
   function as..."

**Exposure calculations must use the locked limit values, not raw
regulatory anchors.** The margin-of-safety narrative must reflect what
the HMTc standard actually requires, not what the regulation requires.

**5. Products Not Likely to Meet [Symbol] Requirements:**

3-column table:

| Product Type | Reason | Alternative Platforms |

This section must reflect the locked limit values. Products built on
contamination platforms that cannot meet the limits must be explicitly
named, with a statement that the limit is set by the clean counterpart
benchmark and reflects what the best performers on each platform can
demonstrably achieve.

**Never state that the limit should be raised.** The Clean Benchmark
Policy governs: contamination-platform products either meet the standard
or do not certify. This is a settled decision.

**6. [Symbol] Remediation Strategies:**

3-column table:

| Strategy | Description | Expected Impact |

Practical strategies for manufacturers to reduce contamination for this
metal: varietal selection, supplier sourcing, processing controls,
formulation diversification.

### References

Consolidated, two-column layout, IEEE-style citation format.
Target: 18–50 citations per Standards Briefing.

Every regulatory value, toxicological claim, occurrence-data figure, and
methodology reference must be cited. No "Sources:" summary blocks.

**Never fabricate citations.** If a real source cannot be identified,
do not include the citation. State the gap explicitly.

---

## Notes Column Rules

The Notes column is the most legally sensitive part of the published
document. It must communicate the basis for each limit without exposing
the formula.

### Required language patterns:

**For clean-platform rows:**
"Achievable with current [platform] sourcing." +
regulatory citation if applicable

**For contamination-platform rows (affected metals):**
"HMTc limit is set by the clean counterpart benchmark." +
"Products on [contaminated platform] may require reformulation." +
regulatory citation if applicable

**For contamination-platform rows where dirty = clean (same value):**
"No platform-specific distinction for this metal." +
regulatory citation if applicable

**For RF-CAPPED rows:**
"Limit set at [regulatory source] maximum level." +
regulatory citation with section number

**For rows with no regulatory floor:**
"No finalized regulatory ML. Limit set by program methodology."

### Prohibited content in Notes:
- P90, P10, percentile values, M values
- The formula or any part of it
- Rounding calculations or "ladder snap" language
- "PROVISIONAL", "HELD TO CLEAN", or "DATA-GROUNDED" tags (internal)
- Any notation that would allow reverse-engineering of inputs
- Inline [N] citation brackets (use superscript numbers)

### Confidence tag handling:
PROVISIONAL and HELD TO CLEAN designations are flagged internally in the
build workbook but are NOT exposed in published Notes. The published Note
says "Limit set by program methodology" without revealing that the
underlying data is provisional or absent.

---

## Formatting Specifications

All formatting follows Methodology Reference Part 6.

| Element | Font | Size |
|---------|------|------|
| Preamble titles | Arial | 18pt |
| Heading 1 | Arial | 16pt, Bold, #1B4F72 |
| Body text | Arial | 12pt |
| Table text | Arial | 10pt |
| References | Arial | 9pt |

Table headers: #1B4F72 dark blue, white text, bold.
Alternating data rows: #EBF5FB and #FFFFFF.
Page: US Letter (12240 × 15840 DXA), margins 1" top / 1" bottom /
0.75" left / 0.75" right.

### Implementation

Build with Node.js using the `docx` npm package. Follow the docx skill
at `/mnt/skills/public/docx/SKILL.md` for all technical implementation.

Key docx-js rules:
- Set page size explicitly (US Letter, not A4 default)
- Use WidthType.DXA for all table widths (not percentages)
- Tables need dual widths (columnWidths array AND cell width)
- Use ShadingType.CLEAR (not SOLID) for table backgrounds
- Never use unicode bullets — use LevelFormat.BULLET
- Override built-in heading styles with exact IDs ("Heading1", "Heading2")
- Include outlineLevel for TOC compatibility

---

## Output

Step 2 produces one file:

**`HMTc_Standards_Briefing_Category_[N]_[Name].docx`**

This file proceeds to Step 3 (validation and audit). It is not delivered
to the user until it passes all validation checks and the factual audit.

---

## What Step 2 Does NOT Do

- Does not compute, recalculate, or adjust any limit value
- Does not add, remove, or rename any subcategory row
- Does not modify the metal order
- Does not create per-metal working files for publication (those are
  internal artifacts of the build process, not published deliverables)
- Does not make formula math visible in any form
- Does not expose percentile thresholds, confidence tags, or any
  internal methodology notation

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | April 2026 | Initial protocol. Consolidates document generation rules from Methodology Reference Parts 5 and 6 and skill file into a single authoritative source. |
| 1.1 | April 2026 | Removed approval gate language (3 instances). Replaced "approved" with "validated," replaced checkbox input verification with programmatic verification, updated "Phase 1, Deliverable 6" reference to "CC Source Data Package (Step 0F)." |
| 1.2 | April 2026 | **Dual-percentile model.** Updated Notes Column Rules: removed T/VME/CC references, added pattern for contaminated rows where dirty = clean. Updated prohibited content list: replaced T/VME/CC with P90/P10/percentile/PROVISIONAL/HELD TO CLEAN. Updated Anti-Circumvention to reference dual-percentile framing in Move 6. Updated Terms and Abbreviations: removed CC definition instruction. Updated input verification to reference both Clean and Contaminated Platform Data Packages. Updated Section 5 language to reference "best performers on each platform." |
