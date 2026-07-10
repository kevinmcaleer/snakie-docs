# Run and stop your code

This page shows you how to run your MicroPython program on your board, how to stop it, and how to make a program start all by itself when the board powers up.

*MicroPython is a small version of the Python language that runs on tiny computers called microcontroller boards.*

!!! note "First, connect a board"
    Running code needs a board plugged in over USB. If you have not done that yet, see [Connect your board](connect-board.md). The **Run** button stays greyed out until a board is connected and a file is open.

## Run your code

1. Open the file you want to run, or type a new program in the editor.
2. Make sure your board is connected (see [Connect your board](connect-board.md)).
3. Press the **Run** button in the toolbar.

Snakie sends the code that is **currently in the editor** straight to the board and runs it. You will see any output (like `print()` messages) appear in the Shell at the bottom of the window.

!!! tip "You do not have to save first"
    Run sends whatever is in the editor right now, even unsaved changes. That makes it quick to try an idea, tweak a line, and run again.

Here is a tiny program you can try. It blinks the little LED that is built into a Raspberry Pi Pico.

```python
from machine import Pin
import time

led = Pin("LED", Pin.OUT)

while True:
    led.toggle()
    time.sleep(0.5)
```

## Stop your code

That blink program never ends on its own, because of the `while True:` loop. To stop it, press the **Stop** button.

- **While a program is running**, the button shows **Stop**. Pressing it interrupts the program, like tapping the brakes.
- **When nothing is running**, the same button changes to **Reset**. Pressing it soft-resets the board.

!!! note "What is a soft reset?"
    A soft reset is a gentle restart of the board's brain. It clears out anything left over from your last program, so you get a clean, fresh start, without unplugging anything.

## Run live vs. run on power-up

There are two different ways your code can run, and it helps to know the difference.

| | Press **Run** | Save as `main.py` on the board |
|---|---|---|
| When it runs | Right now, while you watch | Every time the board powers up |
| Needs Snakie open? | Yes | No |
| Great for | Testing and tinkering | Finished projects, robots left on their own |

When you press **Run**, the code lives in the board's memory for that one run. Unplug the board, and it forgets.

If you want your program to start **by itself** every time the board gets power, save it onto the board with the special name **`main.py`**. When MicroPython starts up, it looks for a file called `main.py` and runs it automatically.

To do that, save your file **onto the device** (not just your computer) and name it `main.py`. Snakie can browse and save files on the board just like files on your computer, Thonny-style. See [Manage your files](manage-files.md) to learn how.

!!! example "📸 Screenshot"
    *Show: the toolbar Run button next to the Stop/Reset button, with LED output printing in the Shell below.*

!!! tip "Stuck in a loop?"
    If you saved a `main.py` that never stops and the board keeps running it, press **Stop** to interrupt it, then use [Manage your files](manage-files.md) to open, fix, or delete `main.py`.

## What to try next

- Learn to browse and save files on the board in [Manage your files](manage-files.md).
- Not connected yet? Start with [Connect your board](connect-board.md).
