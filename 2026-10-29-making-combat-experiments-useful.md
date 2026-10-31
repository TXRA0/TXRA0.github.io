---
title: "How to Make Screeps Combat Experiments Useful"
date: 2026-10-29 09:00:00 +0000
categories:
  - research
tags:
  - research-methods
  - testing
  - combat-ai
excerpt: "A useful experiment starts with a specific question, a controlled change, and measurements chosen before the result is known."
---

It is easy to change a combat bot, watch a match, and decide that the new version feels better. The problem is that one match can be misleading: room layout, opponents, timing, and random variation can all affect the result.

A small amount of experimental discipline makes your notes much more valuable.

## 1. Write down the question first

Avoid vague goals such as “make combat better”. Turn the goal into a question that can be investigated.

For example:

> Does the new decision rule reduce the number of ticks our squad spends disengaged from its assigned objective in the test scenarios?

A good question identifies the system being changed and an observable outcome.

## 2. Change one meaningful variable

Keep a baseline version. Then change one system or parameter at a time where practical. If you change movement, target scoring, and squad composition together, it becomes difficult to know which change explains the result.

Record the version or commit identifier for every run.

## 3. Choose measurements before testing

Pick a small set of metrics that reflect the question. Depending on the experiment, these might include:

- objective completion rate;
- time taken to complete a scenario;
- units lost or recovered;
- resource or CPU cost;
- time spent idle, blocked, or out of position.

Define each metric precisely. For example, decide what counts as “out of position” before collecting results.

## 4. Use repeatable scenarios

Where possible, compare versions in the same controlled scenarios. Keep notes about room layout, opponent behaviour, unit composition, and any other conditions that could influence the outcome.

Do not treat one unusually good or bad run as proof. Repeat the test and look for a consistent pattern.

## 5. Keep a result table

A simple log is often enough to begin:

| Run | Bot version | Scenario | Metric | Result | Notes |
|---|---|---|---|---:|---|
| 1 | baseline | scenario A | define metric | — | initial reference |
| 2 | candidate | scenario A | define metric | — | record observations |
| 3 | candidate | scenario A | define metric | — | repeat the run |

Replace the placeholders with measurements from your own tests. Avoid inventing precision that the data does not support.

## 6. Record negative results

A change that does not help is still useful information. Write down what you expected, what happened, and what you would test next. This prevents cycling back to approaches that have already been evaluated.

## A compact experiment template

1. **Question:** What are you trying to learn?
2. **Hypothesis:** What do you expect, and why?
3. **Change:** What exactly changed from the baseline?
4. **Scenario:** Under what conditions was it tested?
5. **Metrics:** What was measured, and how was it defined?
6. **Results:** What did the runs show?
7. **Limitations:** What could have influenced the result?
8. **Next step:** Keep, revise, or revert the change?

## Takeaway

Treat every combat improvement as a hypothesis to test. A clear question, repeatable scenario, and honest result log will teach you more than a collection of unstructured match impressions.
