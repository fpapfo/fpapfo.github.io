---
layout: page
title: Workshop
permalink: /workshop/
---


A look behind the scenes at workflows and decision-support tools currently under development. This is where I document ideas, prototypes and lessons learned as they evolve.


## FTE Decision Support Workflow 

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


### The two-sided flow
**Side 1 — the model (mine, in Excel)**
staff costs & FTE budget model.xlsx → the single source of truth. Establishment, actuals/forecast, current budget, three budget years, candidate scenarios. Everything downstream reads from it and reconciles back to it.

**Side 2 — the pipeline (mine, in Python) — five scripts, run in order:**

Step	Script	Does
1	extract_model.py	Reads the workbook → tidy CSVs
2	reconcile.py	Gate — extract must tie to the workbook or everything stops
3	build_scenario_data.py	Role-level primitives → JSON + the decision tool
4	verify_engine.py	Proves the JS engine reproduces every cell
5	analyse.py	Outturn, variance, bridge, by department/band
Then the presentation builders: build_csuite.py (the C-suite tool) and build_board.py (the board pack).

The three-stage story

ANALYSE ─────────────▶ DECIDE ──────────▶ GOVERN
(C-suite tool)         (C-suite HITL)     (Board pack)
full disclosure        pick scenario      curated, locked
Analyse — csuite-tool.html: how did we do (−8.62%), where we're heading (standstill waterfall + pay-award lever), departments drill-down, scenarios, concerns & flags. C-suite see everything.
Decide — the human checkpoint. C-suite lock the pay award and the candidate roles.
Govern — board-pack.html: same numbers, board-framed, function-level, locked to the decision.
What runs it
/run-workflow — the orchestrator that chains the stages, with a learn-mode toggle. Learn mode on → fp-coach teaches at each step (What / Why / The idea / Watch for / Your turn), grounded in your real numbers.
The board-presentation skill pack underneath: input-fte-model, fp-data-check, variance-analysis, mgmt-report, fin-storytelling, board-deck, viz-design, html-slides, exec-summary, fp-coach.
The through-line
One reconciled dataset, many views. Every output — c-suite tool, board pack, exec summary — renders from the same tied-back numbers. Change the workbook, re-run the pipeline, everything refreshes and nothing can silently disagree. That's what the reconciliation gate and the engine-parity check protect.

