---
name: empirical-study-design-and-gold-set-toolkit
description: Designs empirical evaluations end to end, from a stated estimand through a power or sensitivity analysis with validity-threat checks, and builds gold-standard reference (annotation/eval) sets with disagreement-preserving typing, annotator blinding, and leakage controls. Use whenever a project needs to plan a study, evaluation, benchmark, or reference dataset — deciding what claims are testable now versus what needs data collection, what validity threats and ethics obligations apply, how to size a sample or reference set defensibly, or how to construct a human-annotated gold set that will not be circular, leaky, artificial, or conflicted.
---

# Empirical Study Design and Gold-Set Toolkit

A methodology for two tightly coupled jobs: (1) designing an empirical evaluation — of a
system, a claim, or a hypothesis — so that its sample size or reference-set size is
*earned* rather than guessed, and (2) constructing the human-annotated reference (gold)
data that evaluation depends on, so the result it produces is not secretly measuring the
person or process that built the thing under test.

The two jobs share one discipline: **never let a number, a label, or a claim arrive
without the chain of reasoning that justifies it.** Every section below exists to make
that chain explicit and checkable.

## When to use this skill

Invoke this skill whenever an agent or team is:
- Planning a study, pilot, evaluation, or benchmark and needs to know what claims the
  design can and cannot support.
- About to propose a sample size, participant count, annotator count, or reference-set
  size, for anything from a user study to an ML eval to a qualitative interview series.
- Building or reusing a human-labeled reference set (gold set, eval set, benchmark,
  rubric-scored corpus) that a system's output will be measured against.
- Reviewing an existing study design or gold set for validity threats, leakage, circular
  reference data, or a builder-as-evaluator conflict.
- Writing the methods, evaluation, or data-management section of a proposal, paper, or
  internal eval report and needs claim-type-appropriate rigor language.

Do **not** use this skill to *run* statistical tests or *perform* annotation — it is a
planning and construction methodology, executed before data collection or coding begins.

## The two non-negotiable rules

1. **No sample size, no power number, and no reference-set size may be stated before an
   estimand, a design, variance assumptions, and a power/sensitivity strategy are
   defined, in that order.** A number that arrives without its chain is not a sample
   size — it is a budget line pretending to be one. See Part A, Step 4.
2. **Adjudicated consensus is never objective correctness, and a synthetic or
   self-authored gold-set item is never a substitute for a real one.** Where a
   reference standard is consensus-based, report agreement with a named panel's
   documented consensus under a named codebook version — never "accuracy," never
   "ground truth." See Part B, Step 1 and Step 3.

---

# Part A — Designing the empirical evaluation

## A0. First: classify every candidate claim by type

Before anything else, sort every claim the study might address into one of three types.
This sort determines which rigor apparatus applies — do it first, or every later step
will silently misapply the wrong one.

| Claim type | Gets |
|---|---|
| **Suitable empirical claim** (a measurable effect, difference, or relationship in a definable population) | A formal estimand, a design, variance assumptions, a power/sensitivity strategy, and (where appropriate) a falsifier — Part A in full. |
| **Conceptual / interpretive claim** (a design instantiates a construct, a reading is defensible, a classification scheme reveals or conceals something) | Not a falsification template. Instead: counterevidence sought and reported; **rival interpretations** stated at their strongest, never as straw positions; **limiting cases** where the reading strains; **defeaters** — what would make it untenable; **explicit revision conditions** — what would require narrowing, extending, or abandoning it. These are challenge criteria of equal seriousness to a falsifier, not a softer alternative to one. |
| **Mixed claim** | Decompose into its parts and give each part the treatment its type requires. "This design instantiates concept X" is interpretive; "this design produces effect Y" is empirical. Keep the two separated through every later document — do not let one borrow the other's vocabulary. |

**Binding rule in both directions:** no interpretive claim may be dressed in empirical
vocabulary (falsifiers, p-values, "significant") to look testable, and no empirical
claim may be relocated to the interpretive register to escape a falsifier.

## A1. Choose a scope tier

Before naming any specific design, decide which of three tiers the study belongs to.
Tiers are not ranked — a later tier is not "more rigorous," it answers a different kind
of question and carries a different cost and ethics load. State which tier(s) apply and
why; do not default to the most ambitious one available.

**Tier 1 — No human subjects (artifact-only / design-research).** Conceptual argument,
system analysis, comparative case study, or artifact-level accuracy measurement. No
participants, no reader/user effect claims. Removes recruitment, attrition, reactivity,
and most ethics burden in one move. Can claim: that an artifact instantiates or departs
from a named construct; that a design choice is formally disconnected from a claim; that
one component's behavior meets or misses a specified floor. Cannot claim: anything about
what a person does, learns, retains, transfers, checks, trusts, or misuses; anything
about effort, load, or error rate experienced by a person; any comparative "better than"
claim about a workflow or tool in the sense of a measured rate.

**Tier 2 — Minimum-viable / artifact-level validation program.** The cheapest
load-bearing claims testable against data already held or lawfully obtainable, with no
participants. The unit of measurement is an artifact — a record, a classification, a
retrieval result, an ordering, a locator. This is the tier Part B (gold-set
construction) exists to serve. Entry conditions:
1. A **frozen evaluation configuration** — every component version, model, prompt,
   retrieval/pipeline configuration, and feature-flag state recorded per run.
2. A **reference-standard type decision per construct**, made before any volume
   question (Part B, Step 1).
3. A **split discipline** — development/calibration data separated from a frozen
   held-out set, split at the correct unit, with leakage detected on every applicable
   axis (Part B, Step 4).
4. **License clearance** on any reused reference data, checked per file, per source,
   with the authority named — not inferred from a badge or a verbal assurance.
5. **Licensing/permission clearance** for any document or content set used as material.

Cost drivers here are the most predictable of the three tiers: annotator/coder time,
adjudication time, engineering time for a frozen evaluation harness, and repeated-run
compute/API cost. No participant payments, no IRB for the artifact work itself (subject
to a domain-specific determination — see A6).

**Tier 3 — Full participant program.** People, sessions, tasks, or reading/use episodes,
possibly longitudinal. Can claim: task-bounded, population-bounded statements about what
participants did under specified conditions, with uncertainty reported; expert
judgments of quality or risk, reported with their agreement structure and disagreements
preserved; qualitative accounts of reasoning, strategy, and breakdown. Cannot claim, even
at full strength: generalization beyond the tested tasks, population, and time horizon;
a learning claim without a retention or transfer measure; a causal claim from an
uncontrolled observational strand.

Entry conditions — all of them, not a subset:
1. The tier-2 program (or equivalent) completed for whatever the participant study
   depends on. Exposing people to a system whose error profile is uncharacterized is
   both a validity problem and an ethics problem.
2. Institutional ethics/IRB approval, or a stated equivalent review route (A6).
3. Research-only measurement instrumentation that does not exist yet, built to a
   data-minimization standard (A6) — not the product's own telemetry, which is typically
   too coarse and lacks condition/consent structure.
4. A frozen system configuration for the study window, with a documented policy for
   what happens if a dependency (e.g., a hosted model) changes mid-study.
5. Comparator materials actually built — a matched control condition is real
   construction work, not something that comes free (A2).
6. A recruitment and compensation position taken, including for the volunteer case (A6).
7. A benefit/claim-decomposition map completed first (A3). Running a participant study
   before "benefit" is decomposed is how a study ends up measuring perceived
   helpfulness and reporting it as effect.

**Selection criteria** (apply at execution time, unweighted — weighting is itself a
decision, not a default): target/audience fit; which tier the *central* claim actually
needs; evidence availability now; feasibility and how many entry conditions are outside
the team's control; ethics load; cost/resourcing envelope; what deliverable survives if
the work stops early at each tier; risk of overclaiming; reversibility (prefer orderings
whose early stages remain usable later — e.g., a frozen tier-2 evaluation corpus often
remains usable as tier-3 study material; a tier-3 study run on an uncharacterized system
cannot be retrofitted with the baseline it was missing).

## A2. Work the design-space dimensions

For any study touching Tier 2 or Tier 3, work through each dimension below and record
the choice and its trade-off. Full option tables are in
`references/design-space-catalog.md`; the essentials:

- **Participants/subjects.** No-subject / domain experts as raters / domain experts as
  task participants / target-population members / general recruited population / mixed
  panels. Treat prior knowledge or relevant background as a design dimension, not a
  nuisance variable — measure it independently of any self-report the system itself
  produces (a system's own self-rated signal cannot validate itself).
- **Recruitment.** Course-linked or otherwise power-relation recruitment carries
  coercion risk and needs explicit safeguards (no using grades/evaluation leverage as
  incentive). Open volunteer calls are cheap in cash and expensive in selection bias.
  Snowball sampling from the team's own network compounds a builder-as-evaluator
  conflict with an anchoring risk.
- **Inclusion/exclusion.** Must be pre-specified before data are seen. Any exclusion
  rule invented after looking at outcomes is an analysis decision wearing an
  eligibility costume — report post-hoc exclusions, with counts by condition, as
  exactly that.
- **Methods: quantitative / qualitative / mixed.** For mixed methods, name the
  integration point(s) explicitly and when each occurs relative to data collection:
  construct definition, instrument development, sampling, interpretation, divergence
  handling, reporting. "Mixed methods" without a named integration point is a label,
  not a design.
- **Controls and comparators.** The dimension where a study most easily becomes
  meaningless, because a real system usually bundles several things at once (e.g.,
  access to material, structure over it, generated content, and a display/interface
  layer). A comparator that varies all of them at once cannot attribute anything to any
  one of them. State, for every planned contrast, which components it varies and which
  it holds constant. A matched-static comparator (same access, no adaptive
  structure/generation) is usually the single most informative control and the most
  expensive to build honestly.
- **Assignment/counterbalancing.** Within-participant counterbalanced / between-
  participant randomized / matched or stratified pairs / cluster assignment /
  observational. Blinding, in descending feasibility: blind coders/raters to condition
  and provenance (usually mandatory); blind analysts to condition labels until analysis
  is locked; blind participants to condition (rarely feasible when the interface *is*
  the manipulation); blind the experimenter.
- **Materials.** Domain and text/task-type sampling must be justified before volume.
  A held-out evaluation corpus that is also the team's own working corpus is not held
  out. The strongest option is material the team has never processed, in a domain it
  has not otherwise written about, under a license that permits the use.
- **Outcomes.** Group outcomes explicitly by what they can and cannot support:
  artifact-level accuracy/coverage/stability outcomes say nothing about people;
  immediate task-performance outcomes say nothing about retention or transfer; only
  retention and transfer outcomes license the word "learning"; subjective outcomes
  (perceived helpfulness, trust, confidence) are legitimate but must never be reported
  as performance; harm/cost outcomes (time, effort, dependency, error acceptance,
  inequity, frustration) are **mandatory whenever any benefit outcome is measured**.
  Declare primary vs. secondary outcomes, multiplicity handling, and the missing-data
  plan before data collection.
- **Procedure.** Setting; session count and spacing (a single session forecloses
  retention); training/familiarization (a real confound if uneven across conditions);
  think-aloud vs. silent (yields process data, changes the process observed); delay
  interval for any retention measure; debrief content (must disclose the system's known
  error profile).
- **Analysis families.** Descriptive with uncertainty intervals plus an error taxonomy
  (the honest default for artifact validation); agreement statistics matched to data
  type; mixed-effects/multilevel models where observations nest in people, items, or
  raters; ordinal models for rating outcomes; planned contrasts declared in advance;
  simulation-based sensitivity analysis (the required instrument before any sample
  size, A4); a labeled preregistered-exploratory strand, never silently converted to
  confirmatory. Report estimates and uncertainty, not significance alone. Inspect and
  report residuals, influential cases, convergence, missingness, and attrition by
  condition.
- **Qualitative components.** Where they attach: pre-study construct elicitation,
  think-aloud, post-task interview, expert open comments alongside ratings,
  diary/longitudinal reflection, critical-incident collection, document/artifact
  interpretation with no participants at all. Full rigor obligations are in A5.

## A3. Build the benefit/claim-decomposition apparatus

Do this **before** choosing any measurement instrument. It defines no benefit as
demonstrated and fills in no threshold — filling thresholds in is a domain-argument
task at execution, not a planning task.

1. **Objective performance vs. perceived helpfulness.** Two distinct constructs a
   single study can easily conflate. They can dissociate — a condition people prefer
   and rate as more helpful can perform worse. Pre-declare which is primary if both are
   measured, and pre-commit to reporting a dissociation as a finding, not resolving it
   in the more favorable direction.
2. **Immediate success vs. retention vs. near transfer vs. far transfer.** Four
   distinct horizons, each licensing different words. Immediate task success licenses
   claims about performance under these conditions, not "learning." Retention licenses
   claims about durability over the tested interval. Near transfer licenses bounded
   generalization to a similar task/text/domain. Far transfer is the hardest to obtain
   and the most often assumed without support. **A claim at a horizon the design does
   not measure is unsupported, regardless of what the design does measure.**
3. **Novice effects vs. prior-knowledge interactions.** Expect the possibility that a
   support helpful to novices is neutral or harmful at higher expertise (expertise
   reversal). Prior knowledge must be measured independently of any self-rated signal
   the system itself produces, and any benefit claim must state the prior-knowledge
   range over which it is claimed. An average effect across a range that includes a
   reversal is a misleading summary of that range.
4. **Benefit against its costs and harms.** A benefit is not established by an outcome
   moving favorably — it is established by that movement surviving its costs: time,
   cognitive effort, dependency/offloading-without-verification, error acceptance
   (including confidently-wrong output accepted), inequity across subgroups, and any
   harm a qualitative strand surfaces unpredicted. **Every benefit outcome must have at
   least one paired cost or harm outcome**, declared at the same time and analyzed with
   the same discipline. A design that can only detect help is not a design — it is an
   advertisement.
5. **Required artifacts, produced before measurement:**
   - A question → construct → evidence → measure-or-interpretive-procedure map, one
     row per question. A question with no defensible fourth column is not yet
     answerable and must be recorded as such, not approximated with the nearest
     available instrument.
   - A theory of change: mechanism → proximal behavior → outcome, with each arrow
     treated as its own claim requiring its own warrant.
   - Predefined baseline benchmarks for every outcome, set before data collection.
   - Causal estimands where appropriate (A4), stated in words before any model is
     chosen; where a question is not causal, record that explicitly and state what
     descriptive or associational quantity replaces it.
   - A smallest meaningful benefit and a harm threshold, both argued from domain
     considerations and both recorded before data are seen. For qualitative/
     interpretive strands, the analogue is a decision rule: what pattern of evidence
     would count as sufficient, and what would count against.
   - Benefit-vs-burden criteria, explicit enough that a detectable-but-trivial effect
     purchased at real cost cannot be reported as a "real" benefit.
6. **Measurement validity, before any instrument is adopted.** For each instrument,
   record: what construct it claims to measure; evidence of its validity **for this
   population and this task type** (not the population it was validated on elsewhere);
   its licensing and permitted-use status; its accessibility; its sensitivity to the
   expected range here; and whether adopting it changes the behavior it measures
   (reactivity). An instrument well validated elsewhere and unvalidated here is an
   assumption, and must be recorded as one.
7. **Wording discipline.** Maintain a per-claim list of permitted and prohibited
   wording (e.g., a claim about a mechanism existing must not drift into language that
   implies its effect is demonstrated). This applies to prose **and** to instrument
   artifacts — event names, variable names, dashboard titles, metric labels, and
   figure captions all encode conclusions if left unguarded. A metric named
   `comprehension_improved` encodes a conclusion inside the instrument before any data
   exist.

## A4. The five-step statistical chain — binding, ordered, no step skippable

**No later step may be performed before an earlier one, and no sample size may be
stated without all four preceding steps attached.**

1. **Estimand.** State in words: target population, treatment or comparison contrast,
   outcome, timing, and how intercurrent events (dropout, non-compliance, condition-
   switching) are handled. If the question is not causal, say so and state what
   descriptive or associational quantity replaces it. If a question is interpretive,
   this chain does not apply to it at all — A0 governs instead, and forcing an
   interpretive question into an estimand is itself an error.
2. **Design.** Unit of analysis; assignment or counterbalancing; nesting structure;
   blinding; materials and their allocation; measurement schedule; exclusion rules —
   all decided before any number is attached.
3. **Variance assumptions.** State where they come from: pilot data, a comparable
   published design, or an explicitly labeled assumption. **Assumptions transplanted
   from a different population, task, or outcome are assumptions, not estimates, and
   must be labeled as assumptions.**
4. **Power or sensitivity strategy.** Preferably simulation-based, using the planned
   analysis model, pilot-estimated variance, and anticipated attrition. A sensitivity
   framing ("what could this design detect?") is often more honest than a power framing
   ("how many do we need for an effect we have guessed?") because it does not require
   an effect-size guess as input.
5. **Only then, a sample size (or reference-set size) — reported with the four
   preceding steps, never alone.** A number without its chain is a budget line.

**Corollaries:**
- No sample size may be inherited from a prior plan, a comparable published study, or
  convention.
- No smallest-meaningful-effect threshold may be set to fit an affordable sample. The
  threshold is argued from domain meaning; the sample follows it, not the reverse.
- A design that cannot reach a meaningful threshold within its resources should say so
  and be re-scoped — a legitimate planning result, not a failure.
- Underpowered work run anyway for pilot/feasibility reasons is reported as pilot or
  feasibility evidence — instrument reliability, task calibration, procedure
  viability — and **never as an effect estimate**.
- This chain applies equally to reference-set sizing (Part B, Step 5): derive the
  needed size from precision, heterogeneity, intended inference, and budget. "We need a
  large gold set" is not a sample-size calculation.

## A5. Qualitative and interpretive rigor

For any qualitative or interpretive component, produce all five of the following.

1. **Sampling rationale**, named specifically: maximum variation, criterion, extreme/
   deviant case, confirming-and-disconfirming case, theoretical sampling with a stated
   stopping rule, or nested sampling drawn from a quantitative strand on a stated rule.
   Report what was actually achieved against what was planned, including shortfalls.
2. **Coding/interpretive protocol.** For codebook-based work: how the codebook was
   developed and from what data; pilot and revision before full coding; how many
   coders and on what proportion of the data; how disagreements are surfaced and
   *recorded*, not merely resolved; whether coders were blind to condition and
   provenance. "Thematic analysis" as an unspecified label is not a protocol — name
   the specific family and perform what it requires. For interpretive/hermeneutic
   work: the reading protocol; what counts as evidence for a reading; how rival
   readings are generated, not merely acknowledged; how the account handles passages
   that resist it.
3. **Any LLM or automated assistance in coding.** Record that it happened, the model,
   version, and prompt; independently verify every assisted label by a human who did
   not see the assistance before it enters a frozen set. An assisted label that is only
   reviewed — approved as presented — is not an independent code and cannot enter an
   agreement statistic (see Part B, Step 3).
4. **Reflexivity and positionality, stated plainly in the methods, not tucked into a
   limitations paragraph.** If the team building the system is also the team studying
   it, that is a structural feature of the research, and it is not solvable by
   disclosure — disclosure is what honesty requires *because* the threat cannot be
   fully removed. State: who directs the system's design and the study; who authored
   the argument being tested; who ratified any existing reference data; whether any
   contributor holds a commercial interest; and what was done to keep that investment
   out of the data path (independent coders, blind analysts, preregistered analysis,
   independent replication) — plus an honest statement of what could not be separated.
5. **Disagreement, negative cases, and the audit trail.** Report pre-adjudication
   agreement separately from post-adjudication outcomes. Retain substantive
   alternatives with their rationales where expert plurality is real; prefer a
   disagreement-preserving standard over an adjudicated single label when a construct
   is genuinely contested, and say which was chosen and why. Actively seek and report
   cases that do not fit the developing account — an analysis with no negative cases
   reported has usually not looked. Keep dated records of coding decisions and
   revisions, analytic memos, codebook version history, sampling decisions and their
   timing, every deviation from plan with its reason, and the provenance of every
   quoted extract.

## A6. Ethics and responsible-research checklist

Applies to any Tier 3 (participant) work, and partly to Tier 2 where reused data
involves people, licensed material, or third-party content.

- **Participant protections.** Voluntary participation with a genuine right to
  withdraw; no penalty for withdrawal; no coercive recruitment; special care where a
  power relation exists (students, supervisees, colleagues). Never use evaluative
  leverage (grades, performance review, access) as an incentive or condition.
  **Debrief must include the system's known error profile** — a participant should
  leave knowing the output can be wrong and how, established by a fresh check at study
  time, not from a stale audit.
- **Consent.** Must distinguish ordinary product/service data from optional research
  data; describe any third-party processing (e.g., a model provider) in terms a
  participant can act on; explain the right to withdraw and its technical limits (what
  cannot be retrospectively removed from aggregate analysis, and why); state retention
  periods and access controls; be readable and accessible. Where participants upload
  their own material, consent must cover what happens to it and to anything derived
  from it.
- **Data minimization and privacy.** Any research event stream should carry the
  minimum necessary: a pseudonym, session/condition identifiers, a timestamp, an
  event type, and a minimized payload. Never store raw uploaded content, prompts,
  credentials, or unrestricted notes in an event stream — content-bearing data belongs
  in a consented research instrument with a documented access policy. Identifier keys
  stored separately from study data; encryption in transit and at rest; role-limited
  access; a retention schedule set **before** collection; direct identifiers deleted on
  schedule. Verify any consent statement about deletion/export against the actual
  system behavior at study time, not against stale documentation.
- **Corpus, copyright, and material licensing.** Study materials must be public-
  domain, licensed, permission-cleared, or institutionally authorized. Public release
  of any study output must contain only analysis code, schema, lawfully shareable
  material, and synthetic or redacted traces — never private uploads, participant
  identifiers, or copyrighted full texts without clearance.
- **Compensation ethics.** Expert judgment and annotation are skilled labor; requesting
  it unpaid selects for those who can afford to give it, which is both an equity and a
  sampling problem. Unpaid participation shifts cost onto participants and skews the
  sample toward the enthusiastic. Compensation that is too high is its own coercion
  risk, particularly for students and precarious workers. Non-cash compensation
  (access, acknowledgment, co-authorship) carries its own conflicts and must be offered
  on terms that create no obligation. Whatever is chosen must appear in consent
  materials before participation.
- **Accessibility.** A design requirement of the study, not a compliance appendix.
  Study materials, instruments, and any interface used must be usable with assistive
  technology, or the study must state who it excludes and why. A manual accessibility
  check (not automated scanning alone) is an entry condition for any participant-facing
  study.
- **Ethics/IRB review.** Required before recruitment. Where no institutional home
  exists, this is a **blocking dependency**: confirm institutional affiliation and the
  applicable ethics route before entering Tier 3 at all. An independent ethics review
  service may be an alternative; whether it is accepted is specific to the target venue
  or funder and must be checked, not assumed.
- **Research misuse and dual use.** Name what could go wrong if the capability under
  study is misused (e.g., lending unearned authority to weak sources, automating the
  appearance of rigor without its substance, inferring sensitive attributes about a
  person). State what the design does about each, and where it does nothing, say so.
- **Conflicts of interest.** Disclose: authorship/ownership of the system under study;
  any commercial interest in the system or a successor product; authorship of any
  reused reference data and its license status; any relationship to individuals
  recruited as experts.
- **Preregistration and reporting-standard decision.** A decision point, not a default.
  Preregistration suits a confirmatory quantitative strand with pre-specified outcomes
  and analyses; it is a poor fit for exploratory qualitative work and a category error
  for interpretive claims. Verify the current reporting standard and registry policy
  from primary sources at the time of the decision, and record who decided and when.

---

# Part B — Building the gold-standard reference set

Everything in Part B assumes Tier 2 or Tier 3 measurement against a human-produced
reference standard: a labeled dataset, an eval set, a benchmark, a rubric-scored
corpus. Full detail and worked examples are in
`references/gold-set-construct-typing.md` and
`references/gold-set-governance-checklist.md`.

## B1. Type each construct before sizing it

**The governing question for every construct: is plurality among qualified experts a
property of the object, or a property of the coder?**

- If two qualified, fully-informed experts applying the same codebook still legitimately
  differ, and the difference is *about the material*, plurality is **substantive** and
  the standard must retain it. Collapsing it produces a number that measures panel
  composition, not the system.
- If the difference traces to fatigue, misreading, codebook ambiguity, or unequal
  access, plurality is **nuisance**, and adjudication is the right instrument.

Six permitted types:

| Type | Use when | What the record stores |
|---|---|---|
| **Canonical** | A single externally checkable fact exists independent of the panel. | One value, plus the external authority consulted and the date. |
| **Consensus-based** | No external authority exists, but plurality is nuisance and a documented adjudication procedure can settle it. | The adjudicated value, plus every pre-adjudication independent code, plus the adjudication rationale. |
| **Multi-label** | The object legitimately instantiates more than one category at once; forcing one is an instrument artifact. | A set of labels per item, each with its own coder support. |
| **Probabilistic / graded** | The construct is a degree, not a kind. | A graded value per coder plus the distribution — never a thresholded binary alone. |
| **Ranked / partial-order** | The judgment unit is an ordering over a set, not a label on one item. | A per-expert ordering, with ties and declared incomparabilities as first-class data. |
| **Explicitly disagreement-preserving** | Plurality is substantive: the disagreement *is* the content. | Every expert position, its warrant, and an explicit statement that no single value is designated correct. |

**A construct may — and often should — be typed differently at different
granularities.** A single type applied across a whole construct is usually a sign the
construct has not been decomposed far enough. E.g., "was this reference cited at all"
can be canonical while "what kind of relation is this citation" is disagreement-
preserving, inside the same overall construct.

**Anti-rule:** never choose a type because it is cheaper to score. Canonical is the
cheapest and the most frequently wrong choice. The justification for a type must be
substantive; anyone who wants to change a construct's type later must argue against
the substantive justification, not against the cost.

See `references/gold-set-construct-typing.md` for eight fully worked illustrative
constructs (record resolution, locator/attribution correctness, categorical
classification, ranking/ordering, retrieval-answer grounding, single-label
classification, contested-mechanism labeling, and structural-completeness), each
showing the unit of analysis, the type decision and its justification, and a disagreement
policy — as a template to adapt, not to copy verbatim.

## B2. The builder/creator-as-annotator firewall

State this plainly whenever anyone who designed, built, or tuned the system also
touches its reference data — this is the single most common source of a circular
"validation."

**Why it's a real threat.** A reference standard produced by the system's own builder
has three specific failure modes: (i) *label-to-instrument fitting* — categories are
drawn where the system already draws them, so the standard cannot detect a wrong
taxonomy; (ii) *example selection toward the recoverable* — synthetic examples written
to illustrate a label are guaranteed to carry it; (iii) *review-not-coding* — approving
a label as presented is a materially easier and differently biased act than producing
it independently, and yields no agreement statistic at all. None of this makes internal
quality assurance bad practice — it just means internal QA is not an independent
reference standard, and the two must never be presented as the same artifact.

**Eight binding requirements:**
1. No person who designed, built, tuned, or selected configuration for a system may
   produce, adjudicate, or audit a label in that system's **frozen held-out** set. This
   is absolute for the frozen partition; relaxable, with a recorded rationale, only in
   the development pool.
2. Role separation is enforced **per item**, not per person globally: a coder never
   adjudicates an item they coded; an auditor never audits a set they coded or
   adjudicated; the person who selects items does not code them.
3. A conflicts register records, per annotator: relationship to the project, to the
   system, to the authors, to the items being coded, and to any commercial interest.
   Version it with the set and release it with it.
4. A builder's own labels, where they exist, are a **distinct, labeled record type**
   (e.g., `builder_reference`) — never pooled with independent codes, never counted in
   an agreement statistic, never adjudicated against. They may be reported *alongside*
   independent codes as a separate series, which is itself informative.
5. Item selection is firewalled from labeling: where the builder must define the
   sampling frame (often true, since only they may know the source corpus), the frame
   is written and fixed before any item is drawn, and drawing is mechanical.
6. Codebook authorship is disclosed and, where feasible, split — a codebook written
   solely by the builder encodes the instrument's own distinctions. At minimum, an
   independent domain expert revises it before calibration, and the revision diff is
   retained.
7. Any statistic computed on a set touched by an unmanaged conflict is reported **with
   the conflict stated in the same sentence** — not in a footnote, not only in a
   limitations section.
8. An existing builder-authored set may be reused, but only under a declared status:
   permitted as a development-pool resource, a codebook draft, a source of edge cases,
   or a `builder_reference` series; **not permitted** as a frozen held-out set, as a
   source of any agreement figure, or as evidence that a taxonomy is codeable by
   independent experts.

## B3. Governance obligations before any set is marked complete

Full table with acceptance criteria is in
`references/gold-set-governance-checklist.md`. Summary of the seventeen obligations:
domain sampling frame (written before selection); licensing basis per item (named
authority, not inference); a versioned codebook with positive **and** negative
exemplars and an explicit "how to code when uncertain" rule; expert eligibility stated
as demonstrable evidence (never inferred from a byline or authorship credit); panel
composition justified against the construct's type; an independence/conflicts register
(B2); training and calibration with a documented threshold, re-run on every codebook
version bump; a pilot on development data whose purpose is codebook revision and
disagreement-rate estimation, not data production; double-coding of every item in the
frozen set by annotators who cannot see each other's codes; agreement statistics
matched to data type and reported pre-adjudication (see the statistic-selection table
below); a documented adjudication procedure naming who adjudicates, on what evidence,
and which disagreements are **not** eligible for adjudication; deliberate inclusion of
negative and edge cases, preferably drawn from actually-observed failures rather than
invented; semantic versioning with an immutable content hash per release; a scheduled
quality re-audit by someone not involved in production, reporting a drift rate; a
storage plan controlling read access and separating labels from restrictively-licensed
source material; a stated refresh trigger and what a refresh does to prior results'
comparability; and per-set release restrictions (publishable / embargoed / metadata-
only / withheld) reconciled against the applicable data-stewardship standard.

**Agreement-statistic selection (never a matter of habit):**

| Data shape | Required statistic class | Explicitly wrong |
|---|---|---|
| Nominal, exactly 2 coders, complete | Cohen's kappa | Raw percent agreement alone |
| Nominal, >2 coders and/or missing data | Krippendorff's alpha; Fleiss' kappa if raters are fixed and complete | Cohen's kappa (undefined for >2 coders) |
| Ordinal/graded (relevance, confidence) | Weighted kappa, or Krippendorff's alpha with an ordinal difference function | Nominal kappa — treats a large disagreement as equal to a small one |
| Multi-label sets | Per-label chance-corrected agreement **plus** a set-distance measure | Pooled single-label accuracy; per-label agreement with no set measure |
| Rankings/partial orders | Kendall's tau-b (ties-aware) per pair; Kendall's W for panel concordance; a partial-order-aware distance | Spearman rho on a forced total order; treating pairwise precedences as independent items |
| Spans/offsets | Exact-match agreement **and** overlap-tolerant agreement at a pre-registered tolerance, reported together | Either alone |

Always additionally report: observed and expected agreement plus marginal
distributions alongside any chance-corrected coefficient (kappa is unstable under
skewed marginals); **per-class** agreement, never pooled alone (pooled figures are
dominated by easy classes); an uncertainty interval on every agreement coefficient by
an appropriate resampling procedure (a point estimate on a thin cell is exactly the
failure this whole rule prevents).

**Every agreement statistic computed is on pre-adjudication independent codes.**
Post-adjudication agreement is definitionally inflated and may not be reported as
reliability.

**Development/calibration pool vs. frozen held-out set.** Every reference set splits
into a development pool (codebook revision, training, piloting, threshold setting,
error analysis) and a frozen held-out set (used exactly once per declared system
version, for the declared inference, never for iteration). **The split unit is not the
item** — it is the smallest unit that can carry information between partitions (e.g.,
the source document, not each extracted sentence from it; the whole ordering set, not
each pairwise precedence within it; the claim pair and both underlying source items
together, not each claim alone). A split function that hashes only the item's own
identifier is item-level and leakage-blind by construction; wrap it to hash the
split-unit's key instead.

## B4. Leakage — four axes, each with a detection procedure

A leakage requirement without a detection procedure is unenforceable. Run all four
before freezing any set; store the results with the release; treat any leak discovered
after freeze as invalidating the affected results — never as license for a quiet
re-partition.

1. **Record/document leakage.** *Risk:* the same source document (or a re-processed
   copy of it) appears in both partitions under different item IDs. *Procedure:*
   compute an identity key per item in both partitions (external ID where one exists,
   else normalized metadata plus a content hash) and assert the intersection is empty,
   as an automated check that fails the release, not a manual review. Pair identity-key
   matching with a raw content hash — any identity-normalization function that under-
   merges (e.g., mishandles edge-case names) will under-report leakage if relied on
   alone.
2. **Author/entity leakage.** *Risk:* the same author, creator, or entity appears on
   both sides, so the system learns an idiom, position, or habit from the development
   pool rather than generalizing. *Procedure:* normalize entity identifiers, build the
   entity set per partition including **all** contributors, not just the primary one,
   and assert disjointness — or, where full disjointness is infeasible for a small
   domain, report the overlap explicitly as a share of the frozen set and treat every
   overlapping item as a declared limitation. Extend to co-authorship/co-creation:
   collaborators are a partial leak for stylistic or positional constructs.
3. **Network/relational leakage.** *Risk:* a development item and a frozen item are
   adjacent in a relevant graph (citation, reference, social, dependency), so a
   relationship or ordering judgment is partly inferable from the other partition.
   *Procedure:* build the relevant graph over the pooled corpus **independently of the
   system under test**, assert no direct edge crosses the partition boundary, and
   report the distribution of shortest-path distances between partitions against a
   pre-registered minimum. Never build this graph from the system's own traversal
   logic — a system that only realizes part of the true graph (e.g., bounded to a
   user's own library, or capped at some recursion depth) will make a leakage check
   built on it under-detect adjacency by construction.
4. **Near-duplicate leakage.** *Risk:* items that are not identical but substantively
   the same content — a preprint and its published version, a reprint, a translation,
   an anthologized excerpt, a self-reused passage. *Procedure, two-stage:* (i) lexical —
   shingle or MinHash over normalized text at the split-unit level, with a
   pre-registered similarity threshold and manual review of the band just below it; (ii)
   semantic — embedding similarity across partitions, surfacing top-similarity
   cross-partition pairs for human review. A domain-specific class often missed by
   generic text-similarity tools: the same underlying work in a different edition,
   translation, or format — different tokens, same content, and possibly a legitimately
   distinct item for one sub-construct while a duplicate for another. Detect this class
   by entity/work identity, not by text similarity alone, and record its handling per
   construct.

## B5. Blinding, LLM/automated assistance, and the freeze discipline

**Annotator blinding.** Blind annotators to: (a) system outputs for the items they
code; (b) any other annotator's codes for those items; (c) experimental condition,
where one exists; (d) where feasible, the study hypothesis. Where a product's own
interface is designed to *show* exactly the provenance/condition information a coding
task needs to hide (e.g., a UI that deliberately surfaces which content was
AI-generated), that is a genuine design tension, not a bug in either — it is why a
blinded coding surface is usually a separate build, not the product surface with a flag
flipped. Where blinding is infeasible, declare it, argue its likely direction of bias,
and pre-specify a sensitivity analysis. Blinding is never quietly dropped.

**Any LLM or automated assistance in labeling.** Record per item: the model, version,
prompt version, date, and the exact role it played (suggesting, pre-filling, ordering,
filtering). Independently verify every assisted label by a human who did not see the
assistance, before it enters any frozen set. A label that is only reviewed — approved as
presented — is `assisted-reviewed`, is not an independent code, and cannot contribute to
an agreement statistic.

**Freeze and mandatory post-change revalidation.** Before any result is reported, four
things are frozen together and recorded as a single immutable manifest: **data** (set
version + content hash), **model** (provider + exact model ID), **prompt** (prompt
version + text hash), and **code** (commit). Any change to any one of the four mandates
revalidation before the prior result may be restated. Pre-declare every acceptance
floor, equivalence bound, and meaningful-difference threshold **before** the frozen set
is scored — never after.

## B6. The size-derivation rule — no numbers without derivation

For each construct, derive the required size in this order and write the derivation
down:

1. **Precision.** What is the smallest difference that would change a decision, and
   what interval half-width around the estimate would make that difference
   distinguishable? State precision per reported quantity (per-class agreement, not
   just pooled) — the binding requirement is almost always the *rarest* class.
2. **Heterogeneity.** What are the strata (domain, format, category, source
   background), what is the expected class prevalence in each, and what disagreement
   rate does a pilot predict? Heterogeneity multiplies: several strata plus a skewed
   rarest class need materially more than the pooled precision requirement implies.
3. **Intended inference.** Descriptive characterization, comparison against a
   comparator, a per-class floor, an equivalence claim, and a promotion/release gate
   each impose different requirements, in roughly ascending order. Fix the inference
   *before* the size — never choose it afterward to fit what was collected.
4. **Budget and effort ceiling.** The feasible size given the effort categories below
   and the resource envelope.

**Reconciliation rule, and it is one-directional.** If the budget-feasible size is
smaller than the precision-required size, **narrow the inference, descope the
construct, or don't run it.** Never hold the size constant while quietly widening the
claim to fit it. A study reporting a comparative or gate-passing inference on a set
sized only for description is misreported regardless of how the number was reached.

**Two guards against false anchors.** Existing coverage-floor constants (e.g., "at
least N examples per category so no class is empty") are not sample-size derivations —
they guard against zero coverage, not against imprecision, and must not be adopted as
targets. A recorded review-time estimate for single-reviewer approval of pre-existing
labels is not an independent-coding estimate and must not be imported as one — it
reflects review, not production, of labels.

**Effort categories to price later (categories and drivers, not numbers):** expert
annotation (drivers: items per session by construct — an ordering task is priced per
ordering, not per item; required source-consultation depth; codebook complexity; domain
specialization needs; the double-coding multiplier; re-coding on codebook version
bumps); coordination (recruitment, scheduling, packet assembly, codebook maintenance,
QA sampling, release/versioning, conflicts-register upkeep — scales with panel size and
construct count, not item count); adjudication (disagreement rate × adjudicable items ×
panel size; non-linear, since an adjudication revealing a codebook ambiguity triggers a
revision that retro-applies to already-coded items); training/calibration (per
annotator, repeated per codebook version, scales with turnover); audit and refresh
(scheduled re-audit sampling plus refresh-triggered re-annotation; a breaking refresh
that changes split assignment costs re-annotation *and* invalidates prior comparisons);
research-engineering support (interface build/maintenance, packet generation, leakage
checks, agreement-statistics tooling, export — belongs to development cost, must not be
double-counted into the annotation line).

---

# Execution checklist

Use this as a final pass before calling a design or a gold set complete.

**Study design:**
- [ ] Every candidate claim classified by type (A0); interpretive claims never dressed
      in empirical vocabulary or vice versa.
- [ ] Scope tier(s) stated and justified against the selection criteria (A1), not
      defaulted to the most ambitious tier available.
- [ ] Every applicable design-space dimension worked and recorded, not left implicit
      (A2).
- [ ] Benefit/harm decomposition artifacts produced before any instrument choice (A3).
- [ ] Estimand → design → variance → power/sensitivity → sample size, in that order,
      with every step attached to the number when it is reported (A4).
- [ ] Qualitative rigor obligations satisfied where a qualitative component exists (A5).
- [ ] Ethics checklist worked, with the IRB/ethics-route dependency resolved before any
      recruitment (A6).

**Gold-set construction:**
- [ ] Every construct typed against the plurality question, and typed at each
      granularity where a single type would misrepresent it (B1).
- [ ] A builder/creator-as-annotator conflict, if one exists, named plainly and
      firewalled per the eight requirements (B2) — not managed away, disclosed.
- [ ] All seventeen governance obligations satisfied or explicitly, reviewedly waived
      (B3) — including a matched agreement statistic and a pre-adjudication /
      post-adjudication distinction.
- [ ] The split unit identified per construct (not defaulted to "the item") and the
      split mechanism grouped accordingly (B3).
- [ ] All four leakage axes checked with an automated procedure before freeze (B4).
- [ ] Blinding declared and enforced, or its infeasibility declared with a bias
      direction and sensitivity plan; any LLM/automated assistance disclosed and
      independently verified before entering a frozen set (B5).
- [ ] Freeze manifest (data + model + prompt + code) recorded before any result is
      reported; revalidation triggered on any change (B5).
- [ ] Reference-set size derived from precision → heterogeneity → inference → budget,
      in that order, with the reconciliation rule applied if budget falls short (B6).

## References bundled with this skill

- `references/design-space-catalog.md` — full option tables for every design-space
  dimension in A2, with trade-offs.
- `references/validity-threat-catalog.md` — a generalized catalog of recurring
  validity threats, each with a detection obligation, a mitigation obligation, and its
  typical residual (what cannot be fully removed).
- `references/gold-set-construct-typing.md` — eight fully worked illustrative
  construct-typing examples covering all six reference-standard types.
- `references/gold-set-governance-checklist.md` — the full seventeen-obligation table
  with acceptance criteria, expanded from the B3 summary.
- `examples/worked-example-synthetic.md` — a complete synthetic walkthrough (estimand
  through sensitivity analysis, plus one gold-set construct fully typed and sized) using
  invented data, clearly labeled synthetic throughout.
