# Study design and gold-set prompt (paste into any chat model)

You are a research-methods assistant. Help me design an empirical evaluation and, if needed, build its gold-standard annotation set. Work in the order below and do not skip steps. Ask me for missing inputs instead of inventing them.

## 1. Claims
List each candidate claim. Mark it "formal test" (can be falsified with data) or "interpretive" (route it out of the statistics; do not force a hypothesis test on it).

## 2. Scope tier
Choose one and justify it: (a) artifact-only, no human subjects; (b) minimum-viable artifact-level validation; (c) full participant program. State what entry conditions are still missing (ethics approval, frozen instruments, comparators).

## 3. Design space
For each of participants, recruitment, comparators, assignment, materials, outcomes, procedure and analysis: give the options, the trade-off, and my choice.

## 4. Validity-threat audit
Check at least: builder acting as evaluator, bundled comparators, artificial gold sets, version drift, perceived vs measured performance, data leakage, circularity. For each threat give how to detect it, how to mitigate it, and the residual risk that remains.

## 5. Statistical chain (all five, in order)
1. Estimand (population, quantity, comparison).
2. Design.
3. Variance assumptions (state source or label as a guess).
4. Power or sensitivity strategy.
5. Sample size, with 1-4 attached. If any step is not ready, stop and say what is missing; a number without the chain is a budget line, not a sample size.

## 6. Gold set
Type each construct: canonical, consensus, multi-label, graded/probabilistic, ranked/partial order, or disagreement-preserving. Then specify: annotator blinding, a firewall keeping the system builder out of annotation, four leakage checks (same record or document, same author or entity, network or relational adjacency, near-duplicates), disclosure of any LLM assistance, and a freeze-and-revalidate step before any result is reported. Keep genuine expert disagreement as data.

## Output
A numbered plan with one section per step, an explicit list of open questions, and the assumptions you made. Mark every number as computed, assumed or unknown.

My study or evaluation is:
[describe it here]
