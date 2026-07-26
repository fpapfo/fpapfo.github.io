---
layout: page
title: Workshop
permalink: /workshop/
---


A look behind the scenes at the workflows and decision-support tools I am building. This is where I document the ideas, prototypes and lessons as they take shape.

---

## Staff Costs & FTE Budget Workflow

*One workflow, three kinds of work. The model stays the source of truth, the workflow does the slow work, and the human owns every decision.*

**Goal.** Turn an existing model, in this case my Staff Costs & FTE budget model, into a full workflow:

* Input the budget model
* Validate and reconcile
* C-suite pack with an interactive decision-support tool
* Board presentation pack

<figure style="text-align:center">
    <img src="/assets/images/workflow-diagram.svg" alt="Workflow diagram showing a trusted finance model flowing left to right through four stages, Validate, Build, Decide and Board pack, with a dotted line looping every stage back to the model. Each stage is colour-coded as deterministic, probabilistic or human in the loop.">
    <figcaption>A model you already trust, validated to the penny, turned into an exec pack and a live decision tool, signed off by a human, then built into a board pack, with everything reconciling back to the workbook. Colour-coded by the three-way split: deterministic, probabilistic, human.</figcaption>
  </figure>


**Current stage.**

* The model exists (my own)
* The workflow architecture is complete
* The first outputs are ready to view below, with more to follow as they firm up

**The outputs.** These render straight from the reconciled model, so they always agree with it.

* **[C-suite analysis](/assets/tools/csuite-tool.html) and [decision tool](/assets/tools/fte-decision-tool.html)**: the interactive pack. How the year landed, where the budget is heading (the standstill waterfall and the pay-award lever), a departments drill-down, live scenario testing, and the concerns and flags.
* **[Board pack](/assets/tools/board-pack.html)**: the same numbers, board-framed at function level and locked to the agreed decision.

**The two-sided flow.**

*Side 1, the model (mine, in Excel).* Staff Costs & FTE Budget Model.xlsx is the single source of truth: establishment, actuals and forecast, current budget, three budget years, candidate scenarios. Everything downstream reads from it and reconciles back to it.

*Side 2, the pipeline (in Python).* Five scripts, run in order:

| Step | Script                 | What it does                                                        |
| ---- | ---------------------- | ------------------------------------------------------------------- |
| 1    | extract_model.py       | Reads the workbook into tidy CSVs                                   |
| 2    | reconcile.py           | The gate: the extract must tie to the workbook, or everything stops |
| 3    | build_scenario_data.py | Role-level primitives to JSON, plus the decision tool               |
| 4    | verify_engine.py       | Proves the JavaScript engine reproduces every cell                  |
| 5    | analyse.py             | Outturn, variance, bridge, by department and band                   |

Then the presentation builders: build_csuite.py for the C-suite tool, and build_board.py for the board pack.

**The three-stage story.**

| Analyse         | Decide             | Govern          |
| --------------- | ------------------ | --------------- |
| C-suite tool    | C-suite checkpoint | Board pack      |
| Full disclosure | Pick the scenario  | Curated, locked |

1. **Analyse** (csuite-tool.html): how we did this year, where we are heading (the standstill waterfall and the pay-award lever), a departments drill-down, the scenarios, and the concerns and flags. The C-suite see everything.
2. **Decide**: the human checkpoint. The C-suite lock the pay award and the candidate roles.
3. **Govern** (board-pack.html): the same numbers, board-framed, at function level, locked to the decision.

**What runs it.**

/run-workflow, the orchestrator that chains the stages, with a learn-mode toggle. Learn mode on: fp-coach teaches at each step (What, Why, The idea, Watch for, Your turn), grounded in the real numbers on screen.

Underneath sits the board-presentation skill pack: input-fte-model, fp-data-check, variance-analysis, mgmt-report, fin-storytelling, board-deck, viz-design, html-slides, exec-summary and fp-coach.

**The through-line.**

One reconciled dataset, many views. Every output, the C-suite tool, the board pack, the exec summary, renders from the same tied-back numbers. Change the workbook, re-run the pipeline, and everything refreshes with nothing able to silently disagree. That's what the reconciliation gate and the engine-parity check protect.


<p style="color: red;">The new addition to my workflows:</p>

## fp-coach

**What it is.** A skill that turns the workflow into a learning experience for whoever runs it, so someone who is not a finance expert understands what's happening rather than clicking through blind.

**How it fires.** It is wired into the /run-workflow orchestrator. At the very start, the workflow asks one question: "Learn mode, or straight through?"

Learn mode on: at each step that carries a real concept (a variance, an assumption, a finding), the coach produces a teaching moment. Straight through: for an experienced user, it skips the teaching and just confirms each step. The coaching is a toggle, never a tax on someone who already knows the material.

**The shape of a teaching moment.** Every one follows the same five parts, kept short:

* **What** the number or step is, in plain English
* **Why it matters**
* **The idea**, the finance concept taught simply
* **Watch for**, the trap that's easy to make and hard to see
* **Your turn**, a prediction the operator makes before the answer is revealed

That last part is the important one. A guess someone makes themselves sticks far better than a fact they read.

**The principles underneath.**

* Teach at the moment the number appears, never a lecture up front
* Always grounded in the real figure on screen, not abstract theory
* Name the trap, because the mistake a totals check will not catch is the most valuable thing to teach
* Verify any rate against source, and let them see you do it, so the habit of not trusting a half-remembered number is part of the lesson
* Respect the operator: do not patronise, and do not re-teach what they clearly know

**The curriculum.** The skill carries a table of the concepts this workflow throws up, each with its idea and its trap: outturn, variance, standstill, committed versus candidate, part-year and full-year effects, on-costs, the NI threshold, DB versus DC pension, SMP and maternity, and successor chains. It is meant to grow as new concepts come up.

**What I have seen it do so far.** I ran the workflow with a teaching moment live, on my real numbers. Claude posed the current-year underspend and asked whether an underspend is good news, and what drove it. I gave my read: pension take-up, part-timers, vacancy gaps, an underpaid bonus. The reveal then scored each one, how much it explained the variance, and whether it was a genuine feature or the main driver.

**State.** The skill is written and wired, and we have proven the format works on one moment. What it has not done yet is run end to end through a full workflow with learn mode on from start to finish. That's the natural next test once the other pieces settle.