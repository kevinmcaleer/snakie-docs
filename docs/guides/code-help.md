# Get help as you type

Snakie's editor knows MicroPython. As you type, it suggests what comes next, shows what a function wants, and links your code to the pins on your board. This page shows each helper and how to use it.

## Autocomplete that knows MicroPython

Start typing and Snakie offers the names that fit. The suggestions come from MicroPython's official API (the Raspberry Pi Pico and ESP32 ports, plus MicroPython's standard library), and they follow your own code:

- After `led = Pin(25, Pin.OUT)`, typing `led.` lists `on`, `off`, `toggle` and `value`.
- After `self.i2c = I2C(0, …)`, typing `self.i2c.` lists `scan`, `writeto` and the rest.
- `import machine as m` then `m.` works, and so does `utime.`.
- `from machine import ` lists everything `machine` has.

Some parts of the API only exist on one kind of board. Those suggestions are labelled **RP2 (Pico) only** or **ESP32 only**.

### Keywords, where they make sense

Python keywords autocomplete too: `fro` offers `from`, `imp` offers `import`, and `for x ` offers `in`. Snakie only offers a keyword where it's valid, so `elif` and `else` appear after an `if` block, `return` inside a function, and `break` inside a loop.

## What does this function want?

Type `Pin(` or `pwm.duty_u16(` and a small card shows the parameters, with the one you're typing highlighted.

Point at any name to see its signature and its documentation.

### Your own functions

Point at one of **your own** functions, where it's called or where it's defined, and the card shows:

- its signature, and whether it's a function or a method,
- its parameters, with their types and defaults,
- its docstring,
- every line that uses it, each one a link that jumps there.

Below that come friendly hints, for example a missing docstring, a function nothing calls, or a name that isn't in `snake_case`.

## Jump to where something is defined

Point at a variable, function, class, import or `self.x` attribute to see the line it was defined on, with a **Go to line N** link.

To jump straight there, do any of these:

- right-click and choose **Go to Definition** (or **Peek** to look without leaving your place),
- press **F12**,
- hold **Cmd** (Mac) or **Ctrl** (Windows, Linux, Chromebook) and click the name.

Snakie follows Python's rules: inside a function, its own parameters and variables come first.

## The code and the board light up together

Point at a pin's variable in your code (say `motor_a_speed`), or put the cursor on it. Its pin glows on the mini board with a pulsing ring, its label turns bold, and the other pins dim. The board scrolls to show it.

It works the other way round too: click a used pin on the mini board and the editor jumps to the line that sets it up.

See [Use the Board View](board-view.md) for more on the mini board.

## MicroPython or CircuitPython?

The status bar says which Python you're writing. Tap it (it says **MicroPython** or **CircuitPython**) to switch.

- **On the simulator**, it switches the simulator itself. The help, the suggestions and the Run and Reset wording all switch with it. See [How the simulator works](../explanation/simulator.md).
- **With nothing connected**, it picks which Python you're writing for.
- **On a real board**, it sets which Python the help and suggestions teach. It also offers to put the other Python on the board, or to try it on the simulator instead.

CircuitPython boards never get MicroPython-only suggestions.

## Where to go next

- [Run and stop your code](run-and-stop.md)
- [Find and replace](find-replace.md)
- [Keyboard shortcuts](../reference/shortcuts.md)
