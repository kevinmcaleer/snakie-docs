# Keyboard shortcuts

This page lists the keyboard shortcuts you can use in Snakie. A "shortcut" is a set of keys you press together to do something quickly, without reaching for the mouse.

On a **Mac** you use the **Cmd** key (⌘). On **Windows and Linux** (including Raspberry Pi) you use the **Ctrl** key. Everything else is the same.

!!! tip "Menus show shortcuts too"
    Many actions also live in the app menus at the top of your screen (or window). Open a menu to see its actions with their shortcuts written next to them. If a shortcut is not on this page, the menus are the best place to find it.

## Editing your code

These work while you are typing in the code editor.

| What it does | macOS | Windows / Linux |
| --- | --- | --- |
| Save the file | Cmd + S | Ctrl + S |
| Undo | Cmd + Z | Ctrl + Z |
| Redo | Cmd + Shift + Z | Ctrl + Shift + Z (or Ctrl + Y) |
| Cut | Cmd + X | Ctrl + X |
| Copy | Cmd + C | Ctrl + C |
| Paste | Cmd + V | Ctrl + V |
| Select all | Cmd + A | Ctrl + A |

!!! note
    Undo, Redo, Cut, Copy, Paste and Select all also appear in the **Edit** menu.

## Files and tabs

Each file you open sits in its own **tab** (like tabs in a web browser).

| What it does | macOS | Windows / Linux |
| --- | --- | --- |
| Close the current tab | Cmd + W | Ctrl + W |
| Move to the next tab | Ctrl + Tab | Ctrl + Tab |
| Move to the previous tab | Ctrl + Shift + Tab | Ctrl + Shift + Tab |

!!! tip
    If a tab has changes you have not saved yet, Snakie will ask you before it closes.

## Find & Replace

Find helps you search your file. Replace swaps one piece of text for another.

| What it does | macOS | Windows / Linux |
| --- | --- | --- |
| Open Find | Cmd + F | Ctrl + F |
| Open Find & Replace | Cmd + H | Ctrl + H |

Inside the Find & Replace box, these single keys help you move around:

| What it does | Key |
| --- | --- |
| Go to the next match | Enter |
| Go to the previous match | Shift + Enter |
| Close the box | Esc |

Want the full tour? See the [Find & Replace guide](../guides/find-replace.md).

## Running your code and the shell

You start and stop your program with the **Run** and **Stop** buttons in the toolbar. See [Run and Stop](../guides/run-and-stop.md) to learn what each one does.

The **shell** (also called the REPL) is the live window where you can talk to your board directly. When you are clicked into the shell, these keys go straight to the board:

| What it does | Key |
| --- | --- |
| Interrupt (stop) the running program | Ctrl + C |
| Soft-reset the board (a gentle restart) | Ctrl + D |

!!! note
    Ctrl + C and Ctrl + D are the same on every computer, because they are sent to your MicroPython board, not to Snakie.

## Windows and the Board View

| What it does | macOS | Windows / Linux |
| --- | --- | --- |
| Open the Board View window | Cmd + Shift + B | Ctrl + Shift + B |

The **View** menu also has handy items with their own shortcuts, such as zoom in, zoom out, reset zoom and full screen. Open the View menu to see them.

## Extra shortcuts in the visual editors

Some windows have their own helpers.

**Part Editor** (for drawing parts):

| What it does | macOS | Windows / Linux |
| --- | --- | --- |
| Undo | Cmd + Z | Ctrl + Z |
| Redo | Cmd + Shift + Z | Ctrl + Shift + Z (or Ctrl + Y) |
| Delete the selected item | Delete or Backspace | Delete or Backspace |

Hold **Ctrl** (or **Cmd** on Mac) while dragging to turn off snapping for a moment, so you can place things freely.

**Robot View** (for building robots in 3-D): Undo and Redo work the same as above. When you use the **Add Joint** tool, **hold Shift** to lock onto the highlighted snap point, so you can click a hole centre exactly.

!!! example "📸 Screenshot"
    _Show: the Snakie Edit menu open, with the Undo, Redo and Save shortcuts visible beside their menu items._
