# HMTc Step Three Protocol
## Validation, Audit, Rebuild, and Publication Gates
### Version 1.2 — April 2026
### Prepared by K. Pendergrass (CEO), K. Eyer, D. Aleru

---

**Governing document: `HMTc_Governing_Principles.md` — read first, apply at every step.**

---

## What This Document Is

This protocol governs everything that happens between "the Standards
Briefing exists" and "the Standards Briefing ships." It covers structural
validation, the 11-step factual audit, the rebuild cycle, and the 9
pre-publication gates.

No Standards Briefing is delivered, published, or shared outside the
build team until every gate in this protocol passes. A single CRITICAL
FLAG blocks publication until resolved.

---

## When This Protocol Runs

Step 3 runs immediately after Step 2 (document generation) produces the
Standards Briefing. It runs as a continuous sequence: validation → audit
→ rebuild → re-validation → gates → delivery. The sequence does not stop
between sub-steps.

---

## Sub-Step 3A: Structural Validation

### Purpose
Verify that the generated document has the correct structure before
checking whether its content is accurate. Structural errors caught here
are cheap to fix. Structural errors caught after the factual audit waste
the audit effort.

### Checks (all mandatory, all programmatic)

**Document structure:**
- [ ] Page sequence matches Step Two Protocol exactly (16 sections)
- [ ] No sections added, removed, or reordered
- [ ] Table of Contents is present and renders correctly

**Master summary table:**
- [ ] Row count matches the Expanded Subcategory List count (exact match)
- [ ] Row names match the Expanded Subcategory List names (exact string
      match, including parenthetical variant identifiers)
- [ ] Row order matches the Expanded Subcategory List order
- [ ] Every cell value matches the Master Limit Table (exact integer match)
- [ ] Metal column order: Pb → iAs → Sn → Ni → Cd → Cr → Al → Hg
- [ ] Header text is present: "All values in ppb (µg/kg or µg/L)..."

**Per-metal sections:**
- [ ] 8 per-metal sections present, in order: Pb → iAs → Sn → Ni → Cd → Cr → Al → Hg
- [ ] Each section has exactly the 6 subsections specified in Step Two Protocol
- [ ] Each standards table has 5 columns (Category | HMTc Std | EU Ref | US Ref | Notes)
- [ ] Each standards table row count matches the Expanded Subcategory List
- [ ] Each standards table HMTc Std value matches the corresponding cell
      in the Master Limit Table (exact integer match)
- [ ] No H2 or H3 headings appear within Toxicology sections

**Anti-circumvention:**
- [ ] All 6 moves are present
- [ ] Move 6 contains all 4 sub-points (a, b, c, d)
- [ ] Move 6(b) references the dual-percentile model (90/10 framing)

**Formatting:**
- [ ] Font: Arial throughout (12pt body, 10pt tables, 16pt H1, 18pt preamble, 9pt references)
- [ ] Table headers: #1B4F72 background, white text, bold
- [ ] Alternating data rows: #EBF5FB and #FFFFFF
- [ ] Page: US Letter (12240 × 15840 DXA)
- [ ] Margins: 1" top/bottom, 0.75" left/right
- [ ] No "Sources:" summary blocks anywhere

**Formula exposure check:**
- [ ] No instance of the formula string appears in the document
- [ ] No P90, P10, percentile values, M values, or rounding calculations appear
- [ ] No "PROVISIONAL" or "HELD TO CLEAN" tags appear
- [ ] No notation that would allow reverse-engineering of inputs

**Author check:**
- [ ] Authors listed as: K. Pendergrass (CEO), K. Eyer, D. Aleru
- [ ] No instance of "Victor Eyer" or "Oluwatobi Aleru"

### Failure handling
Any structural validation failure is a build error. The document returns
to Step 2 for regeneration. Do not proceed to the factual audit with a
structurally invalid document — the audit would be checking content that
will be regenerated anyway.

---

## Sub-Step 3B: Factual Audit

### Purpose
Verify that every factual claim in the Standards Briefing is accurate,
traceable, and not fabricated. This is the most important step in the
entire build pipeline.

### Scope
The audit covers every:
- Regulatory value (ML, action level, PTWI, TWI, TDI, BMDL, MADL)
- Regulatory citation (regulation name, section number, year)
- Toxicological claim (mechanism, endpoint, dose-response)
- Occurrence-data figure (contamination levels, market data)
- Exposure calculation (intake assumptions, body weight, margin of safety)
- Literature citation (author, year, journal, finding)

### The 11-Step Audit Protocol

For every auditable claim, run all 11 steps in order. The protocol is
defined in HMTc_Methodology_Reference, Part 4 (Section 4.2). The
steps are:

1. **Identify the exact claim** — State category, source, and value.
2. **Verify citation existence** — If you cannot confirm the source
   exists, STOP. Flag as SUSPECTED FABRICATION.
3. **Check for regulatory applicability overstatement** — Does the
   regulation actually cover this specific product category?
4. **Check occurrence-data provenance** — Is the data from a real study?
   STOP if the backing paper may be fabricated.
5. **Decompose the citation** — Exact section, article, annex.
6. **Check for range fabrication** — Is the specific numeric range real?
7. **Check for cross-metal contamination** — Is this value actually from
   a different metal's limit for a similar category?
8. **Check for category existence in regulation** — Is the food category
   explicitly named, or inferred? If inferred, flag as INFERRED.
9. **Assign confidence rating:**
   - VERIFIED: Confirmed against regulation text with traceable section
   - PLAUSIBLE: Consistent but exact section not confirmed
   - FLAG: Could not be confirmed, source may not exist, or
     applicability overstated
10. **Verify formula compliance** — Confirm every published limit is
    consistent with the locked Master Limit Table. No limit in the
    document may differ from the Step 1 output. For contaminated rows,
    verify the clean floor rule holds (dirty limit ≥ clean limit on
    affected metals).
11. **Verify Regulatory Floor compliance** — Confirm every published
    limit does not exceed the most protective applicable finalized
    regulatory value. Any violation is a **CRITICAL FLAG** that blocks
    delivery.

### Additional audit checks

**Confirmed Corrections check:** Cross-reference every regulatory value
against the Confirmed Corrections list (Methodology Reference Section
3.2). Known hallucination patterns include:
- FDA CTZ applied to infant formula (it's exempt)
- FDA CTZ applied to cadmium or arsenic (not finalized)
- FDA CTZ dry infant cereals cited as 10 ppb (correct: 20 ppb)
- EFSA MeHg TWI cited as 4.0 (correct: 1.3; 4.0 is inorganic Hg)
- JECFA Al PTWI conflated with EFSA Al TWI
- Prop 65 Lead NSRL cited instead of MADL
- ASTM F963 §4.3.5 values fabricated for Ni or Sn

**Notes column check:** Verify no Notes cell contains formula math,
percentile values (P90, P10), or any other prohibited content
(see Step Two Protocol, Notes Column Rules).

**Clean benchmark consistency check:** Verify that every Section 5
(Products Not Likely to Meet Requirements) correctly identifies
contamination-platform products that cannot meet the limit, and does
not suggest the limit should be raised.

### Audit output format

| # | Claim | Source Cited | Step Failed | Confidence | Action Required |
|---|-------|-------------|-------------|-----------|----------------|

Every FLAG requires a specific action in the rebuild.
Every CRITICAL FLAG blocks publication.

### Principle behind the audit

From Methodology Reference Section 4.1: "Verify the source exists before
verifying the value is correct. If the citation is fabricated, every
downstream check passes against a fiction."

False negatives are far more costly than false positives. When in doubt,
FLAG. A flag that turns out to be correct costs a few minutes of review.
A fabricated citation that ships costs the program's credibility.

---

## Sub-Step 3C: Rebuild with Corrections

### Purpose
Incorporate all corrections from the audit into a full rebuild of the
Standards Briefing. This is a complete regeneration, not a partial patch.

### Mandatory actions

For every SUSPECTED FABRICATION flag:
- Remove the citation entirely
- If the claim depended on the citation, remove or soften the claim
- Do not replace a fabricated citation with another unverified citation

For every INFERRED flag:
- Add "INFERRED" caveat language to the relevant Notes cell
- Verify the inference is reasonable

For every numeric error:
- Correct the value to match the locked Master Limit Table
- If the error was in the Master Limit Table itself (formula computation
  error), STOP — return to Step 1 to correct and re-lock

For every regulatory applicability overstatement:
- Narrow the claim to what the regulation actually covers
- If the regulation doesn't cover this category, remove the regulatory
  reference

For every occurrence-data provenance failure:
- Replace quantitative claims with qualitative language: "expected to
  test well below the limit" instead of specific ppb ranges
- Do not fabricate replacement data

### After rebuild

Return to Sub-Step 3A (structural validation) and Sub-Step 3B (factual
audit). The rebuild must pass both checks. If new flags emerge, rebuild
again. This cycle continues until the document passes cleanly.

In practice, a well-executed build should require at most one rebuild
cycle. If the document requires three or more cycles, the Step 2
generation process has a systematic problem that should be diagnosed
rather than patched.

---

## Sub-Step 3D: Pre-Publication Gates

All 9 gates must PASS. A single failure blocks publication.

### Gate 1: Structural Integrity
The document passes all structural validation checks from Sub-Step 3A.
**Test:** Sub-Step 3A checklist is complete with no failures.

### Gate 2: Factual Accuracy
The document passes the 11-step factual audit with zero CRITICAL FLAGs
and zero unresolved FLAGs.
**Test:** Audit report shows all claims VERIFIED or PLAUSIBLE.

### Gate 3: Regulatory Floor Compliance
No published limit exceeds the most protective finalized regulatory
value for its metal-subcategory pair.
**Test:** For every cell where a regulatory floor exists, published
value ≤ floor value. Zero exceptions.

### Gate 4: Master Limit Table Fidelity
Every value in the published Standards Briefing matches the locked
Master Limit Table from Step 1. Zero deviations.
**Test:** Cell-by-cell comparison, master summary table and all 8
per-metal standards tables.

### Gate 5: Publication Increment Ladder Compliance
Every published limit value is on the primary increment ladder:
1, 2, 3, 5, 10, 15, 20, 25, 50, 100, 200, 500, 1000, 1300, 1500,
2000, 5000, 10000.
**Test:** No published value exists that is not on this list.

### Gate 6: Formula Concealment
No formula math, percentile values (P90, P10), M values, rounding
calculations, or reverse-engineering notation appears anywhere in the
published document.
**Test:** Text search for prohibited strings returns zero hits.
Prohibited strings include: "P90", "P10", "10th percentile",
"90th percentile", "2×M", "column median", "ladder snap",
"PROVISIONAL", "HELD TO CLEAN", "DATA-GROUNDED".

### Gate 7: Anti-Circumvention Completeness
The Anti-Circumvention & Integrity section makes all 6 argumentative
moves, including Move 6 with all 4 sub-points.
**Test:** Each move identifiable in the text.

### Gate 8: Citation Integrity
Every citation in the References section corresponds to a real,
verifiable source. Zero fabricated citations remain.
**Test:** Audit report shows zero SUSPECTED FABRICATION flags.

### Gate 9: Author and Attribution Accuracy
Authors are correctly listed. No hallucinated author names appear
anywhere in the document.
**Test:** "Victor Eyer" and "Oluwatobi Aleru" return zero hits.
"K. Pendergrass", "K. Eyer", "D. Aleru" are present and correct.

### Gate results format

| Gate | Test | Result | Notes |
|------|------|--------|-------|
| 1 | Structural integrity | PASS / FAIL | |
| 2 | Factual accuracy | PASS / FAIL | |
| 3 | Regulatory floor compliance | PASS / FAIL | |
| 4 | Master limit table fidelity | PASS / FAIL | |
| 5 | Increment ladder compliance | PASS / FAIL | |
| 6 | Formula concealment | PASS / FAIL | |
| 7 | Anti-circumvention completeness | PASS / FAIL | |
| 8 | Citation integrity | PASS / FAIL | |
| 9 | Author accuracy | PASS / FAIL | |

**All 9 PASS → proceed to delivery.**
**Any FAIL → return to Sub-Step 3C (rebuild), then re-run all gates.**

---

## Sub-Step 3E: Final Delivery

### Deliverables to present

1. **The Standards Briefing** (.docx file)
2. **Build Summary** containing:
   - Category name and taxonomy version
   - Percentile thresholds used (P_clean and P_dirty, if different from
     defaults of 90/10)
   - Expanded Subcategory List (16 rows for Category 1; varies by category)
   - Contamination Platform Map
   - Master Limit Table
   - Data source summary (how many Path A vs. Path B values, how many
     HELD TO CLEAN designations)
   - Audit findings and corrections made
   - Values flagged as requiring verification before publication
     (from Methodology Reference Section 4.4)
   - Pre-publication gate results (all 9)
   - Any PROVISIONAL values that will trigger mandatory review
     at the first revision cycle
   - Any HELD TO CLEAN designations that will trigger mandatory
     review at the first revision cycle
   - Watch Items from Step 0E

### What the Build Summary communicates

The Build Summary exists so that:
- Any future revision can trace every limit back to its inputs
  (Principle 4 — legal defensibility)
- The two-year revision cycle knows which values to review first
  (PROVISIONAL and HELD TO CLEAN values, version-control triggers)
- The program operator can confirm the build followed the documented
  process (Principle 5 — scalability)

### Post-delivery

After delivery, the build is complete. The Standards Briefing enters the
program's document management system. The Build Summary is archived with
the build workbook.

The next action is either:
- Build the next category (return to Step 0 for a new category)
- Publish (after any additional review by the program operator)

---

## How This Connects to the Full Pipeline

```
Step 0: Step Zero Protocol (subcategory expansion + data sourcing)
    ↓ (Expanded Subcategory List, Contamination Platform Map,
       Regulatory Floor Table, Clean Platform Data Package,
       Contaminated Platform Data Package — all validated)
Step 1: Step One Protocol (limit determination, floor check)
    ↓ (Master Limit Table validated)
Step 2: Step Two Protocol (document generation)
    ↓ (Standards Briefing draft produced)
Step 3: Step Three Protocol (THIS DOCUMENT)
    3A: Structural validation
    3B: 11-step factual audit
    3C: Rebuild with corrections
    3A/3B: Re-validate and re-audit
    3D: 9 pre-publication gates
    3E: Final delivery
```

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | April 2026 | Initial protocol. Consolidates audit, validation, and publication gate requirements into a single authoritative workflow. Defines the 9 pre-publication gates previously referenced but not specified in the skill file. |
| 1.1 | April 2026 | Updated pipeline diagram and post-delivery text: removed "Phase 1: Pre-Build Protocol" (retired), updated Step 0 description to include data sourcing outputs, updated Step 1 description to reflect formula-only scope. |
| 1.2 | April 2026 | **Dual-percentile model.** Updated formula exposure check: replaced T/VME/CC references with P90/P10/percentile references. Updated audit step 10 to verify clean floor rule instead of CC×(1+T). Updated Gate 6 prohibited strings list. Updated Build Summary to include percentile thresholds, HELD TO CLEAN designations, and Contaminated Platform Data Package. Updated pipeline diagram to show 5 Step 0 outputs. Updated Move 6 validation to check for dual-percentile framing. |
