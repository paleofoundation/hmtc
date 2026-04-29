# HMTc Methodology Reference v5.1 Addendum

**Evidence Fitness, No-Data Handling, Speciation, and Regulatory Cap Terminology**

**Draft date:** 2026-04-29

**Status:** draft for review

**Governing document:** `HMTc_Governing_Principles.md` remains controlling. This
addendum does not modify the governing principles. It clarifies how the v5.0
dual-percentile methodology should accept, reject, model, and audit occurrence
data before standards are calculated.

## 1. Purpose

Version 5.0 correctly establishes the dual-percentile model:

- Clean platform and unsplit rows use P90 of the clean platform distribution.
- Contaminated-platform affected rows use P10 of the contaminated platform
  distribution.
- Contaminated-platform unaffected rows inherit the paired clean value.
- No separate contaminated limit may be published without contaminated-platform
  occurrence data.

This addendum adds the missing gate between source extraction and limit
calculation: **Evidence Fitness**. A percentile can only enter Step 1 if the
underlying evidence is fit for that exact use.

The goal is to prevent the standards engine from treating all numbers as
equivalent. A source-reported P90 for rice cereal lead, a study mean for mixed
baby foods cadmium, and a maximum value from a small NGO report are not the same
kind of evidence. They may all be useful, but they do not deserve the same
confidence tag or the same publication authority.

## 2. Insert New Section After v5.0 Section 1.4

### 1.4A Evidence Fitness Gate

Before any P90_clean or P10_dirty value may enter the Step 1 limit formula, the
evidence must pass an Evidence Fitness Gate.

The Evidence Fitness Gate is mechanical. It does not choose the desired outcome.
It determines whether a piece of evidence is eligible for:

1. DATA-GROUNDED percentile use;
2. PROVISIONAL modeled use;
3. context-only use; or
4. exclusion from limit computation.

Every evidence record used in Step 0F or Step 0G must receive an Evidence
Fitness verdict before Step 1 runs.

### Required Evidence Fitness Fields

Each occurrence evidence record must store:

| Field | Required meaning |
|---|---|
| `source_id` | Stable source identifier. |
| `source_tier` | A, B, or C under the shared evidence contract. |
| `source_type` | Government survey, peer-reviewed article, regulatory report, NGO report, lab report, dataset, etc. |
| `metal_species` | Exact analyte, such as Pb, Cd, iAs, tAs, tHg, MeHg, Ni, Al, Cr-VI, total Cr, or Sn. |
| `product_matrix` | Product or ingredient matrix tested. |
| `hmtc_row_match` | Exact row match, clean counterpart match, contaminated counterpart match, adjacent matrix, or non-matching. |
| `basis` | As sold, reconstituted, wet weight, dry weight, or not reported. |
| `unit_original` | Unit as reported by the source. |
| `unit_normalized` | Deterministic normalized unit, normally ppb or ug/kg. |
| `statistic_type` | P90, P10, percentile, raw sample set, mean, median, maximum, range, detection frequency, regulatory limit, or other. |
| `sample_size` | Number of samples when reported. |
| `censoring_status` | Whether non-detects, LOQ, LOD, substitution, or left-censoring are reported. |
| `date_scope` | Year or survey period represented by the data. |
| `quote_trace` | Source quote or table reference supporting the value. |
| `review_state` | Machine extracted, needs review, reviewed, approved for internal, rejected, or superseded. |

No occurrence value may enter Step 1 unless `metal_species`, `product_matrix`,
`basis`, `unit_normalized`, `statistic_type`, and `quote_trace` are present.
Missing values may be retained for research, but they are not computation-ready.

## 3. Evidence Fitness Verdicts

The following verdicts replace informal use of "good enough" occurrence data.

| Verdict | Meaning | Step 1 use |
|---|---|---|
| EF-1 Direct Percentile | Source directly reports P90 for the clean platform or P10 for the contaminated platform, with matching metal species, matrix, basis, and unit. | May support DATA-GROUNDED Path A. |
| EF-2 Reconstructable Distribution | Source provides sample-level data or a sufficiently described distribution that allows deterministic percentile calculation. | May support DATA-GROUNDED Path A after deterministic calculation and audit. |
| EF-3 Modeled Percentile | Source provides mean/SD, median/IQR, ranges, maximums, or source-level summaries from which a percentile is estimated. | Internal candidate only unless reviewed and approved; default confidence is PROVISIONAL-MODELED, not DATA-GROUNDED. |
| EF-4 Context Only | Source is relevant but does not support a concentration percentile for the exact row-metal-platform cell. | May inform narrative, gap reports, and source discovery. Must not drive Step 1. |
| EF-5 No Usable Data | No adequate occurrence data exists for the exact cell. | Clean rows go Path B 5x LOQ. Contaminated affected rows are HELD TO CLEAN. |
| EF-X Rejected | Fabricated, unverifiable, wrong metal, wrong matrix, wrong unit, regulatory value mistaken for occurrence data, or otherwise unusable. | Excluded. |

### DATA-GROUNDED Eligibility

A value may be labeled DATA-GROUNDED only if all of the following are true:

1. The analyte matches the certification analyte or has an approved speciation
   bridge.
2. The product matrix matches the HMTc row or an explicitly approved clean or
   contaminated counterpart.
3. The concentration basis is known or defensibly normalized.
4. The unit conversion is deterministic and auditable.
5. The statistic is either source-reported P90/P10 or deterministically
   calculated from sample-level or distribution-level data.
6. The source is A-tier or approved B-tier for internal standards use.
7. The value is backed by a source quote, table, or dataset reference.

If any of these conditions fails, the value must not be labeled
DATA-GROUNDED.

## 4. Modeled Percentiles

Modeled percentiles are allowed for internal review, but they must not be
mistaken for observed occurrence percentiles.

Examples of modeled percentiles include:

- `mean + 1.28 x SD` used as an approximate P90;
- `mean - 1.28 x SD` used as an approximate P10;
- percentiles calculated over study-level means rather than sample-level
  observations;
- percentiles inferred from a maximum, range, median, IQR, or threshold
  exceedance rate;
- imputed values from censored datasets without the source's censoring method.

### Rule

Modeled percentiles receive the confidence tag **PROVISIONAL-MODELED** unless a
human reviewer approves them for a specific category-metal-row with documented
justification.

PROVISIONAL-MODELED values may:

- identify data gaps;
- prioritize review;
- support internal scenario analysis;
- serve as a temporary candidate when no better evidence exists.

PROVISIONAL-MODELED values may not:

- be called DATA-GROUNDED;
- silently replace missing P90/P10 data;
- support a separate contaminated-platform limit unless reviewed and approved;
- appear in public standards briefings as a formula input or rationale.

## 5. Multi-Source Adjudication

When multiple eligible sources exist, Step 0 must not simply choose the
lowest P90 or highest P10 by default. The system must first group comparable
evidence and select the best-fit evidence according to the following hierarchy:

1. Exact HMTc row, exact metal species, exact basis, government or
   intergovernmental source.
2. Exact row, exact species, exact basis, peer-reviewed sample-level dataset.
3. Explicit clean or contaminated counterpart, exact species, exact basis.
4. Adjacent matrix with documented applicability.
5. Approved B-tier source with strong matrix and species match.
6. Modeled or summary-derived evidence.

If two sources are comparable in quality and scope, use the more protective
value for the relevant platform:

- For clean P90, the more protective value is the lower eligible P90.
- For contaminated P10, the more protective value is the lower eligible P10
  unless using the lower value would place the contaminated row below the clean
  floor. The clean floor rule still applies.

If sources conflict by 20% or more after unit and basis normalization, the cell
must be flagged `SOURCE_CONFLICT_REVIEW` before publication.

## 6. No-Data and Held-To-Clean Rules

### Clean and Unsplit Rows

If no EF-1 or EF-2 clean-platform evidence exists, the clean or unsplit row
uses Path B:

```text
P90_clean = 5 x LOQ
confidence = PROVISIONAL
review_required = true
```

The LOQ must be metal-specific and matrix-appropriate. If no matrix-appropriate
LOQ exists, Step 1 must block publication for that cell until a lab method or
approved default LOQ is documented.

### Contaminated Affected Rows

If no EF-1 or EF-2 contaminated-platform evidence exists for an affected metal,
no separate contaminated limit may be published.

The contaminated row must inherit the paired clean row:

```text
Limit_dirty = Limit_clean
confidence = PROVISIONAL - HELD TO CLEAN
review_required = true
```

This rule applies whether the no-data condition is discovered by an AI agent,
a source-first extractor, a manual review, or any other pathway. "No event" is
not equivalent to "data grounded."

### No Zero Default

No HMTc concentration limit may default to 0 ppb because of missing data,
missing clean counterpart, missing LOQ, or missing source extraction.

If the engine cannot identify a valid clean counterpart for a contaminated
affected row, Step 1 must stop with:

```text
BLOCKED_MISSING_CLEAN_COUNTERPART
```

If the engine cannot identify a valid LOQ for a Path B clean or unsplit row,
Step 1 must stop with:

```text
BLOCKED_MISSING_LOQ
```

## 7. Clean Counterpart Integrity

Every contaminated-platform affected row must have an explicit clean
counterpart in the Contamination Platform Map before Step 1 runs.

The map must state:

| Field | Meaning |
|---|---|
| `contaminated_row_id` | HMTc row containing the contamination platform. |
| `clean_counterpart_row_id` | Row used for the clean benchmark. |
| `contamination_platform` | Rice, soy, root vegetable, predatory fish, tinplate can, etc. |
| `affected_metals` | Metals affected by that platform. |
| `unaffected_metals` | Metals that inherit the clean row without separate dirty data. |
| `evidence_required` | Whether P10 dirty evidence is required for a separate limit. |

Validation must confirm:

1. Every contaminated affected row has a clean counterpart.
2. Every contaminated affected cell either has eligible P10 evidence or inherits
   the clean counterpart.
3. No contaminated affected published value is below its clean counterpart.
4. No contaminated affected cell is published from a missing input.

## 8. Regulatory Cap Terminology

The v5.0 term `Regulatory_Floor` is directionally confusing because the rule
operates as an absolute ceiling:

```text
Limit_published = min(Limit_formula, Regulatory_Cap)
```

Future documents and software should use:

- `Regulatory_Cap`
- `Government_Maximum_Cap`
- `Regulatory_Ceiling`

The term `Regulatory_Floor` may remain as a backward-compatible alias in older
workbooks and code, but new documents should state:

> No HMTc limit may exceed the most protective finalized regulatory maximum,
> action level, or maximum level applicable to the same metal-category pair.

This is a cap, not a floor.

## 9. Chromium Speciation

The active HMTc testing panel must distinguish total chromium from hexavalent
chromium.

### Rules

1. If the certification analyte is Cr-VI, standards must be modeled, tested,
   and published as Cr-VI.
2. Total chromium may not be substituted for Cr-VI without an approved
   speciation bridge.
3. A total chromium regulatory limit may not be used as a Cr-VI regulatory cap
   unless the underlying regulation expressly applies to Cr-VI or the
   applicability has been reviewed and approved.
4. Total chromium may be retained as a screening analyte or speciation trigger.
5. If total chromium exceeds the HMTc speciation trigger, Cr-VI testing is
   required before certification for that product or matrix.

Recommended canonical codes:

| Code | Meaning |
|---|---|
| `Cr-total` | Total chromium, screening or regulatory context only unless adopted as a certification analyte. |
| `Cr-VI` | Hexavalent chromium, certification analyte when the HMTc panel calls for Cr(VI). |

## 10. Role of AI Models

AI models may assist the methodology by:

- locating candidate sources;
- extracting candidate values with quotes;
- classifying source type, source tier, matrix, analyte, and statistic type;
- identifying conflicts and missing data;
- drafting internal rationales and public prose after deterministic values are
  locked.

AI models must not:

- invent occurrence values;
- choose limits directly;
- override the Evidence Fitness Gate;
- convert modeled estimates into DATA-GROUNDED values;
- weaken no-data rules for convenience;
- cite public-facing standards rationales from internal formula inputs.

The standards determination is made by deterministic rules over audited
evidence. AI contributes evidence extraction and reasoning support; it is not
the source of the number.

## 11. Step 0 Deliverable Changes

Step 0 must now produce six locked outputs instead of five:

1. Expanded Subcategory List.
2. Contamination Platform Map.
3. Regulatory Cap Table.
4. Clean Platform Data Package.
5. Contaminated Platform Data Package.
6. **Evidence Fitness Register.**

The Evidence Fitness Register must include one row for each candidate
source-value pair reviewed for Step 0F or Step 0G.

Minimum columns:

```text
category_id
subcategory_id
metal_species
platform_type
source_id
source_tier
source_type
matrix_match
basis
unit_normalized
statistic_type
sample_size
censoring_status
evidence_fitness_verdict
confidence_tag
review_state
quote_trace
exclusion_reason
```

Step 1 may consume only Evidence Fitness Register rows with verdict EF-1 or
EF-2 for DATA-GROUNDED Path A. EF-3 rows may be consumed only as
PROVISIONAL-MODELED internal candidates and must be marked review-required.

## 12. Audit Protocol Additions

Add these checks to the v5.0 11-step audit:

1. Verify that every Step 1 input has an Evidence Fitness verdict.
2. Verify that every DATA-GROUNDED input is EF-1 or EF-2.
3. Verify that every modeled percentile is labeled PROVISIONAL-MODELED.
4. Verify that no contaminated affected row published a separate limit without
   eligible P10 evidence.
5. Verify that no cell defaulted to 0 ppb.
6. Verify that every contaminated affected cell has a clean counterpart.
7. Verify that total chromium and Cr-VI were not conflated.
8. Verify that regulatory caps apply to the same product category, metal
   species, and concentration basis as the HMTc cell.

Any failure in checks 4, 5, 6, 7, or 8 is a critical publication blocker.

## 13. Software Implementation Requirements

The Standards Generator should implement this addendum as follows:

1. Add an Evidence Fitness verdict to every extracted occurrence value before
   aggregation.
2. Split Chromium into `Cr-total` and `Cr-VI`, or explicitly mark total
   chromium as screening-only.
3. Rename `regulatory_floor` to `regulatory_cap` in new code while retaining a
   backward-compatible alias if needed.
4. Treat missing dirty evidence as HELD TO CLEAN even when the source-first
   pipeline, rather than an AI agent, discovered the gap.
5. Block Step 1 if a contaminated affected row lacks a clean counterpart.
6. Block Step 1 if Path B requires an LOQ and no acceptable LOQ exists.
7. Downgrade mean/SD, range, max, and source-summary estimates to
   PROVISIONAL-MODELED unless reviewed.
8. Validate contaminated affected cells by looking up the paired clean row, not
   by comparing values within the same cell object.
9. Add regression tests for:
   - contaminated affected row below clean counterpart;
   - fish/mercury or other dirty row with no P10 and no clean counterpart;
   - source-first no-data cell;
   - mean/SD modeled percentile confidence downgrade;
   - total chromium vs Cr-VI regulatory mismatch.

## 14. Version History Entry

Recommended entry for the next Methodology Reference version history:

| Version | Date | Changes |
|---|---|---|
| 5.1 | 2026-04-29 | Added Evidence Fitness Gate before Step 1; defined EF-1 through EF-X verdicts; restricted modeled percentiles to PROVISIONAL-MODELED unless reviewed; clarified no-data handling and no-zero-default rule; required explicit clean counterparts for contaminated affected rows; renamed Regulatory Floor concept to Regulatory Cap/Regulatory Ceiling for future documents; clarified total chromium vs Cr-VI speciation; added AI role boundaries and software implementation requirements. |
