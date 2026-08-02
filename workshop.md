---
layout: page
title: Workshop
permalink: /workshop/
---


A look behind the scenes at the workflows and decision-support tools I am building. This is where I document the ideas, prototypes and lessons as they take shape.

*Last updated: 2 August 2026.*

---

## Staff Costs & FTE Budget Workflow

*One workflow, three kinds of work. The model stays the source of truth, the workflow does the slow work, and the human owns every decision.*

**Goal.** Turn an existing model, in this case my Staff Costs & FTE budget model, into a full workflow that runs from a trusted workbook all the way to a locked, signed-off board position, with everything reconciling back to the model at every step.

<figure style="text-align:center">
    <img src="/assets/images/workflow-diagram.svg" alt="Workflow diagram showing a trusted finance model flowing left to right through four stages, Validate, Build, Decide and Board pack, with a dotted line looping every stage back to the model. Each stage is colour-coded as deterministic, probabilistic or human in the loop.">
    <figcaption>A model you already trust, validated to the penny, turned into an exec pack and a live decision tool, signed off by a human, then built into a board pack, with everything reconciling back to the workbook. Colour-coded by the three-way split: deterministic, probabilistic, human.</figcaption>
  </figure>


**Where it is now.** The model exists (my own), the architecture is mapped end to end as the 0 to 7 flow below, and the first outputs render straight from the reconciled model. The early stages, validate, analyse and build, are working. The later stages, the feedback loop back into the model, the board re-run and the archive, are being built and firmed up. Still very much in progress, and documented here as it moves.

**The full workflow, stage by stage.** Every stage is one of three kinds of work: deterministic (one right answer, must be exact), probabilistic (judgement and language, where the AI drafts), or a human stop (a decision only a person can own).

| Stage | What happens | Kind | State |
| ----- | ------------ | ---- | ----- |
| 0 | Pre-flight: confirm the year's inputs and the output formats before anything runs | Deterministic check, human confirm | Being wired in |
| 1 | Validate: extract, reconcile, engine parity. No output unless it ties to the workbook | Deterministic, hard gate | Built |
| 2 | Analyse and build: C-suite pack, decision tool, audit. Human reviews before the meeting | Numbers deterministic, commentary probabilistic | Built |
| 3 | Exec decision: choose the scenario and the pay award. The workflow pauses | Human stop | Human step |
| 4 | The user records the approved scenario and pay award into the model and saves an exec-approved version. The LLM never writes to the model | Human write-back | In progress |
| 5 | Re-run on the approved model: board pack, exec summary, Q&As, audit | Deterministic and probabilistic | Outputs drafted |
| 6 | Board governance: approve the envelope and its margin, with the right to challenge | Human stop | Planned |
| 7 | Archive: the signed pack and the audit, versioned and locked | Deterministic | Planned |

The two human stops matter as much as the gates. Stage 3 is where the exec team choose the scenario and the pay award, and nothing moves until they do. Stage 6 is the board approving the envelope, with a standing right to challenge. Between them sits stage 4, the feedback loop, and it is deliberately a human hand on the keyboard. The user, not the LLM, records the approved scenario and pay award into the model and saves a new exec-approved version of the workbook to its own folder. The LLM never makes a writable change to the source-of-truth files anywhere in this workflow: it reads the model and renders from it, but the model itself is only ever edited by a person. Everything downstream then re-runs from that approved position, not a draft of it.

**The outputs so far.** These render straight from the reconciled model, so they always agree with it. Still in progress. Today they are HTML, with the audit also in Excel. In a real deployment the board summary would usually be Word or PDF, and the Q&As Word or PDF depending on who is asking and what they are used to, which is exactly what the pre-flight stage confirms up front.

*Before the exec decision (stage 2):*

* **[C-suite analysis](/assets/tools/csuite-tool.html)** and **[decision tool](/assets/tools/fte-decision-tool.html)**: the interactive pack. How the year landed, where the budget is heading (the standstill waterfall and the pay-award lever), a departments drill-down, live scenario testing, and the concerns and flags.
* **[Audit pack](/assets/tools/audit-pack.html)**, also **[in Excel](/assets/tools/audit-pack.xlsx)**: the working, laid open, so every number can be traced back to the model.

*After the exec decision, for the board (stage 5):*

* **[Board pack](/assets/tools/board-pack.html)**: the same numbers, board-framed at function level and locked to the agreed decision.
* **[Exec summary](/assets/tools/exec-summary.html)**: the short version, the position on a page.
* **[Exec Q&A](/assets/tools/exec-qa.html)** and **[Board Q&A](/assets/tools/board-qa.html)**: the questions each audience is likely to ask, answered from the numbers.

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

Then the presentation builders, which now produce the C-suite tool, the board pack, the exec summary, the exec and board Q&As, and the audit pack.

**What runs it.**

/run-workflow, the orchestrator that chains the stages, with a learn-mode toggle. Learn mode on: fp-coach teaches at each step (What, Why, The idea, Watch for, Your turn), grounded in the real numbers on screen.

Underneath sits the board-presentation skill pack: input-fte-model, fp-data-check, variance-analysis, mgmt-report, fin-storytelling, board-deck, viz-design, html-slides, exec-summary and fp-coach.

**The through-line.**

One reconciled dataset, many views. Every output, the C-suite tool, the board pack, the exec summary, the Q&As, the audit, renders from the same tied-back numbers. Change the workbook, re-run the pipeline, and everything refreshes with nothing able to silently disagree. That is what the reconciliation gate and the engine-parity check protect.

---

## What's next

The architecture is mapped, so the work now is closing the open stages and hardening the run:

* **The feedback loop (stage 4).** The user records the exec decision into the model and saves the exec-approved version, then the workflow re-runs for the board. The write-back stays in human hands; the LLM never edits the source of truth. This is the piece that closes the loop, and the current focus.
* **Pre-flight (stage 0).** A short confirm step for a workflow that only runs once or twice a year: check the year's inputs, the output formats (Word or PDF versus HTML), and the details that quietly drift, such as whether logos or branding have changed since last time.
* **A finalisation checklist.** Review and optimise the skills, and run a pre-mortem to surface what could go wrong before it does, rather than after.
* **Token tracking.** Capture the token count at the start and the end of a run, to build a real picture of what the workflow costs to operate.

---

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

---

## Progress log

*August 2026.* Added the post-approval outputs: a refreshed board pack, the exec summary, the board and exec Q&As, and the audit pack in both HTML and Excel. Mapped the whole workflow as the 0 to 7 flow, with its two human-stop gates. Started planning the pre-flight step, a finalisation checklist and token-usage tracking.

*July 2026.* Wrote and wired the fp-coach teaching skill, and proved the teaching-moment format live on real numbers. First outputs, the C-suite tool, the decision tool and the board pack, rendering from the reconciled model.
