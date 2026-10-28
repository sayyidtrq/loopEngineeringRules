# Companion skills and tools

Third-party. Not vendored here: review each repo before installing (several install
hooks that run on your machine), pin versions, and re-check they still work after updates.
Install per project and per mode. Every skill/plugin adds descriptions to session start;
use `/context` and `/usage` to see what each one costs you.

| Tool | Modes | Role in the loop |
|---|---|---|
| RTK | all | Compresses Bash output (git, tests, logs) before it enters context |
| Ponytail | builder, all modes | Minimal-code discipline: reuse stdlib/existing code before writing new |
| Impeccable | UI work only | Design shape -> audit -> polish for frontend tasks |
| PM skills | new-product, FDE | Discovery, strategy, PRD, stories, launch; feeds the AC list |

## RTK (Rust Token Killer) - github.com/rtk-ai/rtk
- Install: `brew install rtk` (or `cargo install --git https://github.com/rtk-ai/rtk`).
  Name collision: another crate called "rtk" exists. `rtk gain` failing means wrong package.
- Setup: `rtk init -g`, restart Claude Code. Check: `rtk gain`, `rtk init --show`.
- A hook rewrites Bash commands (git status -> rtk git status). It only affects Bash calls;
  built-in Read/Grep/Glob bypass it. Prefer shell commands or `rtk read` / `rtk grep` for large output.
- Verifier caution: compressed test output shows failures only. If evidence is unclear,
  rerun raw with `rtk proxy <command>`.
- Track savings: `rtk gain`, `rtk discover`.

## Ponytail - github.com/DietrichGebert/ponytail
- Install in Claude Code, as two separate prompts:
  `/plugin marketplace add DietrichGebert/ponytail` then `/plugin install ponytail@ponytail`.
  Commands: `/ponytail`, `/ponytail-review`, `/ponytail-audit`, `/ponytail-help`. Node needed for hooks.
- Savings claims vary: an independent JetBrains test of 80 paired tasks measured smaller
  gains than advertised, and only where there was room to over-build. Measure on your own tasks.
- Rule here: AC tests are the floor. Ponytail may shrink the implementation, never the spec.
- Known issue at time of writing: slash-command mode switching may not register in Claude Code
  (repo issue #584). Check the repo for status.

## Impeccable - github.com/pbakaus/impeccable
- Install: `/plugin marketplace add pbakaus/impeccable` then install from `/plugin`, or
  `npx skills add https://github.com/pbakaus/impeccable --skill impeccable`.
- First time per project: `/impeccable init` (older docs call it `teach`) writes PRODUCT.md and DESIGN.md.
- Use: `shape` (plan UX before code), `critique`, `audit` (a11y, performance, responsive),
  `polish`, `distill`. It also ships deterministic detector rules: cheap evidence for the verifier.
- Brownfield: tell it to follow the existing design system.

## PM skills - github.com/phuryn/pm-skills
- Add marketplace: `claude plugin marketplace add phuryn/pm-skills`.
- Install only what you need, e.g. new-product: `pm-product-discovery`, `pm-product-strategy`,
  `pm-execution`, `pm-market-research`. FDE: `pm-execution`, `pm-toolkit`.
  Format: `claude plugin install pm-execution@pm-skills`.
- Commands: `/discover`, `/strategy`, `/north-star`, `/write-prd`, `/plan-launch`, `/pre-mortem`, `/sprint`.
- Alternative: Anthropic's official product-management plugin (roadmap, specs, research synthesis).
- Always convert the output into numbered ACs (templates/feature_list.json). Prose PRDs are not testable.
