---
title: "The #SPILL! error you didn't see"
excerpt: "A single formula on your QC tab that catches blocked spill ranges before they cause silent errors downstream."
---

3 Minute Read


# One formula that catches silent model errors before they matter

There is a category of Excel error that is particularly dangerous in financial models: the kind that doesn't look like an error at all.

A blocked spill range is exactly that. If a dynamic array formula can't spill because another value is sitting in its path, Excel returns a `#SPILL!` error in the formula cell itself. That part is visible. What's less obvious is that any formula elsewhere in your model that references the spill range will simply return zero or blank, with no error of its own to flag that something is wrong. Totals update, reports populate and everything looks fine. But it's really not fine.

I now add a check for this on the QC tab of every model that uses dynamic arrays.



### The SpillError formula

```excel
=IFERROR(
    IF(ERROR.TYPE(SheetName!A1)=9,
        "ERROR: Spill range is blocked"
    ),
    "Spill Range OK"
)
```

Replace `SheetName!A1` with the first cell of the spill range you want to check.

How it works: Excel's `ERROR.TYPE` function returns a number identifying the type of error in a cell. A blocked spill range produces a `#SPILL!` error, which has error type 9. If the cell contains no error at all, `ERROR.TYPE` has nothing to evaluate and returns `#N/A`. The formula uses this behaviour: `IF(ERROR.TYPE(...)=9)` to catch the blocked spill specifically, and the outer `IFERROR` catches the `#N/A` that appears when everything is working correctly, converting it to "Spill Range OK". The result is a clean two-state output: either the range is blocked, or it is not.



### How I use it on the QC tab

I add one row per spill range in the model, with the check result in the first column and a description in the second:

| Check Status | Description |
|-------|-------------|
| `=IFERROR(IF(ERROR.TYPE(Model!A5)=9,"ERROR: Spill range is blocked"),"Spill Range OK")` | E.g. Spill range on Model tab. Feeds summary table. Dependency: named range `Model_LastRow` |

The description column does two things. First it tells anyone reading the QC tab what that spill range feeds, so they know what is affected if the check fails. Second it notes any named range dependencies. If the spill range relies on a dynamic range control (see the previous post on dynamic ranges) and the check fails without an obvious blocked cell, the named range is the first place to look.

![QC tab showing Check Status column with 'Spill Range OK' and Description column with relevant information to diagnose errors](/assets/images/SpillRangeCheck.jpg)



### What causes a spill range to block?

The most common culprits:

- A value or formula left in a cell that falls within the spill area
- A merged cell anywhere in the spill path (merged cells block spill ranges entirely)
- A stray space character in what looks like a blank cell
- Another formula's output landing in the spill area

The last one is worth highlighting. In a complex model with multiple dynamic arrays, it is possible for one spill range to expand into the path of another. This tends to happen when datasets grow beyond their original anticipated size. The QC check catches it immediately rather than leaving it to surface through a wrong number in a report.



### A note on the previous post

If you are using the dynamic range control technique [from the previous post](/2026/06/16/dynamic-ranges-in-financial-models.html) alongside spill ranges, the two work well together. The `Model_LastRow` named range keeps the spill area bounded, which reduces the risk of a spill range expanding unexpectedly into another part of the model. The QC check is the safety net for when it happens anyway.

### Further reading: ERROR.TYPE reference
If you'd like to extend this approach to catch other error types on your QC tab, here is the full list of what ERROR.TYPE returns:

| Error | ERROR.TYPE value |
|-------|-----------------|
| `#NULL!` | 1 |
| `#DIV/0!` | 2 |
| `#VALUE!` | 3 |
| `#REF!` | 4 |
| `#NAME?` | 5 |
| `#NUM!` | 6 |
| `#N/A` | 7 |
| `#GETTING_DATA` | 8 |
| `#SPILL!` | 9 |
| `#UNKNOWN!` | 10 |
| `#FIELD!` | 11 |
| `#CALC!` | 12 |
| No error in cell | `#N/A` |

**Tip:**
 `#N/A` has a useful property beyond error handling! Most Excel charts won't plot a data point if the cell returns `#N/A`. This makes `NA()` or `IFERROR(formula, NA())` a handy technique for dynamic charts where you want missing or incomplete data to simply not appear. For example, a line chart where an actuals line transitions to a forecast dotted line rather than plotting zeros which can distort the chart scale.

*The SpillError formula takes thirty seconds to add per spill range. The alternative is finding out a range was blocked three weeks later when you're about to present your figures*
