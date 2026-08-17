# Gold-set construct typing — worked illustrative examples

Eight illustrative constructs, each showing how to apply the six-type decision
procedure from SKILL.md §B1 to a real construct: state the unit of analysis, decide the
type (and justify it substantively, not by cost), state a disagreement policy, and note
what an existing or reused asset can and cannot serve as. These examples are drawn from
the scholarly-research / AI-reading-tool domain as illustrative flavor — the pattern
generalizes to any domain with classification, ranking, extraction, or retrieval
constructs (support-ticket routing, medical coding, content moderation, search
relevance, and so on). Treat them as a template to adapt, never as a checklist to copy
verbatim into an unrelated construct.

---

## Construct 1 — Record resolution (e.g., citation-to-catalog-entry resolution)

| Field | Content |
|---|---|
| **Unit of analysis** | One extracted reference string, in its surrounding context, paired with the external identity (or non-identity) it should resolve to. |
| **Purpose** | Separate *recall* (did it find a candidate match), *correctness* (is the match the right record), and *honest abstention* (did it decline rather than guess) — three distinct outcomes a single accuracy number collapses. |
| **Type** | **Canonical, with a mandatory abstain value and a disagreement-preserving residue.** A reference either does or does not denote a specific catalogued external record, checkable against an independent authority. The residue is not decorative: some categories of reference (older editions, translations, works in multiple compilations) have genuinely contested canonical identity, and forcing them to a single record manufactures false ground truth. Type those cases disagreement-preserving and report them separately — never fold them into the canonical denominator. |
| **Disagreement policy** | Two coders resolve independently against named external authorities and record which authority settled it. Retained per item: every authority consulted, the resolved identifier, and the abstain flag. Adjudicated: cases where coders resolve to different records and one is demonstrably a metadata error in the external source itself. **Not adjudicated:** cases where two records are both defensible identities for the same reference (edition/translation plurality) — those carry both, and any metric computed over them is reported with and without them. |
| **Reuse note** | An existing gold set that scores a coarser routing decision (e.g., "book" vs. "journal" vs. "unclear") is *adjacent, not the same construct* as resolution correctness — a useful design precedent for "score the coarse label, preserve the fine distinction descriptively," not a substitute for a resolution-specific set. A negative-case set drawn from **actually observed** false positives (not invented) is the strongest kind of asset here. |

---

## Construct 2 — Locator and attribution correctness

| Field | Content |
|---|---|
| **Unit of analysis** | One `(quoted span, recorded locator, recorded attributed source)` triple, evaluated against a correctly rendered version of the cited source. **Decomposes into three sub-constructs that must not share a denominator:** (a) locator correctness — does the recorded page/section actually contain the quoted span; (b) attribution correctness — does the span belong to the work cited; (c) nested-attribution correctness — where the cited work is itself quoting a third party, is the utterance attributed to the right original speaker. |
| **Purpose** | Test a failure a plain substring/verbatim check is structurally blind to: transcription artifacts, locator defects, and nested quotation are all invisible to a check that only asks "does this string appear somewhere." This construct audits the audit. |
| **Type** | (a) **Canonical** — a page either contains the span or it does not, checkable by anyone with the source. (b) **Canonical with adjudicated edition handling** — attribution is a fact about the work, but which pagination is authoritative across editions/translations is a coder decision requiring a documented rule. (c) **Consensus-based, with a disagreement-preserving residue** — nested attribution is canonical when the source marks the quotation explicitly, and genuinely contested when the source paraphrases, free-indirectly reports, or quotes a quotation. The contested band is not a coding failure; it is the phenomenon. |
| **Disagreement policy** | Independent double-coding at the span level, with character offsets recorded (not just page numbers), scored both exact-match and overlap-tolerant against a pre-registered tolerance. Retained per item: each coder's offsets, the edition/printing consulted, and a boolean for "the source itself marks this as a quotation of a third party." Adjudicated: locator disputes traceable to different editions, under a documented rule (e.g., the edition recorded in the manifest governs; if silent, the item is quarantined rather than decided). **Disagreement-preserving:** the nested band — where two qualified coders read the same span as the citing author's own voice versus a reported voice, both readings are stored with warrants, and the *disagreement rate itself* is a reported finding about the difficulty of the construct, not a defect in the panel. |
| **Reuse note** | A pre-existing, human-produced enumeration of locator defects (even an informal one from prior quality work) is a rich *seed* for the codebook's defect taxonomy — reuse it for categories, not as a finished reference standard, if its own denominator or completeness status is unsettled. |

---

## Construct 3 — Multi-value categorical classification (e.g., typed relationship labeling)

| Field | Content |
|---|---|
| **Unit of analysis** | One `(source item, target item, context)` triple — **not** one system-emitted annotation row. The coding unit must be the relationship itself, or the reference standard inherits the system's own one-label-per-item constraint as if it were a property of the world. |
| **Purpose** | Measure agreement between a system's typed classification and independent human coding — and, prior to that, whether the category vocabulary is *codeable at all* by independent humans, which a system's own internal tests never establish. |
| **Type** | **Multi-label and disagreement-preserving, with a canonical sub-layer.** If the categories are not mutually exclusive in principle but the system is constrained to assign exactly one, a reference standard that also assigns exactly one encodes the *instrument's* constraint as ground truth — high agreement would then be evidence that coders were forced, not that they concurred. Coders should assign a **set**, with an optional designated primary. Any category whose value records provenance about the classifier rather than a judgment about the world (e.g., "machine-inferred, unreviewed") is excluded from the human coding vocabulary entirely — it is a fact about origin, not something a human codes. The canonical sub-layer is whatever narrow slice is externally checkable (e.g., "is this relationship explicitly stated in the text" is adjudicable against the text). The disagreement-preserving band is the interpretive cluster of categories, where a classification scheme's own contingent choices about what counts as related are the phenomenon under study, not noise to be removed. |
| **Disagreement policy** | Independent multi-coding without any sight of system output. Retained: every coder's full label set, per-label confidence, and free-text warrant. Adjudicated: the canonical sub-layer only, and only against the source material. **Disagreement-preserving:** the interpretive cluster, reported as a per-pair label distribution. The headline statistic is per-label chance-corrected agreement plus a set-agreement measure — never pooled single-label accuracy. |
| **Reuse note** | An existing gold set built for regression testing of a classifier is very often **single-label by construction and majority-synthetic**, which disqualifies it as a research reference standard even while it remains valuable as a regression fixture and codebook draft. A set scored on the classifier's full data with no held-out partition, because the classifier has no tunable parameters, becomes a leak the moment the same harness is pointed at any tunable (e.g., model-based) system — that reasoning does not transfer across a fixed-vs-tunable boundary. |

---

## Construct 4 — Ranking / ordering agreement (e.g., a recommended sequence)

| Field | Content |
|---|---|
| **Unit of analysis** | **One ordering over a defined set of items, for a defined target and a defined viewer/reader profile** — not one pairwise precedence judgment, and not one item. This is the construct most often mis-unitized: scoring pairwise precedences as independent items inflates apparent sample size and violates independence, since precedences within one ordering are structurally dependent. Pairwise precedences may be a *derived scoring representation*; they are never the unit. |
| **Purpose** | Test whether a system's ordering is a defensible ordering — against what qualified experts producing the same ordering actually produce — where the ordering threshold or logic is often a design parameter chosen by the system's designers and not independently validated. |
| **Type** | **Ranked / partial-order, explicitly disagreement-preserving.** Two justifications. Formal: a real ordering is typically a partial order, not a total one — genuinely parallel items are incomparable, and forcing a total order manufactures precedences no expert holds. The instrument must let an expert declare ties and incomparabilities as first-class data. Substantive: expert plurality is often the object of study itself — two qualified experts may defensibly order the same material differently for the same target reader, and the design question is partly answered by how much experts converge. Adjudicating to a single consensus ordering deletes the answer. |
| **Disagreement policy** | Each expert produces an ordering independently, with declared ties/incomparabilities and a per-position rationale. **Nothing is adjudicated into a single reference ordering.** Retained: every expert's ordering in full. Reported: (a) pairwise expert-to-expert concordance, establishing the *ceiling* any system could be scored against; (b) system-to-each-expert concordance; (c) the profile of positions where experts converge versus diverge. A "core ordering" — the sub-order on which all experts agree — may be defined and labeled as such, but never presented as "the correct order." A single expert's ordering is never designated the standard. |
| **Reuse note** | An existing, informally produced "floor" ordering — explicitly framed as a floor that later evidence may reorder or extend, rather than a fixed answer key — is the right *scoring stance* template, even when it comes from a single, non-independent process and cannot itself serve as the reference standard. Specification-acceptance test cases (asserting a ranker does what its designers specified) must never be re-described as expert agreement. Verify any scope bound on the system's own ordering logic (e.g., it only traverses material a user has personally supplied) before building a held-out corpus, or the study risks measuring corpus construction rather than ordering quality. |

---

## Construct 5 — Retrieval-answer grounding (RAG-style)

| Field | Content |
|---|---|
| **Unit of analysis** | Two nested units, kept deliberately separate. (a) *Retrieval*: one `(query, candidate passage)` pair with a graded relevance judgment. (b) *Grounding*: one `(query, answer span, cited source chunk)` triple — does the cited chunk actually support the specific span attributed to it. Scoring (b) at the whole-answer level rather than the span level hides partially-grounded answers, which is the failure mode that matters most. |
| **Purpose** | Test the gap between citation *existence* (a system architecturally guarantees every cited identifier resolves to something real) and citation *support* (whether the cited material actually backs the specific claim attributed to it) — a gap architectural guarantees do nothing to close. |
| **Type** | (a) **Probabilistic / graded** — relevance is a degree, not a binary; encode it with a small ordinal scale (e.g., 0–3). (b) **Multi-label with a canonical spine and a disagreement-preserving band.** Canonical: whether the cited chunk contains the asserted proposition verbatim or in unambiguous paraphrase. Disagreement-preserving: whether an inferential step from chunk to answer span is *warranted* — a judgment qualified readers legitimately differ on, and one that collapses into a false binary if adjudicated. |
| **Disagreement policy** | Graded relevance: multiple independent graders, agreement scored with an **ordinal-appropriate** statistic (weighted kappa or Krippendorff's alpha with an ordinal difference function — plain nominal kappa treats a large-magnitude disagreement as identical to a one-step disagreement, which is wrong here). Retained: every grade. Adjudicated: only grades differing by more than a pre-registered ordinal distance, resolving to a grade, never to a binary. Grounding: independent double-coding of support / non-support / inferential; the inferential band is retained with warrants and reported as its own rate. **A "not-found" response is a scored outcome, not a missing datum** — a reference set that omits unanswerable queries cannot measure whether abstention is calibrated. |
| **Reuse note** | A graded-relevance fixture ported from an unrelated codebase or third-party source often carries its own license constraints — verify the license basis before any research or publication use, independent of whether the data is technically structurally apt. A completed, honestly reported retrieval evaluation with a pre-declared meaningful-delta threshold and an explicit refusal to over-read a small sample is a good methodological precedent for the pre-declared-threshold discipline (SKILL.md §B5) — reuse the discipline, not necessarily the numbers. |

---

## Construct 6 — Single-label categorical classification with a contested boundary

| Field | Content |
|---|---|
| **Unit of analysis** | One extracted unit (e.g., a sentence-level claim), in its surrounding context. |
| **Purpose** | Test whether a vocabulary spanning several distinct categorical values is reliably codeable by independent humans, and whether a system agrees with them. This construct is typically *prior* to more granular classification and ranking constructs in the dependency order: if the coarse vocabulary is not reliably codeable, downstream finer labels inherit its unreliability. |
| **Type** | **Consensus-based with a disagreement-preserving band.** Most of a well-designed vocabulary is nuisance-plural — a coder either has the necessary context or does not. But a subset of values is often substantively contested by the underlying domain itself (e.g., interpretive vs. conceptual vs. definitional distinctions in a humanities domain), which concedes that the categories carry real theoretical commitments. Retain those specific values plural rather than adjudicating them. |
| **Disagreement policy** | Independent double-coding; adjudication permitted on the values outside the contested band; the contested subset reported as a confusion structure rather than adjudicated to a point. Per-class agreement must be reported even where pooled agreement looks adequate — a pooled number will be dominated by the easy classes. |
| **Reuse note** | A set drafted by a single reviewer's sign-off ("approved as labeled") is not an independent-coding record and carries no agreement statistic — it is a legitimate internal quality act, not a reference standard. Flag explicitly if the same person reviewing is also the system's builder (a builder-as-annotator conflict — SKILL.md §B2), and flag explicitly if any part of the category vocabulary itself is locally invented rather than adopted from an established scheme, pending independent confirmation. |

---

## Construct 7 — Contested-mechanism / fine-grained explanatory labeling

This construct type deserves special attention because it is the strongest available
argument against defaulting to canonical typing: a real project ran exactly this
construct, and the result was a measured, denied promotion of the underlying capability.

| Field | Content |
|---|---|
| **Unit of analysis** | One item pair already judged to be in some broader relation (e.g., "these two claims diverge somehow"), paired with a finer mechanism label explaining *why* they diverge. |
| **Purpose** | Test whether a fine-grained explanatory vocabulary is codeable and classifiable at all. |
| **Type** | **Explicitly disagreement-preserving. No other typing is defensible on evidence like this.** In one documented instance, mechanism-labeling accuracy against a small evaluation set landed far below a pre-declared floor, and the failure was characterized as *systematic, not random* — the classifier over-predicted one catch-all mechanism, with most misses being one of the other mechanisms mislabeled as the catch-all. A vocabulary whose categories a competent classifier cannot differentiate is a vocabulary whose *boundaries are not yet established*, and the honest reference standard for a construct in that state records positions, not answers. |
| **Disagreement policy** | Multiple independent expert positions per pair, each with a warrant, with **no adjudication to a single mechanism** until a separate, prior study establishes that independent experts can differentiate the values above chance. The primary reported quantity is inter-expert differentiation itself. If experts cannot differentiate the values either, that is a finding about the vocabulary — arguably the most publishable finding available for this construct — and it must be reportable as such, rather than absorbed into a low system score. |
| **Reuse note** | Labels drafted by the same program that built the classifier being scored, and ratified by a single non-independent reviewer, are usable as the *study's own object* (a documented example of a vocabulary's boundary problem) but **unusable as a reference standard**. A genuinely small evaluation sample (e.g., where a single flipped label materially changes the headline number) must be reported as exactly that thin, not smoothed over. If the underlying capability is deliberately withheld from production pending stronger evidence, a study of it studies a capability that is switched off — legitimate, but must be stated, and studying it does not itself un-gate it (see the instrumentation-versus-claim discipline note below). |

---

## Construct 8 — Structural/processing completeness (a supporting construct)

| Field | Content |
|---|---|
| **Unit of analysis** | One source document, with its structural/layout class, against an expected-structure floor (e.g., expected page or section count, expected block count, expected apparatus separation, expected section titles). |
| **Purpose** | Establish what fraction of source material is processed well enough for any downstream locator, attribution, or grounding judgment (Construct 2, Construct 5) to be meaningful. Without this, defect rates in those constructs confound processing failure with the thing actually being measured. |
| **Type** | **Canonical with a declared floor, not a fixed answer key.** State explicitly that expected structure is a floor a given run may exceed or reorder when evidence supports doing so, not an answer key to match exactly. |
| **Disagreement policy** | Structural facts are adjudicable against the source directly. The *layout or processing class* is a coded judgment and takes independent double-coding against a documented class list. |
| **Reuse note** | Multiple independent automated detectors run over a sample of source material, cross-checked and self-corrected in both directions, are the closest thing to a research-grade instrument with an honest error profile — but a multi-instrument agreement design is not the same as a human-coded reference standard, and the layout/processing classes still need a codebook of record if none exists yet. |

---

## Cross-cutting notes for any domain

1. **Two structurally distinct classification vocabularies must never be conflated** if
   a project maintains more than one (e.g., a coarse reader-facing category set and a
   finer internal mechanism set). They are typically scored by different gold families,
   answer different questions, and mixing them in one results table is a category
   error even when every individual number is correct.
2. **An agreement statistic implemented as "predicted vs. gold" is a performance
   metric, not inter-rater reliability.** Check every existing agreement-computation
   utility for what its two inputs actually are before reusing it for anything claimed
   as human-vs-human reliability. It is common for a codebase to have *zero* true
   human-vs-human IRR figures even while having a working, well-documented system-
   vs-gold metric.
3. **A deterministic split function keyed only on an item's own identifier is
   leakage-blind by construction.** Verify this before trusting any existing split
   utility, and wrap it to hash the correct split-unit key instead (SKILL.md §B3, §B4).
4. **The pre-declared-threshold discipline generalizes well and should be inherited
   wherever it already exists** in some form (a gate that denies promotion against a
   floor set in advance, a feature held off pending a re-run showing real improvement,
   a documented note that a capability "did not reach the accuracy thresholds set for
   it in advance, so it was not turned on"). Generalize the pattern into a standing
   rule rather than treating each instance as a one-off.
5. **A flag or status field meaning "labeled but not yet independently accepted"**
   (e.g., a `provisional` boolean) is a good existing mechanism to build a hard gate
   around — fail loudly if any record in a frozen set is still marked provisional,
   rather than silently including it.
