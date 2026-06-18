---
title: "Excel's 56 ColorIndex"
excerpt: "A VBA macro that generates Excel's complete 56-colour index reference in seconds with hex codes and RGB values you can copy paste."
---

3 Minute Read


# Generate your own reference in two seconds

If you've spent any time writing VBA in Excel or you want to add colour to conditional formatting or custom formats, you will have encountered ColorIndex. It is Excel's legacy colour system: 56 colours, each assigned a number, and it appears everywhere in older macros and in certain formatting operations where the newer RGB or hex approaches are not available or simply not necessary.

The problem is that nobody remembers which number maps to which colour. There are reference sheets online, but they are scattered, some are outdated and most are low quality screenshots of uncertain origin and frankly I would rather generate my own directly from Excel.

So here is a macro that builds the reference for you.



## What it produces

Run this on a blank worksheet and it generates a table with one row per colour index (all 56 of them) showing:

- The colour as a cell background with the index number inside it
- The index number
- The hex code (e.g. `#FF0000`)
- The RGB values (e.g. `RGB(255, 0, 0)`)
- The VBA syntax ready to copy (`ColorIndex = 3`)

Text in each colour cell automatically switches between black and white depending on whether the background is dark or light, so the index number is always readable. Headers are styled, columns are auto-fitted, and the header row is frozen.



## The macro

Paste this into a module in a macro-enabled workbook and run it on a blank sheet:

```vba
Sub MapColorIndex()

    Dim i As Integer
    Dim ws As Worksheet
    Dim hexCode As String
    Dim colourLong As Long
    Dim r As Integer, g As Integer, b As Integer
    
    Set ws = ActiveSheet
    
    ' Clear any existing formatting on the output range first
    ws.Range("A1:D57").Clear
    
    ' Set consistent font across entire output range
    With ws.Range("A1:D57")
        .Font.name = "Calibri"
        .Font.Size = 11
        .Font.Color = RGB(51, 51, 51)
        .HorizontalAlignment = xlCenter
        .VerticalAlignment = xlCenter
    End With
    
    ' Set column widths
    ws.Columns("A").ColumnWidth = 15      ' ColorIndex swatch
    ws.Columns("B").ColumnWidth = 15      ' Hex Code
    ws.Columns("C").ColumnWidth = 16.57   ' RGB - slightly wider for the numbers
    ws.Columns("D").ColumnWidth = 15      ' VBA ColorIndex
    
    ' Set a standard row height
    ws.Rows("1:57").RowHeight = 20
    
    ' Add headers
    ws.Cells(1, 1).Value = "ColorIndex"
    ws.Cells(1, 2).Value = "Hex Code"
    ws.Cells(1, 3).Value = "RGB"
    ws.Cells(1, 4).Value = "VBA ColorIndex"
    
    ' Style headers
    With ws.Range("A1:D1")
        .Font.Bold = True
        .Font.Size = 11
        .Font.name = "Calibri"
        .Interior.ColorIndex = 15
        .Font.Color = RGB(51, 51, 51)
        .HorizontalAlignment = xlCenter
    End With
    
    ' Loop through all 56 colour indices
    For i = 1 To 56
    
        ' Apply colour to swatch cell
        ws.Cells(i + 1, 1).Interior.ColorIndex = i
        
        ' Get the long colour value
        colourLong = ws.Cells(i + 1, 1).Interior.Color
        
        ' Extract RGB components
        ' Excel stores colour as BGR not RGB so we need to reverse
        b = (colourLong \ 65536) And 255
        g = (colourLong \ 256) And 255
        r = colourLong And 255
        
        ' Build hex code
        hexCode = "#" & Right("00" & Hex(r), 2) & Right("00" & Hex(g), 2) & Right("00" & Hex(b), 2)
        
        ' Write values
        ws.Cells(i + 1, 1).Value = i
        ws.Cells(i + 1, 2).Value = UCase(hexCode)
        ws.Cells(i + 1, 3).Value = "RGB(" & r & ", " & g & ", " & b & ")"
        ws.Cells(i + 1, 4).Value = "ColorIndex = " & i
        
        ' Ensure consistent font on data rows
        With ws.Range(ws.Cells(i + 1, 1), ws.Cells(i + 1, 4))
            .Font.name = "Calibri"
            .Font.Size = 11
            .Font.Color = RGB(51, 51, 51)
            .HorizontalAlignment = xlCenter
        End With
        
        ' Make text in colour cell white or black depending on darkness
        ' so the index number is readable against the background
        If (r * 0.299 + g * 0.587 + b * 0.114) < 128 Then
            ws.Cells(i + 1, 1).Font.Color = RGB(255, 255, 255)
        Else
            ws.Cells(i + 1, 1).Font.Color = RGB(0, 0, 0)
        End If
        
    Next i
    
    ' Freeze the header row
    ws.Rows("2:2").Select
    ActiveWindow.FreezePanes = True
    ws.Cells(1, 1).Select
    
    MsgBox "Colour index map complete!" & vbCrLf & vbCrLf & _
           "56 colours mapped with hex codes and RGB values.", _
           vbInformation, "MapColorIndex"

End Sub
```



### Turning it into a reference you can actually use

Once the macro has run, set you print layout and save the sheet as a PDF (**File > Save As > PDF**). This preserves the colour swatches visually but also keeps the hex codes and RGB values as selectable, copyable text. You can have the PDF open alongside your workbook and copy values directly rather than retyping them.

The macro, PDF and XLSX version are both available to download below.
[Download the macro as TXT file](/assets/downloads/Mod_MapColorIndex.txt)
[Download as PDF](/assets/downloads/ColorIndex-Reference.pdf)
[Download as Excel](/assets/downloads/ColorIndex-Reference.xlsx)


### A note on when to use ColorIndex

ColorIndex is the legacy system and has limitations. It only covers 56 colours and the values are not always consistent across different Excel themes. For most modern VBA work, `RGB()` or direct hex assignment via `.Color` gives you more control and is not restricted to 56 options.

That said, ColorIndex still has its uses (eg. in adding colour to custom formats). It is slightly faster to apply in loops over large ranges and some older shared macros use it throughout. Knowing what each index actually looks like is useful whether you are writing new code or maintaining something that was written years ago.

### On Office Scripts

This macro is written in VBA which works in any version of Excel that allows macros to be run. The same functionality can be achieved with an Office Script, but that requires a Microsoft 365 subscription and OneDrive, so VBA remains the more portable option for most use cases.


*The macro takes two seconds to run. The PDF takes another ten seconds to export. You will never need to google "Excel ColorIndex" again.*
