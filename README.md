# AI-Native Lending: Product Strategy Portfolio

Product thinking applied to Constantinople's Senior PM – Lending role. Five artefacts, each mapped to a specific requirement in the job description.

---

## The throughline

Constantinople's CEO has written clearly about why AI keeps failing in banking: fragmented data, no captured decision reasoning, no governed execution paths. The argument is that the next moat belongs to whoever builds **decision infrastructure**: not just a system of record, but a system that captures *why* decisions get made.

This repo takes that thesis seriously and asks: what does a Senior PM do with it in the lending domain specifically? The answer is five connected artefacts: a competitive frame, a product opportunity, a metrics system, an experimentation discipline, and a customer milestone map.

---

## Artefacts

### 1. [Competitive Teardown](competitive-teardown.md)
*JD requirement: "assessing the competitive and market landscape to inform decision-making"*

Analysis of Mambu, Thought Machine, Backbase, Temenos, NextGen, and the US lending platforms. The frame is not cloud-native vs. legacy. It's who owns the decision layer. Covers where Constantinople wins, where it is exposed, and what the lending-specific competitive risks are.

### 2. [Opportunity Brief](opportunity-brief.md)
*JD requirement: "driving the vision, strategy and roadmap for your strategic domain"*

A scoped product bet: embedding Australia's Consumer Data Right (CDR) natively into Constantinople's AI credit decisioning pipeline to enable same-day conditional approvals on retail lending. Structured as a real opportunity brief: hypothesis, users, problem, success metrics at 30/60/90 days, risks, and what we're not doing.

### 3. [Metrics Framework](metrics-framework.md)
*JD requirement: "determining, developing, measuring, and analysing metrics to drive insights, inform the roadmap"*

Two layers: **platform metrics** (how bank clients adopt and use the lending product suite, B2B SaaS health) and **borrower journey metrics** (how end borrowers move through lending experiences the platform powers). Twelve metrics, each with: what it measures, when to act on it, and the failure mode of over-indexing on it alone. Benchmarks sourced from NextGen Australian Lending Technology 2026, Pennant Technologies, and ResolvePay research.

### 4. [Experimentation Framework](experimentation-framework.md)
*JD requirement: "experience with iterative hypothesis-driven product development and experimentation"*

Six specific lending journey experiments, each with a hypothesis, primary metric, credit quality guardrail, expected lift, and space for results. Grounded in the specific funnel stages mapped in the milestone tracker. Includes a prioritisation scoring model and explicit guidance on null results: what counts as a failure versus a learning.

### 5. [Lending Journey Milestone Tracker](lending-milestone-tracker.html)
*JD requirement: "align all teams on key customer milestones and lending experiences"*

Open in a browser. An interactive funnel visualisation of 1,000 borrowers moving through a retail personal loan journey. Toggle between Legacy Bank and Constantinople Platform to see stage-by-stage conversion, time-at-stage, drop-off causes, and the four headline KPIs. This is the artefact you would use in a cross-functional alignment session to show engineering, design, and solution engineering exactly where customers are losing and why.

---

## How it fits together

```
Competitive teardown  →  establishes the market context and Constantinople's position
        ↓
Opportunity brief     →  identifies the highest-leverage product bet in lending (CDR)
        ↓
Metrics framework     →  defines how we'd know if it's working (two-layer: platform + borrower)
        ↓
Experimentation log   →  structures how we'd iterate toward the best outcome
        ↓
Milestone tracker     →  the customer-facing view that aligns the cross-functional team
```

---

## About

Ben Drayton. Director, Pomona Property Group. Previously: Senior PM at UBank, Honey, Employment Hero. 14 years in regulated financial services and enterprise SaaS. Based in Sydney.

[LinkedIn](https://www.linkedin.com/in/bendrayton) · bencdrayton@gmail.com
