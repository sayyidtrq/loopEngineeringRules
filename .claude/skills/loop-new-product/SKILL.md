---
name: loop-new-product
description: Loop-engineering workflow for building a NEW product or feature from scratch (CEO/CTO mode) across all stages - brief, spec, design, slicing, build, integration, release. Use whenever the user wants to start something new, greenfield, "build X from zero", or plan a product end to end, even if they do not say "loop".
---

# New product workflow (greenfield)

Follows .claude/rules/loop-engineering-rule.md. Loops only start after Gate 2.
Stages 1-3 are interactive; do not loop them.

## Stages
1. **Brief** - problem, user, success metric, constraints, non-goals. One page.
2. **Spec + AC** - numbered ACs, observable outcomes, edge cases. Write the
   verifier plan (how each AC will be checked) alongside it.
   **GATE 1: human approves spec.**
3. **Design** - architecture, data model, key decisions as short ADRs (decision,
   why, alternatives). Every design element must trace to an AC; remove what does not.
   **GATE 2: human approves design.**
4. **Initialize** - create STATE.md, feature_list.json (every AC -> test, passes=false),
   init/run script that starts the app and runs tests, repo + first commit.
5. **Walking skeleton** - thinnest end-to-end slice (UI -> API -> data) that runs and has one passing test.
6. **Loop per slice** - for each AC/slice: tests from AC (red) -> builder -> verifier -> commit.
   One slice per iteration. Respect budget and no-progress stop.
7. **Integration** - end-to-end tests of the real flows from the spec, not only unit tests.
8. **Release readiness** - all AC passes=true, DoD met, known gaps listed.
   **GATE 3: human reviews diff + evidence pack.**

## Evidence pack (output of stage 8)
AC trace table (AC -> test -> pass), test output, how to run, known gaps/risks.

## Token notes
Keep the design and spec docs short; the loop re-reads them every iteration.
Use the cheaper model for verification. Read by path and line range.

## Companion skills (see COMPANIONS.md)
- Stage 1-2: pm-skills `/discover`, `/strategy`, `/north-star`, `/write-prd`, `/pre-mortem`.
  Convert the PRD into numbered ACs before Gate 1; the ACs are the contract.
- Stage 3 (UI products): `/impeccable shape`, then `/impeccable teach` or `init` once for PRODUCT.md/DESIGN.md.
- Stage 6: builder may use Ponytail; UI slices get `/impeccable audit` output passed to the verifier.
- Stage 8: `/impeccable polish` on UI, `/plan-launch` for launch plan.
- RTK on for the whole build.
