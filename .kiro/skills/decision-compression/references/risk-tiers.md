# Risk tiers: when to act, when to ask

The purpose of tiering is **not** to be careful. It is to make the human's attention expensive again, so that when you do ask, they actually read it.

An agent that asks about everything and an agent that asks about nothing fail identically: the human stops evaluating.

---

## The two axes

Everything reduces to these. Score both, then read the tier off the grid.

**Reversibility** — how hard to undo?
- `easy` — one command, no side effects, no one saw it
- `costly` — undoable, but with real cost (time, money, credibility, re-work)
- `irreversible` — cannot be undone (money sent, message delivered, data deleted, contract signed, thing published)

**Blast radius** — who is affected if this is wrong?
- `self` — only the agent's own scratch work
- `user` — only this person's data/time
- `team` — colleagues, shared systems
- `external` — customers, public, counterparties, regulators

---

## The grid

|  | self | user | team | external |
|---|---|---|---|---|
| **easy** | 1 | 1 | 2 | 3 |
| **costly** | 2 | 3 | 4 | 4 |
| **irreversible** | 3 | 4 | 5 | 5 |

---

## Tier behaviors

### Tier 1 — Routine → **execute silently**

Reversible, contained. Do it. Do not narrate.

Formatting cache files, re-running a failed read, sorting, deduping, drafting into a scratch buffer, retrying a transient error, reading anything.

> Do not say "I'm going to check the config file now." Just check it.

---

### Tier 2 — Notable → **execute, then inform in one line**

Reversible, but the human would want to know it happened.

Renaming files they'll look for, archiving mail, rescheduling an internal meeting, installing a dependency, creating a branch, reformatting a shared doc.

> "Rescheduled the Tuesday sync to Wednesday 11am — only slot all 5 people had free."

One line. Past tense. No approval theater.

---

### Tier 3 — Judgment → **recommend + ask**

Either costly to reverse, or dependent on preference you cannot infer.

Choosing an architecture, picking between two viable libraries, deciding tone in a reply to someone they know, rolling back production, changing a schema, altering someone else's work.

Full Decision Card. **Still recommend one option** — asking is not an excuse to hand back a menu.

---

### Tier 4 — High-impact → **require explicit approval**

Large commitment, external exposure, or expensive to unwind.

Spending real money, signing, hiring/firing, anything customer-visible, security or access changes, data migrations, public commitments.

Card + uncertainty block + assumptions. Do not proceed on ambiguous assent ("sounds good", "ok"). Get an unambiguous yes to a stated action.

---

### Tier 5 — Irreversible → **force a deliberate choice**

Cannot be undone, and affects others.

Sending email/messages externally, deleting data without backup, force-pushing over history, transferring funds, publishing, submitting filings, revoking access others depend on.

Requirements:
1. **State the irreversibility explicitly.** "This cannot be undone. Once sent, it's sent."
2. **No default and no pre-selected option.** The human must supply the choice, not confirm yours.
3. **Name what specifically happens**, with the actual values: recipients, amount, records, target.
4. **Never batch** tier 5 actions behind one approval. Each one gets its own.
5. **Ambiguous assent is not approval.**

```
⚠️ **Irreversible.** This sends the contract to legal@acme.com and 3 others, and
cannot be recalled.

Recommend sending — terms match what you approved Tuesday, 8% better than last year.

Main risk: clause 7 (auto-renewal) wasn't in the version you reviewed.

**Confirm explicitly:** "send it" — or tell me to hold while you read clause 7.
```

---

## Escalation and de-escalation rules

**Escalate one tier when:**
- You're genuinely unsure of the blast radius
- The action touches money, identity, access, or anything legal
- The user has previously corrected you on something similar
- You're operating on stale information

**Escalate to tier 5 regardless of the grid when** the action is externally visible and cannot be recalled. Reversibility beats blast radius here.

**De-escalate one tier when:**
- The user explicitly delegated this class of decision ("stop asking about branch names")
- You're inside an approved plan and this is a step the human already signed off on
- A trivially cheap undo exists and you'll state it ("reverted with one command if wrong")

**Never de-escalate below 3** for anything irreversible, no matter how much was delegated.

---

## The two failure modes

| Over-asking | Under-asking |
|---|---|
| Approval requests on reversible trivia | Silent irreversible actions |
| Batching unlike things into one "approve all?" | Treating ambiguous assent as consent |
| Confirming your own suggestion back to the user | Assuming a plan approval covers new tier-4 steps |
| Asking, then not recommending | Recommending so strongly there's no real choice |
| **Result:** reviewer fatigue → rubber-stamping | **Result:** unrecoverable damage |

The first is more common and feels safe. It isn't — it's how you consume the attention you'll need for the decision that actually matters. See `psychology.md` §4 and §7.

---

## One-line test

> **Would a competent colleague be annoyed that I asked — or alarmed that I didn't?**

Annoyed → tier 1–2, just do it.
Alarmed → tier 4–5, ask properly.
Genuinely unclear → tier 3, recommend and ask.
