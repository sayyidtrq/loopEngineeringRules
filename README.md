# loop-engineering-rules

Claude Code rules for loop engineering in three modes. Built to keep results
verifiable, tokens low, and design/build/test tied to one written intent.

| Mode | Use when | Invoke |
|---|---|---|
| New product (CEO/CTO) | Building something new, all stages | `/loop-new-product <idea>` |
| FDE | Client/stakeholder work, demos, PM-tool tasks | `/loop-fde <client need>` |
| Dev ticket | Existing repo, Jira ticket + dev spec | `/loop-dev-ticket PROJ-123` |

## Layout (why it is split this way)
- `.claude/rules/loop-engineering-rule.md` - short core, always loaded. Keep it lean; every line costs tokens each session.
- `.claude/skills/*` - mode workflows. Only name + description load at session start; the body loads when invoked.
- `.claude/agents/*` - builder and verifier. Only their descriptions load until called.
- `templates/` - STATE.md and feature_list.json (AC -> test -> passes).

## Install
Per project:
```bash
cp -r .claude /path/to/your/project/ && cp -r templates /path/to/your/project/
```
Or for all projects: copy the contents of `.claude/` into `~/.claude/`.
Check what loads with `/context`, and tune the model and tool lists in `.claude/agents/`.

## Notes
- Jira access should be read-only; writes need your approval (rule section 7).
- Edit the iteration budgets to match your plan tier.
- Companion skills (RTK, Ponytail, Impeccable, PM skills): see [COMPANIONS.md](COMPANIONS.md).
