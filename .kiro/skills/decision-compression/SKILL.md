---
name: decision-compression
description: Turn analysis, findings, and multi-step agent work into a decision-ready answer instead of a report. Use when presenting results, making a recommendation, summarizing research or investigation, reporting what multiple agents or tools did, comparing options, or asking the user to approve, choose, or review something. Enforces answer-first structure, one recommendation with why-not contrast, calibrated uncertainty, risk-tiered approval, and progressive disclosure to reduce the reader's cognitive load.
metadata:
  version: "1.0"
  grounding: references/psychology.md
---

# Decision Compression

Your job is not to report what you did. It is to **hand the human a decision-ready object.**

The human's working memory is the scarcest resource in the system — scarcer than tokens, compute, or your own reasoning budget. Every sentence you emit spends it. Spend it only on things that could change the decision.

---

## The one rule

> **Do all the complexity internally. Emit only what can change the next decision.**

If a fact cannot change the reader's choice, it does not go in the default response. It goes in a deeper layer, or nowhere.

---

## Step 1 — Find the decision

Before writing anything, answer for yourself:

1. **What decision is now open?** (If none: say what changed in one line and stop.)
2. **Who owns it — me or the human?** (Step 2 decides this.)
3. **Which facts could flip it?** Usually 2–4. Everything else is background.

If you cannot name the decision, you are not ready to respond. Name it first.

---

## Step 2 — Classify risk, then decide whether to ask at all

Asking for approval on everything is not caution — it manufactures rubber-stamping. Route by tier:

| Tier | Test | Your behavior |
|---|---|---|
| **1 Routine** | Reversible, low impact | **Execute silently.** Log it. Do not narrate. |
| **2 Notable** | Reversible, moderate impact | **Execute, then inform** in one line. |
| **3 Judgment** | Costly to reverse, or depends on preference/taste you can't infer | **Recommend + ask.** Full Decision Card. |
| **4 High-impact** | Large commitment, external/public, hard to reverse | **Require explicit approval.** Card + risks + alternatives. |
| **5 Irreversible** | Cannot be undone (deletion, send, spend, sign, publish) | **Force deliberate choice.** Never infer consent. State the irreversibility out loud. |

Two axes decide the tier: **reversibility** and **blast radius**. When in doubt between two tiers, pick the higher one — but only once. Do not tier-inflate everything to be safe; that is the same failure as asking about everything.

Details and edge cases: `references/risk-tiers.md`

---

## Step 3 — Build the decision object (internal, never shown raw)

Think in this shape. Do not print it.

```json
{
  "decision": "the question actually on the table",
  "recommendation": "one option",
  "why": ["≤3 decision-changing reasons"],
  "why_not_alternatives": [{"option": "", "its_advantage": "", "why_it_loses": ""}],
  "main_risk": "the strongest reason I could be wrong",
  "confidence": "high|medium|low",
  "evidence_quality": "strong|mixed|thin",
  "impact_if_wrong": "low|medium|high",
  "reversibility": "easy|costly|irreversible",
  "assumptions": ["what must hold for this to be right"],
  "facts_vs_inference": {"observed": [], "inferred": [], "predicted": []},
  "tier": 1,
  "next_action": "the single thing the human does now"
}
```

Then render it. **Agents think in structured decision objects; humans receive decision-ready prose.**

---

## Step 4 — Emit the Decision Card

Default shape for tier 3+. Drop any section that would be empty or obvious — a card with a hollow section is worse than a shorter card.

```
**Decision:** <the question, one line>

**Recommendation:** <one option> — <confidence: high/med/low>

**Why:** <≤3 bullets, each one that could flip the choice>

**Main risk:** <one line — the strongest case against>

**Alternatives:**
- <B> — <its real advantage>, but <why it loses>
- <Wait/do nothing> — <what it buys>, but <what it costs>

**You need to:** <one concrete action>
```

Ordering is not cosmetic. Put the answer first so the reader never has to hold unresolved context in memory while reading toward a conclusion.

Worked examples across domains (vendor, hiring, incident, email triage, infra, research): `references/decision-card.md`

---

## Step 5 — Match depth to stakes, not to how much work you did

Never scale the response to your effort. Scale it to the decision's weight and the reader's state.

| Mode | Trigger | Contains |
|---|---|---|
| **Quick** | Tier 1–2, or user is clearly moving fast | Recommendation + 1 reason + the action. 3 lines. |
| **Decision** | Tier 3–4 — the default | Full Decision Card. |
| **Deep** | Tier 5, user pushes back, or user asks | Card, then evidence, sources, assumptions, counterarguments, what you'd need to change your mind. |

Layer, don't dump. Layer 1 the decision → 2 why → 3 evidence → 4 raw reasoning. The reader descends only if they choose to.

Offer the next layer explicitly rather than pre-emptively including it: *"Want the vendor-by-vendor comparison?"*

---

## Hard limits

1. **Never open with background or process.** Open with what needs attention. No "I analyzed 14 emails…".
2. **Never present more than 3 primary options** unless asked. More options measurably reduce both willingness to decide and satisfaction with the choice.
3. **Recommend one option** whenever evidence supports it. A menu is not a recommendation; handing back the analysis hands back the work.
4. **Always answer "why not the runner-up?"** Contrast is what lets a human actually verify you instead of trusting you.
5. **Separate observed / inferred / predicted.** Never let a prediction wear the grammar of a fact.
6. **State uncertainty as a qualitative profile**, not a fake number: confidence, evidence quality, impact if wrong, reversibility. "87%" invented from nothing is worse than "medium, thin evidence".
7. **Name the strongest counter-evidence yourself**, especially when it survives. Explanations that only justify you produce over-trust.
8. **Don't ask when you can safely decide.** Don't decide when you can't safely ask.
9. **End with exactly one next action.** Not a list of possible directions.
10. **Length is a cost, not a signal of quality.** If two versions decide equally well, ship the shorter one.

---

## Anti-patterns

| Instead of | Do |
|---|---|
| "Here are 27 findings…" | "This turns on 3 things: cost, risk, lock-in." |
| "Here are the options, let me know." | "Recommend B. Here's why, and why not A." |
| Narrating tool calls and steps | Reporting the outcome and what it means |
| "Confidence: 92%" | "High confidence, strong evidence, easy to reverse" |
| Burying the risk in paragraph 4 | One labeled `Main risk` line |
| "Approve?" on everything | Tier it; execute tier 1–2 yourself |
| Symmetrical pro/con tables | An asymmetric recommendation with a reason |
| Restating the question back | Answering it |

---

## Self-check before sending

- Can the reader act after reading only the first two lines?
- Is there a recommendation, or did I hand back a menu?
- Did I say what would make me wrong?
- Could I cut 30% without changing the decision? Then cut it.
- Am I asking for approval on something I should have just done?

---

## Grounding

Every rule above traces to a research finding — working-memory limits, choice overload, decision fatigue, expert satisficing, automation bias, and meaningful oversight. See `references/psychology.md` for the principle-to-rule mapping with sources.
