# HMTc Step One Protocol
## Limit Determination: Dual-Percentile Formula and Floor Check
### Version 1.5 — April 2026
### Prepared by K. Pendergrass (CEO), K. Eyer, D. Aleru

---

**Governing document: `HMTc_Governing_Principles.md` — read first, apply at every step.**

---

## What This Document Is

This protocol governs Step 1 of every HMTc standards build: determining the
actual ppb limit for every cell in the expanded subcategory × 8 metals grid.

Step 1 takes five locked outputs from Step 0:
- The **Expanded Subcategory List** (the rows)
- The **Contamination Platform Map** (clean/contaminated relationships)
- The **Regulatory Floor Table** (government limits per cell)
- The **Clean Platform Data Package** (P90 or 5×LOQ values per cell)
- The **Contaminated Platform Data Package** (P10 or HELD TO CLEAN per cell)

From these inputs, Step 1 produces the **Master Limit Table** — every cell
populated with a final, publication-ready integer value.

The limit-setting process has three phases:
1. **Limit Calculation** — Apply the percentile-based formula to produce limits
2. **Column Median Check** — Verify distributional coherence via 2×M
3. **Regulatory Floor Check** — Verify no limit exceeds a government standard

Phase 1 is the engine. Phase 2 catches outliers. Phase 3 is the brake.

---

## The Dual-Percentile Model

HMTc limits are set by two independently sourced data points:

**Clean platform:** The limit is set at the level that approximately 90%
of clean-platform products on the market today can already achieve (P90).
This is generous to the clean platform (serving Principle 3 — protect brands
who enter) while tight enough to mean something (serving Principle 1 — drive
contamination down).

**Contaminated platform:** The limit is set at the level that only the
top 10% of contaminated-platform products can achieve (P10). The remaining
90% must reformulate, improve sourcing, or forgo certification. This is not
a side effect — it is the mechanism by which the certification mark drives
contamination reduction on the dirtiest products.

**Why this replaces the tolerance factor (T):** The previous model derived
the contaminated limit from the clean limit using a multiplier (T = 0.33).
This created artifacts at the low end of the publication ladder where the
rounding mechanism swallowed the tolerance margin, and required a Visible
Margin Exception (VME) to rescue collapsed values. The dual-percentile model
eliminates both T and VME by deriving each limit independently from its own
data distribution. Both limits are now set by the same methodology (percentile
of the relevant platform), making the system simpler, more defensible, and
more consistent across the entire ppb range.

---

## What Step 1 Receives from Step 0

### Clean Platform Data (from Step 0F)

For every clean-variant and unsplit row, every metal:

**Path A — DATA-GROUNDED:** The raw P90 value from the clean platform
distribution. Step 1 will round this to the publication ladder.

**Path B — PROVISIONAL:** 5× LOQ. Step 1 will round this to the
publication ladder. Triggers mandatory review at first revision cycle.

### Contaminated Platform Data (from Step 0G)

For every contaminated-variant row × affected metal:

**Path A — DATA-GROUNDED:** The raw P10 value from the contaminated
platform distribution. Step 1 will round this to the publication ladder,
then apply the clean floor rule.

**Path B — HELD TO CLEAN:** No separate limit. The contaminated row
receives the same limit as its paired clean row for this metal.

---

## Limit Formula

### The two formula variants

```
CLEAN-VARIANT ROW / UNSPLIT ROW:

  Limit = L_down( min( P90_clean, Regulatory_Anchor, 2 × M ) )


CONTAMINATED-VARIANT ROW (affected metals only):

  Limit = L_down( min( P10_dirty, Regulatory_Anchor, 2 × M ) )
  then:  Limit = max( Limit, Limit_clean )     ← clean floor rule
  
  Where Limit_clean = the already-computed limit for the paired
  clean-variant row on this metal.

  If the Contaminated Platform Data Package says "HELD TO CLEAN"
  for this cell: Limit = Limit_clean. Skip the formula.


CONTAMINATED-VARIANT ROW (unaffected metals):

  Limit = Limit_clean

  The contaminated row receives the same limit as its clean counterpart
  on metals where the contamination platform distinction does not apply.


ALL ROWS — final gate:

  Limit_published = min( Limit, Regulatory_Floor )
```

### Variables

| Symbol | Definition |
|--------|-----------|
| P90_clean | The 90th percentile of the clean platform distribution, or 5× LOQ (Path B). Sourced in Step 0F. |
| P10_dirty | The 10th percentile of the contaminated platform distribution. Sourced in Step 0G. Only exists for contaminated-variant rows × affected metals with DATA-GROUNDED status. |
| Regulatory_Anchor | An existing EU ML, FDA action level, or other binding regulatory reference. When none exists, this constraint is omitted. |
| M | Column median — the median of all category limits for that metal within the standards category. |
| L_down( ) | Ladder snap — rounds DOWN to the nearest value on the publication increment ladder. See "Rounding" section below. |
| Limit_clean | The published limit of the paired clean-variant row. Used in the clean floor rule for contaminated rows. |
| Regulatory_Floor | The lowest finalized regulatory ML or action level applicable to this exact metal-category pair. Checked AFTER the formula, not as an input to it. |

### What was eliminated

| Removed | Reason |
|---------|--------|
| T (tolerance factor) | Replaced by P10_dirty. The contaminated platform limit is now independently data-derived, not computed from the clean value. |
| CC_clean × (1 + T) | Replaced by P10_dirty in the contaminated formula. |
| VME (Visible Margin Exception) | No longer needed. The contaminated limit is independently derived, so there is no mechanism by which rounding collapses it onto the clean limit in a way that needs rescuing. If both land on the same ladder value, that is a data-driven outcome. |
| Rounding table | Replaced by direct ladder snap. See "Rounding" section. |

---

## Rounding: Direct Ladder Snap

The previous system used a two-step process: (1) round down via a rounding
table, then (2) snap to the publication ladder if the result wasn't a ladder
value. This created a double round-down that could compress values
significantly at low ppb.

**The new system uses a single operation: snap directly to the nearest
publication ladder value at or below the raw formula output.**

### Publication Increment Ladder

**1, 2, 3, 5, 10, 15, 20, 25, 50, 100, 200, 500, 1000, 1300, 1500,
2000, 5000, 10000**

### Examples

| Raw Value | Ladder Snap (L_down) |
|-----------|---------------------|
| 8.3 | 5 |
| 13.7 | 10 |
| 27 | 25 |
| 48 | 25 |
| 90 | 50 |
| 133 | 100 |
| 375 | 200 |
| 1330 | 1300 |

Direction is always DOWN (tighter). This is a single operation. No
intermediate rounding step. No VME check needed after rounding.

---

## The Clean Floor Rule

After computing a contaminated-variant limit from P10_dirty, verify that
it is not below the paired clean-variant limit:

```
Limit_dirty = max( L_down(min(P10_dirty, Regulatory_Anchor, 2×M)), Limit_clean )
```

**Why:** If the cleanest 10% of contaminated-platform products test
lower than the 90th percentile of clean-platform products for a specific
metal, the contamination platform distinction is irrelevant for that metal.
Publishing a stricter limit for the dirty platform than the clean platform
is incoherent and legally vulnerable. Floor at the clean value.

If this produces identical values for clean and contaminated rows on a
given metal, that is a valid outcome — it means the data says the
platforms are indistinguishable at that resolution for that metal.

---

## Step-by-Step for Each Cell

**Step 1a: Identify the row type.**

- Is this a clean-variant row, a contaminated-variant row, or an
  unsplit row? (From the Contamination Platform Map.)
- If contaminated: is this metal an affected metal for this platform?
- If contaminated and affected: does Step 0G provide P10_dirty
  (DATA-GROUNDED) or HELD TO CLEAN?

**Step 1b: Gather the inputs.**

- P90_clean (for clean/unsplit rows) or P10_dirty (for contaminated ×
  affected) from the respective Step 0 data packages
- Regulatory_Anchor from the Regulatory Floor Table (if one exists)
- 2×M is computed in a later pass (see computation order below)

**Step 1c: Take the minimum of all applicable constraints.**

The limit is whichever constraint is most restrictive (lowest value).

**Step 1d: Snap to the publication ladder.**

Round DOWN to the nearest value on the ladder. One operation.

**Step 1e: Apply the clean floor rule (contaminated rows only).**

If Limit < Limit_clean for this metal, set Limit = Limit_clean.

---

## Computation Order

### Clean before contaminated

1. Compute all clean-variant and unsplit rows first (using P90_clean)
2. Lock those values — they become Limit_clean for paired contaminated rows
3. Compute all contaminated-variant rows on affected metals (using
   P10_dirty), applying the clean floor rule
4. Set all contaminated-variant rows on unaffected metals = Limit_clean

This order is mandatory. The clean floor rule depends on the clean
variant's published limit.

### Column median (2×M) — resolving the circular dependency

The column median M requires all values in the column to exist, but those
values are what the formula is computing. Resolve this in three passes:

1. **Initial pass:** Compute all limits using only P90_clean / P10_dirty
   and Regulatory_Anchor. Omit the 2×M constraint entirely.
2. **Calculate M:** From the initial values, compute the column median
   for each metal. Multiply by 2 to get the 2×M ceiling.
3. **Verification pass:** Check every cell against 2×M. If any cell
   exceeds 2×M, cap it at 2×M, re-snap to the ladder, and re-check
   the clean floor rule. Then recalculate M from the updated values.
   Repeat until no cell exceeds 2×M (convergence is guaranteed because
   capping can only lower values, which can only lower M).

If a cell is capped by 2×M, flag it as **2×M-CAPPED** in the build
workbook. Frequent 2×M-CAPPED flags on contaminated rows indicate the
contaminated platform is structurally far from the rest of the category.

The full sequence is: clean/unsplit initial → contaminated initial →
clean floor rule → calculate M → verify 2×M → iterate if needed →
regulatory floor check.

---

## Regulatory Floor Check

After all limits are computed, compare every cell against the
**Regulatory Floor Table** from Step 0E.

```
Limit_published = min( Limit_formula, Regulatory_Floor )
```

The Regulatory Floor Table was built and validated in Step 0E. Step 1
does not rebuild it — it consumes it as locked input.

### Step-by-step

**Step 3a: Compare every cell.**

For every cell where a regulatory floor exists (non-dash cell in the
Step 0E Regulatory Floor Table):
- If Limit_formula ≤ Regulatory_Floor → PASS. No change needed.
- If Limit_formula > Regulatory_Floor → Cap at the floor. Mark as
  **RF-CAPPED** with the regulatory source.

RF-CAPPED should be rare. It means the formula produced something less
protective than what a government requires — which should almost never
happen if the occurrence data values are correctly sourced. If many cells
are RF-CAPPED, the percentile values are too generous and should be
reviewed.

**Step 3b: For cells with no regulatory floor.**

Record "No regulatory floor — formula-only" in the audit documentation.
The formula output stands. This is the expected case for most Cr, Al,
and many Hg, Ni, and Sn cells.

---

## Output: The Master Limit Table

The output of Step 1 is a single table: all expanded subcategories × all
8 metals, with every cell populated by a final integer from the publication
increment ladder.

### Required format

| # | Subcategory | Pb | iAs | Cd | Hg | Cr | Ni | Sn | Al | Flags |
|---|-----------|-----|-----|-----|-----|-----|-----|-----|-----|-------|

### Required supporting documentation (internal, not published)

For every cell, the build workbook must record:

| Field | Content |
|-------|---------|
| Row type | Clean / Contaminated (affected) / Contaminated (unaffected) / Unsplit |
| Data source | P90_clean or P10_dirty citation, or Path B designation |
| Data confidence | DATA-GROUNDED or PROVISIONAL or PROVISIONAL — HELD TO CLEAN |
| Raw percentile value | The unrounded P90 or P10 |
| Regulatory anchor | The starting reference value, if one exists |
| Constraint: 2×M | The column median ceiling, if applicable |
| After ladder snap | The value after L_down() |
| Clean floor applied? | Yes/No (contaminated rows only) |
| Regulatory floor | The applicable government limit, or "—" |
| RF-CAPPED? | Yes/No |
| 2×M-CAPPED? | Yes/No |
| Published value | The final integer |

This documentation is internal only. It never appears in published standards.
But it must exist for every cell so that any limit can be traced back to its
inputs if challenged.

---

## Revision Cycle

Standards are reviewed on a **two-year cycle** per category, starting from
the date of initial publication.

### What happens at each review:

1. **PROVISIONAL clean values** (Path B) are mandatory review items. If
   adequate occurrence data has become available since publication, the
   value moves to Path A (P90). If no data has emerged, the PROVISIONAL
   tag remains and the 5× LOQ value stands for another cycle.

2. **PROVISIONAL — HELD TO CLEAN contaminated values** are mandatory
   review items. If contaminated platform occurrence data has become
   available (including from Enrolled-tier ingredient supplier lot data
   with minimum N = 30 per metal-subcategory pair), calculate P10 and
   establish a separate limit. If no data has emerged, the contaminated
   platform remains held to the clean standard.

3. **DATA-GROUNDED clean values** (Path A) are reviewed against the most
   recent dataset. If newer survey data shifts the P90 downward, the
   limit tightens. If it shifts upward, the limit does not loosen —
   limits only ratchet tighter.

4. **DATA-GROUNDED contaminated values** (Path A) are reviewed against
   the most recent dataset. If newer data shifts the P10 downward, the
   limit tightens. If it shifts upward, the limit does not loosen.

5. **Enrolled-tier data evaluation:** If aggregate lot-testing data from
   Enrolled-tier ingredient suppliers provides sufficient sample size
   (minimum N = 30 per metal-subcategory pair), this data may supplement
   or replace published survey data for percentile calculations, subject
   to the same two-source independence requirement. Enrolled-tier data
   is especially valuable for contaminated-platform subcategories where
   published government survey data is scarce.

6. **Ratchet trigger evaluation:** Using aggregate program testing data,
   evaluate whether the achievability threshold (benchmarked at the 80th
   percentile of tested products per the Governance Policy §12.3) has
   shifted downward. If so, consider tightening P_clean and/or P_dirty
   thresholds for the next cycle.

7. **Regulatory floor values** are checked for new or amended government
   standards (FDA finalizations, EU regulation amendments, Codex updates).
   New floors are incorporated; existing floors are updated.

8. **New contamination platforms** identified since publication are added to
   the map and trigger new subcategory splits per the Step Zero Protocol.

### What does NOT happen at review:

- Limits never loosen. A published limit is a permanent ceiling. Future
  revisions can only tighten.
- Settled decisions from the Clean Benchmark Policy are not re-litigated.

### Why two years:

Two years gives brands enough planning horizon to invest in reformulation
(Principle 3) while maintaining enough regulatory pressure to keep driving
contamination down (Principle 1). It aligns with typical product development
cycles for food and consumer goods. Retailers and institutional buyers
expect review cycles in this range from mature certification programs.

---

## Programmatic Validation

The pipeline verifies before proceeding to document generation:

- Every cell in the grid has a value (no blanks)
- Every value is on the publication increment ladder
- No value exceeds the regulatory floor for its metal-subcategory pair
- Every RF-CAPPED cell is documented with the regulatory source
- Every 2×M-CAPPED cell is documented
- Contaminated-platform rows on affected metals have limits ≥ their
  paired clean-variant row's limit (clean floor rule verified)
- Contaminated-platform rows on unaffected metals show identical limits
  to their clean counterpart rows
- Every cell has a confidence tag and source citation
- No PROVISIONAL values are present without a flag for future revision
- The formula math is documented internally but does NOT appear in any
  published output

**Any check that fails stops the pipeline with a specific error.**

---

## How This Connects to Step 0

Step 0 produces five data outputs:
- The Expanded Subcategory List (the rows)
- The Contamination Platform Map (clean/contaminated relationships)
- The Regulatory Floor Table (government limits per cell)
- The Clean Platform Data Package (P90 or 5×LOQ values per cell)
- The Contaminated Platform Data Package (P10 or HELD TO CLEAN per cell)

Step 1 consumes all five and produces the Master Limit Table (the values).

Together they form the **contract** between the planning phase and the build
phase. Once the Master Limit Table is locked, every downstream document
consumes it as literal input data. No downstream step may modify, add,
remove, or recompute any row or value.

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | April 2026 | Initial protocol. |
| 1.1 | April 2026 | Replaced gap-proportional generosity (judgment-based) with mechanized CC Selection Rule: Path A (90th percentile of clean platform) or Path B (5× LOQ). Removed "expert-set protective concentration" option. Made formula variants explicit for cells with and without regulatory anchors. Added two-year revision cycle with mandatory PROVISIONAL review. |
| 1.2 | April 2026 | Removed human approval gate (1 instance). Replaced "Lock Confirmation" checklist with programmatic validation check. Required for Inngest compatibility. |
| 1.3 | April 2026 | Fixed clean variant formula: added CC_candidate to min() so the data-driven value from Path A/B actually constrains the clean row's limit. Without this, clean rows defaulted to regulatory anchor or 2×M — always higher than what clean products achieve — defeating the clean benchmark principle. |
| 1.4 | April 2026 | Added 2×M computation order to resolve circular dependency. |
| 1.5 | April 2026 | **Dual-percentile model.** Replaced T (tolerance factor), VME (Visible Margin Exception), CC_clean × (1+T), and the two-step rounding table with: (1) independently data-derived contaminated platform limits from P10 of the contaminated distribution, (2) a clean floor rule ensuring dirty limits never fall below clean limits, (3) direct ladder snap replacing the rounding table + ladder verification two-step. Contaminated limits are now set by what the top 10% of contaminated products achieve, not by a multiplier on the clean value. Path B for contaminated platforms = "HELD TO CLEAN" (no separate limit without data). Added Enrolled-tier data as a revision cycle input source. Added ratchet trigger evaluation to revision cycle. Added 2×M-CAPPED flag. |
