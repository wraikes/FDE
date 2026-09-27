# Tenets

What each exercise exists to teach. One line each. If you can't state the tenet, you
haven't done the rep.

## Always

- Look at the data before you design anything.
- A null beats a guess.
- Measure before you optimize.
- The deliverable for the client is not the code.
- Sort every question: derivable / needs data / ask the client.

## Rep 1 — extraction + evals

1. The schema is a business decision wearing a data-type costume.
2. Never require a value the source may not contain — forcing non-null manufactures fiction.
3. Ground truth must answer the same question the system answers. Label the source, not the outcome.
4. Metrics are per-field. Aggregates hide the field with the money on it.
5. Thresholds come from cost of error, not from what the model happens to score.
6. For rare, high-value classes, optimize recall and buy precision later with human time.
7. Distinguish "absent from the source" from "extraction failed." Same null, opposite response.

## Rep 2 — retrieval + tool calling

1. Retrieval quality dominates model quality.
2. A tool's return shape is a context-budget decision, not a convenience.
3. Citations are the unit of trust. Unsourced output is unsellable.
4. Abstention is a feature you design, not a failure you tolerate.
5. Engagements break on the corpus, not the prompt.

## Rep 3 — ship it

1. The human-in-the-loop design *is* the product. Review speed is the metric.
2. Write-back must be idempotent. The world retries.
3. Instrument before you scale. You cannot debug what you did not log.
4. Corrections are the flywheel. Capture them or you never improve.
5. The last mile is most of the work.

## November — discovery and commercial

1. Ask about the workflow before proposing anything.
2. The stated problem is rarely the real one.
3. Quantify the current process in dollars, or you cannot price the new one.
4. Price the outcome, not the hours.
5. Scoping is saying no.

## December — full engagement

1. Surface the binding constraint before you architect.
2. The person who'll be blamed is the person you must convince.
3. Sometimes the right deliverable is "don't build this."
4. Demo the failure mode, not just the happy path.
5. Handoff is part of delivery.

## January — Rep 4

1. Answer the three questions clients ask — MCP, multi-agent, fine-tuning — with your own
   measurements, not opinions.
