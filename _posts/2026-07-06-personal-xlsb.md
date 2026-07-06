---
title: "The macro workbook that opens every time Excel does"
excerpt: "PERSONAL.XLSB makes your macros available in every workbook, every session. Here is how to create it, find it and ensure you never lose it."
---

Every macro you write lives somewhere. The question is where, and whether it will be there the next time you need it.

The most common answer is: in the workbook where you built it. Which means it travels with that workbook, it is unavailable everywhere else, and if you ever send the file to someone else, the macro goes with it whether you intended that or not. `PERSONAL.XLSB` is the alternative. It is a hidden workbook that Excel opens automatically at startup. You will not see it in the taskbar or the window switcher; it runs quietly in the background, making every macro stored in it available in any workbook, in any session, on that machine.

One important note before you run macros: macros cannot be undone (CTRL-Z). Excel's undo stack doesn't apply to VBA changes. If you are running a macro against a workbook, save your workbook first so you have an up-to-date restore point.

```
PERSONAL.XLSB is one approach to macro storage. There are others: add-ins, the Quick Access Toolbar, and a custom ribbon tab each have their own use cases. Those are worth a post of their own.
```

### Creating it

Excel does not create `PERSONAL.XLSB` automatically. You have to trigger it, and the easiest way is through the macro recorder.

(If you do not have the Developer tab visible, go to **File > Options > 'Customize' the Ribbon**, tick Developer in the right-hand column, and click OK.)

Go to **Developer > Record Macro**. In the dialogue that appears, set "Store macro in" to **Personal Macro Workbook**, then click OK. Click one cell, stop the recording. That's it. Excel's now created `PERSONAL.XLSB` for you and stored a one-click macro in it that you'll remove in the next step.

Open the VBA editor with `Alt+F11`. In the Project Explorer on the left, find **VBAProject (PERSONAL.XLSB)**. Right-click and choose **Insert > Module**, then paste your actual code into that module. You can delete the previous recorded macro stub at this point.

To run any macro stored in `PERSONAL.XLSB` against another workbook, bring that workbook to the front so it becomes the 'active window', then use `Alt+F8` to open the macro list, pick the macro you want, and select Run.

(Alternatively to run a macro you can **Developer > MAcros** and select the macro you want to run from the list.)


### Finding the file

`PERSONAL.XLSB` lives in a folder Excel checks at startup called XLSTART. The full path can be found at:

```
C:\Users\username\AppData\Roaming\Microsoft\Excel\XLSTART\PERSONAL.XLSB
```

Replace `username` with your Windows username. AppData is a hidden folder by default, so you may need to show hidden files in Windows Explorer to navigate there directly, or simply paste the path into windows explorer and hit enter.

The practical tip: create a shortcut to the file and put it somewhere you will actually find it, your Documents folder, your desktop, or wherever you keep your working files. You'll thank yourself every time you try to find it.

As it opens in Excel hidden, you'll not see it alongside your other workbooks. If you ever need to unhide it to edit it directly, go to View > Unhide and select `PERSONAL.XLSB`. For most purposes though, `Alt+F11` gets you straight to the VBA editor without needing to unhide it at all.

### Back it up

This is the part most people skip and eventually regret.

`PERSONAL.XLSB` is a single file on your local machine. It is not synced to OneDrive unless you have specifically set that up. It does not travel with your profile if you change computers. If your machine is rebuilt, or replaced, or develops a fault at an inconvenient moment, every macro you have ever stored there goes with it.

Back it up. Copy it to OneDrive, SharePoint, a network drive, wherever your important files live. Do it regularly, especially after you have added something new. If you use the file as a personal macro library built up over years, losing it is a genuinely painful experience.

Experienced Excel users set it up once, years ago and never thought about it again. That is why it rarely comes up in conversation.




