# Lending Metrics Framework: Day 30 Instrument Panel
### Ben Drayton, June 2026

---

## The framing

Two layers of metrics apply to a Constantinople SPM. The first is **platform metrics**: how bank clients are adopting and using the lending product suite (B2B SaaS health). The second is **borrower journey metrics**: how end borrowers are moving through lending experiences the platform powers (product outcomes). Both matter. Conflating them is how a platform PM ends up optimising the wrong thing.

For each metric: what it measures, the threshold or direction that would trigger action, and, critically, the failure mode of over-indexing on it alone.

---

## Layer 1: Platform metrics (B2B, how bank clients use Constantinople)

### 1. Feature adoption rate by bank client
**What it measures:** % of available lending configuration features actively used by each bank client in Justinian (e.g. CDR income integration, AI decisioning rules, credit policy templates, portfolio reporting). Segmented by client and feature.  
**Act on it when:** A client is live but using <40% of available lending features after 60 days. This signals onboarding gaps, UX friction in Justinian, or a mismatch between what was scoped and what was delivered.  
**Failure mode of over-indexing:** Feature adoption rate can be gamed by counting any click as "use." Pair with actual loan origination volume through the feature. A feature that is configured but not generating decisions is not being adopted in the meaningful sense.

### 2. Time-to-configure a new lending product
**What it measures:** End-to-end time (days) for a bank client's product team to configure, test, and launch a new lending product on the platform using Justinian, from brief to live.  
**Act on it when:** >10 business days for a standard personal loan product configuration. If it takes the bank PM two weeks to launch a new loan type, the platform is not delivering the speed advantage it promises.  
**Failure mode of over-indexing:** Compressing configuration time by reducing testing gates creates risk. Track time-to-configure alongside post-launch incident rate.

### 3. Loan origination volume through the platform
**What it measures:** Total loan applications submitted and decisions made via Constantinople-powered channels per month, per client. Absolute volume and month-on-month growth.  
**Act on it when:** Volume plateaus or declines at a client after ramp-up. Investigate whether the bank is routing volume through a legacy channel rather than the platform, or whether there is a product/UX issue suppressing applications.  
**Failure mode of over-indexing:** High volume with poor credit outcomes for the bank damages the commercial relationship. Volume is a health metric, not a success metric on its own.

### 4. Bank client NPS / satisfaction with lending tooling
**What it measures:** Periodic (quarterly) satisfaction score from bank product managers, credit teams, and ops staff who use Justinian for lending workflows. Separate from end-borrower NPS.  
**Act on it when:** Score below 7/10 from any active user type; declining trend across quarters.  
**Failure mode of over-indexing:** NPS without verbatim feedback is directionally useful but insufficient for root-cause analysis. Always pair with a "what would you change?" question.

---

## Layer 2: Borrower journey metrics (end-borrower experience through the platform)

### 5. Application completion rate
**What it measures:** Two distinct readings. (a) From first landing: % who ever start the application form (~32% is the industry baseline; ResolvePay 2024 found 68% of financial services applicants abandon without completing). (b) From form-start: % who submit after beginning to enter data. Best-in-class digital lenders achieve 55–70% on this second measure.  
**Act on it when:** Form-start completion drops below 50%. Investigate which step is causing abandonment. Document upload (income verification step) is the most common culprit; idle time on that step >5 minutes is the primary behavioural signal.  
**Failure mode of over-indexing:** Pushing completion rate by removing friction at the wrong points can degrade credit quality downstream. Always read alongside 90-day arrears.

### 6. CDR consent rate
**What it measures:** % of eligible applicants who consent to CDR data sharing when offered. Current Australian market baseline is very low (<20%; CDR.gov.au confirms adoption "not as high as it could be" as of 2025). Government simplifying consent rules in 2026 should lift this.  
**Act on it when:** Below 30% within 6 months of CDR launch. Investigate consent UX framing (speed benefit framing converts better than data-sharing framing), consent step placement, and fallback clarity. Target: 40–50% by month 12.  
**Failure mode of over-indexing:** Consent rate is meaningless without tracking what happens to non-consenting applicants. If 60% don't consent and drop off entirely, the fallback flow needs fixing. Pair with abandonment rate at the consent step specifically.

### 7. Time-to-conditional-approval (TCA)
**What it measures:** Time from application submission to a conditional credit decision (approve/refer/decline). The target for an AI-native personal loan platform is <30 minutes for standard applications. Industry average for online lenders in Australia is ~20 hours; traditional banks are 3–5 business days (NextGen Lending Technology 2026 report).  
**Act on it when:** >2 hours for standard (non-exception) applications. Investigate whether the CDR data pipeline is running as expected, whether the AI decisioning model is routing too many applications to manual review, or whether the manual review queue is backed up.  
**Failure mode of over-indexing:** Speed-to-decision can be gamed by auto-approving more applications. TCA must be read alongside STP rate and arrears. A fast bad decision is worse than a slow good one.

### 8. Straight-through processing (STP) rate
**What it measures:** % of applications that reach a credit decision (approve or decline) without requiring manual credit assessor intervention. Traditional banks: ~22%. Leading digital lenders: 80–90% (Pennant Technologies, 2025).  
**Act on it when:** Below 70% for a CDR-enabled standard personal loan product. Investigate whether the AI credit policy rules are too narrow, whether CDR data quality is triggering too many exceptions, or whether the exception criteria need tuning.  
**Failure mode of over-indexing:** An STP rate pushed toward 100% by widening auto-approval criteria is how credit quality degrades silently. High STP is only good news if arrears are stable. Run both.

### 9. Cost per application
**What it measures:** Blended average cost to process one loan application, combining STP cost ($5–$15) and manual review cost ($150–$300), weighted by STP rate. Source: Pennant Technologies 2025. At 22% STP, blended cost ≈ $185. At 85% STP, blended cost ≈ $35.  
**Act on it when:** Cost per application is above $50 for a CDR-enabled product. STP rate is too low, or manual review cost per case is too high (assessor hours are being spent on cases the AI should be handling).  
**Why this metric matters for bank clients:** A bank processing 5,000 personal loan applications per month at $185 each is spending $11.1M/year on underwriting ops. At $35, that's $2.1M: a $9M annual saving. This is the commercial story Constantinople needs to tell. The PM should own this number.

### 10. Drawdown conversion rate
**What it measures:** % of conditional approvals that proceed to drawdown (funded loan). Industry benchmark for prime personal lending: 75–85% (CULytics consumer lending KPI benchmarks). If it is lower, applicants are accepting conditional approval then not proceeding, usually because the settlement experience is slow or another lender offered a better rate while they waited.  
**Act on it when:** Below 70%. Investigate whether the drawdown experience (acceptance flow, signing, settlement) is introducing friction, or whether the conditional approval is arriving too slowly relative to competitors.  
**Failure mode of over-indexing:** A high drawdown conversion can mask a thin approval population (tight credit policy, few approvals, but the ones who get through all proceed). Read alongside total approved volume.

### 11. 30/60/90-day arrears rate by verification method
**What it measures:** % of approved loans in arrears at 30, 60, and 90 days post-drawdown, segmented by verification method (CDR-sourced vs. manual/document). The primary measure of whether CDR-powered decisioning improves or degrades credit quality versus the baseline.  
**Act on it when:** CDR-verified cohort arrears rate diverges from manual cohort by >1.5pp at 90 days. Investigate model calibration for CDR income data. Note: 30-day arrears misses slow-developing credit stress. Weight the 90-day reading.  
**Failure mode of over-indexing:** Short look-back periods miss default patterns that emerge at 6–12 months. Arrears at 90 days are the minimum; track through to 6 months before drawing firm credit quality conclusions.

### 12. Decision explainability rate
**What it measures:** % of credit decisions (approve and decline) where a structured, compliant reason is recorded in Constantinople's decision audit trail, not a free-text note, but a queryable, categorised record of the decision context.  
**Act on it when:** Below 95%. Any decline without a structured reason is a regulatory risk under NCCP/RG 209. For Constantinople specifically, this metric is also a proxy for how well the decision infrastructure is capturing the "why" behind each decision (the foundation for improving AI over time).  
**Failure mode of over-indexing:** Formulaic reasons applied uniformly ("insufficient income" on every decline) satisfy the structure requirement but defeat the purpose of decision infrastructure. Review a random sample of decisions for genuine context capture.

---

## What I'd add at 60 days

Once baseline data exists:

**AI model confidence distribution:** the spread of model confidence scores across all decisions. A healthy model has a bimodal distribution (high confidence approvals and declines, with a smaller middle band going to manual referral). A model drifting toward a flat distribution is losing discriminatory power and will push more volume to manual review over time.

**Exception rate by product type and income verification method:** which loan products and which verification methods are generating the most manual referrals? This informs credit policy configuration priorities in Justinian.

---

## Summary: what each metric drives

| Metric | Layer | Drives |
|--------|-------|--------|
| Feature adoption | Platform (B2B) | Onboarding quality, Justinian UX |
| Time-to-configure | Platform (B2B) | Platform flexibility, bank PM productivity |
| Origination volume | Platform (B2B) | Platform adoption, bank revenue growth |
| Bank client NPS | Platform (B2B) | Retention, contract renewal |
| Application completion | Borrower | UX quality, form design, CDR consent flow |
| CDR consent rate | Borrower | Consent UX, trust, open banking adoption |
| Time-to-approval (TCA) | Borrower | AI pipeline performance, manual queue |
| STP rate | Borrower | AI decisioning coverage, credit policy tuning |
| Cost per application | Borrower + commercial | ROI story for bank clients |
| Drawdown conversion | Borrower | Settlement experience, rate competitiveness |
| 30/60/90-day arrears | Borrower | Credit quality, model calibration |
| Decision explainability | Borrower + compliance | Regulatory readiness, AI improvement |
