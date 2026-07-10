# Plot a sensor live

In this tutorial you will read a value that changes over time and watch Snakie draw it as a moving line graph. You will use the Raspberry Pi Pico's built-in temperature sensor, so you don't need any extra wiring.

By the end you will have a graph that wiggles when you warm the board with your finger. Let's go!

!!! note "What you need"
    - A Raspberry Pi Pico (or Pico 2) plugged in over USB.
    - Snakie open, with your board **connected**. New to this? See [How Snakie talks to your board](../explanation/how-snakie-talks-to-your-board.md).

## How this works

A **sensor** is a part that measures something in the real world, like heat or light. Your Pico has a tiny temperature sensor inside it.

Your program will **print** each reading, and Snakie will read that stream and draw it. This is called **telemetry** (data your board sends back about itself). Because it is just printing, it never interrupts your loop.

## Step 1 — Install the telemetry library (one click)

The readings need to be printed in a shape Snakie understands. A tiny helper library called `instruments.py` does that for you.

When your board is connected but doesn't have the library yet, a banner appears at the top of Snakie:

> The Snakie instrument library isn't on your board — install it to stream live scope/meter/plotter readings.

1. Click **Download & install** on that banner.
2. Wait a second while Snakie writes the library onto your board.

That's it — the library is now on your Pico.

!!! example "📸 Screenshot"
    _Show: the top-of-window banner with the "Download & install" button highlighted._

## Step 2 — Write the code

Make a new file, paste this in, and save it to your board:

```python
from machine import ADC
import time
import instruments as inst

sensor = ADC(4)             # the Pico's built-in temperature sensor
conversion = 3.3 / 65535    # turns the raw reading into volts

while True:
    volts = sensor.read_u16() * conversion
    temp = 27 - (volts - 0.706) / 0.001721   # volts -> degrees Celsius
    inst.plot(temp=round(temp, 1))           # send one reading to the Plotter
    time.sleep(0.5)                          # half a second between readings
```

The important line is `inst.plot(temp=round(temp, 1))`. That prints one row for the graph, with a named series called `temp`. You can plot more than one thing at once, like `inst.plot(temp=21.4, light=80)`.

!!! tip "Give your line a name"
    The name you use (`temp` here) becomes the label on the graph. Pick something clear, like `temp`, `light`, or `speed`.

## Step 3 — Open the Plotter and run

1. Open the **Plotter** instrument. It lives with Snakie's other live instruments beside the shell — see [Live instruments](../guides/instruments.md) if you can't spot it.
2. Press **Run**.

Watch the graph. You should see a line for `temp` slide across from the right as new readings arrive.

!!! example "📸 Screenshot"
    _Show: the Plotter with a moving "temp" line while the program runs._

## Step 4 — Make it move

Pinch the top of your Pico gently between two fingers for a few seconds. Your body heat warms the chip, and the line climbs. Let go and it drifts back down. That's your first live graph reacting to the real world!

When you're done, press **Stop**.

## What you learned

- Telemetry lets your board **print** readings that Snakie graphs live, without pausing your loop.
- `inst.plot(name=value)` sends one point to the **Plotter**.
- The built-in temperature sensor is `ADC(4)` on the Pico.

## Where next

- Try a **potentiometer** (a twisty knob) wired to an ADC pin, and plot its value as you turn it.
- See every helper (`scope`, `meter`, `plot` and friends) in the [Telemetry API reference](../reference/telemetry-api.md).
- Learn about the Oscilloscope and Multimeter in [Live instruments](../guides/instruments.md).

Ready for something bigger? Build your [first robot](first-robot.md) next.
