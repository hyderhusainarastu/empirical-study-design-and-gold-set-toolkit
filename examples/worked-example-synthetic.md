# Worked example (fully synthetic)

> **Every name, number, quote, and data point in this file is invented for
> illustration.** "System-R" is a fictional AI reading-assistant tool used only to
> demonstrate the methodology in `SKILL.md`. Nothing here describes a real product,
> a real study, or real measured results.

## Scenario

System-R is a fictional tool that ingests a user's uploaded documents, resolves the
citations inside them against public bibliographic databases, classifies the
relationship between cited works using a ten-value category scheme, and generates a
suggested reading order across the user's library. A team wants to know two things:
(1) how well the citation-resolution and relationship-classification components
actually perform against a defensible reference standard, and (2) whether exposing a
suggested reading order changes what a novice reader actually reads first, compared to
reading in whatever order they'd have chosen unaided.

---

## Step A0 — Classify the claims

| Claim | Type |
|---|---|
| "System-R's relationship classifier agrees with independent expert coding at a defensible rate." | Suitable empirical claim |
| "The reading-order suggestion changes what novice readers open first, compared to no suggestion." | Suitable empirical claim |
| "System-R's design instantiates a 'scaffolded reading' pedagogical construct." | Interpretive claim — decomposed separately; not carried into the statistical chain below. |

Only the two empirical claims are carried through Steps A1–A4 below.

## Step A1 — Scope tier

- **Claim 1** (classifier agreement) is a **Tier 2** claim: artifact-level, no
  participants, testable against data already held plus new independent human coding.
- **Claim 2** (reading-order behavior) is a **Tier 3** claim: it requires participants
  and a behavioral outcome. It is scoped as a *later* phase, entered only after Claim 1's
  underlying mechanism has a characterized error profile — exposing readers to an
  uncharacterized classifier's downstream output would be both a validity problem and
  an ethics problem (SKILL.md §A1, Tier 3 entry condition 1).

This example works Claim 1 all the way through the statistical chain (Steps A2–A4) and
Claim 2 only far enough to show what a Tier 3 estimand looks like (Step A4 only).

## Step A2 — Design-space dimensions (Claim 1)

- **Participants:** domain experts as raters (not task participants) — five qualified
  raters recruited from outside the System-R team, none of whom contributed to its
  design or codebook.
- **Materials:** a held-out corpus of citation contexts from public-domain academic
  works the System-R team has never processed, spanning two humanities sub-domains not
  represented in any existing internal fixture.
- **Comparator:** none needed — this is a measurement of agreement, not a between-
  condition contrast.
- **Outcome:** artifact outcome — chance-corrected multi-label agreement between
  System-R's classification and independent expert coding, per category and pooled.
- **Analysis:** descriptive with uncertainty intervals, using the agreement-statistic
  selection table (references/gold-set-governance-checklist.md) for a multi-label
  construct.

## Step A3 — Benefit/claim decomposition (Claim 1)

Not applicable in the benefit sense — Claim 1 is an artifact-accuracy claim, not a
benefit claim, so no cost/harm pairing is required. The question→construct→evidence map
row is still required:

| Question | Construct | Evidence | Measure |
|---|---|---|---|
| Does System-R's relationship classifier agree with independent expert coding? | Typed relationship classification (multi-label, disagreement-preserving with a canonical sub-layer — see Construct 3 in `gold-set-construct-typing.md`) | New independent human coding over a held-out corpus | Per-label chance-corrected agreement + set-agreement measure |

## Step A4 — The statistical chain (Claim 1)

1. **Estimand.** The target quantity is the population-level chance-corrected
   agreement (Krippendorff's alpha with a set-distance function) between System-R's
   relationship classification and the classification an independent panel of
   qualified domain experts would produce, over the population of citation contexts in
   the two sampled sub-domains, under the frozen System-R configuration version
   `synthetic-v0` as of the study date. Not causal — a descriptive agreement estimand.
2. **Design.** Unit of analysis: one `(source item, target item, context)` triple.
   Five independent expert coders, blind to System-R's output, each code every item in
   the frozen held-out set (full double-plus-coding, not a 2-coder minimum, chosen
   because the disagreement-preserving band is expected to be large and more coders
   sharpen the distribution estimate). No adjudication on the disagreement-preserving
   cluster; adjudication only on the canonical sub-layer, by a sixth coder not among
   the five.
3. **Variance assumptions [SYNTHETIC].** A ten-item pilot (discarded from the frozen
   set, per G-08) produced an illustrative pre-adjudication pairwise raw agreement of
   0.61 on the canonical sub-layer and a per-label positive-rate range of 0.12–0.44
   across the ten category values — both figures invented for this example. These are
   labeled explicitly as pilot-derived, not transplanted from an unrelated population.
4. **Sensitivity strategy.** A simulation-based sensitivity analysis was run
   [SYNTHETIC]: 2,000 simulated frozen-set draws at each of several candidate sizes,
   using the pilot's per-label prevalence and disagreement-rate estimates, computing
   the width of a bootstrap confidence interval on the *rarest* category's per-label
   agreement at each candidate size (per SKILL.md §B6's rule that precision is stated
   per reported quantity, not only pooled). The simulation reported [SYNTHETIC]: at a
   held-out set of 90 items, the rarest category's 95% interval half-width was
   projected at ±0.19 — too wide to distinguish a meaningfully-differentiated from an
   undifferentiated vocabulary; at 220 items, the projected half-width narrowed to
   ±0.11, judged sufficient against a pre-declared decision threshold of ±0.12.
5. **Sample size, with its chain attached.** A frozen held-out set of 220 items is
   proposed, **reported together with**: the descriptive (non-causal) estimand above;
   the five-independent-coder, no-adjudication-on-the-contested-band design; the
   pilot-derived variance assumptions, explicitly labeled as pilot-derived; and the
   simulation-based sensitivity strategy that produced this number as the smallest size
   clearing the pre-declared ±0.12 threshold on the rarest category. [SYNTHETIC number,
   for illustration only — a real application must run its own pilot and simulation.]

## Step A4 (Claim 2, Tier 3, estimand only — illustrative)

**Estimand.** The target quantity is the average difference in "consulted the roadmap's
suggested next item first" (a binary behavioral outcome) between a suggested-order
condition and a no-suggestion condition, among novice readers (operationalized via an
independently administered domain-knowledge screener, not System-R's own self-rated
signal — see SKILL.md §A3 item 3) working with the same held-out reading materials,
within a single session, with non-completion handled by treating non-completers as a
separate reported category rather than excluding them silently. This estimand is
recorded here to show the *form* required before any Tier 3 sample size could be
discussed — no design, variance assumption, sensitivity strategy, or sample size is
supplied for Claim 2 in this example, because Tier 3 entry conditions (ethics approval,
frozen instrumentation, comparator materials) are not yet satisfied in this scenario.

---

## Step B — Gold-set construction for Claim 1's reference standard

### B1 — Construct typing

Applying Construct 3 from `gold-set-construct-typing.md` directly: the relationship
classification is typed **multi-label and disagreement-preserving, with a canonical
sub-layer**, for the reasons given there (the underlying category scheme is not
mutually exclusive in principle even though the system assigns one value; a
machine-inferred provenance value is excluded from the human coding vocabulary
entirely).

### B2 — Builder-as-annotator firewall

The System-R team drafted an earlier, small internal set of illustrative examples while
building the classifier. That set is **not** eligible for the frozen held-out set under
any circumstance (firewall requirement 1). It is retained only as a `builder_reference`
series (firewall requirement 4) and as a source of codebook boundary cases (firewall
requirement 8) — never pooled with the five independent coders' output, never counted
in any agreement statistic.

### B3 — Governance obligations, status

| Obligation | Status in this scenario |
|---|---|
| G-01 sampling frame | Written before item selection: two named sub-domains, stratified by document format, drawn from a named public-domain source collection. |
| G-02 licensing | All source material confirmed public-domain before inclusion; recorded per item. |
| G-03 codebook | Versioned `codebook-v1`, drafted by an independent domain expert (not the System-R team), with negative exemplars for each of the ten category values. |
| G-04 expert eligibility | Written criteria: a research or teaching credential in a relevant humanities field, checked per coder, recorded in the conflicts register. |
| G-06 conflicts register | Five coders, none affiliated with the System-R team; register versioned with the set. |
| G-08 pilot | Ten-item pilot, discarded from the frozen set [SYNTHETIC numbers as in Step A4]. |
| G-09 double-coding | All 220 frozen items coded by all five coders independently, no visibility into each other's codes. |
| G-10 agreement statistics | Per-label chance-corrected agreement (Krippendorff's alpha) plus a set-distance measure, reported per class with bootstrap intervals, computed pre-adjudication. |
| G-13 versioning | Release tagged `relationship-gold-v1.0.0` with a content hash. |
| G-17 release restrictions | Set marked publishable-with-labels; underlying public-domain source excerpts included; no restricted material involved. |

### B4 — Leakage check

- **Record leakage:** identity key (title/author/year + content hash) computed for
  every item in both the development pool and the frozen set; intersection confirmed
  empty.
- **Author leakage:** author sets per partition confirmed disjoint at the 220-item
  frozen-set level; two minor co-authorship overlaps found and reported as a declared
  limitation rather than excluded, per the "report the overlap explicitly" option.
- **Network leakage:** a citation graph built independently over the pooled corpus
  (not from System-R's own traversal) confirmed no direct citation edge crosses the
  partition boundary.
- **Near-duplicate leakage:** lexical shingling plus embedding similarity found one
  cross-partition pair above the pre-registered threshold — a passage anthologized in
  two different collections — moved entirely into the development pool.

### B5 — Freeze manifest

```
data:  relationship-gold-v1.0.0  (content hash: [SYNTHETIC])
model: system-r-classifier, version synthetic-v0
prompt: relationship-prompt-v3 (text hash: [SYNTHETIC])
code:  commit [SYNTHETIC]
```

Any change to any of the four fields above triggers mandatory revalidation before the
resulting agreement figures may be restated, per SKILL.md §B5.

---

## What this example demonstrates

- A claim was classified before any design choice was made (A0), and an interpretive
  claim was deliberately kept out of the statistical chain.
- A Tier 2 artifact-level claim was carried all the way through the five-step chain to
  a sample size that arrives with its full justification attached — no number appears
  without the estimand, design, variance assumptions, and sensitivity strategy beside
  it.
- A Tier 3 claim was stopped at the estimand precisely because its entry conditions
  were not yet met, rather than being pushed forward with a guessed number.
- The reference standard backing the Tier 2 claim was typed substantively (not for
  cost), built with a builder-as-annotator firewall enforced, checked on all four
  leakage axes, and frozen with a manifest — before any agreement figure was reported.

Every numeric value marked `[SYNTHETIC]` above is illustrative only. A real application
of this methodology must run its own pilot, its own simulation, and its own leakage
checks against its own data.
