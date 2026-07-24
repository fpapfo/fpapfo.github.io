---
layout: page
title: Workshop
permalink: /workshop/
---


A look behind the scenes at workflows and decision-support tools currently under development. This is where I document ideas, prototypes and lessons learned as they evolve.


### staff costs & FTE Budget Workflow 

**Goal**

Turn an existing model (in this case my staff costs & FTE budget model) into a full workflow, including:

* Input budget model
* Verify, C-Suite Budget presentation pack with
* Interactive decision-support tool

* C-Suite presentation pack with interactive decision-support tool
* Board presentation pack

**Current stage** 
* Model exists (my own)
* Workflow architecture complete
* Outputs undergoing design and testing (to be added here over next few days)


#### The two-sided flow

**Side 1 — the model (mine, in Excel)**

staff costs & FTE budget model.xlsx → the single source of truth. Establishment, actuals/forecast, current budget, three budget years, candidate scenarios. Everything downstream reads from it and reconciles back to it.

**Side 2 — the pipeline (mine, in Python) — five scripts, run in order:**

  | Step   | 	Script   | 	Does   | 
|----------|----------|----------|
  | 1  | 	extract_model.py  | 	Reads the workbook → tidy CSVs   | 
  | 2  | 	reconcile.py  | 	Gate — extract must tie to the workbook or everything stops  | 
  | 3  | 	build_scenario_data.py   | 	Role-level primitives → JSON + the decision tool   | 
  | 4  | 	verify_engine.py   | 	Proves the JS engine reproduces every cell   | 
  | 5  | 	analyse.py   | 	Outturn, variance, bridge, by department/band   | 

Then the presentation builders:
build_csuite.py (the C-suite tool) and build_board.py (the board pack).

The three-stage story

| ANALYSE ───────►  | DECIDE ───────►  | GOVERN | 
|----------|----------|----------|
| (C-suite tool) |         (C-suite HITL)|     (Board pack) |
| full disclosure |        pick scenario |      curated, locked |

1) Analyse — csuite-tool.html:
 - how did we do (−8.62%), 
 - where we're heading (standstill waterfall + pay-award lever), 
 - departments drill-down, 
 - scenarios, 
 - concerns & flags. 
 - C-suite see everything.

2) Decide — the human checkpoint. C-suite lock the pay award and the candidate roles.

3) Govern — board-pack.html: 
 - same numbers, 
 - board-framed, 
 - function-level, 
 - locked to the decision.

**What runs it**

/run-workflow — the orchestrator that chains the stages, with a learn-mode toggle. 

Learn mode on → fp-coach teaches at each step (What / Why / The idea / Watch for / Your turn), grounded in your real numbers.

The board-presentation skill pack underneath: input-fte-model, fp-data-check, variance-analysis, mgmt-report, fin-storytelling, board-deck, viz-design, html-slides, exec-summary, fp-coach.
The through-line

One reconciled dataset, many views. Every output — c-suite tool, board pack, exec summary — renders from the same tied-back numbers. Change the workbook, re-run the pipeline, everything refreshes and nothing can silently disagree. That's what the reconciliation gate and the engine-parity check protect.


## fp-coach

**What it is**

A skill that turns the workflow into a learning experience for whoever runs it, so a person who is not a finance expert understands what is happening rather than clicking through blind.

**How it fires**

It is wired into the /run-workflow orchestrator. At the very start, the workflow asks one question: "Learn mode, or straight through?"

**Learn mode on: at each step that carries a real concept (a variance, an assumption, a finding), the coach produces a teaching moment.**

Straight through: for an experienced user, it skips the teaching and just confirms each step. The coaching is a toggle, never a tax on someone who already knows the material.
The shape of a teaching moment

Every one follows the same five parts, kept short:
- **What** the number or step is, in plain English
- **Why it matters**
- **The idea**, the finance concept taught simply
- **Watch for**, the trap that is easy to make and hard to see
- **Your turn**, a prediction the operator makes before you reveal the answer

That last part is the important one. A guess someone makes themselves sticks far better than a fact they read.

**The principles underneath**

- Teach at the moment the number appears, never a lecture up front
- Always grounded in the real figure on screen, not abstract theory
- Name the trap, because the mistake a totals check will not catch is the most valuable thing to teach
- Verify any rate against source and let them see you do it, so the habit of not trusting a half-remembered number is part of the lesson
- Respect the operator: do not patronise, do not re-teach what they clearly know

**The curriculum**

The skill carries a table of the concepts this workflow throws up, each with its idea and its trap: outturn, variance, standstill, committed versus candidate, part-year and full-year effects, on-costs, the NI threshold, DB versus DC pension, SMP and maternity, and successor chains. It is meant to grow as new concepts come up.

**What I've seen it do so far**

I ran this workflow with teaching moment live, on my real numbers. Claude posed the current-year underspend and asked whether an underspend is good news and what drove it. I explained the various drivers - pension take-up, part-timers, vacancy gaps, underpaid bonus, then the reveal scored each explaining the variance and whether it was a real feature or the main driver. 

**State**
The skill is written and wired, and we've proven the format works on one moment. What it has not done yet is run end to end through a full workflow with learn mode on from start to finish. That is the natural next test once the other pieces settle.
