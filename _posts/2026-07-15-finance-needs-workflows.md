---
title: "Finance Doesn't Need Better AI Prompts. It Needs Finance Workflows."
excerpt: "Finance needs numbers it can reproduce and evidence, not answers taken on trust. Here's why deliberately designed AI workflows matter for finance."
---


Ask a finance team how they would use AI and most describe the same thing: a chat window, a question typed in, an answer read back. It's the obvious mental model, and it's the *wrong one* for most finance processes. 

An answer you can't reproduce is an answer you can't rely on, and reliance is the whole job. We reconcile, we compare period on period, we put our name under the numbers. A tool that returns a slightly different reply each time you ask has failed that test before it starts.

So the useful question is not what you can get an AI to say. It's:

*"What happens when you stop treating AI as something you prompt and start treating it as one governed step inside a process you control?"*

In this article (10 minute read):
- [Why a prompt isn't a process](#why-a-prompt-isnt-a-process)
- [What an AI workflow actually looks like](#what-an-ai-workflow-actually-looks-like)
- [What determinism buys you](#what-determinism-buys-you)
- [Where AI earns its place](#where-ai-earns-its-place)
- [Why the human remains essential](#why-the-human-remains-essential)
- [What makes it auditable](#what-makes-it-auditable)
- [Closing thoughts](#closing-thoughts)




### Why a prompt isn't a process

A large language model (LLM) is probabilistic by design. Ask the same question twice and you'll likely get two answers that are both reasonable and not quite the same. 

For most of the jobs AI is given, that variation is harmless, even useful; it's what makes the tool good at drafting, rephrasing and summarisation. For finance it's a problem, because our outputs are not opinions. A variance is a number, and it's the same number every time or something has gone wrong.

This is the gap that a prompt can't close on its own. However careful the wording, you are still asking a probabilistic system to produce a result you need to be exact, and hoping it obliges. Hope is not a control. The answer is not a better prompt; it's to stop asking the model to do the parts that must be deterministic and to give those parts to something that behaves the same way every time.

In finance, that requirement isn't optional.
    - The numbers have to be consistent, so that this month can be compared with last. 
    - They have to be reliable, because decisions and (eventually) filed accounts rest on them. 
    - They have to be comparable across periods and entities, or the comparison means nothing. 
    - And they have to be auditable, the strictest test of all: someone who was not there must be able to see what was done.

A process built on "the model said so" fails that test on the first question.




### What an AI workflow actually looks like

Picture a chain of steps rather than a conversation. Each step takes something in, does one defined job, and passes something out, and the output of one step becomes the input of the next. 

Some of those steps are **deterministic**: given the same input they produce the same output every time. Calculating a variance, joining two ledgers, working out days sales outstanding; these have a right answer and must return it identically on every run. 

Other steps are **probabilistic**: they interpret, they weigh, they draft. Asked to explain why a variance moved, or to turn a set of figures into commentary a budget holder will read, they produce something *considered* rather than something *certain*, and a little variation is the point. These are two of the three forces a workflow draws on. The third is the human, and it matters enough to get its own section later.

The skill is putting each job in the right layer. The numbers are calculated deterministically, so they are exact and reproducible. The interpretation of those numbers is done probabilistically, because that is the part where judgement and language matter. Keep the two apart and you get the best of each; blur them and you get a variance that changes when you ask twice.

There is code underneath this. The deterministic layer runs on Python, and Python is what makes a step repeatable: written once, it behaves the same way every time it runs. The good news is, you don't write the Python code. You work in an editor (in my case Visual Studio Code) with Claude and the Python tooling alongside, defining what each step must do and checking that it did it. If you have technical skills they are far from wasted; you'll understand what's happening underneath and build faster. But the barrier to starting is judgement, not syntax.

The reusable pieces are building blocks called **Skills**. A Skill is a defined task you shape around your company's specifics and refine through testing: a variance calculation, a cash conversion cycle, a commentary step. Once it has been tested and proven, it can be used again, so the next workflow is built from parts you already know and trust.

AI-enabled finance workflows don't all look the same. Some improve existing finance processes, while others create entirely new decision support capabilities.

**Example workflow 1: Variance analysis to board-ready executive briefing.**
<figure>
  <img src="\assets\images\board-deck-workflow.png" alt="Example workflow 1 diagram showing a variance analysis process progressing through audit documentation, management reporting, financial storytelling, human review, board deck preparation, executive summary and meeting preparation.">
  <figcaption>Traditional FP&A reporting redesigned as a governed AI-enabled workflow. Each step has a defined purpose, produces a defined output and uses the most appropriate force before progressing to the next stage.</figcaption>
</figure>


**Example workflow 2: Working capital analysis to interactive decision simulator.**
<figure>
  <img src="\assets\images\ccc-workflow-map.png" alt="Example workflow 2 map showing three analysis skills feeding a CCC report, then a HITL checkpoint, then a decision support tool">
  <figcaption>The same principles can also produce interactive decision-support tools. The workflow validates the analysis, pauses for human review and then generates a business tool rather than a static report. The simulator itself is linked at the end of the article.</figcaption>
</figure>




### What determinism buys you

A deterministic step earns its place because of what becomes possible once you have it. 

**Genuine comparability**
If this month's variance is calculated by exactly the same process as last month's, then a change in the result means the business changed, not that the method drifted. That sounds obvious, but finance processes can fail here: a spreadsheet edited by hand each month, a formula someone extended differently, a step that depends on who ran it. When the process is fixed, the comparison is clean, and comparison is most of what management reporting is for.

**Controls**
A step that behaves identically every time is a step you can put a control around, because you know what it should produce and can test that it did. You can reconcile its output, check it against a total, prove it. A probabilistic step cannot be controlled in the same way; you can review what it produced, but you can't know in advance exactly what it will say. This is precisely why the deterministic and probabilistic work must sit in different layers: controls belong on the parts that have a right answer, and the parts that have a right answer must be the ones producing your figures.

**Repeatability**
A workflow built this way runs the same next month, and the month after. You're not rebuilding it; you're running it. The effort goes in once, into shaping and proving the process, and after that the month-end that used to consume days of careful assembly becomes a process you execute and check. That's not only faster. It's safer, because the thing most likely to introduce an error, a person rebuilding the same work by hand under time pressure, has been taken out of the path.

**Supporting Documentation**
Because the process is fixed, the shape of its evidence can be fixed too. A deterministic step can be made to produce not just a figure but a record of how the figure was reached. I've started building this into my workflows as an output file: an Excel workbook showing the calculations with the formulas behind them, tying to the final numbers, laid out the same way every month. A figure you can reproduce is good; a figure you can reproduce and evidence in a consistent form is what finance actually needs.




### Where AI earns its place

Everything so far has been about keeping the model away from the numbers. So it is fair to ask: What is AI doing here at all? 

The answer is that once the figures are fixed and trustworthy, there is a large amount of work left that has no single right answer, and that is exactly the work a language model is great at.

**Interpretation**
A variance report tells you that overheads are up by a certain amount; it does not tell you what that means. A model given the figures, the prior period, the budget and enough context can read across the whole picture at once and surface what stands out: which movements are large enough to matter, which are unusual against the trend, which cluster together in a way a human scanning column by column might miss. It's not deciding what is true; the numbers already did that. It's directing your attention.

**Analysis & Drivers**
Ask the model why a number moved and it will propose explanations worth investigating. Perhaps a cost increase lines up with a known volume change. Perhaps a timing difference explains an apparent overspend. Perhaps a figure simply sits wrong against everything around it. These are candidates, not conclusions, and that distinction is the whole discipline of this layer. The model is good at generating the hypotheses a reviewer would want to test; it is not the thing that confirms them.

**Narrative**
The most obviously useful and most quietly valuable. Turning a set of movements into commentary a budget holder will actually read, in a consistent voice, pitched to the audience, is slow and repetitive work done by hand, and it's work a model does well. Give it the figures and the drivers and it will draft commentary that is clear and appropriately hedged, ready for a human to sharpen and approve. 

The figures are exact because the deterministic layer made them exact. The words are good because the probabilistic layer is good at words. Each part is doing what it is best at.

**Knowing When to Ask**
A well-built step can also be told when not to guess. Some questions cannot be answered from the figures alone: whether an overspend is genuine or a timing difference that will reverse, whether a movement reflects a real change or a reclassification. Rather than pick an answer and sound confident, the step can be set to pause and ask, putting the question to the person who actually knows. Recognising the limits of what the numbers can tell it is a strength, not a weakness. 

**Decision Support Tools**
There is one more thing a process like this can produce: not just evidence to review, but a tool to use. The second workflow example ends in a cash simulator, a single self-contained HTML file (it opens in any browser with nothing to install), with a slider for each lever and a covenant line that moves as you do. It is only trustworthy because of everything above it: the numbers it starts from were reconciled and reproducible, and the assumptions it carries are the ones the checkpoint named. An auditable process not only lets you check the past; it lets you build something you can act on, because you know what's underneath it.




### Why the human remains essential

It is easy to say a human should stay in the loop. (Everyone says it!) The harder and more useful question is what the human is actually for, because "someone checks it at the end" is not a role, it is a formality.

This is what "human in the loop" should mean: not a person watching the process run, but a person the process is built to consult, at defined points, on the questions only they can answer.

**Judgement**
Go back to the variance that might be a genuine overspend or a timing difference. The model can't settle that if the answer isn't in the figures. The answer is in what you know about the business, the invoice that landed early, the project that slipped. When the step pauses and asks for your input, your answer is not data entry. It's judgement, applied at the one point where judgement is what's missing.

**Challenge**
A model can produce a plausible explanation for almost anything, but plausible is not the same as right. Someone has to look at a driver the model proposed and say "That doesn't match what I saw on the floor during the month," or, "That number looks too clean. Where did it come from?" The workflow generates candidates; a person still has to be willing to reject them.

**Approval**
This should be a decision, not a rubber stamp. Signing off a set of figures means putting your name to them as fit to go forward, and that act only means something if the person doing it *could have said no*. A process that can't be stopped by the human hasn't been approved *by them*; it has merely passed *through them*.

**Accountability**
This is the reason none of this can be delegated to an LLM. When the numbers go to the board, a person has to own them. You can't put a language model in front of an audit committee, and you can't tell a regulator "the process decided". Accountability has to rest with someone who understands what was done and is answerable for it. The machine can perform the work assigned to it; it can't carry the responsibility.

**Example workflow 2: Human-in-the-loop review and approval checkpoint.**
<figure>
  <img src="\assets\images\HITL_checkpoint-lm.png" alt="A Human in the Loop checkpoint in Example Workflow 2: it reports 9 of 9 tests passed, reconciliations tying to the dollar, a table of the numbers that will drive the simulator, a flagged assumption, and a question asking the user to sign off before proceeding">
  <figcaption>The workflow pauses for sign-off. It shows what reconciles, names the one figure that is an assumption rather than a fact, points to the file holding the full working, and asks before going further. This is the human in the loop: not watching, but being asked.</figcaption>
</figure>




### What makes it auditable

An auditor, a reviewer, or you looking back six months later, doesn't want to be simply told the numbers are right. They want to be shown *how they were reached*, and to satisfy themselves without having been in the room. A workflow built the way I've described can give them that, because auditability was designed in rather than added afterwards.

**Defined Steps**
It starts with defined steps. The process is not a person improvising each month; it is a fixed sequence, and you can point to each step and say what it does. Nothing happens that is not one of those steps.

**Defined Inputs and Outputs**
Each step has defined inputs and outputs. The output of one step is the input to the next, so the whole thing is a chain you can walk. You can take any figure at the end and trace it back through the step that produced it, to the step that fed it, to the numbers it started from. There is no point where a value simply appears.

**Defined Artefacts**
Because the deterministic steps behave identically, the evidence arrives in the same form each month. A reviewer learns the layout once; the workbook of calculations, the reconciliation that ties, and the checkpoint that records what was asked and answered all sit in the same place, in the same shape, every period. The form each artefact takes is a design choice, not an afterthought: in testing I keep them as plain Markdown, readable and easy to version; in real use each output takes the form its reader needs, a workbook where the formulas must be checked, a fixed PDF for a board pack. Matching the format to who reviews it is part of the governance.

And the process leaves a record of what actually happened, not just what was meant to happen. The checkpoint shown earlier is part of that record. It states the tests that ran and passed, the reconciliations that tied, and, plainly, the one figure that was an assumption rather than a fact. It names the file where the full working is kept. Then it asks a person to sign off before going further, and that decision becomes part of the record too.

That is the difference between a result and an audit trail. A result is a number. An audit trail is the number, the steps that produced it, the evidence at each step, the point where a human looked at it and approved it, and the file you can open to check the lot. One is an answer. The other is an answer you can stand behind.


**Example outputs from Workflow 1. Each step produces a defined artefact, from audit workbooks and governance records through to management reports, board materials and QA documentation.**
<figure>
  <img src="\assets\images\outputs.png" alt="Example output folder from the example workflow 1, showing sequentially numbered artefacts including variance analysis, audit workbook, governance analysis, management reporting, board deck and quality assurance documents..">
  <figcaption>Example outputs from Workflow 1. Each step produces a defined artefact, from audit workbooks and governance records through to management reports, board materials and QA documentation.</figcaption>
</figure>




### Closing thoughts

None of this replaces finance. The judgement, the challenge, the sign-off and the accountability all stay exactly where they were, with a person who understands the numbers and answers for them. What changes is the machinery underneath: a governed process where the deterministic work is exact and reproducible, the interpretive work is done well and fast, and the human is consulted at the points that need them.

And there's a second change, one you've already seen: A workflow like this can produce the artefact the business actually needs: a controlled workbook, a validated dataset, a board pack, or a decision tool like the cash simulator. The output is designed into the workflow rather than improvised at the end. Building a tool like that used to mean a specification, a developer and a wait. Now a finance professional who understands the problem can commission one directly, shaped to the exact decision in front of them. The understanding was always there; what fell away was the build.

The shift isn't finance handing its work to a model. It is finance keeping every judgement it already owns, and putting a governed, auditable, repeatable process underneath it, with better tools at the end than we have had before.

The numbers still have to be right, and they still have to be yours. This just gives you a better way to get there.


<p>
  <a href="/assets/tools/ccc-simulator.html" target="_blank" rel="noopener noreferrer">
    Open the cash simulator in a new tab
  </a>
  <span aria-hidden="true">↗</span>
</p>


--- 



### Where do you learn how to do this?

The workflow approach described in this article reflects concepts I'm currently exploring through <a href="https://www.tacticfinancial.com/accelerator" target="_blank" rel="noopener noreferrer">Tactic Financial's Accelerator with Carolina Lago</a>.

Beyond the underlying methodology, the course also covers the practical aspects of building AI-enabled finance workflows: designing reusable skills, combining them into governed workflows, and using modern AI development tools effectively.

The workflow diagrams shown throughout this article were created using Tactic Financial Workflow Studio. The methodology isn't dependent on the software, but I found it an excellent way to visualise, communicate and refine finance workflows before and during the build.

If you'd like to explore the methodology in more depth and learn to design and build workflows like these yourself, I'd highly recommend taking a look at the Accelerator.