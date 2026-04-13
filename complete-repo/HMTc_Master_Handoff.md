# HMTc Program — Master Handoff Document
## RETIRED — All items resolved as of April 3, 2026
### Original: April 2, 2026

---

## THIS DOCUMENT IS RETIRED

**Do not follow the instructions in this document.** All 5 known issues
and all Priority 1 edits described below have been completed. The
corrected protocol documents in this project are now authoritative.

**If anything in this document conflicts with a protocol document,
the protocol document is correct and this document is stale.**

This file is retained for traceability only — it documents what was
wrong and why it was fixed. It is not an instruction set.

### What was resolved (April 3, 2026):
1. ✅ All approval gates removed (12 instances across 4 files)
2. ✅ Step 0 / Step 1 boundary resolved (Step 0 sources data, Step 1 computes)
3. ✅ 2×M computation order added to Step One Protocol
4. ✅ Rounding-to-ladder clarification added to Methodology Reference §1.6
5. ✅ Pre-Build Protocol retired, content absorbed into Step Zero
6. ✅ Clean variant formula fixed (CC_candidate added to min())
7. ✅ Step Two and Step Three updated for consistency
8. ✅ Skill file updated to v4.3
9. ✅ SKILL.md rewritten to match corrected architecture

### Current authoritative files:
- HMTc_Step_Zero_Protocol_v1.2.md
- HMTc_Step_One_Protocol_v1.4.md
- HMTc_Step_Two_Protocol_v1.1.md
- HMTc_Step_Three_Protocol_v1.1.md
- HMTc_Methodology_Reference_v4.1.md
- hmtc-standards-v4_3.skill

---

## ORIGINAL DOCUMENT BELOW (for traceability only)

---

## READ THIS FIRST (RETIRED — see above)

This document was the single source of truth for any new Claude conversation
working on the HMTc program. It has been superseded by the corrected
protocol documents listed above.

The purpose of this document was to prevent new conversations from
re-discovering and re-fixing problems that have already been solved.
Every decision listed here is SETTLED. Do not revisit, re-derive, or
re-debate them. Execute from where this document says the work stands.

---

## Project Owner

K. Pendergrass (CEO, Paleo Foundation). Co-authors: K. Eyer, D. Aleru.
**NEVER "Victor Eyer" or "Oluwatobi Aleru" — those are hallucinated names.**

---

## What the HMTc Program Is

A third-party certification program setting ppb limits for 8 heavy metals
(Pb, iAs, Hg, Cd, Cr, Ni, Sn, Al) across 23 consumer product categories.
The standards are published as Standards Briefings (one .docx per category).
The pipeline runs on Inngest dev server to keep each step in a clean,
short-context call and prevent hallucination from compounding.

---

## The 5 Governing Principles (memorize these)

1. Drive down contamination (clean benchmark, not contamination benchmark)
2. Protect consumers (especially infants; regulatory floor is absolute ceiling)
3. Protect brands who enter (limits ratchet tighter, never loosen)
4. Legal defensibility (every value traceable, every process documented)
5. $2B valuation by 2030 / scalability across 23 categories without manual
   intervention at every step

**Principle 5 means: NO MANUAL APPROVAL GATES in the pipeline.** The pipeline
runs end-to-end. The human sees the finished output. The audit is programmatic,
not a human review checkpoint.

---

## SETTLED DECISIONS — Do Not Revisit

These have been debated and resolved across multiple conversations:

1. **Slash notation is retired.** Every contamination platform split gets
   its own row. No "100/125*" with footnotes. The Expanded Subcategory
   List defines the exact rows.

2. **Gap-proportional generosity is retired.** CC selection is mechanized:
   Path A (90th percentile of clean platform distribution) or Path B
   (5× LOQ). No third path. No expert judgment. No Wide/Moderate/Narrow
   gap tiers.

3. **The clean benchmark is not negotiable.** Limits are set by the
   cleanest viable platform. If contaminated-platform products can't meet
   the limit, they don't certify. Do not raise achievability concerns.
   Do not suggest loosening. See HMTc_Clean_Benchmark_Policy.md.

4. **No manual approval gates.** The pipeline runs from trigger to finished
   Standards Briefing. The 11-step audit and 9 publication gates are
   programmatic steps inside the pipeline, not human checkpoints. The
   Inngest dev server architecture requires this — approval gates block
   automated execution.

5. **Regulatory floor values and occurrence data are pipeline steps,
   not external research tasks.** Claude with web search sources these
   values during Step 0. They are not manual pre-build deliverables and
   they are not Perplexity tasks.

6. **Anti-circumvention makes 6 moves.** Move 6 is the clean benchmark
   principle. All 6 are mandatory in every Standards Briefing.

7. **The audit is 11 steps, not 9.** Steps 10 (formula compliance) and
   11 (regulatory floor compliance) were added after the v1 review found
   HMTc Cd limits exceeding FDA CTZ action levels.

8. **The Standards Briefing is the published product.** Per-metal working
   files are internal. One document per category, all 8 metals inside it.

9. **Metal order in the document:** Pb → iAs → Sn → Ni → Cd → Cr → Al → Hg

10. **EFSA Ni TDI is 13 µg/kg bw/day** (2020 update, pregnancy loss
    endpoint). Not the 2015 value of 2.8 µg/kg bw/day. The Methodology
    Reference Section 3.2 may not reflect this — the regulation text
    (EU 2024/1987) confirmed 13 µg/kg bw/day.

---

## CONFIRMED CORRECTIONS — Apply to Every Build

These are known hallucination patterns. Check for them in every audit:

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

---

## CURRENT FILE INVENTORY (what should be in the project)

### Protocol Documents (7 files)

| File | Version | Status | What It Governs |
|------|---------|--------|----------------|
| HMTc_Governing_Principles.md | 1.0 | CURRENT | The 5 principles. Read first. |
| HMTc_Pre_Build_Protocol.md | 1.0 | NEEDS UPDATE | Phase 1 deliverables. Written with manual approval gates and external research dependencies. Deliverables 1-4 should fold into Step Zero. Deliverable 6 (CC source data) should be a Step 0 sub-step using web search, not a Perplexity task. |
| HMTc_Step_Zero_Protocol.md | 1.0 | NEEDS UPDATE | Steps 0A-0F. Currently has "person reviewing must confirm" approval gates (lines 186, 282). These must be removed for Inngest compatibility. |
| HMTc_Step_One_Protocol.md | 1.1 | CHECK FOR GATES | CC selection and formula application. May contain approval gates from earlier version. |
| HMTc_Step_Two_Protocol.md | 1.0 | CURRENT | Document generation. No known issues. |
| HMTc_Step_Three_Protocol.md | 1.0 | CURRENT | Validation, audit, publication gates. No known issues. |
| HMTc_Clean_Benchmark_Policy.md | 1.0 | CURRENT | Policy rationale. Settled decisions. No changes needed. |

### Reference Documents (2 files)

| File | Version | Status |
|------|---------|--------|
| HMTc_Methodology_Reference_v4.md | 4.0 | CURRENT but may have stale content. §1.3 was reconciled (Path A/B replaces gap-proportional). §5.2 was reconciled (expanded subcategory replaces slash notation). Rule 17 updated. §1.2 Variables table updated. Parts 3-7 are the technical reference and should be authoritative for regulatory anchors, confirmed corrections, audit protocol, and formatting specs. |
| Comprehensive Testing Category Taxonomy | v2.0 | CURRENT. PDF. 23 categories. |

### Skill File (1 file)

| File | Version | Status |
|------|---------|--------|
| hmtc-standards-v4.1.skill | 4.1 | CURRENT. References all protocol documents correctly. Contains Rule 12 (mechanized CC selection) and Rule 13 (9 gates required). Still contains "Wait for approval" in Phase 2 workflow description — this needs to be removed. |

### Category-Specific Files (2 files)

| File | Status |
|------|--------|
| Category1_Pre_Build_Deliverables_1-5.md | CURRENT. Contains verified regulatory floor table for all 16 subcategories × 8 metals. Ni values verified against EU 2024/1987 regulation text. FDA CTZ values verified against Jan 2025 final guidance. 3 INFERRED mappings flagged. |
| Category1_Step_0_Output_LOCKED.md | CURRENT. 16-row expanded subcategory list. Contamination platform map with within-row splits and cross-row CC relationships. CC constraint application map. Regulatory floor table. |

---

## KNOWN ISSUES IN CURRENT FILES

### Issue 1: Approval gates still present
**Files affected:** Step Zero Protocol, Step One Protocol (possibly),
Pre-Build Protocol, skill file
**Problem:** "Wait for approval" / "person reviewing must confirm" language
blocks Inngest execution
**Fix:** Remove all approval gate language. Replace with programmatic
validation checks that pass/fail without human input.

### Issue 2: Pre-Build Protocol creates external dependencies
**Files affected:** HMTc_Pre_Build_Protocol.md
**Problem:** Deliverable 6 (CC source data) is described as a Perplexity
deep research task. Regulatory floor values are described as a manual
pre-build activity. Both should be pipeline steps using web search.
**Fix:** Fold Deliverables 1-4 into Step 0. Make Deliverable 6 a Step 0
sub-step (0F or similar) that uses web search for occurrence data, cites
sources, and defaults to Path B where data isn't found.

### Issue 3: Step Zero and Step One overlap
**Files affected:** Step Zero Protocol (0F), Step One Protocol
**Problem:** Step Zero 0F describes formula application. Step One Protocol
also describes formula application. The CC selection logic (Path A/B) lives
in Step One but is needed during Step Zero 0F.
**Fix:** Either merge Step One into Step Zero (making Step Zero the complete
planning-through-limit-table step) or clearly delineate: Step Zero produces
subcategory list + regulatory floors + CC source data, Step One consumes
those and produces the Master Limit Table. The boundary must be unambiguous.

### Issue 4: Rounding table vs publication ladder tension
**Files affected:** Methodology Reference §1.6, Step One Protocol
**Problem:** Rounding table says <10 ppb rounds to nearest 1, implying
values like 4, 6, 7, 8, 9. But the publication ladder only has 1, 2, 3, 5
in that range. Step One Protocol Step 2e handles this ("round down to
nearest ladder value") but the Methodology Reference doesn't include that
instruction. An LLM could produce non-ladder values.
**Fix:** Add Step 2e-equivalent to Methodology Reference §1.6, or rewrite
the rounding table to show only ladder-valid values per range.

### Issue 5: Column median (2×M) circular dependency
**Files affected:** Methodology Reference §1.4, Step One Protocol
**Problem:** Column median requires all values in the column to be set,
but those values are what the formula is computing. No document specifies
computation order.
**Fix:** Add instruction: "Compute initial limits using only CC×(1+T) and
regulatory floor. Calculate M from initial results. Verify 2×M compliance.
Iterate if needed."

---

## PIPELINE ARCHITECTURE (AUTHORITATIVE — overrides any conflicting step document)

This is the definitive pipeline. If a protocol document contradicts this
section, this section wins. The next task is to update those documents
to match. Until then, this is what the Inngest pipeline follows.

```
Trigger: "Build Category [N]"
    |
    +-- Step 0A: Extract base subcategories from taxonomy
    +-- Step 0B: Apply contamination platform splits (Known Platforms table)
    +-- Step 0C: Add missing product types
    +-- Step 0D: Lock Expanded Subcategory List
    +-- Step 0E: Build Regulatory Floor Table
    |            Web search each authority x metal x subcategory.
    |            Cite regulation name, section number, year.
    |            Apply Confirmed Corrections. Mark INFERRED where needed.
    +-- Step 0F: Source CC Data
    |            Web search for 90th percentile occurrence data (Path A).
    |            Where not found: CC = 5 x LOQ (Path B), tag PROVISIONAL.
    |            LOQ source: published method LOQ, or default table below.
    |
    +-- Step 1:  Apply Formula -> Master Limit Table
    |            Compute order: initial limits without 2xM, then calc M,
    |            then verify 2xM, iterate if needed.
    |            Protective rounding -> VME check -> Regulatory Floor cap.
    |            Every value must be on the publication increment ladder.
    |
    +-- Step 2:  Generate Standards Briefing from locked table
    |            No computation. Pure formatting and presentation.
    |
    +-- Step 3A: Structural validation (programmatic)
    +-- Step 3B: 11-step factual audit (programmatic)
    +-- Step 3C: Rebuild if any flags (full regeneration, not patches)
    +-- Step 3D: 9 publication gates (all must PASS, no human gate)
    +-- Step 3E: Output finished Standards Briefing + Build Summary
    |
    +-- Done. Human sees finished output.
```

### Step Ownership (no overlaps, no ambiguity)

| What gets computed | Which step owns it | No other step touches it |
|-------------------|-------------------|------------------------|
| Expanded Subcategory List | Step 0 (0A-0D) | Step 1, 2, 3 consume only |
| Regulatory Floor Table | Step 0 (0E) | Step 1 consumes only |
| CC Values | Step 0 (0F) | Step 1 consumes only |
| Master Limit Table | Step 1 | Step 2, 3 consume only |
| Standards Briefing | Step 2 | Step 3 validates only |
| Audit + Gates | Step 3 | Terminal |

### No approval gates anywhere

No step waits for human input. No step says "wait for approval,"
"person reviewing must confirm," or "must be completed and approved."
Each step runs, produces its output, and the next step consumes it.
If a step produces invalid output, the pipeline fails with a specific
error — it does not pause for human intervention.

### LOQ Default Table (for Path B last resort)

When Step 0F cannot find occurrence data (Path A) AND cannot find a
published method LOQ for the specific metal x matrix pair, use these
conservative defaults:

| Metal | Default LOQ | Path B Value (5x LOQ) |
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
consistent with Principle 1 (drive contamination down). They are tagged
PROVISIONAL and trigger mandatory review at the first revision cycle.
Step 0F should exhaust web search before falling back to these.

---

## WHAT REMAINS TO BE DONE

### Priority 1: Make the protocol documents match the pipeline above

These are the ONLY things blocking Inngest readiness. They are all
edits to existing documents — no new documents needed.

1. **Remove all approval gates** from Step Zero Protocol, Step One
   Protocol, Pre-Build Protocol, and skill file. ChatGPT found 10
   instances. Search for "wait for approval," "person reviewing must
   confirm," "must be completed and approved." Delete or replace with
   programmatic validation.

2. **Resolve Step 0 / Step 1 boundary.** The pipeline above is
   authoritative: Step 0 owns 0A-0F (everything through CC data).
   Step 1 owns formula application and Master Limit Table production.
   Update Step Zero Protocol to clearly end at 0F output. Update Step
   One Protocol to clearly begin by consuming Step 0 outputs. Remove
   any formula computation from Step Zero 0F — it sources data only.
   Remove any floor-table building from Step One — it consumes only.

3. **Add 2xM computation order to Step One Protocol.** "Compute initial
   limits without 2xM. Calculate M from initial results. Verify 2xM
   compliance. Iterate if needed." This resolves the circular dependency.

4. **Add rounding clarification to Methodology Reference Section 1.6.**
   After the rounding table, add: "After rounding, verify the result is
   on the publication increment ladder (1, 2, 3, 5, 10, 15, 20, 25, 50,
   100, 200, 500, 1000, 1300, 1500, 2000, 5000, 10000). If not, round
   down to the nearest ladder value. Then check VME."

5. **Retire or fold the Pre-Build Protocol.** Its useful content (category
   confirmation, regulatory authority identification, watch items) is now
   covered by Step 0. The CC Source Data Package is Step 0F. The approval-
   gate architecture is eliminated. Either delete the file or reduce it
   to a reference that says "see Step 0."

Once these five edits are made, the pipeline can run for any category.

### Priority 2: Run the pipeline

After Priority 1 is complete, the pipeline is structurally ready.
Running it for Category 1 (or any category) is a matter of triggering
it and letting it execute Steps 0 through 3. Step 0E sources the
regulatory floor values via web search at runtime. Step 0F sources CC
data via web search at runtime. No pre-built data tables are required —
the pipeline builds its own.

---

## WHAT NOT TO DO

- Do not re-derive the expanded subcategory list for Category 1.
  It's locked. 16 rows.
- Do not re-debate the clean benchmark principle. It's settled.
- Do not re-debate slash notation vs expanded subcategories. Settled.
- Do not re-debate gap-proportional vs Path A/B. Settled.
- Do not add approval gates. The pipeline runs end-to-end.
- Do not write a Perplexity prompt for occurrence data. The pipeline
  sources its own data via web search at runtime (Step 0E, 0F).
- Do not produce intermediate outputs for human review. Produce finished
  outputs.
- Do not spend tokens verifying exact regulatory ppb values. The pipeline
  does that at runtime via web search. Fix the LOGIC and STEPS first.
- Do not write new protocol documents. Update the existing ones to match
  the pipeline architecture in this handoff.

---

## CHATGPT AUDIT FINDINGS (April 2, 2026)

A ChatGPT deep research audit was run against the full project file set.
The findings below are CONFIRMED or UNRESOLVED. The next conversation
MUST address the unresolved items before the pipeline can produce correct
values.

### CRITICAL: Category 1 Regulatory Floor Table Has Errors

The Category1_Pre_Build_Deliverables_1-5.md regulatory floor table
(Deliverable 3) contains multiple incorrect or incomplete values.
**This table must be rebuilt from the actual consolidated text of
EU 2023/915 Annex I (current version including all amendments).**

Specific problems identified:

1. **EU Pb for infant formula powder may be 20 ppb, not 10 ppb.**
   ChatGPT claims the correct subsection is §3.1.24.1 (powder = 0.020
   mg/kg) and §3.1.24.2 (liquid = 0.010 mg/kg). I cited §3.1.7 which
   may be the wrong entry. UNRESOLVED — needs verification against
   consolidated regulation text.

2. **EU Pb for infant fruit juice exists.** ChatGPT claims §3.1.25.1
   = 0.020 mg/kg (20 ppb) for "drinks for infants and young children
   including fruit juices." I marked this cell "—" (no finalized action
   level). If ChatGPT is correct, this is a regulatory floor I missed.
   UNRESOLVED — needs verification.

3. **FDA CTZ excludes teething snacks and puffs.** CONFIRMED. The
   January 2025 final guidance explicitly states it does not cover
   "snack foods like puffs and teething biscuits." Rows 15-16 Pb floors
   cannot cite FDA CTZ. Must use EU MLs instead.

4. **EU iAs MLs exist for infant formula and baby food.** ChatGPT
   claims §3.4.2.1 (formula powder) = 20 ppb, §3.4.2.2 (formula
   liquid) = 10 ppb, §3.4.3 (baby food) = 20 ppb. I said "all others,
   no finalized action level." My section citation (§3.5.1) was in the
   wrong section (3.5 is Tin, not Arsenic). UNRESOLVED — needs
   verification, but the section numbering error is confirmed.

5. **EU Cd values are more granular than represented.** ChatGPT claims
   §3.2.17.1–3.2.17.4 distinguish powder vs liquid and soy vs non-soy,
   with different values (powder cow's milk = 10 ppb, liquid cow's milk
   = 5 ppb, powder soy = 20 ppb, liquid soy = 10 ppb). I collapsed
   all formula variants to 5 ppb. UNRESOLVED — needs verification.

**ACTION REQUIRED:** Fetch the actual consolidated EU 2023/915 Annex I
text from EUR-Lex and rebuild the entire Category 1 Pb, iAs, and Cd
floor tables from the source. Do not rely on the current Deliverable 3
or the Methodology Reference Section 3.4 — both may contain errors
propagated from the same incorrect source.

### CRITICAL: Taxonomy PDF Contains Retired "Expert-Set" Language

The Comprehensive Testing Category Taxonomy PDF contains the phrase
"expert-set protective concentrations" as an active methodological
instruction. This contradicts the Methodology Reference v4 which
explicitly prohibits this concept. The taxonomy PDF needs revision,
but since it's a PDF, it requires a new version from the program
operator.

### CRITICAL: LOQ Default Table Missing for Path B

Path B (5× LOQ) is structurally underspecified. No document contains
validated LOQ values for each metal × food matrix combination. Without
these, "5× LOQ" is a formula with no input. The Methodology Reference
or a new controlled document needs a matrix-specific LOQ table with
approved analytical methods.

### HIGH: Approval Gates Still Present

ChatGPT found 10 instances of blocking gate language across 4 files:
- HMTc_Pre_Build_Protocol.md: 3 instances
- HMTc_Step_One_Protocol.md: 1 instance
- HMTc_Step_Zero_Protocol.md: 3 instances
- hmtc-standards-v4.1.skill: 3 instances ("Wait for approval")

All must be removed for Inngest compatibility.

### HIGH: Step 0 / Step 1 Ownership Overlap

Step Zero defines 0E (regulatory floor table) and 0F (Master Limit
Table via formula). Step One also defines formula application and
floor-table building. Step Three's pipeline map treats Step 0 as
ending after subcategory expansion, with Step 1 producing the Master
Limit Table. These contradict each other.

Resolution needed: either Step 0 ends at 0D (expansion + lock) and
Step 1 does everything from floor tables through formula, OR Step 0
includes 0E and 0F and Step 1 is eliminated as a separate step.

### MEDIUM: "EXPERT-SET" Notation Remnants

The Methodology Reference still references "EXPERT-SET notation" as
something that exists in internal working files (§5.1, §5.8). This
should be replaced with the current binary: DATA-GROUNDED (Path A)
and PROVISIONAL (Path B).

### MEDIUM: "taxonomy subcategory" in Step Zero Checklist

Step Zero line 189 (approximate) says "Every base taxonomy subcategory
is accounted for." Should read "Every base subcategory" (for 0A input)
or "Every expanded subcategory" (for 0D output).

---

## VERSION HISTORY OF THIS HANDOFF

| Date | What Changed |
|------|-------------|
| April 2, 2026 | Initial handoff. Created after ~1 month of work across multiple conversations revealed that each new conversation was re-discovering solved problems due to lack of a state document. |
| April 2, 2026 (update) | Integrated ChatGPT deep research audit findings. Added CRITICAL flags for regulatory floor table errors (Pb, iAs, Cd values and section citations), missing LOQ default table, and taxonomy PDF stale language. Added HIGH flags for remaining approval gates and Step 0/Step 1 overlap. |
