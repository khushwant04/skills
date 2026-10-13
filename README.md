# skills

Agent skills. Each lives in `.kiro/skills/<name>/` with a `SKILL.md`.

| Skill | What it does |
|---|---|
| [`decision-compression`](.kiro/skills/decision-compression/) | Makes an agent output a decision-ready answer instead of a report. Answer-first, one recommendation, why-not contrast, calibrated uncertainty, risk-tiered approval. |

---

## decision-compression

**The shift:** not "make agents give shorter answers" — *make every agent turn complexity into a decision-ready object.*

```
10 agents → 100 actions → 10 notable events → 2 decisions → 1 clear recommendation each
```

**Before**
> I analyzed 14 emails, compared 3 vendors, checked the budget, and found several considerations…

**After**
> **Recommendation:** Approve Vendor B — high confidence
> **Why:** 23% cheaper · meets all must-haves · lowest migration risk
> **Main risk:** support quality unproven (2 references, both smaller than us)
> **Why not A?** Better support SLA, but ₹2.4L/yr more and needs a custom connector
> **You need to:** approve, or tell me to negotiate a 6-month out-clause first

### What it enforces

1. Answer before explanation — never open with background or process
2. Max 3 options, max 3 reasons
3. Always recommend one — a menu hands the work back
4. Always answer "why not the runner-up?" — contrast is what lets a human verify you
5. Separate observed / inferred / predicted
6. Qualitative uncertainty (confidence · evidence · impact if wrong · reversibility), not invented percentages
7. Name your own strongest counter-evidence
8. Risk tiers 1–5 — execute the routine, escalate the irreversible, stop asking about trivia
9. Progressive disclosure — Quick / Decision / Deep, chosen by stakes not by effort spent
10. One next action, always

### Files

| File | Read it when |
|---|---|
| `SKILL.md` | The operating protocol. Loads on activation. |
| `references/psychology.md` | You want the research behind each rule, with sources. |
| `references/decision-card.md` | You need the exact format for a specific case (7 worked examples). |
| `references/risk-tiers.md` | You need to decide whether to act or ask. |

### Research basis

Cognitive Load Theory and working-memory limits · the transient information effect · choice overload · decision fatigue · Klein's Recognition-Primed Decision model · automation bias and rubber-stamping in human-AI oversight · prior-knowledge tailoring.

The through-line across all of it: **more information does not produce better decisions.** Structure, prioritization, honest uncertainty, and selective context do. Full citations and a rule-to-finding mapping table in [`references/psychology.md`](.kiro/skills/decision-compression/references/psychology.md).

### Use it

Committed under `.kiro/skills/`, so any Kiro workspace with this repo picks it up automatically — or invoke directly with `/decision-compression`.

To inherit it in a custom agent, add to the agent's `resources`:

```json
"resources": ["skill://.kiro/skills/decision-compression/SKILL.md"]
```

To use it in another project, copy the skill folder into that workspace:

```bash
mkdir -p /path/to/project/.kiro/skills
cp -r .kiro/skills/decision-compression /path/to/project/.kiro/skills/
```

`SKILL.md` uses the standard Agent Skills layout (YAML front matter with `name` and `description`,
plus a `references/` folder), so the same folder can be dropped into other tools that read that
format, such as `.claude/skills/` for Claude Code.
