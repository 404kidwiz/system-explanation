---
name: system-explanation
description: "Opt-in coaching for explaining software systems clearly. Use only after an explicit invocation of system-explanation or System explanation on. A normal summary request does not activate it. System explanation off or normal summaries stops the coaching supplement."
disable-model-invocation: true
user-invocable: true
---

# System Explanation

Help the user explain how a system works, using evidence they can understand and discuss. The assistant examines the source; the learner practices the explanation. Independent coding or debugging is not a prerequisite.

## Activation

Start **OFF** in a fresh conversation. Merely discovering this skill, reading its documentation, or receiving a summary request does not switch it on.

- Explicitly invoking this skill or saying **System explanation on** turns it **ON for this conversation**. If there is no accompanying task, acknowledge briefly and wait.
- **System explanation off**, **normal summaries**, or an invocation with the argument **off** turns it **OFF immediately**. If one message contains both directions, OFF wins.
- While ON, supplement requested summaries and provide coaching when asked. Keep unrelated replies unchanged.
- While OFF, omit the standing coaching section and practice question. Still answer architecture questions the user directly asks.
- Follow the latest explicit toggle within the conversation. Retain it in a compaction summary of that same conversation; if the state is unavailable, default OFF. Never write ON to persistent memory, change settings, or schedule future work.

This is a conversational convention. It does not unload context, disable a plugin, or enforce a runtime state machine. Respect the host's normal permissions and instruction hierarchy.

## Explain the system

First establish the scope: the whole application, one feature, or a small change. Use existing context when sufficient; ask a focused question only when the scope is materially unclear.

Inspect relevant source, configuration and available tests with the host's tools. Do not execute the application, access production, or perform writes solely to produce an explanation unless the task calls for it. When evidence is unavailable, explain the gap rather than filling it with a plausible design.

For a requested summary while ON, add a concise **System explanation** covering:

1. **Components:** what each relevant component does, receives and returns, and where its responsibility ends.
2. **Communication:** one concrete request or event, traced from entry to outcome. Name calls, protocols and asynchronous boundaries only when supported.
3. **State:** where durable records, caches, browser state, process memory and connection/session state live. Identify the source of truth and who can change it.
4. **Failure and recovery:** what can fail, how the failure is detected, what happens to the user or data, and the actual recovery path. Distinguish implemented recovery from a recommendation.
5. **Trade-offs:** a meaningful benefit, its cost, and when an alternative might be justified.
6. **Say it aloud:** a short natural explanation, followed by one conceptual practice question.

For a small change, explain the affected component and its immediate context. Combine points where that improves clarity; omit irrelevant categories rather than inventing them. Define necessary jargon in plain language.

## Evidence discipline

Attach a nearby source path or other evidence reference to material claims. Use the labels **Implemented**, **Historical**, **Proposed**, and **Unknown** when a claim's status could be confused. Source inspection establishes what the inspected version contains; static checks do not prove deployment status or runtime health. Treat old notes as leads to verify.

Consider these lenses when applicable:
- Component boundaries and responsibilities.
- Load distribution, connection ownership and session state.
- Queues, events or pub/sub, including missed-event recovery.
- Configuration/control decisions versus request/data processing. This conceptual distinction does not imply separately deployed services.
- Model-agent loops: model proposals, runner execution, tool validation, permissions, limits and termination.

Also examine authentication and tenant boundaries, retries, idempotency and observability where relevant. Do not invent a load balancer, event bus, failover mechanism or other infrastructure to complete a checklist. A missing mechanism can itself be an important finding.

## Practice and deeper coaching

Offer one question the learner can answer conceptually, such as “Which record survives a process restart, and why?” Invite an explanation in their own words, then refine one unclear boundary using the evidence. Avoid memorization-only scripts or unsolicited coding drills. Describe AI-assisted work honestly.

When deeper coaching is requested, expand into a 30-second overview, 2-minute walkthrough, short glossary, component map, request lifecycle and likely follow-up questions with evidence-backed answers. Do not force that full briefing into routine summaries.
