# What is MicroPython?

A friendly, no-tasks read about MicroPython — the small version of Python that runs on tiny computers. If you have ever wondered what makes your little board blink and beep, this page is for you.

## Python, made tiny

**Python** is a popular programming language. People love it because it reads almost like plain English, so it is a gentle place to start learning to code.

**MicroPython** is a small, re-packaged version of Python. It was carefully shrunk down so it can run on very small, low-power computers. You write code that looks almost exactly like normal Python, but it runs on a chip that fits on your fingertip.

!!! note "Two words that sound alike"
    *Python* runs on big computers (like your laptop). *MicroPython* runs on tiny ones (like your board). The code you write looks nearly the same.

## What is a microcontroller?

A **microcontroller** is a whole little computer squeezed onto a single chip. It has a brain (the processor), a bit of memory, and — the fun part — **pins**.

A **pin** is a metal leg on the board. Your code can switch a pin on or off, or read whether something outside is on or off. That is how a microcontroller *controls electronics*: it turns lights on, spins motors, reads buttons, and listens to sensors.

Boards like the **Raspberry Pi Pico 2 W**, the **ESP32**, and the Pimoroni **Tiny 2040** are all built around microcontrollers. They are cheap, tough, and perfect for making things move and glow.

!!! example "📸 Screenshot"
    _Show: a small microcontroller board with its pins labelled, next to a coin for size._

## Why MicroPython is great for learning

- **It reads like English.** Less puzzling punctuation, more "do this, then that".
- **You see results in the real world.** A blinking LED is more exciting than words on a screen.
- **Mistakes are cheap and safe.** Change a line, run it again, watch what happens.
- **It grows with you.** The same skills carry over to full Python later.

Here is a tiny MicroPython program that blinks the built-in light on a Raspberry Pi Pico:

```python
from machine import Pin
import time

led = Pin("LED", Pin.OUT)   # the Pico's onboard light

while True:
    led.toggle()            # flip it on/off
    time.sleep(0.5)         # wait half a second
```

Want to try it for real? Follow the [Blink tutorial](../tutorials/blink.md) — it walks you through every step.

## How does MicroPython get onto a board?

A brand-new microcontroller does not know Python yet. First you give it **firmware** — the built-in software that teaches the chip how to understand MicroPython.

!!! tip "Firmware in one line"
    *Firmware* is the special program that lives inside the board and makes it able to run your code. You only install it once (or when you want to update it).

You copy the firmware onto the board just once. After that, the board speaks MicroPython, and you can send it as many programs as you like.

Snakie makes this easy with a built-in board catalog — see [Flash firmware](../guides/flash-firmware.md).

## Where Snakie fits in

Once your board has MicroPython firmware, **Snakie** is the friendly workshop where you write code, press **Run**, and watch it happen on the real board. Snakie talks to the board over a USB cable using a simple back-and-forth conversation.

Curious how that chat actually works? Read [How Snakie talks to your board](how-snakie-talks-to-your-board.md).

!!! note "The short version"
    MicroPython = small Python. It runs on a microcontroller (a tiny computer on a chip). You add firmware once, then Snakie sends it your code. That is the whole magic.

Now you know what MicroPython is — next, make a light blink in the [Blink tutorial](../tutorials/blink.md). Have fun!

!!! tip "Want a longer learning path?"
    [Follow Kev's free Learn MicroPython pathway on
    KevsRobots](https://www.kevsrobots.com/learn/learning_pathways/micropython.html)
    to continue through the basics, Pico GPIO, sensor projects, robotics, and
    I2C/SPI communication.
