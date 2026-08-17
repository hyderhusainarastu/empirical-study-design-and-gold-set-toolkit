# Design-space catalog

Full option tables for the design-space dimensions summarized in SKILL.md §A2. A study
design must cover, and record a choice for, each applicable dimension: participants,
recruitment, inclusion/exclusion, methods, controls/comparators, assignment or
counterbalancing, materials, outcomes, procedure, analysis, and qualitative components.
A cell that reads well below is not thereby selected — every dimension interacts with
several others (assignment constrains analysis, materials constrain generalization,
comparator choice constrains what any outcome can mean), and the interactions are noted
where they bite.

## 1. Participants / subjects

| Option | What it buys | What it costs / limits |
|---|---|---|
| **No human subjects** (artifact-only) | Removes ethics, recruitment, attrition, and reactivity in one move; makes a frozen-configuration discipline the only hard requirement | Cannot address any human-facing question at all |
| **Domain experts as raters/judges** | Reaches interpretive quality and risk judgments no artifact metric reaches | Small populations; anchoring and conformity risk; honoraria; expert consensus is not truth |
| **Domain experts as task participants** | Tests the system where interpretive judgment actually lives | Expertise-reversal risk: supports that help novices may not help, or may hinder, experienced users |
| **The population the construct most plausibly names** (e.g., early-career practitioners for a "novice" construct) | Best construct-population match | Power-relation risk if recruited from the team's own institution or supervision line |
| **A more easily recruited adjacent population** (e.g., students where the target is working professionals) | Recruitable at scale and speed | Furthest from the actual use case; literature backing the design's rationale may not have studied this population either |
| **General population via a recruitment platform** | Scale and speed | Weakest construct match; attention and task-seriousness threats; platform fee structures |
| **Mixed panels** (experts for judgment, target-population members for tasks) | Matches unit of analysis to construct | Two recruitment pipelines, two ethics profiles, two instruments |

**Prior knowledge / baseline ability is a design dimension, not a nuisance variable.**
Options: measure and stratify; measure and model as a continuous moderator; restrict
eligibility to a band; or treat the boundary itself as the primary question (e.g., "at
what level of prior knowledge does a given support cease to help"). A system's own
self-rated signal about a user's prior knowledge is not a valid external measure of
it — a study using the system's own rating as its prior-knowledge measure is measuring
the instrument with itself.

## 2. Recruitment

Options: institutional advertisement; disciplinary mailing lists and societies;
snowball from an expert seed; a paid recruitment platform; open volunteer call;
course- or workplace-linked recruitment.

Trade-offs that matter specifically:
- **Course- or workplace-linked recruitment** carries the strongest coercion risk.
  Participation, perceived evaluation, and access to materials can create pressure; the
  protocol must not use grades, performance reviews, or similar leverage as an
  incentive, and evaluators must not see identifiable performance before grading or
  review is complete.
- **Open volunteer calls** are cheapest in cash and most expensive in selection bias and
  ethical debt (volunteer labor is not costless — see the ethics checklist in SKILL.md
  §A6).
- **Expert snowball sampling** from the team's own network compounds builder-as-
  evaluator risk with anchoring risk — the raters may be people invested in the
  project's success.
- **Paid platforms** introduce fee structures, jurisdictional worker-protection
  questions, and a population whose fit to the actual use case must be argued, not
  assumed.

## 3. Inclusion / exclusion

Dimensions available: domain/task familiarity (band, floor, or ceiling); language
competence in the material's language; prior use of the system (naive vs. returning,
once any deployment exists); accessibility and assistive-technology needs (an
**inclusion** design question, not an exclusion criterion); device and connectivity
requirements; completion and data-quality exclusions.

**Binding obligation regardless of option chosen:** exclusion rules must be
pre-specified before data are seen, and post-hoc exclusions must be reported with
counts by condition. An exclusion rule invented after looking at outcomes is an
analysis decision wearing an eligibility costume.

## 4. Methods: quantitative, qualitative, mixed

| Option | Fit | Trade-off |
|---|---|---|
| **Quantitative only** | Artifact validation; task performance with pre-specified outcomes | Silent on *why* anything happened; weakest on interpretive constructs |
| **Qualitative only** | Reasoning, strategy, breakdown, interpretive quality, unanticipated harms | No comparative or estimand-bearing claim; requires its own rigor apparatus |
| **Mixed, sequential (qual → quant)** | Qualitative work generates the constructs and instruments the quantitative strand then measures | Long; the first strand's timeline gates the second |
| **Mixed, sequential (quant → qual)** | Quantitative result, then qualitative explanation of the result and its outliers | Risk of recruiting qualitative data purely to explain away an unwelcome number |
| **Mixed, concurrent** | Both strands on the same sessions; efficient | Integration must be designed in advance or it degrades into two reports stapled together |
| **Design-research / critical analysis** | Interpretive claims handled as interpretive claims natively | Not a method for effect questions and should not be dressed as one |

**Integration points for mixed methods** — name which of these six a design uses, and
when each occurs relative to data collection. "Mixed methods" without a named
integration point is a label, not a design:
1. **Construct definition** — qualitative work defines what an outcome measure should
   capture before it is built.
2. **Instrument development** — codes become rubric items or scale anchors.
3. **Sampling** — the qualitative sample is drawn *from* the quantitative one on a
   stated rationale.
4. **Interpretation** — joint displays that put a measured pattern beside the accounts
   participants gave.
5. **Divergence handling** — a pre-committed rule for what happens when the strands
   disagree, since the disagreement is usually the finding.
6. **Reporting** — whether the strands are reported as one integrated narrative or as
   separable components with a stated relationship.

## 5. Controls and comparators

This is the dimension where a study most easily becomes meaningless, because a real
system usually bundles several things at once — e.g., **access** to material,
**structure** over it (ordering, typing, organization), **generation** (produced
content), and a **display/interface** layer. A comparator that varies all of these at
once cannot attribute anything to any one of them.

| Comparator | Isolates | Fails to isolate | Construction cost |
|---|---|---|---|
| **No-support / baseline only** | The whole bundle vs. nothing | Everything internal to the bundle; also the most flattering and least informative contrast | Lowest |
| **Conventional / current-practice workflow** | The bundle vs. actual current practice — the ecologically meaningful contrast | Internal decomposition | Low, but requires specifying and holding constant what "ordinary access" means |
| **Matched static equivalent** (same underlying material, presented plainly, no adaptive structure or generation) | Access from structure-plus-generation — usually the single most important control | Structure from generation | Moderate; must be genuinely matched, which is real editorial/construction labor |
| **Structure-without-generation** | Structure from generation | Display/interface effects from the rest | Moderate; may require a research-only build |
| **Generation-without-display** | The display/interface layer specifically | — | Requires a research build that deliberately conceals what the product deliberately shows; often ethically and practically awkward |
| **A generic off-the-shelf alternative** (e.g., a general-purpose tool with equivalent access) | The system vs. the obvious alternative a user would otherwise reach for | Confounds tool, interface, and constraint regime unless access is genuinely equated | Moderate; usually best treated as an exploratory addition, not the sole baseline |
| **Within-system feature toggles** | Individual mechanisms | Whole-product claims | Depends on flags whose actual deployment state must be verified, not assumed from documentation |

**A general hazard worth stating in any design.** Adjacent literature on similar
interventions sometimes reports adverse results — e.g., an unsupported condition
outperforming an assisted one on the specific outcome that matters. Any comparator
design must be able to detect a *negative* result as readily as a positive one; a
design that can only register improvement is not measuring anything.

## 6. Assignment and counterbalancing

| Option | Buys | Costs |
|---|---|---|
| **Within-participant, counterbalanced** | Each participant is their own control; efficient for a small population | Carryover, learning, and fatigue across conditions; needs comparable non-overlapping materials; order effects must be modeled, not assumed away |
| **Between-participant randomized** | No carryover | Needs more people; between-person variance |
| **Latin-square material × condition** | Balances material with condition | Constrains the number of conditions and materials to a compatible structure |
| **Matched pairs / stratified on a key covariate** | Directly addresses a known confound (e.g., prior knowledge) | Requires a valid covariate measure that is not the system's own self-rating |
| **Cluster or site-level assignment** | Feasible where individual assignment is not | Nested dependence must be in the model |
| **Single-case / n-of-1 replicated designs** | Viable where the population is genuinely tiny | Needs strong within-case measurement and a stated replication logic |
| **No assignment (observational / field)** | Ecological validity | Self-selection; weak identification |

**Blinding options, in descending feasibility:** blind coders/raters to condition and
provenance (usually feasible and usually mandatory); blind analysts to condition labels
until analysis is locked (feasible); blind participants to condition (rarely feasible
when the interface itself is the manipulation); blind the experimenter (interacts with
builder-as-evaluator risk).

## 7. Materials

Dimensions: **domain** (single vs. multi-domain — sampling must be justified before
volume); **format/type** (the specific format the design targets vs. the format
adjacent evidence actually covers — these commonly differ and the gap must be named);
**difficulty calibration**; **length/duration** (a session-sized excerpt vs. a real
task — a validity/feasibility trade-off with no free option); **licensing status**
(public-domain, licensed, permission-cleared, or institutionally authorized only);
**processing modality** (a real variable if the underlying pipeline degrades to a
flatter fallback under some condition — this must be checked, not assumed constant);
**freshness** (whether materials postdate any relevant training data, for ML-adjacent
systems); and **overlap with the team's own working corpus**.

A held-out corpus that is *also* the team's own working corpus is not held out. The
strongest available option is material the team has never processed, in a domain it has
not otherwise written about, under a license that permits the use — and each of those
three conditions costs something.

## 8. Outcomes

Grouped by what they can and cannot support.

**Artifact outcomes** (no participants needed): resolution precision/recall,
error/failure rate, unsupported-output rate, agreement with human coding, ordering
agreement, retrieval/relevance quality, stability across repeated runs and versions,
latency, cost, graceful degradation under partial failure. — Say nothing about people.

**Immediate task-performance outcomes**: rubric-scored task products, accuracy of a
specific sub-task, discrimination of correct from incorrect system behavior, time on
task. — Say nothing about retention or transfer.

**Retention and transfer outcomes**: delayed post-test on the same material
(retention); near transfer to a similar task/text/domain; far transfer to a different
domain or task type. — These are the outcomes that license the word *learning*. Without
at least one of them, no learning claim is available at any sample size. The delay
window is itself a design parameter with no default.

**Process and behavioral outcomes**: what a person opens, expands, checks, verifies, or
ignores; whether a supporting signal is consulted before or after forming a judgment;
navigation paths; abandonment. These require instrumentation that usually does not
already exist (a product's own telemetry is typically too coarse) and raise
measurement-reactivity risk.

**Subjective outcomes**: perceived helpfulness, self-reported effort, usability, trust,
confidence. — Legitimate outcomes about perception and **must never be reported as
performance**. The perception/performance dissociation is a specific, well-documented
hazard. Instrument licensing and task-fit must be confirmed before adopting any
standard scale.

**Trust-calibration outcomes**: reliance appropriateness given known system error;
agreement with the system when it is right vs. when it is wrong. Note that transparency
and trust often relate non-monotonically in the broader literature, and explanations do
not straightforwardly improve human-system team performance — any design here must be
able to find that more transparency does not help.

**Harm and cost outcomes** — mandatory whenever any benefit outcome is measured: time
cost; effort cost; dependency and offloading-without-verification; error introduction
(including confidently-wrong output accepted); inequity across relevant subgroups
(prior knowledge, language, assistive-technology use); attention displacement;
frustration/abandonment.

**Primary vs. secondary designation, multiplicity handling, and the missing-data plan
must be declared before data collection** — outcome proliferation is where this
obligation is most often violated.

## 9. Procedure

Dimensions: setting (lab, remote-supervised, remote-unsupervised, in-situ); session
count and spacing (a single session forecloses retention; multiple sessions introduce
attrition); training and familiarization (a real confound if uneven — an unfamiliar
system imposes an interface-learning cost that a familiar baseline does not); think-
aloud vs. silent work (yields process data and changes the process it observes); the
delay interval for any retention measure; and debrief content (must disclose the
system's known error profile).

## 10. Analysis families

Options and what each presupposes:
- **Descriptive with uncertainty intervals plus a documented error taxonomy** — the
  honest default for artifact validation; presupposes nothing about distributional
  form; the error taxonomy is usually the more valuable output.
- **Agreement statistics appropriate to the data and scale type** — for coding and
  rater work; the choice among them is a data-type decision, not a preference, and
  disagreement-preserving designs need agreement measures that do not assume a single
  truth.
- **Mixed-effects / multilevel models** — appropriate wherever observations nest in
  participants, materials, sources, or raters; presuppose enough clusters at each
  level, convergent random-effect structure, and a pre-specified structure rather than
  one arrived at by searching.
- **Ordinal models** for rating outcomes rather than treating ordinal ratings as
  interval.
- **Planned contrasts** declared in advance rather than all-pairs testing after the
  fact.
- **Simulation-based sensitivity analysis** using pilot-estimated variance — the
  correct instrument to precede any sample-size statement.
- **Bayesian estimation** — an option, not a loophole; requires prior justification and
  does not exempt anyone from the estimand-first chain.
- **Qualitative analytic families**: codebook/framework analysis, reflexive thematic
  analysis, interpretive/hermeneutic reading, negative-case analysis. Each carries
  different rigor obligations, and naming one is not the same as doing it.
- **Preregistered exploratory strand**, labeled as such throughout, never converted to
  confirmatory by later narrative.

Report estimates and uncertainty, not significance tests alone. Inspect residuals,
influential cases, convergence, missingness patterns, and attrition by condition — and
report what the inspection found, not merely that it was performed.

## 11. Qualitative components — where they attach

Available attachment points: pre-study construct elicitation; think-aloud during task;
post-task interview; expert open comments alongside rubric ratings; diary or log-based
reflection in a longitudinal strand; critical-incident collection (breakdowns, errors,
surprises); and document/artifact interpretation with no participants at all. Each has
different data-protection consequences and different reactivity profiles. Full rigor
requirements are in SKILL.md §A5.
