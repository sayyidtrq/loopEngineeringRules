# Loop Engineering Rule (core, applies to every mode)

Goal: ship faster with a verifiable result, spend tokens deliberately, keep
design, build and test serving ONE written intent.

## 1. Intent contract (before any loop)
- Work from a written spec with numbered acceptance criteria: AC-1, AC-2, ...
  Each AC is an observable outcome ("after checkout the order ID is shown"),
  not an implementation detail.
- Definition of Done (DoD) is external and machine-checkable: AC tests pass,
  lint/typecheck clean, diff inside scope. "The agent says it's done" is never DoD.
- Ambiguous spec? Ask the human once, up front. Do not guess inside the loop.

## 2. Verifier first
- Verification (tests/checks) is derived from the AC, written or confirmed
  BEFORE implementation, and shown failing (red baseline).
- BUILDER may not edit the spec or the AC tests. If a test looks wrong,
  stop and report; do not bend it to go green.

## 3. Roles (two by default)
- BUILDER (.claude/agents/builder.md): one AC / feature slice per iteration.
- VERIFIER (.claude/agents/verifier.md): fresh context, read-only, sees spec +
  diff + test output, never the builder's reasoning.
- Deterministic checks (tests, lint, diff size) run before any LLM review.
- Add a third role only for a recurring failure the verifier misses; run it once at the end.

## 4. State (memory lives on disk, not in the conversation)
- Read STATE.md + feature_list.json at the start of every iteration; update at the end.
- Traceability: every AC maps to a test and a feature_list entry (templates/).
- One small commit per passing slice.

## 5. Budget and stop rules
- Set before starting: max iterations (default 10), max time, no-progress stop
  (2 iterations with no new passing AC => stop and escalate).
- Same failure twice => stop and escalate with evidence. Never retry blindly.
- Discovery and design are interactive, not looped. Loop only well-defined execution.

## 6. Token rules
- Fresh context per iteration; re-read STATE.md instead of re-exploring.
- Read by path and line range; delegate wide reading to a read-only subagent
  that returns a short summary.
- Use the cheaper model for triage and verification where quality holds.
- Do not fan out the verifier into panels without evidence it finds more.

## 7. Human gates
- Human approves: spec/AC, design (new products), final diff before merge/demo.
- Loop produces evidence (test output, diff, trace table); the human gives the verdict.
- Writes to external systems (Jira comments/transitions, PRs, messages) need
  explicit approval. Jira access is read-only by default.

## 8. Git hygiene
- Small, descriptive commits. Reference the ticket ID when one exists.
- Never add a Co-Authored-By trailer or any Claude/AI attribution to commits.

## 9. Companion skills (details + install: COMPANIONS.md)
- RTK compresses Bash output (tests, git, logs). Run tests/lint via Bash so it applies.
  The verifier must get raw output when evidence is unclear (`rtk proxy <cmd>`).
- Ponytail (builder only): reuse/stdlib before new code. It never overrides an AC:
  if an AC needs it, build it.
- Impeccable: only for UI work. `/impeccable shape` before building, `/impeccable audit`
  as verifier evidence, `/impeccable polish` last.
- PM skills (new-product, FDE): their PRD/story output must be converted into the
  numbered AC list. The AC list is the contract, not the PRD prose.
- Install companions per mode at project scope, not all globally. Each adds context.
