---
name: loop-fde
description: Loop-engineering workflow for forward-deployed-engineer work - turn a client or CEO need into PM-tool tasks, design, implement and test a thin working slice, then produce a demo and evidence pack. Use when the user is working with a client, stakeholder demo, prototype, proof of concept, or says FDE, even if they do not say "loop".
---

# FDE workflow (client-facing, demo-driven)

Follows .claude/rules/loop-engineering-rule.md. The audience is a client/CEO,
so "done" has two levels. Always say which one you are delivering.

- **Demo-ready DoD**: the agreed demo scenario runs end to end, checked by a script or test.
- **Production-ready DoD**: full AC tests, lint, error handling, no demo-only shortcuts.
Never present a demo-ready slice as production-ready.

## Steps
1. **Capture the need** - restate the client's problem and desired outcome in your own
   words; list assumptions and open questions; get the human to confirm.
2. **Write the demo scenario** - 3-7 steps a client would watch. This becomes AC-1..n
   and the demo script (acceptance test) before any code.
3. **Create tasks** - draft Jira/PM tasks (one per AC, outcome-phrased, with AC ids).
   Show drafts to the human; create them only after approval.
4. **Design the thinnest vertical slice** that makes the scenario real. Mark anything
   mocked or hard-coded in STATE.md under "Decisions / invariants".
5. **Time-boxed loop** - set a smaller budget than usual (e.g. max 6 iterations per slice).
   Builder -> verifier -> commit. Stop and escalate on no progress rather than polishing.
6. **Demo prep** - run the demo script, capture output/screenshots, write the evidence pack.
7. **Feedback** - client feedback becomes NEW or amended ACs with new ids (keep the old
   ones). Update the spec first, then tests, then code. Never change a test to fit feedback silently.

## Evidence pack
What was asked, what is shown, AC trace table, how to run it, what is mocked,
known gaps, proposed next slice and its ACs.

## Companion skills (see COMPANIONS.md)
- Step 1-3: pm-skills `/write-prd` or user-story skills to structure the need; convert to
  numbered ACs and the demo script. Draft Jira tasks from the ACs.
- Step 4-5: UI demos use `/impeccable shape` then `/impeccable audit` (evidence for the verifier).
  Builder may use Ponytail to keep the slice thin. Never let it cut an AC.
- Step 6: pm-skills release-notes / stakeholder skills for the client summary; `/impeccable polish` last.
- RTK on.
