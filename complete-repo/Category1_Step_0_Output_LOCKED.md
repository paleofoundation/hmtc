# Category 1: Infant and Child Foods (Ages 0–5)
## Step 0 Output — Locked
### April 2, 2026

**Built against HMTc Taxonomy v2.0, dated March 30, 2026**

**Status: LOCKED.** No downstream step may modify, add, remove, or
recompute any row in this document.

---

## Expanded Subcategory List

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
| 12 | Mixed meals, non-rice | Mixed meals | Clean benchmark |
| 13 | Mixed meals, rice-containing | Mixed meals | Contamination platform (iAs, Cd, Pb) |
| 14 | Fruit juice (not canned) | — | No split |
| 15 | Teething & snacks (non-rice) | Teething & snacks | Clean benchmark |
| 16 | Teething & snacks (rice-based) | Teething & snacks | Contamination platform (iAs, Cd, Pb) |

**Total: 16 expanded subcategories from 9 base taxonomy rows.**

---

## Contamination Platform Map

### Within-Row Splits

| Clean Row | Contaminated Row | Platform | Affected Metals | CC Direction |
|-----------|-----------------|----------|----------------|-------------|
| #1 Infant formula, powder (non-soy) | #2 Infant formula, powder (soy-based) | Soy | Al, Ni, Cd | #1 sets CC for #2 |
| #3 Infant formula, RTF liquid (non-soy) | #4 Infant formula, RTF liquid (soy-based) | Soy | Al, Ni, Cd | #3 sets CC for #4 |
| #5 Baby cereals, dry (non-rice) | #6 Baby cereals, dry (rice-based) | Rice | iAs, Cd, Pb | #5 sets CC for #6 |
| #12 Mixed meals, non-rice | #13 Mixed meals, rice-containing | Rice | iAs, Cd, Pb | #12 sets CC for #13 |
| #15 Teething & snacks (non-rice) | #16 Teething & snacks (rice-based) | Rice | iAs, Cd, Pb | #15 sets CC for #16 |

### Cross-Row CC Relationships

| Clean Row | Contaminated Row | Platform | Affected Metals | CC Direction |
|-----------|-----------------|----------|----------------|-------------|
| #8 Non-root vegetable purées | #9 Root-vegetable purées | Root vegetables | Cd, Pb | #8 sets CC for #9 on Cd, Pb |
| General non-fish baby foods | #11 Fish-containing baby foods | Predatory fish | MeHg | Lowest applicable non-fish Hg value sets CC for #11 on Hg |

### CC Constraint Application Map

This table shows which rows receive the CC × (1 + T) constraint on
which metals. "—" means no CC constraint applies (either this IS the
clean row, or no contamination platform relationship exists for that
metal).

| # | Subcategory | Pb | iAs | Cd | Hg | Cr | Ni | Sn | Al |
|---|-----------|-----|-----|-----|-----|-----|-----|-----|-----|
| 1 | Formula, powder (non-soy) | — | — | — | — | — | — | — | — |
| 2 | Formula, powder (soy) | — | — | CC from #1 | — | — | CC from #1 | — | CC from #1 |
| 3 | Formula, RTF liquid (non-soy) | — | — | — | — | — | — | — | — |
| 4 | Formula, RTF liquid (soy) | — | — | CC from #3 | — | — | CC from #3 | — | CC from #3 |
| 5 | Cereals, dry (non-rice) | — | — | — | — | — | — | — | — |
| 6 | Cereals, dry (rice) | CC from #5 | CC from #5 | CC from #5 | — | — | — | — | — |
| 7 | Fruit purées | — | — | — | — | — | — | — | — |
| 8 | Non-root veg purées | — | — | — | — | — | — | — | — |
| 9 | Root-veg purées | CC from #8 | — | CC from #8 | — | — | — | — | — |
| 10 | Meat/poultry purées | — | — | — | — | — | — | — | — |
| 11 | Fish baby foods | — | — | — | CC* | — | — | — | — |
| 12 | Mixed meals, non-rice | — | — | — | — | — | — | — | — |
| 13 | Mixed meals, rice | CC from #12 | CC from #12 | CC from #12 | — | — | — | — | — |
| 14 | Fruit juice | — | — | — | — | — | — | — | — |
| 15 | Snacks (non-rice) | — | — | — | — | — | — | — | — |
| 16 | Snacks (rice) | CC from #15 | CC from #15 | CC from #15 | — | — | — | — | — |

*CC for #11 Hg: derived from the lowest Hg limit among non-fish rows.

### Metals Unaffected by Platform Split

For within-row splits: the contaminated row receives the SAME limit
as the clean row on metals NOT listed as affected. For example, soy
formula (#2, #4) gets the same Pb, iAs, Hg, Cr, Sn limits as non-soy
formula (#1, #3). Only Al, Ni, Cd differ.

---

## Regulatory Floor Table (from Pre-Build Deliverable 3)

All values in ppb. "—" = no finalized limit exists.

| # | Subcategory | Pb | iAs | Cd | Hg | Cr | Ni | Sn | Al |
|---|-----------|-----|-----|-----|-----|-----|-----|-----|-----|
| 1 | Formula, powder (non-soy) | 10 | — | 5 | — | — | 250 | — | — |
| 2 | Formula, powder (soy) | 10 | — | 5 | — | — | 400 | — | — |
| 3 | Formula, RTF liquid (non-soy) | 10 | — | 5 | — | — | 100 | — | — |
| 4 | Formula, RTF liquid (soy) | 10 | — | 5 | — | — | 100 | — | — |
| 5 | Cereals, dry (non-rice) | 20 | — | 40 | — | — | 3,000 | — | — |
| 6 | Cereals, dry (rice) | 20 | 100 | 40 | — | — | 3,000 | — | — |
| 7 | Fruit purées | 10 | — | 10 | — | — | 500 | — | — |
| 8 | Non-root veg purées | 10 | — | 10 | — | — | 500 | — | — |
| 9 | Root-veg purées | 20 | — | 10 | — | — | 500 | — | — |
| 10 | Meat/poultry purées | 10 | — | 10 | — | — | 500 | — | — |
| 11 | Fish baby foods | 10 | — | 10 | 100 | — | 500 | — | — |
| 12 | Mixed meals, non-rice | 10 | — | 10 | — | — | 500 | — | — |
| 13 | Mixed meals, rice | 10 | — | 10 | — | — | 500 | — | — |
| 14 | Fruit juice | — | — | 10 | — | — | 250 | — | — |
| 15 | Snacks (non-rice) | 10 | — | 10 | — | — | 500 | — | — |
| 16 | Snacks (rice) | 10 | — | 10 | — | — | 500 | — | — |

INFERRED mappings: #11 Pb (fish not named in CTZ), #15–16 Pb (teething
snacks mapped as "other baby foods").

---

## Lock Confirmation

- [x] Every base taxonomy subcategory is accounted for (9/9)
- [x] Every contamination platform split is explicit as separate rows
      (5 within-row splits + 2 cross-row relationships)
- [x] Every real product type without a home has been added (2: meat
      purées, fish baby foods)
- [x] No rows added for packaging variants
- [x] Row names are unambiguous and consistently formatted
- [x] Row order: clean variant precedes contaminated variant
- [x] Cross-row CC relationships explicitly declared
- [x] Regulatory floor table complete (128 cells populated)
- [x] All INFERRED mappings flagged

**This output is consumed by Step 1 (Master Limit Table) and Step 2
(Standards Briefing). No downstream step may modify any row or value.**

---

## What Step 1 Needs to Proceed

Step 1 requires the CC Source Data Package (Pre-Build Deliverable 6)
to set CC values for each clean-platform row × metal pair. Until that
deliverable is complete, the formula cannot run and the Master Limit
Table cannot be produced.

Specifically, Step 1 needs 90th percentile values (or 5× LOQ defaults)
for these clean-platform rows:

| Clean Row | Metals Where CC Is Needed |
|-----------|--------------------------|
| #1 Formula, powder (non-soy) | Al, Ni, Cd (feeds into soy variant) |
| #3 Formula, RTF liquid (non-soy) | Al, Ni, Cd (feeds into soy variant) |
| #5 Cereals, dry (non-rice) | iAs, Cd, Pb (feeds into rice variant) |
| #8 Non-root veg purées | Cd, Pb (feeds into root-veg purées) |
| #12 Mixed meals, non-rice | iAs, Cd, Pb (feeds into rice variant) |
| #15 Snacks (non-rice) | iAs, Cd, Pb (feeds into rice variant) |
| Non-fish baby foods (general) | Hg (feeds into fish baby foods) |

All other cells (rows without a contamination platform relationship,
or metals not affected by a platform) use only Constraints 1 and 3
(column median ceiling and regulatory floor).
