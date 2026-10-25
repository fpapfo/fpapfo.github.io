---
title: "Moving your AutoCorrect shortcuts to a new computer"
excerpt: "Your AutoCorrect entries are not stranded on the old machine. They sit in a file you can copy, as long as Office is closed when you put them back."
---
A new laptop arrives, or the IT rebuild finally happens, and Office opens on a clean profile. Every AutoCorrect shortcut you built up has gone with the old machine, and the only record is whatever you happened to write down at the time.

I assumed for a long time that retyping them was the only way back. It is not. The entries live in a file, and the file copies across like any other. The shortcuts I use for commentary are in [an earlier post](/2026/06/15/office-shortcuts-for-financial-commentary.html); this is how to take them with you.

### Where they live

Open File Explorer, paste this into the address bar and press enter:

```
%AppData%\Microsoft\Office
```

That resolves to `C:\Users\YourName\AppData\Roaming\Microsoft\Office`. The `%AppData%` part is a Windows shortcut that stands in for your own user folder, so the same path works on anyone's machine without editing the username. Paste the full path instead if you prefer, Explorer will take you there either way. AppData is hidden by default, which goes some way to explaining why these files are not better known.

You are looking for files named `MSOxxxx.acl`. On my machine there are three:

```
MSO0127.acl
MSO1033.acl
MSO2057.acl
```

The number is a locale ID. 2057 is English (United Kingdom), 1033 is English (United States). In practice one file holds everything you have added, but which one that is depends on your Office language, so copy all of them and save yourself working it out.

### The mistake that undoes it

Office keeps the AutoCorrect list in memory whilst it runs. Copying from the old machine is usually fine: I added two entries today with Word and OneNote open and the file updated as I went.

The risk is at the other end. Paste your files onto the new machine whilst an Office application is running, and that application is sitting there holding its own AutoCorrect list in memory. When it closes, it writes that list back out, over the files you have just pasted. Nothing warns you. You find out later, when a trigger does nothing.

So the rule that matters is this one: close every Office application on the machine you are pasting onto. Word, Excel, PowerPoint, Outlook and OneNote. Outlook in particular has a habit of sitting in the system tray long after you think you have shut it, so check there, and check Task Manager if you want to be certain.

Closing them on the old machine as well does no harm, and removes any doubt that what you are copying is current.

### The move itself

1. On the old machine, copy every `MSOxxxx.acl` file from `%AppData%\Microsoft\Office` onto a USB stick or into a cloud folder.
2. On the new machine, close every Office application.
3. Back up the `.acl` files already sitting there. The new machine has its own, and you are about to replace them.
4. Paste yours in, overwriting.
5. Open Word and type one of your triggers.

If the trigger fires, the whole list came with it.

### The one thing the file does not carry

The `.acl` holds plain text replacements. If you have AutoCorrect entries that carry formatting, bold, a colour, a particular font, Word keeps those in your `Normal.dotm` template instead, over in `%AppData%\Microsoft\Templates`.

Symbols like Δ and ▲ are plain text, so the `.acl` copy brings them. If you have built formatted entries, copy only the `.acl` and you will find them missing with no obvious explanation. Copy `Normal.dotm` as well if that applies to you, although be aware it carries your default styles and page setup too, so you may not want it wholesale.

### Keep the written list anyway

Copying the file is faster, but it only helps while you still have the old machine. A laptop that dies, or a rebuild done at short notice, leaves you nothing to copy from. A plain list of your triggers in your notes costs nothing and covers the case the file copy cannot.

*The file was there the whole time, in a hidden folder, under a four digit number. You're unlikely to find that by accident unless you're poking around in AppData to see what else might be there.*
