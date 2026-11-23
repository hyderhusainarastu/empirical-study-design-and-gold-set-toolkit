# empirical-study-design-and-gold-set-toolkit

An Agent Skill (plain Markdown) for designing empirical evaluations and building gold-standard annotation sets.

## Using this in your project

- Use the skill when the task is to plan a study, evaluation, benchmark or reference dataset: decide which claims are testable, audit validity threats, size a sample, or build a human-annotated gold set.
- Invoke: load `SKILL.md` (native skill via `./install.sh`) or paste `PROMPT.md` into a chat model.
- Follow the order in `SKILL.md`: classify claims, pick a scope tier, work the design space, audit validity threats, run the five-step statistical chain (estimand, design, variance assumptions, power/sensitivity, sample size), then type and govern the gold set.
- Never give a sample size without its estimand, design and variance assumptions attached.
- Never adjudicate genuine expert disagreement into a single label; preserve it.
- Never let the builder of the system under test annotate its gold set.
- Load detail on demand from `references/`; `examples/worked-example-synthetic.md` shows a full run on invented data.
- The skill writes nothing by itself. Any plan or gold-set document goes where the user says.
- No scripts are bundled and no network is used.

## Working on this repo

- Setup: none (Markdown only).
- Test: `./test_install.sh` (offline; uses temporary HOME and project directories).
- Keep `SKILL.md` frontmatter `description` at 300 characters or fewer.
- Do not add real participant data or unpublished text to `examples/`; keep it synthetic.
