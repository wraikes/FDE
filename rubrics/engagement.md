# Rubric

Scored 1-5. Below 3 on any line = rep not done.

## Eval harness
- Ground truth is real, hand-labeled, and large enough to mean something
- Metrics are **per-field**, not aggregate
- Threshold stated **before** results were seen
- Known blind spots documented

## System
- Failure modes handled, not hoped away
- Cost and latency measured against a stated budget
- Human is in the loop where the risk actually is
- Someone else could run it from the README

## Client memo (1 page)
- Written for a business owner, not an engineer
- Leads with the outcome, not the architecture
- States what it can't do, and the error rate, honestly
- Has a number in it

## Cold defense
- Explained design decisions without reading the code
- Knew what the eval would miss
- Debugged the injected failure without being handed the cause

## Discovery (Nov/Dec)
- Asked about the workflow before proposing anything
- Caught at least one contradiction in what the client said
- Quantified the cost of the current process
- Scoped to something deliverable, and said no to the rest
