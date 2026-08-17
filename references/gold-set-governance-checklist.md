# Gold-set governance checklist

Seventeen binding obligations on any team constructing a human-annotated reference
(gold) set, each with an acceptance criterion. A set may not be marked complete with any
obligation unmet or waived without a recorded, reviewed exception. This expands the
summary in SKILL.md §B3.

| ID | Obligation | Acceptance criterion |
|---|---|---|
| **G-01** | **Domain sampling.** A written sampling frame naming the population, the strata, the inclusion/exclusion rules, and the selection procedure, per construct. | The frame is written *before* any item is selected, and every selected item traces to a frame rule. If the source corpus lacks a field needed to stratify (e.g., no domain/category tag), a documented coding pass with an explicit rule is a prerequisite — not a regex guess. |
| **G-02** | **Licensing.** Every item's license basis recorded before it enters the set, with the authority (not a badge, not an inference) named. | No item enters without a recorded basis. A badge or informal marker with no accompanying license text is not itself a license grant. |
| **G-03** | **Codebook / ontology.** A versioned codebook per construct: value definitions, positive and negative exemplars, decision rules for the hard boundaries, an explicit "how to code when uncertain" rule, and a change log. | Every value has at least one negative exemplar (what it is *not*), and every hard boundary named in the construct's typing entry has an explicit rule. The codebook version is stamped on every record. Where a vocabulary is inherited from elsewhere, its provenance is recorded — including any part that is locally invented rather than adopted wholesale. |
| **G-04** | **Expert eligibility.** Written criteria per construct, stated as demonstrable evidence, never as a byline or a repository/project-contribution credit. | Expertise may not be inferred from authorship or contribution history alone. Criteria must be checkable (credential, publication in the domain, teaching, editorial or professional work) and recorded per annotator. |
| **G-05** | **Panel composition.** Per construct: number of coders per item, coder diversity across the substantively plural dimensions, and a documented rationale. | Composition is justified against the construct's type — a disagreement-preserving construct with a homogeneous panel cannot detect the plurality it exists to record. Composition is recorded and reported with every statistic derived from the panel. |
| **G-06** | **Independence and conflicts.** A conflicts register naming, per annotator: relationship to the project, to the system under evaluation, to the authors/team, and to the items coded. | See SKILL.md §B2 — the builder-as-annotator conflict is named there and firewalled. No annotator with an unmanaged conflict contributes to a frozen held-out set. |
| **G-07** | **Training and calibration.** A training pass on non-study items, with a documented calibration threshold that must be met before an annotator codes study items, and re-calibration on every codebook version bump. | Calibration items are drawn from the development pool, never the frozen set. Re-calibration is mandatory, not discretionary, after a codebook change. |
| **G-08** | **Pilot.** A pilot on a development sample, whose purpose is to revise the codebook and estimate the disagreement rate — not to produce data. | Pilot items are discarded from the final set or explicitly re-coded under the final codebook, with the choice recorded. A pilot producing no codebook change is reported as such — that is itself information about codebook maturity. |
| **G-09** | **Double-coding.** Every item in the frozen held-out set is independently coded by at least two eligible annotators who cannot see each other's codes. | Independence is enforced by the interface, not by instruction alone. Single-coded items may exist in the development pool; they may not exist in the frozen set. |
| **G-10** | **Agreement statistics, chance-corrected and data-appropriate.** | See the statistic-selection table in SKILL.md §B3. All agreement is computed on **pre-adjudication** independent codes; post-adjudication agreement is definitionally inflated and may not be reported as reliability. |
| **G-11** | **Principled adjudication, where appropriate.** A documented adjudication procedure specifying who adjudicates, on what evidence, under what rule, and — critically — which disagreements are **not** eligible for adjudication. | The adjudicator is not one of the original coders for that item. Every adjudication records the rationale and the pre-adjudication codes. The ineligible band per construct is exactly as typed in the construct-typing decision and may not be widened for convenience. |
| **G-12** | **Negative and edge cases.** Deliberate inclusion of true negatives, near-misses, and boundary cases, drawn from **observed** failures wherever possible. | A three-way outcome vocabulary (e.g., accept / reject / quarantine-as-unresolved) usually expresses reality better than a binary reference standard can. Invented negatives are permitted only where observation is genuinely impossible, and must be flagged as invented. |
| **G-13** | **Versioning.** Semantic versioning of the set, with an immutable content hash per release, a change log, and a rule that any label change is a new version and never an in-place edit. | Every reported result names the set version and hash. Extend any existing per-file provenance/hashing discipline from source files to full releases. |
| **G-14** | **Quality audit.** A scheduled re-audit of a random sample of the frozen set by an annotator not involved in its production, reporting a drift rate. | The audit is scheduled at set creation, not triggered by suspicion after the fact. Its findings are published with the set, including when they are unfavorable. |
| **G-15** | **Storage.** Where the set lives, who can read it, how the frozen partition is protected from accidental exposure to a tunable system, and how source material with restrictive licenses is held separately from labels. | Labels and short anchor excerpts may live openly; licensed or restricted source material stays in access-controlled storage the evaluated system cannot itself address. A `.gitignore`-style exclusion is a guard, not a substitute for an actual access-control decision — document it as such. |
| **G-16** | **Refresh.** A stated refresh trigger and procedure — what change to the domain, the taxonomy, or the system obliges re-annotation, and what the refresh does to prior results' comparability. | A refresh that changes the split assignment (e.g., changing a hash function or a grouping key) is a **breaking** refresh and invalidates cross-version comparison; it must be declared as such, not treated as routine maintenance. |
| **G-17** | **Release restrictions.** For each set: may it be published, under what license, with what embargo, and what must be withheld. | Reconciled against the applicable data-stewardship standard for the target venue or audience (e.g., an open-science standard that pushes toward openness) while respecting that some source material may be explicitly private/non-redistributable and some reused data may carry an unresolved license gap. State, per set, which posture applies. This is a policy decision requiring explicit sign-off, not a default an engineer picks. |

## Agreement-statistic selection (G-10, expanded)

The statistic follows the data type, never habit:

| Data shape | Required statistic class | Explicitly wrong |
|---|---|---|
| Nominal, exactly 2 coders, complete | Cohen's kappa | Raw percent agreement alone |
| Nominal, >2 coders and/or missing data | Krippendorff's alpha; Fleiss' kappa where raters are fixed and complete | Cohen's kappa (undefined for >2 coders) |
| Ordinal / graded (relevance, confidence) | Weighted kappa, or Krippendorff's alpha with an ordinal difference function | Nominal kappa — treats a large-magnitude disagreement as equal to a one-step disagreement |
| Multi-label sets | Per-label chance-corrected agreement **plus** a set-distance measure (e.g., alpha with a set metric) | Pooled single-label accuracy; per-label agreement without a set measure |
| Rankings / partial orders | Kendall's tau-b (ties-aware) per expert pair; Kendall's W for panel concordance; a partial-order-aware distance where incomparabilities are declared | Spearman rho on a forced total order; treating pairwise precedences as independent items |
| Spans / offsets | Exact-match agreement **and** overlap-tolerant agreement at a pre-registered tolerance, reported together | Either one alone |

Three further mandatory reporting rules:
1. **Report observed agreement, expected agreement, and the marginal distributions**
   alongside every chance-corrected coefficient — kappa is unstable under skewed
   marginals.
2. **Report per-class agreement, never pooled alone** — pooled figures are dominated
   by easy classes.
3. **Report an uncertainty interval on every agreement coefficient**, by an appropriate
   resampling procedure. A point estimate computed on a thin cell (where flipping a
   single label materially moves the number) is precisely the failure this rule
   prevents.

## Development/calibration pool vs. frozen held-out set (expanded)

**The obligation.** Every reference set is partitioned into a **development/calibration
pool** (codebook revision, annotator training, pilot work, threshold setting, error
analysis) and a **frozen held-out set** (used exactly once per declared system version,
for the declared inference, and never for iteration).

**The split unit is not the item.** It is the smallest unit that can carry information
between partitions. Examples, generalized across construct types:

| Construct family | Typical split unit | Why |
|---|---|---|
| Record/entity resolution | The source document containing the record | Multiple extractions from one document share pipeline, format, and style |
| Locator/attribution correctness | The cited/referenced work (and, where an edition is at issue, the edition) | Multiple extracts from one work share pagination and format defects |
| Categorical/relationship classification | The source document, and where an entity recurs, the entity-identity cluster | A system that has seen an entity's role in one pair has information about its role in another |
| Ranking / ordering | The whole ordering set — never split across partitions | Orderings are internally dependent by construction |
| Retrieval / grounding | The source document, not the query | Multiple queries retrieve from the same underlying chunks |
| Single-label classification | The source document | Items from one document share register, style, and author idiom |
| Contested-mechanism labeling | The item pair *and* both underlying source items | The pairing itself is the phenomenon |

**Common gap to check for.** A pre-existing split function that hashes only an item's
own identifier is an item-level, group-blind split — exactly what the split-unit rule
forbids for every construct family above. Wrap any such function so it hashes the
correct *split-unit key* rather than the item id; if the function is a pure function of
a string, this preserves its idempotence at the group level (new items do not reshuffle
existing assignments).
