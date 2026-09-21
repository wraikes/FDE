# Rep 1 — Brightline Mechanical

**Rep 1 of 3. Capability added: schema-constrained extraction + a real eval harness.**

---

Brightline Mechanical is a commercial HVAC contractor outside Sacramento. 12 people:
8 field techs, 2 in dispatch, an office manager named Dana, and the owner.

After every job a tech files a service report. It's free text, typed on a phone or a
tablet, sometimes dictated. Length runs from one line to five paragraphs. Spelling is
approximate. Equipment gets called by nickname. About 40 reports a week.

Dana reads each one and retypes the key fields into their job management system so the
job can be invoiced. She estimates 6 hours a week. Her real complaint isn't the typing —
it's that she catches billing errors doing it, and nobody else would.

The owner wants the retyping gone. Dana is not against it, but she's the one who'll be
blamed if an invoice goes out wrong.

## What they need out of each report

- Customer / site
- Equipment serviced (make, model, serial if present)
- Parts used
- Labor hours
- Follow-up required (yes/no + what)
- **Warranty claim flag**

## Things they said in passing

- "The warranty one matters. We ate about eleven grand last year on claims we never filed."
- Warranty-eligible jobs are maybe 1 in 20.
- Invoicing runs Friday. Reports come in all week.
- Their job system has an API. Not for this rep — Rep 3.

## Constraints

- Python, GCP.
- Budget is small. This is a 12-person company; they are not spending $2k/month on tokens.
- No UI this rep. CLI is fine.

## Deliverables

1. Working extraction over the fixture set
2. **Eval harness** — hand-labeled ground truth, per-field accuracy, threshold stated
   before you see results
3. One-page memo for the owner. Business language. Include the error rate honestly.

## Before Claude writes any code, you specify

- [ ] The output schema
- [ ] What the eval measures, per field, and what passing means
- [ ] What happens when the model returns something invalid
- [ ] Where Dana is in the loop
- [ ] Cost per report, and your budget

---

_Fixtures generated on request. Ask when you start._
