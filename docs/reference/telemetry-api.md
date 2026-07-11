# Instrument telemetry API

This page lists the exact MicroPython functions your program calls to feed Snakie's live instruments — the **Oscilloscope**, **Multimeter** and **Plotter**. Telemetry means your board *prints* its readings and Snakie reads them from the serial link. (Serial = the USB cable your board talks over.)

For a friendly walkthrough of opening and using the instruments, see the [Instruments guide](../guides/instruments.md). To build your first live graph step by step, try [Plot a sensor](../tutorials/plot-a-sensor.md).

## Why telemetry?

Your program does a single, tiny `print()` for each reading. Snakie spots those special lines, sends each one to the right instrument, and hides them from the console. Because it is just printing, it is safe to call inside a fast `while True:` loop and it never interrupts your program.

## Getting the library onto your board

The helpers live in one file, `instruments.py`. It is plain MicroPython with no extra parts needed, so it runs happily on a Raspberry Pi Pico.

1. Install it onto the board. Snakie can copy it for you with one click (see the [Instruments guide](../guides/instruments.md)), or you can drag `instruments.py` into the board's files next to your `main.py`.
2. Import it at the top of your program:

```python
import instruments as inst
```

## Core functions

These three are the ones you will use most. Call them again and again inside your loop.

| Function | Feeds | What it does |
| --- | --- | --- |
| `inst.scope(value, ch="ch1")` | Oscilloscope | Sends one waveform sample. Call it repeatedly to draw a moving line. |
| `inst.meter(value, ch="adc0", unit="V")` | Multimeter | Sends one reading. Snakie shows the latest value and tracks MIN / MAX / AVG. |
| `inst.plot(*args, **kwargs)` | Plotter | Sends one row of one or more series over time. |

`plot()` is flexible. Plain numbers become numbered series, and `name=value` pairs become named ones — and you can mix them:

```python
inst.plot(1, 2, 3)               # three numbered series
inst.plot(temp=21.4, light=80)   # two named series
```

!!! note "What is `ch`?"
    `ch` (short for *channel*) is a label you pick, like `"pwm"` or `"adc0"`. Snakie uses it to match a reading to the right instrument. If only **one** scope (or meter) is open, it receives your readings whatever the label — so the simple case just works.

## Reader helpers

These read a hardware object for you, send the value, and also return it so you can use it in your code. (ADC = analog-to-digital converter, which measures a voltage. PWM = pulse-width modulation, a way to fake a varying output.)

| Function | Feeds | Returns |
| --- | --- | --- |
| `inst.read_adc(adc, ch="adc0")` | Multimeter | The voltage in volts. Reads `adc.read_u16()` and converts it (3.3 V reference, 16-bit). |
| `inst.read_pwm(pwm, ch="pwm")` | Oscilloscope | The duty as a fraction from 0 to 1 (`pwm.duty_u16() / 65535`). |

## Short examples

**Oscilloscope** — send a changing value each loop:

```python
import time, math
import instruments as inst

t = 0
while True:
    inst.scope(math.sin(t))   # a smooth wave on the scope
    t += 0.1
    time.sleep(0.02)
```

**Multimeter** — measure a voltage on ADC pin 26:

```python
import time
from machine import ADC
import instruments as inst

adc = ADC(26)
while True:
    inst.read_adc(adc, ch="adc0")   # shows volts on the meter
    time.sleep(0.1)
```

**Plotter** — graph two named series together:

```python
import time
import instruments as inst

while True:
    inst.plot(temp=21.4, light=80)   # two lines on the plotter
    time.sleep(0.2)
```

Open the matching instrument in Snakie, run your program, and the readings appear live — no extra button needed.

## What the wire lines look like

Under the hood, each helper does one `print()` of a single line that starts with the token `SNK`. You do not need to type these yourself, but it can help to know what Snakie is looking for:

```
SNK SCOPE <ch> <value>            # one oscilloscope sample
SNK METER <ch> <value> [<unit>]   # one meter reading (default unit "V")
SNK PLOT  <tok> [<tok> ...]       # one plotter row (numbers and/or name=value)
```

The `SNK` marker does three jobs: it **routes** the line to the correct instrument, **hides** it from the REPL console, and keeps the Plotter from mistaking scope or meter lines for graph data.

!!! tip
    Because each helper is just a little text-formatting plus one `print()`, it is cheap and does not block. You can safely call it at speed inside a tight loop.

!!! example "📸 Screenshot"
    _Show: a running program printing telemetry while the Oscilloscope, Multimeter and Plotter update side by side._

The same library also includes helpers for robotics (orientation, distance, buttons, encoders, small displays) and an IDE-to-board **control channel** — the path the Poses bench uses to drive your servos. Those are beyond this core reference; to explore them see the [Instruments guide](../guides/instruments.md), the [snakie module](snakie-module.md) (the hardware classes `Servo`, `Buzzer`, `Led`), and [Bind servos and animate](../guides/motion-studio.md).
