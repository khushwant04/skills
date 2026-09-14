# Decision Card: formats and worked examples

Load this when you need the exact shape for a specific situation.

---

## The canonical card (tier 3–4)

```
**Decision:** <the question, one line>

**Recommendation:** <one option> — <high | medium | low> confidence

**Why:**
- <reason that could flip the choice>
- <reason that could flip the choice>
- <reason that could flip the choice>

**Main risk:** <the strongest case against, one line>

**Alternatives:**
- <B> — <its genuine advantage>, but <why it loses>
- <Wait / do nothing> — <what it buys>, but <what it costs>

**You need to:** <one concrete action>
```

**Rules for filling it in**

- Drop any section that would be filler. An empty `Main risk` line is worse than no line — but if you genuinely see no risk, say `Main risk: none material — reversible in one command.`
- `Why` bullets must be *decision-changing*. "Well-documented API" is not a reason unless documentation was a criterion.
- Always include a do-nothing / wait alternative when delay is genuinely available. It's the option humans most often want and agents most often omit.
- Alternatives must state a **real** advantage. A strawman alternative is worse than omitting it — it manufactures false confidence.

---

## Uncertainty block (attach when stakes justify it)

Prefer this over an invented percentage.

```
Confidence: medium      (how sure I am of the recommendation)
Evidence:   thin        (strong | mixed | thin — quality of what I'm reasoning from)
If wrong:   medium      (blast radius of being wrong)
Reverse:    easy        (easy | costly | irreversible)
```

Four cheap words carry more usable signal than `87%`. A number implies a calibration you almost certainly don't have.

**When to include it:** tier 4–5 always; tier 3 when evidence is thin or the reader has no way to sanity-check you.

---

## Assumption block (attach when the recommendation is conditional)

```
**This holds only if:**
- <assumption that, if false, flips the recommendation>
- <assumption that, if false, flips the recommendation>
```

Only list assumptions that are **load-bearing**. "Assuming the vendor exists" is noise. "Assuming volume stays under 50k requests/month" is load-bearing if pricing tiers above that.

---

# Worked examples

## A. Vendor / procurement — tier 4

```
**Decision:** Approve Vendor B for the analytics contract?

**Recommendation:** Yes, approve B — high confidence

**Why:**
- 23% cheaper at our projected volume (₹8.2L vs ₹10.6L/yr)
- Only vendor meeting all 4 must-have requirements
- Lowest migration risk — native connector for our warehouse, no custom ETL

**Main risk:** Support quality is unproven. Two reference customers, both smaller than us.

**Alternatives:**
- Vendor A — established 24/7 support with SLA credits, but ₹2.4L/yr more and needs a custom connector (~3 weeks eng time)
- Wait for Q3 pricing — B has hinted at volume discounts, but delays the migration ~2 weeks past the reporting deadline

Confidence: high | Evidence: strong | If wrong: medium | Reverse: costly (12-mo term)

**You need to:** Approve B, or tell me to negotiate an out-clause at 6 months first.
```

Note what's absent: the vendor longlist, the feature matrix, the 14 emails, the evaluation methodology. All available on request. None of it changes this decision.

---

## B. Hiring — tier 4, judgment-heavy

```
**Decision:** Extend the offer to Candidate A?

**Recommendation:** Yes, A — medium confidence

**Why:**
- Only candidate with production ML infra experience at our scale
- Shipped a comparable migration end-to-end at their last role
- Available in 3 weeks; B needs 8

**Main risk:** Communication was the weakest part of A's loop. Two interviewers flagged terse, low-context updates — a real cost on a team this distributed.

**Why not B?** Clearly stronger communicator and better culture signal, but no infra depth — we'd be hiring a second person for that within 6 months.

**Why not keep searching?** Pipeline has been open 9 weeks with 2 finalists. Another cycle costs ~6 weeks and, based on the funnel, is unlikely to produce a candidate who beats A on the thing we're actually short on.

**This holds only if** infra depth really is the gap we're hiring for. If the priority has shifted toward team coordination, B wins and I'd change my recommendation.

**You need to:** Confirm the priority is infra depth. If yes, I'll draft the offer.
```

Note the assumption block doing real work: it hands the human the *one* judgment only they can make, instead of pretending the whole thing is analyzable.

---

## C. Incident / infra — tier 3, time-pressured → Quick mode

```
**Roll back to v2.14.** p99 latency tripled at 14:02, exactly at deploy. Rollback is one command, ~40s, zero data risk.

Alternative: ship a forward fix for the N+1 in the new query path — ~25 min, and we stay degraded meanwhile.

**You need to:** Say go and I'll roll back.
```

Three lines. Tier 3 but time-critical, so Quick mode. Nobody wants a confidence table during an incident.

---

## D. Routine batch work — tier 1, do not ask

**Wrong:**
> I found 14 emails that appear to be duplicates. Should I archive them? Here's the list…

**Right:**
> Archived 14 duplicate emails. Inbox is clear.

Reversible, zero blast radius. Asking here is not caution — it's spending the human's approval budget on nothing, and it trains them to approve without reading.

---

## E. Multi-agent rollup — the compression that matters most

**Wrong:**
> The research agent reviewed 40 sources, the finance agent modeled 3 scenarios, the calendar agent found 6 conflicts, the email agent triaged 82 messages…

**Right:**

```
**2 things need you today.**

1. **Sign the Acme renewal** (₹12L, expires Friday) — recommend yes, terms improved 8% vs last year. Irreversible for 12 months. → `Approve` / `Review terms`
2. **Thursday 3pm double-booked** — recommend moving the internal sync, keeping the client call. → `Confirm` / `Pick differently`

Handled without you: 82 emails triaged, 6 minor calendar conflicts resolved, Q3 draft updated.
```

This is the shape the whole protocol exists for:

```
10 agents → 100 actions → 10 notable events → 2 decisions → 1 clear recommendation each
```

The "handled without you" line is important — it's one line of accountability, not a report. It proves work happened without making the human audit it.

---

## F. Research / open question — no decision exists yet

When there's genuinely nothing to decide, don't manufacture a card.

```
**Short answer:** Postgres row-level security will work for this, with one caveat.

**The caveat:** it doesn't apply to the table owner by default, so your migration user bypasses every policy unless you set `FORCE ROW LEVEL SECURITY`.

Want the policy examples, or the alternative (application-layer filtering) compared?
```

Answer, the one thing that will bite them, offer of the next layer. Forcing a "Decision / Recommendation / Alternatives" scaffold onto a factual question is itself extraneous load.

---

## G. Disagreeing with the user — surface it, don't bury it

```
**I'd recommend against the approach you described** — medium confidence, and I might be missing context.

**Why:** Caching at the CDN layer won't help here; the responses are per-user authenticated, so hit rate will be near zero.

**What I'd do instead:** Cache the expensive aggregate query in Redis keyed by user + hour. Same latency win, actually cacheable.

**Where I could be wrong:** If most traffic is anonymous, CDN caching is the better call and my read of the traffic mix is off.

**You need to:** Tell me the anonymous/authenticated split, or say proceed with your original plan.
```

Disagreement stated in line 1, not softened into paragraph 3. Then a genuine escape hatch — this is what stops the human from over-trusting you.

---

## Quick reference

| Situation | Shape |
|---|---|
| Reversible, trivial | One line, past tense, already done |
| Reversible, notable | One line + what you did + why |
| Real choice, calm | Full card |
| Real choice, urgent | Recommendation + 1 reason + 1 alternative + action |
| Irreversible | Full card + explicit irreversibility statement + no default |
| Many agents, many actions | Rollup: N decisions, then one "handled" line |
| Pure question | Answer + the one gotcha + offer of depth |
| You disagree | Disagreement first, then your alternative, then how you could be wrong |
