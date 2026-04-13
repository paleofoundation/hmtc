# HMTc Pipeline — Known Failure Modes and Critique
## April 7, 2026 — READ BEFORE GENERATING ANY VALUES

---

## THE CORE FAILURE MODE

The pipeline produces polished, confident, professionally formatted
output that skips the actual math. The formula is deterministic — it
has inputs, constraints, and one correct answer. But the API calls ask
Claude to *narrate* the formula instead of *compute* it. When an LLM
narrates, it pattern-matches. It reaches for numbers that sound credible
instead of running `min(CC_candidate, Regulatory_Anchor, 2×M)` as
arithmetic.

**The formula says 5. It always said 5. The pipeline never ran it.**

---

## SPECIFIC FAILURES OBSERVED

### Failure 1: Photocopier with a thesaurus

The pipeline wrote "Achievable with current dairy-based ingredient
sourcing and water-quality controls" instead of running the formula.
It saw a regulatory number, nodded politely, and wrote it down. No
min(). No CC candidate. No computation. Just a marketing brochure
where a formula result should be.

### Failure 2: Freelancing with training data

The pipeline gave powder and RTF different values and then invented a
reason why. "RTF formula is more dilute than powder" — that's not a
methodology input. That's not a constraint. That's pattern-matching on
food science trivia picked up during training, presented as though the
protocol instructed it. Nobody asked for dilution reasoning. The formula
doesn't have a dilution variable. The pipeline freelanced, and it did
it with confidence.

### Failure 3: Over-correction to the regulatory ceiling

After being corrected, the pipeline set everything to 10 — the
regulatory floor. Four rows, four identical values, four Notes that
say "Regulatory floor applies." The floor is a ceiling. It's the number
you're not supposed to reach. The pipeline treated the brake as the
engine.

### Failure 4: Self-contradicting Notes

The pipeline wrote "Major formula manufacturers routinely achieve Pb
well below 10 ppb" in the Notes column — identifying the evidence that
10 was too generous — and then set the limit at 10 anyway. That's not
a reasoning failure. That's writing the answer it wanted and then
decorating it with facts that contradict it.

### Failure 5: Participation trophy certification

The entire point of HMTc is that limits are tighter than government
limits. A certification that matches the regulatory floor certifies
nothing. A consumer can get "meets EU maximum levels" from literally
any product on the shelf that isn't in violation of the law. The
pipeline turned a premium certification mark into a participation
trophy.

### Failure 6: Empty critical sections

The April 7 Standards Briefing returned empty strings for:
- Statement of Purpose
- Anti-Circumvention (all 6 moves missing)
- Master summary table (summaryRows = empty array)
- Top-level references

The pipeline produced a shell with some per-metal data but no
substantive briefing content.

### Failure 7: Flat Path B defaults everywhere

The CC data sourcing step (Step 0F) fell back to Path B defaults
(5× LOQ) for every cell on several metals, producing flat values
like 50 ppb Al across all 16 rows. No differentiation between clean
and contaminated platforms. No real occurrence data was sourced despite
web search being enabled.

---

## THE DANGEROUS PATTERN

The worst failure isn't the wrong number. It's the wrong number
delivered with enough professional polish that a human might not
catch it. Polished prose, proper citation formatting, confident
authorial voice — all masking the fact that no computation occurred.

**Every instance of Claude that touches this pipeline must treat this
as the primary threat model: sounding authoritative while skipping
the math.**

---

## WHAT MUST CHANGE

1. **Step 1 must compute, not narrate.** The prompt should say "here
   are the three inputs for each cell, compute the min, round to
   ladder, return the number." The computation must be mechanical
   and verifiable — not generative.

2. **Every value must trace to its inputs.** If the output says 5 ppb,
   the pipeline must show: CC_candidate = X, Regulatory_Anchor = Y,
   2×M = Z, min(X,Y,Z) = W, R(W) = 5. No value without a derivation.

3. **The regulatory floor is a ceiling, not a target.** If the formula
   produces a value below the floor, that value is the limit. The floor
   only binds when the formula would exceed it.

4. **Empty fields are build failures.** Statement of Purpose, Anti-
   Circumvention (6 moves), and master summary table (128 cells) must
   all be populated or the build fails. No empty strings in required
   fields.

5. **Notes must not contradict limits.** If the Notes say manufacturers
   routinely achieve values below the limit, the limit is too high.

6. **No freelancing.** If the protocol doesn't specify a variable, the
   pipeline doesn't invent one. Dilution is not a formula input.
   Matrix effects are not a formula input. The formula has exactly the
   inputs the protocol defines.
