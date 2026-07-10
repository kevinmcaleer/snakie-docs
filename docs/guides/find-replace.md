# Find and replace

Need to change a word, or hop straight to a line in your code? The Find and Replace window helps you search your file and swap text in one place or everywhere at once.

## Open Find and Replace

You have two easy ways to open it:

1. Open the file you want to search.
2. Click the **Find** button at the top of the editor, **or** press the find shortcut (`Ctrl`/`Cmd` + `F`).

Find and Replace opens in its own small window that floats above the editor, so your search box never gets in the way of your code. You can drag it by its title bar to move it wherever you like.

!!! tip
    `Ctrl`/`Cmd` + `H` opens the same window. See the full list on the [Keyboard shortcuts](../reference/shortcuts.md) page.

!!! example "📸 Screenshot"
    _Show: the floating Find and Replace window over the editor, with a word typed in the Find box and matches highlighted in the code._

## Search for text

1. Type the word or phrase you want in the **Find** box.
2. Watch the **match count** update live under the boxes — it tells you how many times your text appears (for example, "3 matches"). If nothing is found, you'll see "No results".
3. Press `Enter` to jump to the next match, or `Shift` + `Enter` to jump to the previous one. You can also use the up and down arrow buttons.

## Replace text

1. In the **Replace with** box, type the new text.
2. To change **one** match at a time, click **Replace**.
3. To replace a match and immediately find the next one, click **Replace+Find**.
4. To change **every** match in the file at once, click **Replace all**.

!!! warning
    **Replace all** changes every match in one go. If it does too much, use **Undo** (`Ctrl`/`Cmd` + `Z`) to put things back, then try a more exact search.

## Make your search more exact

Two toggle buttons help you find just the right text:

| Button | What it does |
| --- | --- |
| **Aa** (Match case) | Only finds text with the same capital and lowercase letters. `Led` will not match `led`. |
| **\|ab\|** (Whole word) | Only finds your text when it stands on its own, not inside a bigger word. `pin` will not match `spinner`. |

Click a button to turn it on; click again to turn it off. The match count updates as you go, so you can see straight away how much your search finds.

!!! tip
    Start with both toggles off for a wide search. Turn one on when you're getting too many matches and want to narrow things down.

## Close the window

When you're done, press `Esc` or close the window. Your changes stay in the file, ready to **Run**.

!!! note
    A quick reminder of the keys: `Enter` finds the next match, `Shift` + `Enter` finds the previous one, and `Esc` closes the window.
