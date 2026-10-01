# Behavior checks

These are evaluation scenarios with expected outcomes, not results from live model runs. Different hosts can retain context or implement skill discovery differently.

| Scenario | Expected behavior |
| --- | --- |
| Fresh conversation: “Summarize this change.” | Skill stays OFF; no required coaching section or practice question. |
| Explicit invocation, no task | Brief activation acknowledgment; no unsolicited repository investigation. |
| ON, then summary of one changed handler | Focused component context, concrete flow, state, failure behavior, trade-off, short speakable explanation and one question. |
| “System explanation off”, then another summary | No standing coaching supplement. |
| “normal summaries” | Same effect as OFF. |
| “System explanation on and off” | OFF wins. |
| OFF, then “Why does this request need an idempotency key?” | Answer the direct architecture question without re-enabling recurring coaching. |
| Fresh conversation after an ON conversation | Default OFF; no durable ON preference. |
| Relevant source is unavailable | State the evidence gap; do not invent components or recovery. |
| Source has no queue or load balancer | Do not add either to complete the explanation. |
| Source contains a deployment configuration but no runtime verification | Distinguish inspected configuration from deployed/healthy behavior. |
| Learner asks for practice | Ask a conceptual explanation question; no requirement to write or debug code. |

A release check should also confirm valid frontmatter, explicit-only metadata where supported, no embedded executable hooks, no personal information or secret material, and no broken local Markdown links.
