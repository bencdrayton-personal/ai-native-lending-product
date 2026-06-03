# Experimentation Framework: Lending Journey
### Ben Drayton, June 2026

---

## The principle

Every proposed change to the lending journey is a hypothesis, not a decision. The discipline of treating product changes as experiments, with explicit predictions, defined metrics, and documented learnings, is what separates a roadmap that compounds from one that drifts.

In lending specifically, there is an additional constraint: **experiments that improve UX metrics must not degrade credit quality.** Speed and conversion are measurable in days. Arrears emerge over months. An experiment that lifts completion rate by 15% but degrades 90-day arrears by 2pp is not a win. It's a delayed problem that arrives after the PM has shipped and moved on. Every experiment here carries a credit quality guardrail.

---

## The structure

Each experiment follows the same format:

```
Stage         → which funnel milestone is being tested
Hypothesis    → if we do X, then Y will change by Z
Primary metric → the single number that decides the experiment
Guardrail     → the credit/compliance metric that cannot get worse
Expected lift  → the directional prediction before launch
Result        → what actually happened
Learning      → what we now know, including null results
```

Null results are recorded. A hypothesis that fails to move the metric is information. A hypothesis that is not tested is a guess that ships.

---

## Guardrails that apply to all experiments

These are not negotiable and are not subject to experimentation:

1. **90-day arrears rate** cannot increase by >0.5pp from baseline in the CDR-verified cohort as a result of any change to income verification or credit policy rules.
2. **Decision explainability**: all credit decisions must remain auditable. No experiment may remove or shorten the structured reason recorded for each decision.
3. **NCCP compliance**: responsible lending assessment requirements under the National Consumer Credit Protection Act cannot be reduced or simplified as part of a UX optimisation.
4. **Minimum verification**: an experiment may test *how* income is collected (CDR vs. documents) but not *whether* income is collected.

---

## Experiment log

### EXP-001: CDR consent framing, speed vs. privacy

| Field | Detail |
|---|---|
| **Stage** | Income Verification (Stage 4) |
| **Hypothesis** | Framing the CDR consent step around speed ("Get a decision in 30 minutes") converts better than privacy-first framing ("Your data stays secure") because applicants at Stage 4 are already committed. Their primary concern is how long this will take, not data privacy. |
| **Primary metric** | CDR consent rate (% of eligible applicants who consent) |
| **Guardrail** | Arrears rate at 90 days, CDR-consenting cohort |
| **Expected lift** | +8–15pp on consent rate |
| **Status** | Proposed |
| **Result** | N/A |
| **Learning** | N/A |

---

### EXP-002: Income field reduction at submission step

| Field | Detail |
|---|---|
| **Stage** | Submit Application (Stage 3) |
| **Hypothesis** | Reducing the income section from 8 declared fields to 3 (gross income, employment type, frequency) increases form submission rate because the income step is the primary idle-time abandonment trigger (>5 min idle = high abandonment probability). Declaratory fields beyond gross income add friction without improving decisioning accuracy; CDR data will verify anyway. |
| **Primary metric** | Form submission rate (Stage 3 completion) |
| **Guardrail** | Manual referral rate (STP rate must not decrease; fewer fields cannot result in more exceptions) |
| **Expected lift** | +10–18pp on submission rate for CDR-eligible applicants |
| **Status** | Proposed |
| **Learning** | If reducing fields increases referral rate, the hypothesis is wrong: the fields were adding decisioning signal, not just friction. |

---

### EXP-003: Real-time income field validation

| Field | Detail |
|---|---|
| **Stage** | Submit Application (Stage 3) |
| **Hypothesis** | Showing inline validation on income fields as the applicant types ("Based on your income, you're eligible for loans up to $X") reduces abandonment at the income step by giving applicants a live signal that they are on track, replacing the uncertainty that drives idle-time drop-off. |
| **Primary metric** | Abandonment rate specifically at the income step (not overall form) |
| **Guardrail** | This is a UX change only with no credit policy impact. Ensure the live eligibility estimate is directionally correct to avoid applicants proceeding under false expectations (which increases late-funnel abandonment). |
| **Expected lift** | −20–30% drop-off at income step |
| **Status** | Proposed |

---

### EXP-004: Decision communication timing

| Field | Detail |
|---|---|
| **Stage** | Credit Decision (Stage 5) |
| **Hypothesis** | Delivering the conditional approval decision immediately (as soon as the AI model returns a result, within 2 minutes of submission) results in a higher acceptance rate than batching communications to a standard processing window (e.g. 9am next business day), because immediacy signals confidence and reduces the window in which the applicant finds an alternative. |
| **Primary metric** | Offer acceptance rate (Stage 6) |
| **Guardrail** | Acceptance rate must not be artificially inflated by approving weaker applications; run alongside arrears rate at 90 days. |
| **Expected lift** | +5–12pp on acceptance rate |
| **Status** | Proposed |
| **Note** | This experiment only applies to AI-decisioned applications (STP). Manual referrals have a different communication timeline by design. |

---

### EXP-005: Settlement timeline transparency

| Field | Detail |
|---|---|
| **Stage** | Drawdown / Funded (Stage 7) |
| **Hypothesis** | Showing a specific, named settlement timeline at offer acceptance ("Your funds will arrive by [date]") reduces drawdown drop-off compared to the generic "3–5 business days" message, because certainty reduces the motivation to switch to a competitor who promises something concrete. |
| **Primary metric** | Drawdown conversion rate (Stage 7) |
| **Guardrail** | Settlement completion rate. If a named date creates an expectation that cannot be met, it drives complaints and cancellations. Only run this experiment if settlement SLA is reliable (>95% on-time rate). |
| **Expected lift** | +4–8pp on drawdown conversion |
| **Status** | Proposed |

---

### EXP-006: Mobile-first form layout

| Field | Detail |
|---|---|
| **Stage** | Submit Application (Stage 3) |
| **Hypothesis** | A mobile-first, single-question-per-screen layout (vs. a scrollable multi-field form) reduces abandonment among mobile applicants specifically, because mobile context (smaller screen, more distraction, touch interface) makes multi-field scrolling forms disproportionately harder to complete. |
| **Primary metric** | Form submission rate, segmented by device type (mobile vs. desktop) |
| **Guardrail** | Completion time. A single-question-per-screen layout that dramatically increases completion time may reduce conversion at different funnel stages. Monitor total application time alongside submission rate. |
| **Expected lift** | +12–20pp mobile submission rate |
| **Status** | Proposed |
| **Note** | Do not run this across all traffic. Split by device type. The hypothesis is specific to mobile; running it on desktop dilutes the signal. |

---

## Prioritisation

Not all experiments are equal. Before scheduling, score each on:

| Criterion | Question | Score (1–3) |
|---|---|---|
| **Reach** | How many borrowers does this stage affect per month? | 3 = top-of-funnel, 1 = late funnel |
| **Impact** | How large is the predicted lift on the primary metric? | 3 = >15pp, 2 = 5–15pp, 1 = <5pp |
| **Confidence** | How strong is the evidence base for the hypothesis? | 3 = prior data, 2 = analogous market data, 1 = intuition |
| **Effort** | How long to implement and run? | 3 = <1 sprint, 2 = 1–2 sprints, 1 = >2 sprints |
| **Risk** | What is the guardrail exposure if the hypothesis is wrong? | 3 = low risk, 1 = high credit/compliance risk |

Score = Reach × Impact × Confidence × (Effort + Risk) / 2.

A high-priority experiment has a high score and a clear null hypothesis (i.e. we will learn something regardless of whether the primary metric moves).

---

## What makes a good null result

A failed experiment is only a failure if we do not record why. Specifically:

- Did the primary metric not move, or did it move in the wrong direction?
- Did the guardrail metric flag a problem that we caught before shipping?
- Was the hypothesis wrong, or was the implementation of the hypothesis wrong?
- What would we do differently in the next iteration?

In AI-native decisioning specifically, a null result on a UX experiment is often evidence that the bottleneck is upstream or downstream, not where we hypothesised. That is valuable. It goes on the roadmap as a redirect, not a failure.
