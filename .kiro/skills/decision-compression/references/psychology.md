# Why this works: the psychology behind each rule

Read this once. You will not need it again — the rules in `SKILL.md` encode it.

*Content on this page was rephrased and summarized for compliance with source licensing restrictions.*

---

## 1. Working memory is the bottleneck, and you are spending it

**Finding.** Cognitive Load Theory (Sweller) holds that working memory can hold and manipulate only a small number of elements at once, and that this ceiling is the constraint on comprehension and learning — not motivation or intelligence. Load beyond capacity degrades performance ([Springer, *Instructional Science*](https://link.springer.com/article/10.1007/s11251-009-9110-0); [AMEE Guide No. 86 on CLT in medical education](https://www.researchgate.net/publication/260523777_Cognitive_Load_Theory_Implications_for_medical_education_AMEE_Guide_No_86)).

CLT splits load into three kinds:

| Type | What it is | Your lever |
|---|---|---|
| **Intrinsic** | Irreducible difficulty of the decision itself | Can't remove — but you can chunk it |
| **Extraneous** | Load created by *how* it's presented | **This is entirely yours. Kill it.** |
| **Germane** | Effort that actually builds understanding | Protect this |

Most verbose agent output is pure extraneous load: process narration, restated context, symmetrical option tables, hedging. It adds difficulty without adding decision quality.

**Capacity number.** Miller's classic 7±2 has been revised downward; contemporary estimates of simultaneously held chunks cluster around four. Holding information also *competes* with processing it — higher processing load directly lowers memory performance ([the cognitive load effect in working memory](https://www.researchgate.net/publication/367290155_The_cognitive_load_effect_in_working_memory_Refreshing_the_empirical_landscape_removing_outdated_explanations); [overview of capacity limits](https://www.alliedacademies.org/articles/cognitive-load-and-multitasking-understanding-the-limits-of-mental-processing.pdf)).

→ **Rules 1, 2, 10** and the "≤3 reasons / ≤3 options" caps. Not stylistic preference — a capacity budget.

---

## 2. Answer first, because context held in suspense decays

**Finding.** The *transient information effect*: information that passes before the reader can process it produces worse outcomes than information presented in a stable, non-transient form ([Springer, *Educational Psychology Review*, 2026](https://link.springer.com/article/10.1007/s10648-026-10132-9)).

Applied to your output: when the conclusion comes last, the reader must hold every intermediate finding in working memory *without knowing which ones matter*. They are paying full price for facts that turn out to be irrelevant. Leading with the recommendation makes every subsequent fact interpretable on arrival — the reader knows what it's evidence *for*.

→ **Step 4's fixed ordering** and **Rule 1**.

---

## 3. More options make people decide worse, and sometimes not at all

**Finding.** Choice overload: past a modest number of alternatives, both the likelihood of choosing at all and satisfaction with the chosen option decline. The relationship between choice-set size and satisfaction is an inverted U, not a rising line ([arXiv review](https://arxiv.org/html/2412.12721v3); [Frontiers in Psychology, 2024](https://www.frontiersin.org/journals/psychology/articles/10.3389/fpsyg.2024.1290359/full); [Chernev et al. meta-analysis](https://www.researchgate.net/publication/48210291_Can_There_Ever_be_Too_Many_Options_A_Meta-analytic_Review_of_Choice_Overload)).

The effect is moderated, not universal — it bites hardest when task difficulty is high, the options are hard to compare, and the chooser has no clear pre-existing preference. **That is exactly the situation an agent hands a human.**

The healthcare framing is blunt about the consequence: excessive options drive decision paralysis, and reducing them is a service to the decider ([*HALM Journal*](https://www.physicianleaders.org/articles/doi/10.55834/halmj.5000639616)).

→ **Rule 2** (≤3 options) and **Rule 3** (recommend one).

---

## 4. Deciding depletes; every trivial ask taxes the important ones

**Finding.** Decision fatigue is a real degradation pattern with identifiable decisional, self-regulatory, and situational antecedents, showing up behaviorally, cognitively, and physiologically ([*Decision Fatigue: A Conceptual Analysis*, PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC6119549/)).

Consequence for agent design: approval requests share one budget. Every "Confirm?" on a reversible triviality is drawn from the same pool as the ₹12L contract approval later that day. An agent that asks about everything doesn't just annoy — it measurably degrades the human's performance on the decisions that mattered.

→ **Step 2's tiering** and **Rule 8**.

---

## 5. Experts don't want a comparison matrix — they want a candidate to evaluate

**Finding.** Klein's Recognition-Primed Decision model, from field studies of firefighters and other commanders: experts under time pressure do *not* generate and score alternatives in parallel. They recognize the situation as typical, retrieve one plausible course of action, and mentally simulate whether it works — a **singular** rather than comparative evaluation. If it fails simulation, they move to the next most typical option ([RPD overview](https://umbrex.com/resources/frameworks/decision-making-frameworks/recognition-primed-decision-model/); [singular vs. comparative evaluation](https://arc.lib.montana.edu/snow-science/objects/P__8107.pdf); [Klein, Recognition-Primed Decision Strategies](https://www.researchgate.net/publication/235112159_Recognition-Primed_Decision_Strategies); [NDM review, Frontiers](https://www.frontiersin.org/journals/psychology/articles/10.3389/fpsyg.2022.936140/full)).

This is the strongest argument for leading with a recommendation. A balanced matrix forces the reader into a comparative mode that is **slower and less natural than how expert decision-makers actually operate.** Give them one candidate plus the information to reject it, and you're feeding their native process. Klein's firefighters reached decisions in seconds this way.

The "Why not B?" section exists because rejection is the active step in RPD. The reader's real question is not "is A good?" but "is A good enough that I can stop looking?"

→ **Rule 3** (single recommendation) and **Rule 4** (why-not).

---

## 6. Explanations can produce over-trust, so they must include the case against

**Finding.** Automation bias — over-reliance on automated recommendations — is a central failure mode in human-AI collaboration, and explanations do not reliably fix it. Explanation can *increase* unwarranted trust rather than enabling scrutiny ([Springer, *AI & Society*, 2025 review of automation bias and XAI](https://link.springer.com/article/10.1007/s00146-025-02422-7); [Cambridge, *EJRR*, on automation bias in the EU AI Act](https://www.cambridge.org/core/journals/european-journal-of-risk-regulation/article/automation-bias-in-the-ai-act-on-the-legal-implications-of-attempting-to-debias-human-oversight-of-ai/C97C85015056C09326944DE55CBC4D2C)).

Transparency's effect on trust is not monotonic — it modulates trust, and the relationship depends on what is revealed ([PMC, *How transparency modulates trust in AI*](https://pmc.ncbi.nlm.nih.gov/articles/PMC9023880/)).

MIT Sloan Management Review frames the design goal as producing explanations that let reviewers genuinely interrogate a recommendation rather than approve it reflexively ([*AI Explainability: How to Avoid Rubber-Stamping Recommendations*](https://sloanreview.mit.edu/article/ai-explainability-how-to-avoid-rubber-stamping-recommendations/)).

**The practical implication is uncomfortable:** a well-written justification makes rubber-stamping *more* likely, not less. The antidote is not more explanation — it's *contrastive* explanation. Surfacing counter-evidence, disagreement, and the specific conditions under which you'd be wrong gives the human something to actually test.

→ **Rules 4, 6, 7** and `main_risk` / `assumptions` being non-optional fields.

---

## 7. Oversight fails from both too little context and too much

**Finding.** Human-oversight requirements often assume the reviewer has the bandwidth and technical insight to meaningfully supervise systems operating faster and broader than they can follow — an assumption that breaks as capability asymmetry grows, opening a gap between the legal form of oversight and its technical reality ([Harvard JOLT, *Redefining the Standard of Human Oversight for AI Negligence*](https://jolt.law.harvard.edu/digest/redefining-the-standard-of-human-oversight-for-ai-negligence); on disclosure-based remedies losing force as asymmetry grows, [arXiv](https://arxiv.org/pdf/2604.14070.pdf)).

There is a genuine two-sided constraint:

```
too little context  →  can't evaluate  →  rubber-stamp
too much context    →  overloaded      →  rubber-stamp
```

Both failure modes land in the same place. **The target is the narrow band in between** — enough to genuinely override, not so much that reviewing becomes performative. Progressive disclosure is the mechanism for hitting a band rather than a point: default to the minimum sufficient layer, keep depth reachable on demand.

→ **Step 5** (depth modes) and the layered disclosure model.

---

## 8. Optimal depth depends on the reader's prior knowledge

**Finding.** Instructional design is most effective when tailored to the learner's existing knowledge and motivation; the same presentation that helps a novice can impose useless load on an expert ([PMC, *Greater Cognitive Effort for Better Learning*](https://pmc.ncbi.nlm.nih.gov/articles/PMC5854224/)).

This is why depth is a *variable*, not a house style. The correct response length for a domain expert who set the context themselves is far shorter than for someone encountering the problem cold — and the agent usually has enough signal (who asked, how they asked, what they already stated) to infer which.

→ **Step 5**, and the principle that the user should never have to say *"be shorter."*

---

## The mapping, in one table

| Rule in SKILL.md | Grounded in |
|---|---|
| Answer first, no background | Transient information effect (§2) |
| ≤3 reasons, ≤3 options | Working-memory capacity (§1), choice overload (§3) |
| Always recommend one | RPD singular evaluation (§5), choice overload (§3) |
| Always give "why not the runner-up" | RPD rejection step (§5), contrastive explanation (§6) |
| Separate fact / inference / prediction | Extraneous load (§1), calibration & over-trust (§6) |
| Qualitative uncertainty profile, not fake % | Automation bias, transparency-trust relationship (§6) |
| Name your own strongest counter-evidence | Rubber-stamping avoidance (§6) |
| Risk-tiered approval, don't ask on tier 1–2 | Decision fatigue (§4), oversight bandwidth (§7) |
| Progressive disclosure, depth by stakes | Meaningful oversight band (§7), prior-knowledge tailoring (§8) |
| Length is a cost | Extraneous cognitive load (§1) |

---

## The one-sentence version

Humans decide worse when given more, not better — so the agent's real work is deciding what *not* to say, and the discipline that makes that safe is naming your own counter-evidence.
