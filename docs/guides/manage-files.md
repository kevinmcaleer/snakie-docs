# Manage files

Snakie shows two sets of files side by side: the ones on **your computer** and the ones on the **board** (the tiny MicroPython computer you plug in). This page shows you how to make, open, rename, and delete files in both places, and how to move a file onto the board so it can run there.

!!! note "What is a file panel?"
    The file panel is the list of files down the side of Snakie. The top part is your computer. The bottom part is your board (once it is [connected](connect-board.md)).

## The two file areas

| Area | What it holds | When you can use it |
| --- | --- | --- |
| Your computer | Files saved on your laptop or Raspberry Pi | Always |
| The board | Files stored on the MicroPython board itself | Only when a board is [connected](connect-board.md) |

The board area is empty until you plug a board in. If you do not see it, check the [Connect your board](connect-board.md) guide first.

!!! example "📸 Screenshot"
    _Show: the file panel with the computer files at the top and the connected board's files below._

## Make a new file or folder

1. Find the small **+** buttons at the top of the area you want (computer or board).
2. Click **New File** to make a file, or **New Folder** to make a folder.
3. Type a name and press Enter.

!!! tip "Name it with `.py`"
    A MicroPython program should end in `.py`, like `blink.py`. This tells Snakie it is Python code so it can colour it in and help you.

## Open, rename, and delete

- **Open** a file by clicking it. It opens in the editor, ready to change.
- **Rename** or **Delete** a file by **right-clicking** it and choosing from the menu.

!!! warning "Delete is forever"
    Deleting a file cannot be undone. Make sure you picked the right one before you say yes.

## Move a file to the board

Your board can only run code that lives **on the board**. So when your program is ready, copy it across.

1. In the **computer** list, right-click the file you want.
2. Choose **Upload to board**.
3. The file appears in the **board** list below.

There are also little **up and down arrows** between the two areas:

- The **down arrow** sends the file you are editing *down* to the board (upload).
- The **up arrow** brings a board file *up* to your computer (download).

To copy a board file back to your computer, right-click it in the board list and choose **Download to computer**.

!!! tip "Keep a copy on your computer"
    It is a good idea to save your work on your computer too. If a board is wiped or swapped, your computer copy is safe.

## The special file: `main.py`

One file name is magic: **`main.py`**.

When your board is switched on (or reset), it automatically looks for a file called `main.py` and runs it. So if you want your program to start on its own — with no computer attached — save it to the board as `main.py`.

!!! example "A tiny `main.py` for a Raspberry Pi Pico"
    ```python
    from machine import Pin
    import time

    led = Pin("LED", Pin.OUT)

    while True:
        led.toggle()
        time.sleep(0.5)
    ```
    Upload this as `main.py`, then unplug and re-plug the board. The onboard light blinks all by itself.

!!! note "Testing first"
    While you are still writing code, you do not need `main.py` — just press **Run** to try it. See [Run and stop your code](run-and-stop.md). Save it as `main.py` on the board only when you want it to start on its own.

## Where to go next

- [Connect your board](connect-board.md) — plug in and get the board list to appear.
- [Run and stop your code](run-and-stop.md) — try your program before you save it as `main.py`.
