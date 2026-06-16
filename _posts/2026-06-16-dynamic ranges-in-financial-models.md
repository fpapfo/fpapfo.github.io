# Set it once, forget it forever

There is a small piece of setup I include whenever I have a formula-heavy sheet referencing a dataset on another sheet that will grow over time. It takes about two minutes, lives quietly on the Assumptions or QC tab and means I never have to update a formula range when my dataset grows. I have refined this over time rather than always done it from the start but having used it consistently on recent models I would not go back to using fixed ranges in my formulas.

The problem it solves is this: most Excel formula ranges are static. You write `$A$5:$A$150` and it works fine until someone adds row 151, at which point your SUMIFs, COUNTIFs and conditional formatting quietly start returning wrong answers with no error and no warning. Just a number that is subtly wrong and waiting to be found at the worst possible moment.

You can use whole-column references (`$A:$A`) to avoid this, but that forces Excel to evaluate the entire column on every recalculation, which is expensive on any model of meaningful size. Dynamic arrays help, but spill ranges can leave blank rows at the bottom of your output and have their own considerations.

The approach I use instead builds a named range that always knows where the data ends.


### Finding the last row

On the Assumptions or QC tab, I add this LastRow formula:

```excel
=LOOKUP(2,1/(Model!$A:$A<>""),ROW(Model!$A:$A))
```

This returns the **row number** of the last populated cell in the specified column. This is a Row number rather than row count, because that is what INDEX needs to build a range later.

One important practical note: point this at a column that will **always** have a value in every row of your dataset. If your data has gaps in that column, the formula will stop at the wrong place. Pick whichever column is mandatory in your data structure, whether that's an ID field, a date or whatever your structure guarantees will be populated in every row.

I then define the name of this cell as `Model_LastRow`, where *Model* is the name of the worksheet or dataset the formula is pointing at. So if your data lives on a tab called *Tracker*, the LastRow formula points to *Tracker* and the named range becomes `Tracker_LastRow`. This keeps named ranges self-documenting and anyone opening the workbook immediately knows which dataset each named range refers to.


### Setting up the control rows

I include this in a structured block on the Assumptions or QC tab:

| Value | Label |
|-------|-------|
| LastRow formula result | Last row on Model — Named Range: `Model_LastRow` |
| Fixed number e.g. 100 | Buffer |
| Sum of above | Max Row — Named Range: `Model_MaxRow` |

The buffer is optional. For some datasets I want headroom below the last row to allow space for the data to grow into without immediately hitting the boundary. For others where the last row should be a hard stop, the buffer is zero and `Model_LastRow` and `Model_MaxRow` are the same value.

If a buffer is involved, this block belongs on the Assumptions tab because the buffer size is a model assumption. If there is no buffer and it is simply tracking the last row automatically, it belongs on the QC tab.


### Using it in formulas

Anywhere I would previously have written a fixed range, I now write this instead:

```excel
Model!$A$5:INDEX(Model!$A:$A,Model_MaxRow)
```

The INDEX function returns the cell at row `Model_MaxRow` in the specified column, giving Excel a concrete cell reference to use as the end of the range. As the dataset grows and `Model_LastRow` updates, every formula using this pattern updates automatically with it. No manual range edits, no formulas silently excluding new rows.

This works in SUMIFS, COUNTIFS, named ranges, array formulas and conditional formatting formula conditions.

Sadly it does **not** work in the "Applies to" box in conditional formatting, that field requires a static range reference. (The Excel team may consider this working as intended, but dynamic "Applies to" ranges would be a very welcome addition!)


### The "calculate to here" use case

This technique also solves a problem specific to financial models: intentional calculation boundaries.

In a financial model it is common to have a dataset where some rows should be included in calculations and some should not: a section below a defined line that exists in the model but should never be scooped up into a SUMIF or a total. With a fixed range like `$A$5:$A$150` this boundary is hidden inside the formula. If someone adds a row at position 152 thinking it is outside the range, there is nothing to tell them they are wrong. The model returns a subtly incorrect answer and the error may not surface until it matters.

The dynamic range approach handles this differently. I add a deliberately blank row at the point where calculations should stop, ensuring the lookup column in that row is empty. The LOOKUP formula sees no value there, treats it as the end of the data, and `Model_MaxRow` stops at the row above. Everything below the blank row is automatically excluded from all formulas using the dynamic range pattern, with no fixed range to maintain and no silent boundary to accidentally breach.

![Spreadsheet showing a boundary row preventing data below from being included in model calculations](../assets/images/CalculateToHere.jpg)

The blank row becomes the explicit, visible boundary. The intention is built into the model structure rather than hidden in a formula reference.


### A note on tables

Excel tables handle dynamic ranges automatically and for straightforward datasets are often the right choice. However they have limitations that make them unsuitable in some situations: they do not support dynamic headers, do not work well with repeating values or gaps in headers, and can interfere with certain formula structures. For the "calculate to here" use case, a second table below the boundary might seem like a solution, but the moment the first dataset grows into the second table's territory you hit expansion conflicts or spill errors. The named range approach handles all of these situations cleanly and sits more comfortably inside complex model structures.



*The two minutes this takes at the start of a model build pays back every time the dataset changes and nothing breaks.*
