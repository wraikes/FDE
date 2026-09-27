# Reading

Read the rows for a rep **before** you start it, not during. Everything here is short —
none of it is a course. If a piece takes more than 45 minutes you're reading it too closely.

Budget: ~1 hour of reading per rep, inside that rep's 10 hours.

## Step zero, before any reading

**Read the raw data first.** Twenty real records teach you more about what's extractable
than any blog post, and most of the design questions become obvious once you've seen the
mess. Reading before looking at data is how you end up guessing at numbers.

## Before Rep 1 — extraction + evals

| Read | Why |
|---|---|
| [Building Effective AI Agents](https://www.anthropic.com/engineering/building-effective-agents) | The canonical piece. Read it for the workflow-vs-agent distinction — most client work is a workflow, and knowing when *not* to reach for an agent is half the judgment |
| Claude docs: **structured outputs / tool use for extraction**, **prompt engineering overview** | Mechanics you'll use in the first hour |
| Hamel Husain, *Your AI Product Needs Evals* (hamel.dev) | The single best thing written on evals. His actual thesis is "look at your data" — do that first |
| Claude docs: **Create strong empirical evaluations** | Task-specific metrics and grading methods. Closest thing to a how-to for the questions Rep 1 asks |
| Anthropic cookbook — classification & eval notebooks (github.com/anthropics/anthropic-cookbook) | Working code for the shape you're about to build |

## Before Rep 2 — retrieval + tool calling

| Read | Why |
|---|---|
| [Writing effective tools for AI agents](https://www.anthropic.com/engineering/writing-tools-for-agents) | Tool design is the actual skill in Rep 2. Token-efficient returns, clear contracts |
| [Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) | What to put in the window and what to keep out — directly governs retrieval design |
| Claude docs: **citations**, **prompt caching**, **batch API** | Citations are a Rep 2 requirement; caching and batch are cost levers clients will ask about |

## Before Rep 3 — ship it

| Read | Why |
|---|---|
| [Effective harnesses for long-running agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents) | Failure handling and recovery in systems that run unattended |
| *What We've Learned From a Year of Building with LLMs* (applied-llms.org) | The operational half — monitoring, drift, the human loop. Skim the ops section |
| GCP docs: Cloud Run + Cloud Scheduler quickstart | Just enough to deploy |

## Before Rep 4 (January)

| Read | Why |
|---|---|
| [Code execution with MCP](https://www.anthropic.com/engineering/code-execution-with-mcp) + modelcontextprotocol.io spec | MCP rep |
| [How we built our multi-agent research system](https://www.anthropic.com/engineering/multi-agent-research-system) | Read this *and* the cost/latency numbers in it. It's the honest case **for** multi-agent — argue with it using your own eval results |
| [Building agents with the Claude Agent SDK](https://www.anthropic.com/engineering/building-agents-with-the-claude-agent-sdk) | If you'd rather not hand-roll the loop |

## November / December — discovery, pricing, selling

Technical reading stops. These are the ones that matter for the back half:

| Read | Why |
|---|---|
| *SPIN Selling*, Rackham — ch. 1-4 only | Situation/Problem/Implication/Need-payoff. The question structure you'll use in every discovery call |
| *The Mom Test*, Fitzpatrick — whole thing, it's short | How to ask about a business without getting flattering lies. The highest-value book on this list |
| *Pricing Creativity* or Jonathan Stark's *Hourly Billing Is Nuts* | Value pricing. You will otherwise default to hourly and undercharge by 5x |
| A few real SOWs / proposals (ask Claude to generate realistic ones, or find public ones) | You've never written one. Read five before writing one |

## Standing

- Anthropic engineering blog: https://www.anthropic.com/engineering — check monthly
- Anthropic cookbook: https://github.com/anthropics/anthropic-cookbook

_Links under "Read" without a URL: search by title. Claude can pull current URLs on request._
