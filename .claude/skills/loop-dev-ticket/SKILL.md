---
name: loop-dev-ticket
description: Loop-engineering workflow for daily developer work on an EXISTING codebase from a Jira ticket with a dev spec - understand, develop, test. Use whenever the user gives a ticket key or ticket text, says implement/fix this ticket, bugfix, or change in an existing repo, even if they do not say "loop".
---

# Dev ticket workflow (brownfield)

Follows .claude/rules/loop-engineering-rule.md. The ticket/dev spec is the contract.
Brownfield rule: match existing architecture and conventions; smallest correct diff.

## 1. Understand (interactive, not looped)
- Read the ticket (and linked dev spec) via the Jira tool, read-only.
- Write the AC list with ids. If the ticket has no clear AC, derive them and ask the
  human to confirm. List ambiguities as questions; ask once.
- Delegate codebase recon to a read-only subagent: relevant files, existing patterns,
  existing tests, how to run them. It returns a short summary only.
- Create STATE.md and feature_list.json (AC -> test).
- Short plan: files to touch, risk, what is explicitly out of scope. Confirm if non-trivial.

## 2. Develop (loop)
- Write/confirm tests from the AC first, run them, show red. Use existing test style.
- Per iteration: builder implements one AC -> verifier checks -> commit
  (message includes ticket key; no Co-Authored-By or AI attribution).
- Run the existing suite for regressions, not only new tests.

## 3. Test and finish
- Full relevant suite + lint/typecheck green; diff inside planned scope.
- Output a PR-ready summary: ticket key, AC trace table, test evidence, risks, out-of-scope notes.
- Offer a Jira comment draft. Post it or transition the ticket only after the human approves.

## Token notes
Never read the whole repo. Prefer subagent summaries and path+line reads.
Stop after 2 iterations without a newly passing AC and report what blocks you.

## Companion skills (see COMPANIONS.md)
- RTK on (biggest win here: test and git output across many iterations).
- Builder may use Ponytail, which fits brownfield: reuse existing code before adding new.
- Only if the ticket touches UI: `/impeccable audit` output goes to the verifier as evidence;
  follow the existing design system, do not redesign.
- PM skills are optional here; the dev spec already exists.
