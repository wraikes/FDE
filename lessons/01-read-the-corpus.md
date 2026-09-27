# Lesson 1 — Read the corpus

**Tenet: look at the data before you design anything.**

You cannot choose a schema, a metric, or a threshold before you know what the source
documents actually contain. Twenty records beat any amount of reasoning about the
domain, and they beat any amount of what the client told you — the client is describing
the process they believe they have.

The mistake this prevents: designing from the brief, encoding assumptions, and
discovering them in production.

---

## The method — seven questions to ask any corpus

Read 20–50 records with these in hand. Write down the answers. It takes 45 minutes and
it determines everything downstream.

| # | Question | What it decides |
|---|---|---|
| 1 | **Presence** — for each field you want, what fraction of records actually contain it? | Nullability. A field present in 90% of records cannot be non-null. |
| 2 | **Form variance** — how many distinct ways is the same fact written? | Prompt design, and whether normalization is a separate step. |
| 3 | **Ambiguity** — where would two careful humans disagree? | These become your eval's hard cases, and sometimes a business rule you must ask about. |
| 4 | **Base rate** — how often does the rare, high-value thing occur? | Sample size, metric choice, and whether accuracy is meaningless. |
| 5 | **Out-of-scope records** — how many aren't the thing at all? | A routing/classification step you didn't know you needed. |
| 6 | **Cross-record dependencies** — does a record only make sense given another? | Whether single-document extraction is even the right unit. |
| 7 | **Not in the document** — what does the business need that this source can never supply? | The scope boundary. The most valuable answer of the seven. |

Question 7 is the one that changes proposals. Everything the business needs that isn't in
the document is either out of scope or a second data source — and in a real engagement
that distinction is the difference between a fixed-fee project and an open-ended one.

---

## Worked example — Brightline Mechanical (50 service reports)

### 1. Presence

| Field | Present | Note |
|---|---|---|
| Labor hours | 45/50 | 5 state none at all |
| Customer/site | 48/50 | 2 are bare fragments |
| Equipment make/model | ~22/50 | Most reports name equipment by nickname only ("the big Trane on the roof") |
| Serial | 1/50 | Effectively never present |
| Parts used | ~30/50 | Often described, rarely identified |

**Consequence:** `labor_hours` and `customer` cannot be non-null. `serial` is present once
in fifty — putting it in the schema at all is close to pointless, and asking the model for
it invites invention.

### 2. Form variance — labor hours alone

> `3.5` · `2` · `1hr` · `.5` · `2 hr` · `45 min` · `about an hour and a half` ·
> `3 hours including travel` · `Full day, 8 hrs` · `Labor 6 hrs, two of us for 3`

Ten ways in fifty records. Note the last two aren't formatting variance — they're
*semantic* variance. "Including travel" may or may not be billable depending on the
contract. That's a question for Dana, not a parsing problem.

### 3. Ambiguity

- **BR-1026:** *"Labor 6 hrs, two of us for 3."* Is that 6 billable hours or 3 elapsed?
  Both readings are defensible. Only Dana knows which the invoice wants.
- **BR-1040:** *"3 hrs. We have now spent about 9 hours on this."* Two numbers, one of them
  cumulative across visits. A naive extractor takes the larger, more prominent one.
- **BR-1006:** Tech waited 40 minutes for a no-show. Billable? Business rule, not extraction.

### 4. Base rate — the warranty flag

Four to five of fifty reports warrant a warranty check: **~8–10%**. The owner estimated
1 in 20 (5%). He was wrong by roughly half, which is normal — owners estimate rates badly,
and this is the kind of thing you correct with data rather than argument.

Now the important part. Look at where the *word* "warranty" appears:

| Report | Says "warranty"? | Should flag? | Why |
|---|---|---|---|
| BR-1014 | yes | **yes** | Coil failure, install Nov 2021, within 5-yr parts |
| BR-1023 | yes | **yes** | VFD failure, 2023 install, tech says check it |
| BR-1040 | yes | **yes** | Line set defect, Aug 2024 install |
| BR-1026 | yes | no | Warranty part *already* received — resolved |
| BR-1029 | yes | no | Already confirmed and claimed — resolved |
| BR-1039 | yes | no | Explicitly says *out* of warranty — negation |
| BR-1046 | yes | no | "Our own warranty" — the contractor's, not the manufacturer's |
| **BR-1004** | **no** | **yes** | Compressor shorted to ground, tag says 2022 install |

Read that table again. **The keyword is present on four records that should not be flagged,
and absent from one of the strongest true positives.** A regex on "warranty" would score
poorly in both directions — and BR-1004, the one it misses, is a compressor, the most
expensive part on the list.

This single table is why the warranty flag needs a model and an eval rather than a rule,
and why your eval set has to contain the *negatives* — 1026, 1029, 1039, 1046 — or you'll
never see the failure.

### 5. Out-of-scope records

Six of fifty are not billable service records: a no-show, a locked gate, a one-word entry
(`pm`), a courtesy call, a sales meeting, a "no charge?" follow-up. **12%.**

**Consequence:** you need a routing decision before extraction. If you don't have one,
the model will dutifully produce a structured record for "gate locked" and Dana will
review fifty records a week instead of forty-four.

### 6. Cross-record dependencies

At least eight reports only make sense with a prior one. *"went back out to riverside,
got it running"* has no customer, no equipment, no hours — it is meaningless alone and
perfectly clear as a follow-up to BR-1014. BR-1037 contains a tech correcting himself
mid-sentence about which customer he's writing about.

**Consequence:** the unit of extraction may not be the document. That's a real
architectural question, and in Rep 1 the honest answer is "these get routed to Dana."

### 7. Not in the document

| Business needs | Actually lives in |
|---|---|
| True on-site time | Dispatch system timestamps |
| Part numbers and cost | Supply house invoices |
| Equipment install date and warranty terms | Equipment registry / install records |
| Whether labor is contract-covered | Service agreements |

**This is the finding.** Warranty *eligibility* requires an install date and warranty
terms, neither of which is in a service report. So the field cannot be "is this covered."
It can only be **"a part was replaced that may be covered — go check."**

And more broadly: Dana's error-catching runs on all four of those external sources. An
extraction-only system cannot replicate it, at any accuracy. That sentence belongs in the
memo, and it is the honest scope boundary of Rep 1.

---

## Your turn — Ridgeline Logistics

Different domain, same seven questions.

**Ridgeline Logistics** is an 18-person freight brokerage in Memphis. Shippers email load
tenders — "here's a load, can you cover it?" Brokers read the email, key a load record
into the TMS, and start calling carriers. About 60 tenders a week.

The money problem the owner mentions in passing: **accessorial charges.** Detention,
layover, driver assist, lumper fees. They're often implied by the tender's terms and
frequently never billed. He thinks it's "a few grand a month."

Records: `engagements/01-brightline/data/ridgeline_tenders.jsonl` (12 tenders).

**Deliverable — answer all seven questions.** Short is fine; a line or two each, except
these three:

- **Q4 (base rate):** which tenders carry accessorial exposure, and *what signal told you*?
  Then check whether the obvious keyword works, the way it failed on "warranty."
- **Q5 (out of scope):** how many of the twelve aren't load tenders at all?
- **Q7 (not in the document):** this is the one I'll grade hardest. What does billing an
  accessorial require that a tender email cannot contain?

I'll score it against the method, not against a key.
