# HMTc Methodology Reference

**Version 5.0 — April 2026**

**Governing document: `HMTc_Governing_Principles.md` — read first, apply at every step.**

This is the single authoritative technical specification for the HMTc Program's
limit-setting methodology, regulatory anchors, audit protocol, document
architecture, and publication presentation rules.

**If you are Claude executing an HMTc build:** Read this entire document before
Step 0. Every rule here is mandatory. No exceptions.

---

# PART 1: LIMIT-SETTING METHODOLOGY

## 1.1 Governing Principle — The Clean Benchmark Standard

HMTc category limits are set based on what a well-formulated product using the
cleanest commercially viable ingredient platform can achieve for each metal.
The Program does not adjust limits upward to accommodate ingredient platforms
with inherently elevated contamination profiles.

A standard that benchmarks to the most contaminated ingredient platform
certifies contamination. A standard that benchmarks to the cleanest viable
platform drives reduction. The HMTc Program exists to drive reduction.

## 1.2 The Dual-Percentile Model

HMTc limits are set by two independently sourced data points, one for each
platform type:

**Clean platform (and unsplit rows):** The limit is derived from the **90th
percentile (P90)** of the clean platform's occurrence distribution.
Approximately 90% of clean-platform products on the market today would pass.

**Contaminated platform (affected metals only):** The limit is derived from
the **10th percentile (P10)** of the contaminated platform's occurrence
distribution. Only approximately 10% of contaminated-platform products on
the market today would pass. The remaining 90% must reformulate, improve
sourcing, or forgo certification.

### Why dual-percentile replaces the tolerance factor

The previous model (v4.x) computed contaminated limits as CC_clean × (1 + T),
where T defaulted to 0.33. This created three problems:

1. **Ladder artifacts at low ppb.** The publication ladder gaps (5 → 10 is
   100%) swallowed the 33% tolerance margin, requiring a Visible Margin
   Exception (VME) to rescue collapsed values.
2. **Arbitrary parameter.** T = 0.33 had no data-driven justification.
   "Why not 0.25 or 0.40?" is unanswerable without empirical measurement.
3. **Disconnection from reality.** T × clean tells you nothing about what
   contaminated products actually achieve. The dual-percentile model
   measures each platform's distribution directly.

The dual-percentile model eliminates T, VME, CC_clean × (1+T), and the
two-step rounding process (rounding table + ladder verification). Both
limits are now set by the same methodology — percentile of the relevant
platform — making the system simpler, more defensible, and consistent
across the full ppb range.

## 1.3 The Limit Formula

```
CLEAN-VARIANT ROW / UNSPLIT ROW:
  Limit = L_down( min( P90_clean, Regulatory_Anchor, 2 × M ) )

CONTAMINATED-VARIANT ROW (affected metals):
  Limit = L_down( min( P10_dirty, Regulatory_Anchor, 2 × M ) )
  then:  Limit = max( Limit, Limit_clean )     ← clean floor rule

CONTAMINATED-VARIANT ROW (unaffected metals):
  Limit = Limit_clean

ALL ROWS — final gate:
  Limit_published = min( Limit, Regulatory_Floor )
```

### Variables

| Symbol | Definition |
|--------|-----------|
| P90_clean | The 90th percentile of the clean platform distribution, or 5× LOQ (Path B). Sourced in Step 0F. Enters the min() for clean-variant and unsplit rows. |
| P10_dirty | The 10th percentile of the contaminated platform distribution. Sourced in Step 0G. Only exists for contaminated-variant rows × affected metals with DATA-GROUNDED status. |
| Regulatory_Anchor | An existing EU ML, FDA action level, or other binding regulatory reference. When none exists for a metal-subcategory pair, this constraint is omitted. |
| M | Column median — the median of all category limits for that metal within the standards category. |
| L_down( ) | Ladder snap — rounds DOWN to the nearest value on the publication increment ladder. Single operation. |
| Limit_clean | The published limit of the paired clean-variant row. Used in the clean floor rule. |
| Regulatory_Floor | The lowest finalized regulatory ML or action level applicable to this exact metal-category pair. Checked AFTER the formula. |

## 1.4 Occurrence Data Selection (CC Selection)

The occurrence data for each platform is determined mechanically. There are
two paths depending on whether adequate data exists. The path selection is
itself mechanical.

### Clean Platform Data (Step 0F)

**Path A — Data-driven (preferred):**

The clean platform value is the **90th percentile of the clean platform
distribution** from the best available dataset.

Data sources in priority order:
1. Government survey data: FDA Total Diet Study, FDA Toxic Elements Program,
   EFSA dietary exposure opinions, JECFA evaluations
2. Two or more independent peer-reviewed studies reporting percentiles or
   distributions for the specific product type and metal

The dataset includes **all commercially available products** on the clean
ingredient platform. No filtering by brand intent, certification status,
or sourcing strategy.

**Confidence tag: DATA-GROUNDED.**

**Path B — Precautionary (when data is insufficient):**

The clean platform value is **5× the analytical limit of quantification
(LOQ)** for that metal in that food matrix.

**Confidence tag: PROVISIONAL.** PROVISIONAL values trigger mandatory
review at the first revision cycle.

**No third path exists.** No expert judgment. No fabricated values.

### Contaminated Platform Data (Step 0G)

**Path A — Data-driven (preferred):**

The contaminated platform value is the **10th percentile of the
contaminated platform distribution** from the best available dataset.

Same source hierarchy as clean platform data. The dataset includes **all
commercially available products** on the contaminated ingredient platform.
No filtering by brand intent, certification status, or sourcing strategy.

The P10 represents what only the cleanest 10% of contaminated-platform
products can achieve. This is intentionally exclusionary.

**Confidence tag: DATA-GROUNDED.**

**Path B — No separate limit (when data is insufficient):**

If contaminated platform occurrence data does not exist, **no separate
limit is published.** The contaminated row receives the same limit as its
paired clean row for the affected metal.

**Confidence tag: PROVISIONAL — HELD TO CLEAN.**

**Rationale:** Granting a higher limit to the contaminated platform without
data demonstrating what the best performers achieve violates the Clean
Benchmark Policy. The burden of proof is on the contaminated platform:
generate the data (through participation in occurrence studies or the
Enrolled-tier supplier program), and a separate limit can be established
at the revision cycle.

### Cross-Row Occurrence Data Mapping

When the contamination platform relationship exists between rows that are
already separate in the taxonomy (e.g., root-vegetable purées vs. non-root
vegetable purées), the occurrence data relationship must be explicitly
declared in the Contamination Platform Map. The clean-platform row's P90
data is sourced from the clean platform distribution, and the contaminated-
platform row's P10 data is sourced from the contaminated platform
distribution, independently.

### Revision cycle for occurrence data

Occurrence data is reviewed on a **two-year cycle** per category, starting
from the date of initial publication.

- **PROVISIONAL clean values** (Path B) are mandatory review items. If
  adequate data has become available, move to Path A (P90).
- **PROVISIONAL — HELD TO CLEAN contaminated values** (Path B) are
  mandatory review items. If contaminated platform data has become
  available (including from Enrolled-tier suppliers with N ≥ 30), calculate
  P10 and establish a separate limit.
- **DATA-GROUNDED values** are reviewed against the most recent dataset.
  If newer data shifts the percentile downward, the limit tightens. If
  it shifts upward, the limit does not loosen — limits only ratchet tighter.
- Limits never loosen. A published limit is a permanent ceiling.

## 1.5 Constraint 1: Column Median Ceiling (2 × M)

For each metal, calculate the median of all category limits within the
standards category. No individual subcategory may exceed 2× that median.

This constraint catches outliers regardless of cause. It does not need to
know why a value is high — it simply enforces distributional coherence.

**Calculation:** Sort all category values for one metal. The median is the
middle value (odd count) or average of the two middle values (even count).
Multiply by 2.

If a cell is capped by 2×M, flag it as **2×M-CAPPED** in the build
workbook. Frequent 2×M-CAPPED flags on contaminated rows indicate the
contaminated platform is structurally far from the rest of the category.

## 1.6 The Clean Floor Rule

After computing a contaminated-variant limit from P10_dirty, verify that
it is not below the paired clean-variant limit:

```
Limit_dirty = max( L_down(min(P10_dirty, Regulatory_Anchor, 2×M)), Limit_clean )
```

**Why this rule exists:** If the cleanest 10% of contaminated-platform
products test lower than the 90th percentile of clean-platform products
for a specific metal, the contamination platform distinction is irrelevant
for that metal. Publishing a stricter limit for the dirty platform than the
clean platform is incoherent and legally vulnerable.

If the clean floor rule produces identical values for clean and contaminated
rows on a given metal, that is a valid outcome — the data says the platforms
are indistinguishable at that resolution for that metal.

## 1.7 Rounding: Direct Ladder Snap — L_down( )

After applying all constraints and taking the minimum, the result is
rounded DOWN to the nearest value on the publication increment ladder.
**This is a single operation.** There is no intermediate rounding table.

### Publication Increment Ladder

**1, 2, 3, 5, 10, 15, 20, 25, 50, 100, 200, 500, 1000, 1300, 1500,
2000, 5000, 10000**

### Examples

| Raw Value | L_down Result |
|-----------|--------------|
| 1.7 | 1 |
| 4.2 | 3 |
| 8.3 | 5 |
| 13.7 | 10 |
| 27 | 25 |
| 48 | 25 |
| 90 | 50 |
| 133 | 100 |
| 375 | 200 |
| 780 | 500 |
| 1330 | 1300 |

Direction is always DOWN (tighter). No exceptions. No VME. If both
platforms land on the same ladder value after rounding, that is a valid
data-driven outcome — publish the same value.

## 1.8 Constraint 2: Regulatory Floor — Absolute Ceiling

No HMTc limit may ever exceed the most protective finalized regulatory action
level or maximum level that applies to the same metal-category pair.

```
Limit_published = min( Limit_formula, Regulatory_Floor )
```

This check happens AFTER the limit formula, AFTER ladder snap, and AFTER
the clean floor rule. It is the final gate.

**If no finalized regulatory limit exists** for a metal-category pair,
Constraint 2 does not bind. The formula operates on Constraint 1 only.

## 1.9 Percentile Threshold Parameters

The default percentile thresholds are adjustable per category:

| Parameter | Symbol | Default | Range | Level |
|-----------|--------|---------|-------|-------|
| Clean pass rate | P_clean | 90th percentile | 85th–95th | Category-level |
| Dirty pass rate | P_dirty | 10th percentile | 5th–15th | Category-level |

For infant and child food categories, the Program Operator may tighten to
P_clean = 95th, P_dirty = 5th, based on Principle 2 (infants receive the
highest level of protection).

Adjustments require documented justification tracing to one or more
governing principles and must be declared before Step 0F runs.

## 1.10 Distinction: CC Threshold vs. Ratchet Trigger

Two different percentile mechanisms operate at different points in the
program lifecycle. They are distinct and must not be confused:

**CC threshold (P_clean / P_dirty):** Governs initial limit publication.
Set in Step 0F/0G. Answers: "what can X% of products on this platform
achieve today?"

**Ratchet trigger (80th percentile of program testing data, per Governance
Policy §12.3):** Governs subsequent tightening at the revision cycle.
Answers: "has industry improved enough that we should lower the bar?"
This uses aggregate lot-testing data collected through the HMTc Program's
own testing infrastructure, not the external survey data used for initial
CC selection.

---

# PART 2: CONTAMINATION PLATFORM IDENTIFICATION PROTOCOL

## 2.1 What Is a Contamination Platform?

A contamination platform is an ingredient, material, or formulation base that:
1. Contains significantly higher concentrations of one or more heavy metals
   than alternative ingredients serving the same functional role, AND
2. The elevated contamination is intrinsic to the ingredient's biology,
   geology, or processing — not a quality-control failure.

## 2.2 Known Contamination Platforms (carry forward to every build)

| Platform | Affected Metals | Mechanism | Applies To |
|----------|----------------|-----------|------------|
| Rice (Oryza sativa) | iAs, Cd, Pb | Flooded paddy cultivation | Infant foods, cereals, snacks |
| Soy (Glycine max) | Al, Ni, Cd | Protein co-precipitation of Al; soil accumulation of Ni/Cd | Infant formula, supplements |
| Seaweed/algae | iAs, Cd | Marine bioaccumulation | Supplements, foods with seaweed |
| Cacao/chocolate | Cd, Pb | Volcanic soil Cd; post-harvest Pb | Child foods, supplements |
| Root vegetables | Cd, Pb | Root uptake from soil | Infant foods, child foods |
| Predatory fish | MeHg | Biomagnification | Infant foods, child foods, supplements |
| Tinplate cans | Sn | Tin dissolution from lining | Any canned food |
| PVC packaging | Organotin | Stabilizer migration | Any PVC-contact product |
| Turmeric/spices | Pb, Cr | Lead chromate adulteration | Supplements, foods with spices |
| Mineral supplements | Al, Cr, Ni | Geological metal loads | Supplements |

## 2.3 Step-by-Step Protocol

**Step 1:** List all testing subcategories from the Comprehensive Testing
Category Taxonomy.

**Step 2:** For each subcategory, identify the 2–3 dominant ingredient platforms.

**Step 3:** Cross-reference each platform against the Known Contamination
Platforms table. For each match, identify which metals are affected.

**Step 4:** For every identified contamination platform, ensure a clean
counterpart exists. If the taxonomy does not include one, CREATE the
pairing as an analytical split even if the published category remains unified.

**Step 5:** Document all pairings in a Contamination Platform Map:
Subcategory | Contamination Platform | Affected Metals | Clean Counterpart

**Step 6:** Source occurrence data for each platform per the Occurrence Data
Selection protocol (Section 1.4): P90 for clean platforms (Step 0F),
P10 for contaminated platforms (Step 0G).

**Step 7:** Apply the limit formula. For subcategories without a
contamination platform, only Constraints 1 and 2 apply (2×M and
regulatory floor).

---

# PART 3: REGULATORY ANCHORS AND KNOWN CORRECTIONS

## 3.1 Per-Domain Primary Regulatory Sources

### Infant and Child Foods (0–5)
- EU Commission Regulation 2023/915 (Annex I, §3.1 Pb, §3.2 Cd, §3.3 Hg, §3.4 Sn, §3.5 As)
- EU Regulation 2024/1987 (amending 2023/915 for Nickel), entries 3.6.13–3.6.16
- FDA Closer to Zero — Lead ONLY finalized (Jan 2025); Cd, iAs, Hg NOT finalized as of April 2026
- FDA action level for iAs in rice cereal: 100 ppb (Aug 2020)
- Codex Alimentarius CXS 193-1995, CXC 56-2004 (Pb), CXC 77-2017 (As in rice)
- JECFA evaluations (Pb WHO TRS 960; Cd WHO TRS 960; As WHO TRS 959; Al WHO TRS 966)
- EFSA scientific opinions (Pb 2010, As 2009/2014/2024, Cd 2009/2011, Hg 2012, Cr 2014, Ni 2020, Al 2008)
- California Proposition 65 MADLs and NSRLs

### Child and Family Foods / General Foods
- Same EU/FDA/Codex framework with different subcategory MLs

### Dietary Supplements (Human)
- USP <2232> elemental impurities limits (PDE values)
- ICH Q3D(R2)
- FDA DSHEA framework
- California Prop 65

### Cosmetics and Personal Care (Leave-on and Rinse-off)
- EU Cosmetics Regulation 1223/2009
- Health Canada impurity guidance
- FDA VCRP data

### Oral Care
- EU Cosmetics Regulation 1223/2009 (oral care falls under cosmetics)
- FDA monographs
- ADA guidance

### Feminine Care
- 21 CFR Part 884 (FDA device classification)
- EU Medical Device Regulation / Cosmetics Regulation overlap

### Household Cleaning and Dishwashing
- EPA Safer Choice (does NOT set numeric heavy metal limits)
- Green Seal GS-8 (does NOT set finished-product metal concentrations)
- EU Ecolabel (does NOT set product-specific metal limits)

### Laundry and Fabric-Contact Home Products
- Green Seal GS-48
- OEKO-TEX Standard 100 (Product Class I for baby textiles)

### Children's Toys, Arts, and Crafts
- CPSIA Section 101 (100 ppm total Pb)
- ASTM F963 (§4.3.5 soluble limits — Ni and Sn NOT among them)
- EU Toy Safety Directive 2009/48/EC
- EN 71-3 (migration limits by material category)
- LHAMA/ASTM D-4236

### Pet Foods and Pet Supplements
- EU Directive 2002/32
- AAFCO
- FDA CVM

### Home Air and Inhalation-Adjacent Products
- RIVM exposure models
- EPA NAAQS (ambient air, not product limits)
- WHO air quality guidelines

### Food-Contact Consumer Goods and Kitchenware
- EU Regulation 1935/2004 (framework)
- EU Regulation 10/2011 (plastics)
- FDA food-contact substance guidance
- CoE CM/Res(2013)9 (metals and alloys)
- California Prop 65

### Water and Water-Based Products
- EPA MCLs
- FDA 21 CFR 165.110 (bottled water)
- EU Drinking Water Directive 2020/2184

## 3.2 Confirmed Corrections (carry forward in EVERY build)

1. **Pb BMDL01 for nephrotoxicity:** 0.63 µg/kg bw/day (NOT 0.50)
2. **Al JECFA PTWI revision trajectory:** 7 → 1 → 2 mg/kg bw/week (NOT 7 → 2).
   Current JECFA PTWI is 2 mg/kg bw/week.
3. **JECFA Al PTWI = 2 mg/kg bw/week; EFSA Al TWI = 1 mg/kg bw/week.** Distinct
   values from distinct bodies. Do not conflate.
4. **EFSA methylmercury TWI:** 1.3 µg/kg bw/week (NOT 4). The 4 µg/kg bw/week
   applies to inorganic mercury only.
5. **Prop 65 Lead:** The relevant value is the MADL (reproductive endpoint,
   0.5 µg/day). Do NOT cite as NSRL (cancer endpoint, 15 µg/day).
6. **ASTM F963 §4.3.5** soluble limits cover 8 elements. Nickel and tin are
   NOT among them. Do not fabricate values.
7. **REACH Cr(VI) leather limit** under Entry 47: ≤3 mg/kg (NOT ≤0.0002%).
8. **Stannous fluoride** appears in EU Cosmetics Regulation Annex III
   (restricted substances), NOT Annex V (preservatives).
9. **FDA Closer to Zero** (Jan 2025 final) applies to baby foods and cereals
   for LEAD ONLY. Does NOT apply to infant formula. Does NOT cover cadmium,
   arsenic, or mercury — those are NOT finalized as of April 2026.
10. **REGULATORY FLOOR RULE:** No HMTc limit may exceed the most protective
    finalized regulatory action level or ML for the same metal-category pair.
11. **FDA Closer to Zero Pb — category-specific values (Jan 2025):**
    - Dry infant cereals: **20 ppb** (NOT 10)
    - Single-ingredient root vegetables: **20 ppb**
    - Other baby foods (fruits, non-root veg, mixtures, meats): **10 ppb**
    - Infant formula: **exempt**
    - Beverages/juices: **exempt** (draft 2022, not finalized)
12. **Cadmium regulatory floors for infant foods come from EU, not FDA.** FDA
    has NOT finalized Cd action levels. Correct EU Reg. 2023/915 values:
    - Infant formula: 5 ppb (§3.2.17)
    - Processed cereal-based food for infants: 40 ppb (§3.2.18)
    - Baby food (other than cereal-based): 10 ppb (§3.2.19)
13. **EU 2024/1987 Ni for liquid formula (§3.6.13.3):** 100 ppb, no soy/non-soy
    distinction. Soy split only exists for powder (§3.6.13.1 vs §3.6.13.2).
14. **EFSA Ni TDI:** 13 µg/kg bw/day (2020 update, pregnancy loss endpoint).
    Not the 2015 value of 2.8 µg/kg bw/day.

## 3.3 Speciation Triggers (apply across most categories)

- **iAs speciation:** Required for all arsenic testing in food categories;
  triggered by biological-source materials (algae, seaweed) in non-food.
  For non-rice foods, triggered if total As exceeds 50% of HMTc limit.
- **MeHg speciation:** Mandatory for fish/seafood-containing products.
  For non-fish, triggered if total Hg exceeds 50% of HMTc limit.
- **Cr(VI) speciation:** Triggered if total Cr exceeds 500 ppb.
- **Organotin speciation:** TBT ≤0.5 ppm, DBT ≤1.0 ppm (for PVC-containing
  components).
- **EN 1811 nickel release rate:** ≤0.5 µg/cm²/week for skin-contact metal
  surfaces.

## 3.4 Regulatory Floor Values — Infant and Child Foods (0–5)

### Lead (Pb)
| Subcategory | Regulatory Floor | Source |
|-------------|-----------------|--------|
| Infant formula (powder and liquid) | 10 ppb | EU Reg. 2023/915, §3.1.7 |
| Baby cereals / grain products (dry) | 20 ppb | FDA CTZ Jan 2025; EU §3.1.8 also 20 ppb |
| Fruit purées, non-root veg purées, mixed meals, teething snacks | 10 ppb | FDA CTZ Jan 2025 |
| Root-vegetable purées | 20 ppb | FDA CTZ Jan 2025 (root veg) |
| Fruit juice (not canned) | — | No finalized action level |

### Arsenic (iAs)
| Subcategory | Regulatory Floor | Source |
|-------------|-----------------|--------|
| Baby cereals (dry) — rice-based | 100 ppb | FDA iAs rice cereal, Aug 2020; EU §3.5.1 |
| All other subcategories | — | No finalized action level |

### Cadmium (Cd)
| Subcategory | Regulatory Floor | Source |
|-------------|-----------------|--------|
| Infant formula | 5 ppb | EU Reg. 2023/915, §3.2.17 |
| Baby cereals (dry) | 40 ppb | EU Reg. 2023/915, §3.2.18 |
| Baby foods (all other) | 10 ppb | EU Reg. 2023/915, §3.2.19 |

### Mercury (Hg)
| Subcategory | Regulatory Floor | Source |
|-------------|-----------------|--------|
| Fish (by species) | 100–500 ppb MeHg | EU Reg. 2023/915, §3.3 |
| Non-fish infant foods | — | No finalized action level |

### Tin (Sn)
| Subcategory | Regulatory Floor | Source |
|-------------|-----------------|--------|
| Canned baby foods | 50,000 ppb | EU Reg. 2023/915, §3.4.2 |
| Non-canned infant foods | — | No regulatory floor |

### Nickel (Ni)
| Subcategory | Regulatory Floor | Source |
|-------------|-----------------|--------|
| Infant formula (powder, non-soy) | 250 ppb | EU Reg. 2024/1987, §3.6.13.1 |
| Infant formula (powder, soy-based) | 400 ppb | EU Reg. 2024/1987, §3.6.13.2 |
| Infant formula (RTF, liquid) | 100 ppb | EU Reg. 2024/1987, §3.6.13.3 |
| Baby cereals (dry) | 3,000 ppb | EU Reg. 2024/1987, §3.6.14 |
| Baby foods (general) | 500 ppb | EU Reg. 2024/1987, §3.6.15 |
| Fruit juice | 250 ppb | EU Reg. 2024/1987, §3.6.16.1 |

### Chromium (Cr) and Aluminum (Al)
| Subcategory | Regulatory Floor | Source |
|-------------|-----------------|--------|
| All infant foods | — | No finalized ML exists |

### Version-Control Triggers
- **FDA Closer to Zero — Cadmium:** FDA 2026 priority deliverables include Cd
  action levels for baby/toddler foods. When finalized, re-run floor reconciliation.
- **FDA Closer to Zero — Inorganic Arsenic:** Same timeline as Cd.
- **FDA Closer to Zero — Lead in Juices:** Draft 2022, not finalized. Monitor.

---

# PART 4: HALLUCINATION-RESISTANT FACTUAL AUDIT PROTOCOL

## 4.1 Principle

Verify the source exists before verifying the value is correct. If the
citation is fabricated, every downstream check passes against a fiction.

**False negatives are far more costly than false positives. When in doubt, FLAG.**

## 4.2 The 11-Step Audit (Per Claim)

1. **Identify the exact claim** — State category, source, and value.
2. **Verify citation existence** — If you cannot confirm the source exists,
   STOP. Flag as SUSPECTED FABRICATION.
3. **Check for regulatory applicability overstatement** — Does the regulation
   actually cover this specific product category?
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
   - FLAG: Could not be confirmed, source may not exist, or applicability
     overstated
10. **Verify formula compliance** — Confirm every published limit is
    consistent with the locked Master Limit Table. For contaminated rows,
    verify the clean floor rule holds (dirty limit ≥ clean limit on
    affected metals). Verify no limit exceeds 2×M.
11. **Verify Regulatory Floor compliance** — Confirm every limit ≤ the most
    protective applicable finalized regulatory value. Any violation is a
    **CRITICAL FLAG** that blocks delivery.

## 4.3 Known Corrections to Check in Every Audit

(Same as Section 3.2 — always cross-check against the Confirmed Corrections list.)

## 4.4 Values Requiring Verification Before Publication

- EFSA 2024 As BMDL01 exact designation
- EFSA 2015 Ni TDI vs. 2020 updated TDI
- EFSA organotin group TDI
- CoE CM/Res(2013)9 SRL numeric values for Cr, Ni, Pb, As
- USP <2232> Table 2 PDE values
- EN 71-3 migration limits (cross-check against purchased standard)
- OEKO-TEX Annex 4 specific values (subject to annual update)

---

# PART 5: PUBLICATION PRESENTATION PROTOCOL

## 5.1 Rule 1: Never Expose the Formula

### Published documents contain:
- The final limit value
- The principle ("set by the clean counterpart benchmark")
- The regulatory reference and section number
- A statement of achievability

### Published documents NEVER contain:
- The formula (Limit = L_down(min(P90, Anchor, 2×M)))
- P90 values, P10 values, percentile thresholds, M values
- Rounding calculations or "ladder snap" references
- "PROVISIONAL", "HELD TO CLEAN", or "DATA-GROUNDED" tags
- Any notation that would allow reverse-engineering of inputs

## 5.2 Rule 2: One Row Per Expanded Subcategory

The standards table shows one row per expanded subcategory as defined in
the Step Zero Protocol. Every contamination platform split produces its
own row with its own unambiguous integer value. Slash notation is not used.

The Expanded Subcategory List from Step 0 defines the exact rows for every
standards table and for the master summary table. Clean-variant rows are
listed first; contaminated-variant rows follow immediately after.

## 5.3 Rule 3: Master Summary Table Required

Every Standards Briefing must include a Master Summary Table: all
subcategories × all 8 metals on one page.

Format: Category | Pb | As | Hg | Cd | Cr | Ni | Sn | Al

Header text: "All values in ppb (µg/kg or µg/L) as sold (powders) or
after reconstitution per label instructions (liquids/concentrates)."

## 5.4 Rule 4: Standardized Value Increments

Published HMTc limits use only values from this primary increment ladder:

**1, 2, 3, 5, 10, 15, 20, 25, 50, 100, 200, 500, 1000, 1300, 1500, 2000,
5000, 10000**

Values are snapped to the nearest ladder value below the raw formula output.
The increment ladder ensures published values are non-forensic.

## 5.5 Rule 5: Document Structure — Standards Briefing

Page sequence:
1. Cover page (title, authors, citation, category list, branding)
2. Table of Contents
3. Statement of Purpose
4. Anti-Circumvention & Integrity (all 6 moves)
5. Product Categories (visual card layout)
6. Terms and Abbreviations
7. HMTc Approved Standards — All Metals (master summary table +
   analytical methods + speciation triggers + LOQ + lab accreditation)
8–15. Per-metal sections in order: Pb → iAs → Sn → Ni → Cd → Cr → Al → Hg
16. References (consolidated, two-column, IEEE-style)

## 5.6 Rule 6: Per-Metal Section Structure

Each metal section contains:
1. Title: "[Metal Name] ([Symbol]) Standards"
2. Scope/measurement paragraph (italicized label)
3. Standards table (5 columns: Category | HMTc Std (ppb) | EU Regulation /
   Reference | US FDA / CPSC Reference | Notes)
4. Toxicology and Margin of Safety (bold lead-in blockquote, 2–3 body
   paragraphs with no subsection headings, closing callout box, 150–270 words)
5. Products Not Likely to Meet [Symbol] Requirements (3-column table)
6. [Symbol] Remediation Strategies (3-column table)

Section names in title case: "Pb Remediation Strategies" not
"DATA-GROUNDED PLAYBOOK."

## 5.7 Rule 7: Notes Column Conventions

- Superscript citation numbers (not inline [N] brackets)
- Principle-based language, never formula trace
- Flag contamination-platform implications: "HMTc limit is set by the clean
  counterpart benchmark."
- State achievability: "Achievable with current dairy-based sourcing."
- Cite regulatory basis with section numbers
- No P90/P10/percentile values, no "PROVISIONAL" or "HELD TO CLEAN" tags

## 5.8 Rule 8: Internal vs. Published Documents

**Per-metal .docx working files** (8 per category): Internal only. Contain
formula trace, percentile values, audit trail. NEVER published.

**Consolidated Standards Briefing** (1 per category): The published document.
Contains all 8 metals, master summary table, principle-based Notes, one row
per subcategory. This is what goes to manufacturers, regulators, and public.

---

# PART 6: DOCUMENT ARCHITECTURE (for working files)

## 6.1 Per-Metal Working Document Structure

6 Heading 1s, 0 Heading 2s, 0 Heading 3s, 3 Word tables.

Sections in order:
1. Preamble (Normal paragraphs)
2. SECTION 1: SCOPE AND MEASUREMENT (H1)
3. SECTION 2: [METAL] ([SYMBOL]) STANDARDS TABLE (H1) — 5-column table
4. SECTION 3: TOXICOLOGY AND MARGIN OF SAFETY (H1) — compressed prose
5. SECTION 4: PRODUCTS NOT LIKELY TO MEET [SYMBOL] REQUIREMENTS (H1)
6. SECTION 5: REMEDIATION STRATEGIES (H1) — 3-column table
7. REFERENCES (H1)

## 6.2 Formatting Specifications

| Element | Font | Size |
|---------|------|------|
| Preamble titles | Arial | 18pt |
| Heading 1 | Arial | 16pt, Bold, #1B4F72 |
| Body text | Arial | 12pt |
| Table text | Arial | 10pt |
| References | Arial | 9pt |

Table headers: #1B4F72 dark blue, white text, bold.
Alternating data rows: #EBF5FB and #FFFFFF.
Page: US Letter (12240 × 15840 DXA), margins 1" top/bottom, 0.75" left/right.

## 6.3 Anti-Circumvention — 6 Argumentative Moves

The Anti-Circumvention & Integrity section in every Standards Briefing must
make all 6 moves:

1. **State the concentration-based unit basis** — ppb on an as-sold basis
2. **Close the serving-size loophole** — explain why serving-based limits fail
3. **Explain why this is dangerous for the target population** — infants don't
   eat labeled servings; intake is variable and weight-proportional
4. **Categorically disqualify serving-based thresholds** — structurally
   inadequate for certification, not a preference
5. **State the measurement basis** — powders as sold, liquids after
   reconstitution per label
6. **State the clean benchmark principle** — clean limits set at P90 of clean
   platform (~90% pass); contaminated limits set at P10 of contaminated
   platform (~10% pass); remaining 90% must reformulate or forgo certification

---

# PART 7: CRITICAL RULES SUMMARY

1. Never fabricate citations. If you don't have a real source, say so.
2. Never fabricate occurrence data. Use qualitative language if unverified.
3. Co-authors are Kimberly Eyer and Divine Aleru. NEVER "Victor Eyer" or "Oluwatobi Aleru."
4. Anti-Circumvention makes 6 moves. Move 6 is the clean benchmark principle with dual-percentile framing.
5. JECFA Al PTWI = 2 mg/kg bw/week. EFSA Al TWI = 1 mg/kg bw/week. Distinct.
6. EFSA MeHg TWI = 1.3 µg/kg bw/week. The 4.0 value is inorganic mercury.
7. Prop 65 Lead = MADL 0.5 µg/day (reproductive). Not NSRL 15 µg/day (cancer).
8. FDA Closer to Zero does NOT apply to infant formula.
9. ASTM F963 §4.3.5 — Ni and Sn are NOT among the 8 elements.
10. Audit before finalizing. No document ships without the 11-step audit.
11. Step 0 before Step 1. No limits without contamination platform identification.
12. Limits are set by the clean benchmark, not the contaminated platform.
13. Clean floor rule: dirty limit never falls below clean limit for same metal.
14. Regulatory Floor is the absolute ceiling. Checked LAST. Overrides everything.
15. Never expose formula math in published documents.
16. Published values use the primary increment ladder only.
17. One row per expanded subcategory in published tables.
18. Master Summary Table required in every Standards Briefing.
19. No separate contaminated limit without occurrence data (HELD TO CLEAN).
20. Direct ladder snap replaces the two-step rounding table. Single operation, always down.

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 4.0 | April 2026 | Consolidated authoritative technical specification. Reconciled Path A/B CC selection (replaces gap-proportional). Expanded subcategory notation (replaces slash notation). Updated Rule 17. |
| 4.1 | April 2026 | Fixed §1.2 tightening formula: split into three explicit variants (clean, contaminated, unsplit) with CC_candidate as an input to clean and unsplit rows. Added publication ladder verification step to §1.6. |
| 5.0 | April 2026 | **Dual-percentile model.** Complete rewrite of Part 1: replaced T, VME, CC×(1+T), and two-step rounding with P90/P10 dual-percentile formula, clean floor rule, and direct ladder snap. Added §1.9 (adjustable percentile thresholds) and §1.10 (CC threshold vs. ratchet trigger distinction). Removed §1.5 (CC × (1+T)) and §1.7 (VME). Renumbered constraints: 2×M is Constraint 1, Regulatory Floor is Constraint 2. Updated Part 4 audit step 10. Updated Part 5 Rule 1 and Rule 7 prohibited content. Updated Part 6 §6.3 Move 6 language. Updated Part 7: added Rules 13, 19, 20; removed VME rule. Added Confirmed Correction 13 (EU Ni liquid formula) and 14 (EFSA Ni TDI 2020). |
