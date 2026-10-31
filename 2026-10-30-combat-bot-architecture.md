---
title: "A Practical Architecture for a Screeps Combat Bot"
date: 2026-10-30 09:00:00 +0000
categories:
  - guides
  - bot-design
tags:
  - architecture
  - combat-ai
  - screeps
excerpt: "A combat bot becomes easier to reason about when observation, evaluation, decisions, and execution are separate stages."
---

A combat bot is not one clever function. It is a collection of smaller systems that transform game state into coordinated actions. The first architectural goal is therefore not maximum sophistication; it is making each decision understandable, testable, and replaceable.

This article lays out a starting structure. It is deliberately framework-level: the exact module boundaries should follow the needs of your bot and the Screeps API version you target.

## 1. Separate the decision pipeline

A useful mental model has four stages:

1. **Observe** — collect the relevant visible game state.
2. **Evaluate** — turn observations into useful facts, scores, and constraints.
3. **Decide** — choose intents or assignments for the current tick.
4. **Execute** — translate those decisions into Screeps API calls and record outcomes.

Keeping these stages distinct makes it easier to answer questions such as: did the bot misunderstand the room, evaluate a situation badly, choose the wrong action, or fail to execute the action it selected?

## 2. Give modules clear responsibilities

A first version might contain modules for:

| Module | Responsibility |
|---|---|
| `combat/observe` | Build a compact snapshot of visible combat state |
| `combat/evaluate` | Derive threat, support, and opportunity information |
| `combat/assign` | Manage squad or creep responsibilities |
| `combat/decide` | Select the next intent for each unit |
| `combat/execute` | Issue movement and action intents |
| `combat/telemetry` | Record decisions and outcomes for later analysis |

These are conceptual names, not required filenames. Start with fewer modules if the project is small; split them when responsibilities begin to overlap.

## 3. Make decisions observable

A bot that only records its final actions is difficult to debug. During development, record a compact explanation of important decisions:

```js
const decisionRecord = {
  tick: Game.time,
  creep: creep.name,
  phase: "combat",
  selectedAction: "example-action",
  reason: "replace this with the actual decision reason"
};
```

Treat this as a shape for your own telemetry, not as a complete logging system. Keep logs bounded: Screeps has memory and CPU constraints, so store summaries rather than copying the entire game state every tick.

## 4. Keep persistent state intentional

Not every value belongs in persistent memory. Separate information that can be recalculated from information that must survive a tick boundary. Cache derived values only when profiling shows the calculation is worth caching, and give cached data an explicit refresh or expiry rule.

A good rule is to make the lifetime of each piece of data obvious: current-tick local variable, heap cache, persistent memory, or another supported storage mechanism.

## 5. Test each layer independently

Useful tests include:

- Does observation produce a stable snapshot for a known room state?
- Do evaluation functions return predictable values for controlled inputs?
- Does the decision layer choose the expected intent for a test scenario?
- Does execution handle unavailable or invalid actions gracefully?
- Does telemetry explain why a decision was selected?

The objective is to narrow failures to one stage rather than debugging the entire bot as a black box.

## 6. What this architecture does not solve

Separating modules does not automatically produce good combat decisions. It gives you a structure in which to improve those decisions. Movement, coordination, action selection, resource limits, and changing battlefield conditions still need to be designed and evaluated against actual game scenarios.

## Takeaway

Start with a small, observable decision pipeline. Make the inputs and outputs of each stage explicit, then use experiments and battle reports to decide which part deserves more complexity. A strong bot is built through repeated measurement and revision, not through architecture diagrams alone.

---

*Next: add a concrete example from your bot, including its current module layout and one decision trace from a test match.*
