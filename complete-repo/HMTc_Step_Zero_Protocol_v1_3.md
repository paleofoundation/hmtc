# HMTc Step Zero Protocol
## Subcategory Expansion and Data Sourcing
### Version 1.3 — April 2026
### Prepared by K. Pendergrass (CEO), K. Eyer, D. Aleru

---

**Governing document: `HMTc_Governing_Principles.md` — read first, apply at every step.**

---

## What This Document Is

This protocol governs Step 0 of every HMTc standards build: the process
of establishing the exact subcategory list and sourcing all input data
**before** any limit computation, per-metal document, or Standards Briefing
is generated.

Step 0 produces five locked outputs:
1. The **Expanded Subcategory List** — the exact rows that appear in every
   Section 2 standards table across all 8 metals
2. The **Contamination Platform Map** — which rows are clean variants,
   which are contaminated variants, and which metals are affected
3. The **Regulatory Floor Table** — the most protective finalized
   government limit for every subcategory × metal cell
4. The **Clean Platform Data Package** — the Path A (P90 of clean platform)
   or Path B (5× LOQ) value for every clean/unsplit cell, with citations
   and confidence tags
5. The **Contaminated Platform Data Package** — the Path A (P10 of
   contaminated platform) or Path B (no separate limit) value for every
   contaminated-variant cell on affected metals, with citations and
   confidence tags

These five outputs are the **inputs** to Step 1 (limit determination).
Step 0 sources data. Step 1 computes limits. The boundary is absolute:
Step 0 never applies the limit formula, and Step 1 never sources
data or modifies the subcategory list.

**This protocol supersedes any conflicting instruction in the Master Build
Prompt, the skill file, or the Operational Guide.** In particular:
- The rule "one row per taxonomy subcategory with slash notation for
  contamination platform splits" is **retired**. Every contamination platform
  split produces its own row.
- The instruction "look up the product category in the Comprehensive Testing
  Category Taxonomy to get the full list of testing subcategories" is
  **replaced** by: "Use exactly the Expanded Subcategory List from Step 0."

---

## When This Protocol Runs

Step 0 runs **once per category**, before any documents are generated.
Its outputs must pass all programmatic validation checks before the
pipeline proceeds to Step 1.

The pipeline executes Step 0 as an automated sequence. Each sub-step
(0A through 0G) runs, produces its output, and the next sub-step
consumes it. If a sub-step produces invalid output, the pipeline fails
with a specific error — it does not pause for human intervention.

---

## Step 0A: Establish the Base Subcategory List

Start from the Comprehensive Testing Category Taxonomy (project knowledge).
Extract the exact subcategory names for the target category.

**Example — Category 1: Infant and Child Foods (Ages 0–5)**

The taxonomy lists 9 base subcategories:
1. Infant formula (powder)
2. Infant formula (ready-to-feed, liquid)
3. Baby cereals / grain products (dry)
4. Fruit purées (general)
5. Non-root vegetable purées
6. Root-vegetable purées
7. Mixed meals (e.g., meat & grain combos)
8. Fruit juice (not canned)
9. Teething & snacks (rice-based and non-rice)

---

## Step 0B: Identify Contamination Platform Splits

For every base subcategory, ask:

1. What are the 2–3 most common ingredient/formulation platforms for
   products in this subcategory?
2. Does any platform appear in the Known Contamination Platforms table
   (see limit-setting-methodology.md)?
3. If yes: does the clean counterpart and the contaminated platform
   have meaningfully different contamination profiles for at least one
   of the 8 HMTc metals?

If the answer to all three is yes, the base subcategory **splits into
two rows**: one for the clean variant and one for the contaminated variant.

### Rules for Splitting

- The split applies to ALL 8 metals, not just the metals where the
  contamination platform is active. If soy formula has elevated Al, Ni,
  and Cd but normal Pb and Hg, there are still two rows (soy and non-soy)
  — the Pb and Hg columns simply show the same value in both rows.
- The clean variant row is listed first; the contaminated variant row
  follows immediately after.
- Row names must clearly identify the variant in parentheses.
  Pattern: "[Base subcategory] ([variant identifier])"
  Examples: "Infant formula, powder (non-soy)" / "Infant formula, powder
  (soy-based)"
- Slash notation (e.g., "100/250*" with footnotes) is **never used**.
  Every variant gets its own row with its own unambiguous integer value.

### Known Contamination Platforms (carry forward to every build)

| Platform | Affected Metals | Typical Categories |
|----------|----------------|-------------------|
| Rice (Oryza sativa) | iAs, Cd, Pb | Infant foods, general foods, supplements |
| Soy (Glycine max) | Al, Ni, Cd | Infant formula, supplements, soy-based products |
| Seaweed/algae | iAs, Cd | Supplements, foods with seaweed |
| Cacao/chocolate | Cd, Pb | General foods, supplements |
| Root vegetables (contaminated soil) | Cd, Pb | Infant foods, general foods |
| Predatory fish | MeHg | Infant foods, general foods, supplements |
| Tinplate cans | Sn | Any canned food category |
| PVC packaging | Organotin (TBT, DBT) | Any category with PVC food contact |
| Turmeric/spices | Pb, Cr | Supplements, foods with spice ingredients |
| Mineral-based supplements | Al, Cr, Ni | Supplements |

---

## Step 0C: Identify Missing Product Types

After applying contamination platform splits, review the expanded list and
ask: **are there real, commercially available products marketed for this
population that have no home in the current list?**

The test is:
1. Does the product type exist on store shelves? (e.g., single-ingredient
   meat purées, fish-based baby foods)
2. Does it have a meaningfully different contamination profile from existing
   rows? (e.g., fish baby foods carry MeHg risk that no other row captures)
3. Would assigning it to an existing row obscure a contamination distinction
   that the methodology needs to express?

If yes to all three, add a new row.

### Rules for Adding Rows

- Only add rows for distinct product types, not for packaging variants.
  "Canned fruit juice" is a packaging distinction handled by Sn achievability
  notes, not a separate product type row.
- A scope boundary qualifier like "(not canned)" stays as a qualifier on
  the existing row, not as a reason to add a canned variant row.
- New rows must be given clear, specific names that unambiguously identify
  the product type.
- New rows are inserted in a logical position within the list (grouped with
  related subcategories).

---

## Step 0D: Lock the Expanded Subcategory List

The output of Steps 0A–0C is the **Expanded Subcategory List**. This is the
exact set of rows that will appear in every Section 2 standards table across
all 8 per-metal documents and in the master summary table of the Standards
Briefing.

### Example — Category 1: Infant and Child Foods (locked)

| # | Subcategory | Split From | Variant Type |
|---|------------|------------|-------------|
| 1 | Infant formula, powder (non-soy) | Infant formula (powder) | Clean benchmark |
| 2 | Infant formula, powder (soy-based) | Infant formula (powder) | Contamination platform (Al, Ni, Cd) |
| 3 | Infant formula, RTF liquid (non-soy) | Infant formula (RTF, liquid) | Clean benchmark |
| 4 | Infant formula, RTF liquid (soy-based) | Infant formula (RTF, liquid) | Contamination platform (Al, Ni, Cd) |
| 5 | Baby cereals / grain products, dry (non-rice) | Baby cereals / grain products (dry) | Clean benchmark |
| 6 | Baby cereals / grain products, dry (rice-based) | Baby cereals / grain products (dry) | Contamination platform (iAs, Cd, Pb) |
| 7 | Fruit purées (general) | — | No split |
| 8 | Non-root vegetable purées | — | No split |
| 9 | Root-vegetable purées | — | No split (cross-row CC from #8) |
| 10 | Meat and poultry purées | — | Added: product type without existing home |
| 11 | Fish-containing baby foods | — | Added: contamination platform (MeHg) |
| 12 | Mixed meals, non-rice (e.g., meat & grain combos) | Mixed meals | Clean benchmark |
| 13 | Mixed meals, rice-containing | Mixed meals | Contamination platform (iAs, Cd, Pb) |
| 14 | Fruit juice (not canned) | — | No split |
| 15 | Teething & snacks (non-rice) | Teething & snacks | Clean benchmark |
| 16 | Teething & snacks (rice-based) | Teething & snacks | Contamination platform (iAs, Cd, Pb) |

**Total: 16 expanded subcategories from 9 base taxonomy rows.**

### Programmatic Validation (0D)

The pipeline verifies before proceeding:

- Every base taxonomy subcategory is accounted for
- Every contamination platform split is explicit as separate rows
- Every real product type without a home has been added
- No rows added for packaging variants
- Row names are unambiguous and consistently formatted
- Row order: clean variant precedes contaminated variant
- Cross-row CC relationships are explicitly declared

**Any check that fails stops the pipeline with a specific error.**

---

## Step 0E: Build the Regulatory Floor Table

For every cell in the expanded subcategory × 8 metals grid, determine the
most protective finalized regulatory value.

**Web search required.** Search for:
- EU Commission Regulation 2023/915 (and amendments) for this metal
- FDA action levels (CTZ, other) for this metal in this food type
- Codex Alimentarius ML values
- National regulations (UK, Japan, other) where applicable

Apply the **Confirmed Corrections** list (Methodology Reference Section 3.2)
to every value found. Known hallucination patterns include FDA CTZ applied
to non-lead metals, wrong ppb values for dry cereals, and formula exemptions.

### Output Format

| # | Subcategory | Pb | iAs | Cd | Hg | Cr | Ni | Sn | Al |
|---|-----------|-----|-----|-----|-----|-----|-----|-----|-----|

Where each cell contains: the floor value in ppb, or "—" if no finalized
limit exists.

### Rules

- The floor is the **most protective** (lowest) value from any jurisdiction.
- Use only **finalized** regulations. Draft, proposed, or under-public-comment
  values go in the Watch Items Table, not the floor table.
- Cite the exact regulation name, section/annex number, and year for every
  non-dash cell.
- Where a regulation names a broader food category but not the exact
  subcategory, flag the mapping as "INFERRED" and note what the regulation
  actually says.
- Apply all Confirmed Corrections from Methodology Reference Section 3.2,
  particularly:
  - EU Reg. 2024/1987 Ni values require final verification before
    publication (flagged as placeholder).
- If unsure whether a regulatory value applies to a specific subcategory,
  mark as "INFERRED" and note what the regulation actually says.
- Do not include draft, proposed, or under-public-comment values as floors.
  Capture them in the **Watch Items Table** (see below).

### Watch Items Table (produced during Step 0E)

During web search for regulatory floor values, capture any regulatory,
scientific, or market developments that could affect this category's
standards within the next revision cycle (2 years). These are NOT inputs
to the formula — they are informational outputs included in the Build
Summary (Step 3E).

**Categories:**
- Regulatory: draft or proposed regulations, active rulemaking proceedings
  (FDA, EU, Codex), pending amendments, state-level initiatives
- Scientific: pending EFSA or JECFA evaluations, ongoing exposure
  assessments, new occurrence data studies
- Market: new product types emerging, reformulation trends, new ingredient
  platforms gaining market share

**Required format:**

| Watch Item | Type | Authority/Source | Expected Timeline | Impact if Finalized |
|-----------|------|-----------------|-------------------|-------------------|

**How to produce:** During Step 0E's web search for each authority × metal
× subcategory, note any draft, proposed, or pending actions encountered.
Additionally search FDA Unified Agenda, EU regulatory pipeline, and Codex
work program for this category.

---

## Step 0F: Source Clean Platform Data

For every cell in the expanded subcategory list × 8 metals grid, determine
the clean platform occurrence value using the mechanical two-path selection
rule. This step applies to **clean-variant rows, unsplit rows, and
contaminated-variant rows on metals where the contamination platform
distinction does not apply** (i.e., all cells that are not covered by
Step 0G).

**Step 0F does NOT apply the limit formula.** It sources input data
only. Limit determination is Step 1's job.

### Path A — Data-driven (preferred)

If a government survey or two independent peer-reviewed studies report
percentile data for the clean platform in this subcategory × metal pair,
the clean platform value = the **P90 (90th percentile) of the clean
platform distribution**.

**Web search required.** Search for occurrence data in this priority order:
1. Government survey data: FDA Total Diet Study, FDA Toxic Elements in
   Food and Foodware Program, EFSA dietary exposure scientific opinions,
   JECFA evaluations with occurrence data
2. Two or more independent peer-reviewed studies reporting percentile
   distributions for the specific product type × metal pair

Extract the 90th percentile value. Cite the dataset with full
bibliographic detail.

**Confidence tag: DATA-GROUNDED.**

### Path B — Precautionary (when data is insufficient)

If Path A data does not exist, the clean platform value = **5× the
analytical limit of quantification (LOQ)** for that metal in that food
matrix.

The LOQ source: the validated LOQ from the analytical method specified
for this metal in this food matrix. If no published method LOQ can be
found via web search, use the default LOQ table below.

**Confidence tag: PROVISIONAL.** PROVISIONAL values trigger mandatory
review at the first revision cycle.

### LOQ Default Table (last resort for Path B)

When web search cannot find a published method LOQ for the specific
metal × matrix pair, use these conservative defaults:

| Metal | Default LOQ | Path B Value (5× LOQ) |
|-------|------------|----------------------|
| Pb | 1 ppb | 5 ppb |
| iAs | 1 ppb | 5 ppb |
| Cd | 1 ppb | 5 ppb |
| Hg | 1 ppb | 5 ppb |
| Cr | 5 ppb | 25 ppb |
| Ni | 5 ppb | 25 ppb |
| Sn | 10 ppb | 50 ppb |
| Al | 10 ppb | 50 ppb |

These are intentionally conservative (low). They produce tight limits,
consistent with Principle 1 (drive contamination down). Step 0F should
exhaust web search before falling back to these.

### Output Format

The Clean Platform Data Package must include, for every applicable
subcategory × metal pair:

| Subcategory | Metal | Path | Data Source | P90 Value | LOQ Source | Clean Platform Value | Confidence |
|-------------|-------|------|-------------|-----------|------------|---------------------|-----------|

Where:
- **Path A row:** Data Source = full citation, P90 Value = the extracted
  90th percentile, LOQ Source = "—", Clean Platform Value = raw P90
  (rounding happens in Step 1), Confidence = DATA-GROUNDED
- **Path B row:** Data Source = "Insufficient data", P90 Value = "—",
  LOQ Source = method citation or "Default LOQ table",
  Clean Platform Value = 5 × LOQ, Confidence = PROVISIONAL

### Programmatic Validation (0F)

The pipeline verifies before proceeding:

- Every applicable cell has a clean platform value (no blanks)
- Every Path A value has a full data source citation
- Every Path B value has an LOQ source (method citation or default table)
- Every cell has a confidence tag (DATA-GROUNDED or PROVISIONAL)
- No value was derived from training data, expert judgment, or
  any source other than Path A or Path B

**Any check that fails stops the pipeline with a specific error.**

---

## Step 0G: Source Contaminated Platform Data

For every **contaminated-variant row × affected metal** pair (as defined
in the Contamination Platform Map), determine the contaminated platform
occurrence value.

**Step 0G does NOT apply the limit formula.** It sources input data
only. Limit determination is Step 1's job.

### Path A — Data-driven (preferred)

If a government survey or two independent peer-reviewed studies report
percentile data for the **contaminated platform** in this subcategory ×
metal pair, the contaminated platform value = the **P10 (10th percentile)
of the contaminated platform distribution**.

The P10 represents what only the cleanest 10% of contaminated-platform
products can achieve. This is intentionally exclusionary: approximately
90% of contaminated-platform products on the market today would NOT pass.

**Dataset definition:** The distribution includes **all commercially
available products** on the contaminated ingredient platform in the
relevant subcategory. The dataset is not filtered by brand intent,
certification status, or sourcing strategy. It represents the market as
it exists.

**Web search required.** Same source hierarchy as Step 0F:
1. Government survey data: FDA Total Diet Study, FDA Toxic Elements
   Program, EFSA dietary exposure scientific opinions, JECFA evaluations
2. Two or more independent peer-reviewed studies reporting percentile
   distributions for the specific product type × metal pair

Extract the 10th percentile value. Cite the dataset with full
bibliographic detail.

**Confidence tag: DATA-GROUNDED.**

### Path B — No separate limit (when data is insufficient)

If Path A data does not exist for the contaminated platform, **no
separate contaminated limit is published.** The contaminated-variant
row receives the same limit as its paired clean-variant row for the
affected metal.

**Rationale:** The justification for granting a higher limit to the
contaminated platform is that data demonstrates what the best
contaminated-platform products can achieve. Without that data, there
is no basis for accommodation. Granting a higher limit without evidence
violates the Clean Benchmark Policy.

**Confidence tag: PROVISIONAL — HELD TO CLEAN.** This triggers mandatory
review at the first revision cycle. If contaminated platform occurrence
data has become available, the P10 is calculated and a separate limit
may be established. If no data has emerged, the contaminated platform
remains held to the clean standard.

### Output Format

The Contaminated Platform Data Package must include, for every
contaminated-variant row × affected metal pair:

| Subcategory | Metal | Path | Data Source | P10 Value | Contaminated Platform Value | Confidence |
|-------------|-------|------|-------------|-----------|----------------------------|-----------|

Where:
- **Path A row:** Data Source = full citation, P10 Value = the extracted
  10th percentile, Contaminated Platform Value = raw P10 (rounding
  happens in Step 1), Confidence = DATA-GROUNDED
- **Path B row:** Data Source = "Insufficient data", P10 Value = "—",
  Contaminated Platform Value = "HELD TO CLEAN", Confidence =
  PROVISIONAL — HELD TO CLEAN

### Programmatic Validation (0G)

The pipeline verifies before proceeding to Step 1:

- Every contaminated-variant × affected-metal cell has either a P10
  value or "HELD TO CLEAN" designation (no blanks)
- Every Path A value has a full data source citation
- Every HELD TO CLEAN designation has a PROVISIONAL tag
- No value was derived from training data, expert judgment, or
  any source other than Path A or Path B

**Any check that fails stops the pipeline with a specific error.**

---

## Percentile Threshold Parameters

The default percentile thresholds are:

| Parameter | Symbol | Default | Range | Adjustable? |
|-----------|--------|---------|-------|-------------|
| Clean pass rate | P_clean | 90th percentile | 85th–95th | Yes, with documented justification per category |
| Dirty pass rate | P_dirty | 10th percentile | 5th–15th | Yes, with documented justification per category |

For **Category 1 (Infant and Child Foods):** The Program Operator may
tighten to P_clean = 95th, P_dirty = 5th, based on Principle 2 (infants
receive the highest level of protection). This must be declared before
Step 0F runs and documented in the Build Summary.

The thresholds are **category-level parameters**, not per-metal or
per-brand. They are documented in the Build Summary but never exposed
in published Standards Briefings (Rule 1: never expose the formula).

---

## How Downstream Steps Consume Step 0 Outputs

### Step 1 (Limit Determination)

Step 1 receives all five Step 0 outputs:
- The **Expanded Subcategory List** (the rows)
- The **Contamination Platform Map** (which rows are clean/contaminated,
  which metals are affected)
- The **Regulatory Floor Table** (government limits per cell)
- The **Clean Platform Data Package** (P90 or 5×LOQ values per cell)
- The **Contaminated Platform Data Package** (P10 or HELD TO CLEAN per cell)

Step 1 applies the limit formula and produces the **Master Limit
Table** — the single table of published ppb values for every cell.

### Step 2 (Document Generation)

Step 2 receives:
- The **Expanded Subcategory List** from Step 0 (the rows)
- The **complete Master Limit Table** from Step 1 (the values)
- The **Contamination Platform Map** from Step 0

The document generation prompt must include this instruction:

> "The following subcategory list and limit values have been validated
> in Steps 0 and 1. Use EXACTLY these subcategory names as Section 2
> table rows, in this exact order. Use EXACTLY these HMTc values. Do not
> recalculate, rename, reorder, add, remove, or deviate from any row or
> value in this table."

### Step 3 (Structural Validation)

The validator checks:
- Section 2 table row count matches the Expanded Subcategory List count
- Section 2 table row names match the Expanded Subcategory List names
  (exact string match)
- Section 2 HMTc values match the Master Limit Table values
  (exact integer match)
- Briefing master summary table matches the complete Master Limit Table

**Any mismatch is a build failure.** The document is rejected and regenerated.

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | April 2026 | Initial protocol. Replaces slash notation approach. Establishes expanded subcategory list and master limit table as locked contract between planning and build phases. Written after Inngest pipeline audit revealed 5 failure modes caused by independent LLM calls not sharing Step 0 outputs. |
| 1.1 | April 2026 | Removed all human approval gates (3 instances). Replaced "Lock Confirmation" checklists at 0D and 0F with programmatic validation checks. Replaced supervised/automated build language with automated pipeline language. Changed "approved" to "validated" in downstream prompt template. Required for Inngest compatibility. |
| 1.2 | April 2026 | Resolved Step 0 / Step 1 boundary. Step 0F rewritten from "Compute the Master Limit Table" (formula application) to "Source CC Data" (Path A/B data sourcing only). Formula application moved entirely to Step 1. Step 0 now produces 4 outputs: Expanded Subcategory List, Contamination Platform Map, Regulatory Floor Table, CC Source Data Package. Master Limit Table is now a Step 1 output. Downstream consumption section rewritten to reflect corrected data flow. Added Watch Items Table as a formal output of Step 0E (absorbs former Pre-Build Protocol Deliverable 5). |
| 1.3 | April 2026 | **Dual-percentile model.** Replaced single CC Source Data Package with two packages: Clean Platform Data Package (P90, Step 0F) and Contaminated Platform Data Package (P10, Step 0G). Eliminated T (tolerance factor) and VME from the methodology. Contaminated platform limits are now independently data-derived from the 10th percentile of the contaminated platform distribution, not computed from the clean value × (1+T). Path B for contaminated platforms = "HELD TO CLEAN" (no separate limit without data). Added adjustable percentile threshold parameters (P_clean 85th–95th, P_dirty 5th–15th) as category-level declarations. Step 0 now produces 5 outputs. |
