# Empirical Study Design and Gold-Set Toolkit

An Agent Skill that packages a rigorous, end-to-end methodology for two coupled jobs:
designing an empirical evaluation (of a system, an intervention, or a claim) so that its
sample size is *earned* rather than guessed, and building the human-annotated
reference ("gold") data that evaluation depends on, so the result isn't secretly
measuring the people or process that built the thing under test.

It grew out of applied research planning for an AI-assisted scholarly-reading tool, and
keeps some of that domain's flavor as illustrative color — but every checklist, table,
and worked example is written to generalize to any domain: a product eval, an ML
benchmark, a UX study, a content-moderation audit, a medical-coding reliability check,
or a classic behavioral-science experiment.

## What it does

Give this skill to an agent (or read it yourself) before planning any of the following,
and it will walk through a complete, checkable process rather than jumping straight to
a number:

- **Deciding what a study can actually claim.** A short classification step sorts
  every candidate claim into "suitable for a formal empirical test" versus
  "interpretive/conceptual, and forcing it into a falsification template is itself an
  error" — before any design work starts.
- **Choosing a scope tier** — no-subjects/artifact-only, minimum-viable artifact-level
  validation, or a full participant program — against explicit selection criteria,
  instead of defaulting to whichever tier sounds most impressive.
- **Working every design-space dimension** that a real evaluation touches:
  participants, recruitment, comparators, assignment, materials, outcomes, procedure,
  and analysis — each with an option table and its trade-offs.
- **Running a validity-threat audit** against a 22-item generalized catalog (builder-
  as-evaluator conflicts, comparator bundling, gold-set artificiality, version drift,
  perception/performance dissociation, data leakage, and more), each with a detection
  obligation, a mitigation obligation, and — honestly — the residual risk that
  mitigation doesn't remove.
- **Running the five-step statistical chain, in order, with no step skippable:**
  estimand → design → variance assumptions → power/sensitivity strategy → sample size.
  A number that arrives without that chain attached is treated as a budget line, not a
  sample size.
- **Typing every gold-set construct** against a six-type decision procedure (canonical,
  consensus-based, multi-label, probabilistic/graded, ranked/partial-order, or
  explicitly disagreement-preserving) — so genuine expert disagreement gets *preserved*
  as data instead of being adjudicated away into a false single truth.
- **Enforcing a builder-as-annotator firewall**, four leakage-detection axes, annotator
  blinding, LLM/automated-assistance disclosure, and a freeze-and-revalidate discipline
  before any gold-set result is reported.
- **Deriving reference-set and sample sizes** from precision, heterogeneity, intended
  inference, and budget — in that order — instead of treating "we need a lot of data"
  as a calculation.

## Installation

This is an [Agent Skill](https://www.anthropic.com/news/skills) following the portable
`SKILL.md` convention. To use it:

- **In Claude Code:** copy this folder into `.claude/skills/empirical-study-design-and-gold-set-toolkit/`
  in your project (or your user-level skills directory), and it will be available for
  Claude to invoke automatically when relevant, or on request.
- **In any other agent runtime that supports the `SKILL.md` convention:** copy this
  folder into that runtime's equivalent skills directory. The package is plain Markdown
  with no external dependencies, so it should load anywhere the convention is
  supported.
- **For a human reader:** `SKILL.md` is a complete, self-contained methodology document
  on its own — open it directly if you just want to read or apply the process by hand.

No scripts are bundled with this skill; it is a planning and construction methodology,
not a runnable tool. Everything an agent needs to execute the process end to end lives
in `SKILL.md`, with longer reference tables split into `references/` so the main file
stays navigable.

## Package contents

```
SKILL.md                                    the complete methodology (start here)
references/design-space-catalog.md          full option tables for every design dimension
references/validity-threat-catalog.md       22-item generalized validity-threat catalog
references/gold-set-construct-typing.md     8 worked construct-typing examples, all 6 types
references/gold-set-governance-checklist.md the full 17-obligation gold-set checklist
examples/worked-example-synthetic.md        a complete synthetic walkthrough, start to finish
LICENSE                                     MIT
```

## Worked usage example

`examples/worked-example-synthetic.md` runs the entire methodology against a fictional
"System-R" AI reading-assistant tool, using entirely invented data (clearly marked
`[SYNTHETIC]` throughout). It:

1. Classifies three candidate claims by type, and routes an interpretive one out of the
   statistical chain entirely.
2. Carries an artifact-level claim ("does the classifier agree with independent human
   coding?") through all five steps of the statistical chain to a sample size that
   arrives with its full justification attached.
3. Stops a participant-level claim at the estimand stage, on purpose, because its entry
   conditions (ethics approval, frozen instrumentation, comparator materials) aren't
   met yet in the scenario — showing what "the design isn't ready for a sample size
   yet" looks like when done honestly instead of skipped.
4. Types the reference-set construct backing claim 1, enforces the builder-as-annotator
   firewall against an internal illustrative set the fictional team had already drafted,
   runs all four leakage checks, and produces a freeze manifest before any agreement
   number is reported.

Read that file for the complete, line-by-line application — it is the fastest way to
see how the abstract checklist in `SKILL.md` cashes out in an actual document.

## License

MIT. See `LICENSE`.
