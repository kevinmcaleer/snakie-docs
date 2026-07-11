# Use the instruments

Snakie has three on-screen instruments — an **Oscilloscope**, a **Multimeter** and a **Plotter** — that show live readings from your running program. This page shows you how to turn them on and feed them.

## What each instrument does

An *instrument* is a little on-screen tool that draws numbers from your board.

| Instrument | What it shows | Great for |
| --- | --- | --- |
| Oscilloscope | A wiggly line (a *waveform*) that changes over time | Watching a signal move fast, like a PWM (a pin flicked on and off quickly) |
| Multimeter | One number, plus its lowest, highest and average | Reading a voltage, like a sensor's output |
| Plotter | One or more lines graphed over time | Comparing values, like temperature and light together |

You can **dock** them (tuck them neatly into a side panel) or **float** them (a separate window you can drag anywhere). Pick whichever helps you see your data best.

!!! example "📸 Screenshot"
    _Show: the Oscilloscope, Multimeter and Plotter docked side by side while a program runs._

## "Non-invasive" — it just watches

The instruments are fed by a tiny helper called the **telemetry library**. *Telemetry* just means "readings sent from far away."

Here is the friendly part: your program simply **prints** its readings, and Snakie **reads them from the serial stream** (the text your board sends back over USB). It only *watches* — it never pauses or changes your program. That means it works happily inside a `while True:` loop, so your robot or sensor keeps running at full speed.

## 1. Install the library (one click)

The library is one small MicroPython file. When Snakie notices it is missing, a banner appears at the top of the app offering to add it for you.

1. Connect your board (see [How Snakie talks to your board](../explanation/how-snakie-talks-to-your-board.md)).
2. When the instruments banner appears, click the button to install the library onto the board.
3. That is it — Snakie copies the file over for you.

!!! tip
    The file is plain MicroPython with no extra parts needed, so it is safe on a small board like the Raspberry Pi Pico.

## 2. Print readings from your program

Import the library, then call one helper per instrument inside your loop.

```python
import time
from machine import ADC, Pin
import instruments as inst

adc = ADC(26)            # a pin that reads a voltage

while True:
    inst.meter(1.65, ch="adc0", unit="V")   # -> Multimeter
    inst.scope(0.5, ch="pwm")               # -> Oscilloscope
    inst.plot(temp=21.4, light=80)          # -> Plotter
    time.sleep(0.1)
```

- `scope(value)` sends one sample to the Oscilloscope — call it in a loop to draw a waveform.
- `meter(value)` sends one reading to the Multimeter.
- `plot(...)` sends named or plain numbers to the Plotter.

The `ch=` label is just a name you choose so Snakie knows which instrument a reading belongs to. If only one Oscilloscope (or Multimeter) is open, it grabs the readings anyway — so the simple case just works.

!!! tip
    There are ready-made readers too, like `read_adc(adc)` and `read_pwm(pwm)`, that read a pin and send the value in one line. See the full list in the [Telemetry API reference](../reference/telemetry-api.md).

## 3. Open an instrument and run

1. Open the instrument you want from its dock button.
2. Press **Run** to start your program.
3. Watch the readings appear live. No extra toggle needed.

!!! note
    The telemetry lines are hidden from the shell, so your console stays clean — you only see your own `print()` messages.

## Pose your servos — the Poses bench

Snakie has more than the three reading instruments above. If your robot has servos bound to joints (see [Bind servos and animate](motion-studio.md)), a **Poses** instrument appears — a live test bench for the servos.

It lists your saved **poses** as buttons and each bound servo as a **slider**:

- **Press a pose** and every servo eases smoothly into it.
- **Drag a slider** to nudge one servo by hand.

Both move the on-screen 3-D model **instantly, with no program running** — so it's the quickest way to check a servo turns the right way. With a small program servicing the control channel, the **real servos** follow too.

!!! tip "Testing the hardware"
    To drive the physical servos from the Poses bench, run the little `inst.start()` + `inst.control.poll()` listener shown in [Bind servos and animate](motion-studio.md#drive-the-real-servos). The 3-D model doesn't need it.

!!! example "📸 Screenshot"
    _Show: the Poses bench with pose buttons across the top and a slider per servo, next to the 3-D robot mid-pose._

## Where next

- [Telemetry API reference](../reference/telemetry-api.md) — every helper and its exact usage.
- [Plot a sensor](../tutorials/plot-a-sensor.md) — a step-by-step first project.
- [How Snakie talks to your board](../explanation/how-snakie-talks-to-your-board.md) — the serial connection behind it all.
- [See the live instruments demonstrated in Kev's Snakie
  tour](https://www.kevsrobots.com/blog/what-if-building-robots-with-code-was-actually-easy.html#the-instrument-panel--seeing-the-feedback-loop)
  — watch a rangefinder, IMU, multimeter and buzzer feed live readings into Snakie.
