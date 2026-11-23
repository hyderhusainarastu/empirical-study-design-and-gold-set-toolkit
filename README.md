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

## Works with

| Surface | How | Status |
|---|---|---|
| Claude Code | native skill (`./install.sh --claude`) | not tested |
| Codex | native skill via `.agents/skills` (`./install.sh --agents`) | not tested |
| Gemini CLI | native skill via `.agents/skills`, pointer in `GEMINI.md` | not tested |
| Cursor | native skill via `.agents/skills`, reads `AGENTS.md` | not tested |
| Copilot | pointer to `AGENTS.md` (`./install.sh --copilot`) | not tested |
| ChatGPT / Claude.ai / Gemini (chat) | prompt (`PROMPT.md`) | not tested |

## Quick start

```sh
git clone https://github.com/hyderhusainarastu/empirical-study-design-and-gold-set-toolkit
cd empirical-study-design-and-gold-set-toolkit
./install.sh --claude              # ~/.claude/skills/<name>
./install.sh --agents --project .  # .agents/skills (Codex, Cursor, Gemini CLI)
./install.sh --copilot --project . # pointer block for Copilot
```

Run `./install.sh -h` for all options (`--copy`, `--dry-run`, `--uninstall`). It never overwrites paths it does not own.

For a chat model with no skill support, paste `PROMPT.md`, or use this short version and then describe your study:

```text
Act as a research-methods assistant. For my study: (1) classify each claim as
testable or interpretive; (2) pick a scope tier; (3) audit validity threats with
detection, mitigation and residual risk; (4) walk estimand -> design -> variance
assumptions -> power -> sample size, and refuse to give a number if a step is
missing; (5) type each gold-set construct and keep expert disagreement as data.
Ask me for missing inputs; do not invent them.
```

`SKILL.md` is also a complete methodology document you can read and apply by hand. No scripts are bundled beyond the installer; the skill is a planning methodology, not a runnable tool.

## Package contents

```
SKILL.md                                    the complete methodology (start here)
references/design-space-catalog.md          full option tables for every design dimension
references/validity-threat-catalog.md       22-item generalized validity-threat catalog
references/gold-set-construct-typing.md     8 worked construct-typing examples, all 6 types
references/gold-set-governance-checklist.md the full 17-obligation gold-set checklist
examples/worked-example-synthetic.md        a complete synthetic walkthrough, start to finish
AGENTS.md, PROMPT.md                        agent instructions and paste-in prompt
install.sh, test_install.sh                 installer and its offline test
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

## Limits

Methodology only: it does not compute power for you or replace a statistician or an ethics review. The install status above is "not tested" until each surface is run.

## Related

- [pre-submission-manuscript-audit](https://github.com/hyderhusainarastu/pre-submission-manuscript-audit)
- [adversarial-peer-review-role](https://github.com/hyderhusainarastu/adversarial-peer-review-role)
- [llm-routing-and-judge-eval-harness-pattern](https://github.com/hyderhusainarastu/llm-routing-and-judge-eval-harness-pattern)

## Keywords

study design, power analysis, sample size, gold standard, annotation, inter-annotator agreement, validity threats, benchmark, LLM evaluation, data leakage.

---
Part of palimnote-skills - more at https://github.com/hyderhusainarastu
