# October — Can I build it?

~31 hours. Three reps of the same pattern, each adding one capability.

## Rep 1 — extraction + evals (~10h)
Lessons: `lessons/01-read-the-corpus.md` -> 02 schema -> 03 ground truth -> 04 metrics
Reading: `curriculum/reading.md` (~1h, before you start)
Brief: `briefs/oct-01-hvac.md`
Adds: schema-constrained output, a real hand-labeled eval set, per-field accuracy.
Lesson: the eval is the product. Aggregate accuracy hides the field with the money on it.

## Rep 2 — retrieval + tool calling (~10h)
Brief: TBD (insurance brokerage — submissions + underwriting guidelines + policy history)
Adds: retrieval over a real corpus, tool calls against BigQuery, citations, abstention.
Lesson: retrieval quality dominates model quality. An agent that can't say "I don't know"
is a liability you can't sell.

## Rep 3 — ship it (~10h)
Brief: TBD (Rep 1 goes live for the office manager)
Adds: Cloud Run + Scheduler, review queue, idempotent write-back, tracing, cost/latency
budgets, corrections feeding back into the eval set.
Lesson: the last mile is most of the work. The human-in-the-loop design IS the product.

## Exit criteria
"Give me a workflow and I can build the system" — demonstrated three times, with evals,
against briefs you did not write.
