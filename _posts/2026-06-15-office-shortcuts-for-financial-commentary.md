3 Minute Read

### Small setup, big impact

There is a five-minute setup I do on new computers before I write a single line of financial commentary or build a single model. It costs nothing and doesn't require an IT ticket and I'm surprised by how few people in finance know it exists.

Microsoft Office syncs AutoCorrect entries across the entire suite: Excel, Word, PowerPoint, Outlook, OneNote. Set it up once and your shortcuts follow you everywhere, giving you instant access to characters you can't type directly from the keyboard:

```
▲ Overtime costs £23k above budget
   ↳ Vacancy unfilled since Q1
   ↳ Agency cover at premium rates offsetting £43k headcount saving
   ∴ Underlying favourable variance of £66k masked by agency cost. Likely to persist until role is filled.
```


### Setup

Go to **File > Options > Proofing > AutoCorrect Options** in any Office application. From there, you can add custom replace-with pairs: type a trigger, and Office swaps it for whatever character or symbol you have defined.

I use a full stop/dot prefix (`.`) to avoid accidental triggers mid-word. Here is my full list:

| Type this | Get this | What it is for |
|-----------|----------|----------------|
| `.delta` | Δ | Variance symbol in commentary |
| `.var` | Δ | Same, for when I blank on the longer one |
| `.sum` | Σ | Summation |
| `.increase` | ▲ | Upward movement |
| `.inc` | ▲ | Shorthand version |
| `.decrease` | ▼ | Downward movement |
| `.dec` | ▼ | Shorthand version |
| `.warn` | ⚠ | Flag for attention items |
| `.w` | ⚠ | Shorthand version |
| `.tick` | ✓ | Confirmed / complete |
| `.t` | ✓ | Shorthand version |
| `.cross` | ✗ | Rejected / incorrect |
| `.x` | ✗ | Shorthand version |
| `.approx` | ≈ | Approximation |
| `.a` | ≈ | Shorthand version |
| `.cont` | ↳ | Continuation, showing a point flows from the one above |
| `.c` | ↳ | Shorthand version |
| `.point` | ► | Leading into a key point or call-out |
| `.p` | ► | Shorthand version |
| `.therefore` | ∴ | Logical conclusion in narrative |
| `.f` | ∴ | Shorthand version (therefore = **f**inally? I know. It is what stuck.) |

I include both long and short versions deliberately. There are days when `.t` comes naturally. There are days when I type `.t` looking for ∴ and have to remind myself that is `.f`. Having both means I get there, either way.


### Why this matters for FP&A commentary

Good financial commentary is precise and scannable. A CFO reading a variance pack before a board meeting is not reading every word, they are scanning for signals. Symbols carry meaning instantly in a way that words sometimes do not.

In practice, this is what tighter commentary looks like:

```
▲ Revenue +£125k vs budget
   ↳ Higher customer volumes in the period
   ↳ Improved product mix offsetting unit price pressure
```

Or at summary level, where the logical thread matters:

```
Revenue ahead of forecast ∴ EBITDA ahead of budget despite cost pressures
```

The symbols are not decoration. Used consistently, they become a visual language your stakeholders learn to read quickly. The `.cont ↳` is particularly underused. It is useful for showing that a sub-point flows from the one above without repeating context, which keeps commentary tight and avoids the padding that dilutes the message.


### A note on the setup process

You will need to add these one at a time in the AutoCorrect dialog as unfortunately there is no bulk import option. I'd suggest doing it in Word or Outlook where you can test immediately by typing in a document. The changes will sync to the rest of the suite automatically over a few minutes.

One caveat: AutoCorrect entries are stored locally, so moving to a new machine means starting again. I keep a reference copy in my notes for exactly this reason. The setup takes five minutes, but only if you can remember what you had.


*Small habits, compounded over time, are where a lot of the real efficiency in this job lives.*
