# Outreach: Constantinople Application
### Drafts for LinkedIn comment and direct message

---

## LinkedIn comment on "Much ado about nothing: why AI agents keep failing in banking"
*Post to: https://www.cxnpl.com/resources/insights/much-ado-about-nothing-why-ai-agents-keep-failing-in-banking*
*Or find the LinkedIn share of the article and comment there (higher visibility to the team)*

---

The framing here is exactly right, and it's more precise than most AI-in-banking commentary gets. The data problem is real but it's not even the binding constraint. The binding constraint is that judgement doesn't get captured at commit time, so there's no precedent, and nothing to compound.

I ran into this firsthand building credit decisioning tooling at UBank and Honey. The decisioning engine recorded outcomes faithfully. What it never captured was the reasoning a credit assessor used when they overrode the model: the context behind the exception. That context lived in a note field if you were lucky, in someone's head if you weren't. Every exception was a one-off. No precedent. No feedback loop. The model couldn't improve on the most important decisions it was making.

The point about moving from advisory to operational resonates. Most bank AI deployments stay read-only because there's no governed execution path: no way to commit an action with traceability and rollback built in. MCPs are the right framing for why this matters architecturally. The advisory layer works fine. The execution layer doesn't exist yet.

"You can't just layer an AI company on top of a bank. It's consulting, with an API." That line lands.

Retail lending is where this plays out hardest. Income verification is the highest-judgement step in a consumer loan, and it's the one most likely to involve an exception: an irregular earner, a seasonal income pattern, a self-employed applicant whose CDR data tells a different story than their payslips. That's exactly the context that needs to be captured at commit time and retained as precedent, not reconstructed case by case. A canonical data model that owns that moment is the only way the decisioning actually gets better.

---

## Direct outreach note to hiring manager or CEO (Macgregor Duncan)
*LinkedIn message: keep under 150 words, no ask for a call in the opening*

---

**Option A: reference the article directly**

Hi Macgregor, your piece on why AI agents fail in banking is the clearest version of this argument I've seen. The point that really landed: it doesn't compound if you don't capture the reasoning at commit time. That's the problem I kept running into building credit decisioning tooling at UBank and Honey: outcomes recorded, reasoning lost, no precedent for the next exception.

I've put together some product thinking on the retail lending extension, specifically how CDR fits into Constantinople's canonical data model to bring the GSB decisioning speed to consumer products. Happy to share if useful.

Ben

---

**Option B: reference the GSB case study**

Hi [Name], I spent time with the Great Southern Bank case study. Automated decisioning with full governance and traceability, built and live in under 12 months. That's the proof point most people thought would take five years to reach.

The next interesting problem from a product standpoint is the retail extension. Income verification is where the judgement gap is widest, and CDR is the unlock. I've written up how I'd approach that roadmap. Happy to share if it's useful ahead of any conversation.

Ben Drayton

---

## Notes on timing and targeting

- Comment on the LinkedIn share of the article *before* applying. It creates an independent signal that shows up in their feed before they see your application.
- The direct message works best after the application is submitted. It references the work you've already done rather than previewing something you're promising to do.
- If you can identify the specific hiring manager via LinkedIn (search Constantinople + "Product"), send to them not just the CEO. The CEO will forward; the hiring manager will act.
- Do not follow up the DM within 7 days. One message. The content does the work.
