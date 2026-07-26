---
title: "Don't Replace Your Finance Model. Give It Wings."
excerpt: "The wings are a workflow. Everyone is asking whether AI can do the budget, which is the wrong question. Here is what happened when I wrapped a workflow around a finance model I already trusted, the three-way split that keeps it safe, and where it is up to now."
---
*The wings are a workflow. Everyone is asking whether AI can do the budget, which is the wrong question. Here is what happened when I wrapped a workflow around a finance model I already trusted, the three-way split that keeps it safe, and where it is up to now.*

Every AI-in-finance demo asks the same thing. Can the model do the budget? Watch it read a spreadsheet, write some commentary, draw a chart. Impressive for about a minute, until you remember that in finance the output has to be repeatable, reliable and auditable. A budget isn't a draft you regenerate when it looks a bit off. Someone signs it. Someone gets held to it.

So the question was never "can AI do the budget". It was "which parts of this are safe to hand over, which parts need me, and how do I keep all of it tied back to something I can defend in a room". That comes down to telling three kinds of work apart, and most of the value is in the telling apart.

## Deterministic, probabilistic, human

**Deterministic** work has one right answer and must give the same answer every time. The arithmetic of a cost model, the reconciliation, pulling the figures out, the on-cost build. This is code and formulas, not judgement, and it should be boringly exact. Let a language model freestyle here and you have lost.

**Probabilistic** work is where judgement and language live. What's worth flagging to the board. How to tell the story of a variance. How to design a tool a non-finance director can actually use. This is where AI earns its keep, because it is fast, tireless and good at the first draft of exactly the things that eat an FP&A week.

**Human in the loop** is the decisions, and the ownership. Which scenario we back. Which roles we defer. The sign-off. Not a rubber stamp at the end, a seat at defined points all the way through. And the human owns the source of truth.

Most of the design was just labelling each step: deterministic, probabilistic, or mine.

## The model isn't the problem, and it's not going anywhere

Here is the bit the demos skip. Finance is not a blank page. We have models, built over years, that hold a fortune in hard-won logic. Mine is a Staff Costs and FTE model: current-year budget, actuals and forecast, a three-year plan, every position with its grade, pension and on-costs. I trust it. I am not binning it to start again with a chatbot.

So this was the opposite of "replace the model". Take the model I already have and know, and use a workflow to build the slow bits, the parts that eat the days: the validation, the analysis, the finessing, and the decision tools Excel makes genuinely hard to build.

The rule, which I never broke, is that the workbook stays the single source of truth and the audit trail. Nothing the workflow produces is allowed to become a second, competing version of the numbers. Everything reads from the workbook and reconciles back to it, to the penny. The tools reflect the model. They never fork it. That one rule is the whole reason this is safe to put in front of a board.

## What the workflow does

It takes the workbook and, in order:

- **Validates it.** Before anything is built, the extract has to tie back to the workbook's own summaries. Hard gate. If it does not reconcile, nothing downstream runs.
- **Builds an exec pack and a decision tool.** The pack is the analysis, done. The tool is the thing Excel will not easily give you: candidate roles you can switch on and off, defer, re-grade, with the cost, the department split and the grade mix all moving in real time. Scenario testing you can think with, live, in front of people.
- **Then, once a budget is agreed, builds a board-ready pack** from that agreed position.

The human sits at every seam. You pick the scenario. You agree the budget before the board version exists. The tool informs the call. It does not make it.

Under the bonnet, that maps cleanly onto the three-way split. The deterministic layer is code that reads the workbook, extracts every figure and reconciles it back. The decision tool reproduces the model's own arithmetic exactly, so its numbers tie to the workbook to the penny, if they ever disagreed, the tool would be the thing that's wrong. The judgement, the narrative and the design sit on top of that, and I stay in the chair for every decision.

  Centred with optional caption:

<figure style="text-align:center">
    <img src="/assets/images/workflow-diagram.svg" alt="Workflow diagram showing a trusted finance model flowing left to right through four stages, Validate, Build, Decide and Board pack, with a dotted line looping every stage back to the model. Each stage is colour-coded as deterministic, probabilistic or human in the loop.">
    <figcaption>A model you already trust, validated to the penny, turned into an exec pack and a live decision tool, signed off by a human, then built into a board pack, with everything reconciling back to the workbook. Colour-coded by the three-way split: deterministic, probabilistic, human.</figcaption>
  </figure>

## Sometimes you improve the model, on purpose

You will occasionally tweak the model itself. Not to fix it, but to give the workflow more to work with. The workflow can only surface what the model knows, so now and then it is worth teaching the model to know a little more.

A small example that pays for itself. I added an establishment count, the approved number of posts for each role, sitting next to a live count of who is actually in them. Costs almost nothing to build. Changes what you can see. A vacancy that used to hide, no error, no broken formula, just a quietly missing person, becomes a single line that reads "4 approved, 3 filled". That's the kind of enhancement worth making: cheap in the model, and it turns something invisible into something the board can act on.

## What broke, and why that's the point

It wasn't friction-free, but that's reassuring, because every bump was caught by something built to catch it.

The reconciliation gate proved itself on day one. I had enhanced a lookup table, added one column, and every formula that pulled from it by position quietly shifted along by one. Cost centres started reading manager names. Nothing errored. The totals still footed, perfectly. Only the cross-check against the workbook caught it. That's the entire case for the gate: in finance, the dangerous errors are the silent ones, the ones that still foot.

The AI got things wrong too, confidently, more than once. It decided a second post-holder was a maternity cover, and that a role was double-funded, and it was wrong on both, because it did not know the business the way I do. I caught it because I did. That isn't the approach failing. That's the approach *working*. The human in the loop is not a courtesy, it is the control. A fast, capable, fallible assistant, never an oracle.

And the lesson that turned up more than once: hard references break when the structure moves, and named or structured references survive. The workflow will not fix that for you. But it will catch it, which is a great deal better than a formula that fails silently for three months.

So none of it slipped through. That's the point. The guardrails did exactly what guardrails are for.

## Where it is now

This is working, and it is early and in progress, and both are true at once.

The outputs are already strong. The [exec pack](assets\tools\csuite-tool.html), the [decision tool](assets\tools\fte-decision-tool.html) and the [board deck](assets\tools\board-pack.html) are the kind of thing that used to eat a week of my time, and they are sitting there reconciled to the model, to the penny. Good enough that the value is obvious. Early enough that I can still see the edges I want to file down.

What's left is the unglamorous, important part, and I am not going to pretend otherwise. Polishing the outputs so they are not just right but a pleasure to read. Pinning down what the workflow looks like end to end, so it isn't a clever one-off but something that runs the same way every single time. And wrapping it in the controls a finance team can actually lean on: reliable, repeatable, auditable, every run, not only the good ones.

So, a work in progress. But the shape of it is already clear, and it is a good shape: a trusted model, a workflow that does the slow work, a human on the decisions, and everything tied back to one source of truth. It is off to a genuinely strong start.

## The takeaway

If you take one thing from this, take the split. Work out which parts of your process are deterministic, which are probabilistic, and where you have to sit. Automate the first without mercy. Let AI draft the second. Guard the third. And whatever you build, tie it back to the model you already trust, or you have simply built a faster way to be wrong.

The current outputs, the exec pack, the decision tool and the board deck, are up in the [workshop](workshop.md), and that's where I will keep posting progress as the workflow firms up. Have a poke around and check back, because it is only going to get better from here.
