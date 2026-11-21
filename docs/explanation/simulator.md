# How the simulator works

Snakie comes with a **simulated device** — a pretend board that lives inside the app. Pick **Simulated device (offline)** in the port list and you can write and run MicroPython with no hardware at all. This page explains what it really is, what it's great at, and where it honestly differs from a real board.

## It's real MicroPython

Here's the important bit: the simulator is **not** a copy-cat that guesses what MicroPython would do. It runs the **official MicroPython interpreter** — the same program that runs on a real board — built to run inside Snakie (using a technology called **WebAssembly**, which lets programs made for one kind of computer run inside another).

That means:

- The **REPL prompt** you see is MicroPython's own prompt, with the same `>>>` and the same error messages.
- Your code is run by the **same language engine** as a real board, so loops, functions, lists and errors behave the same way.
- When you move to real hardware later, your code doesn't need translating — it was real MicroPython all along.

## A pretend `machine` module

On a real board, `from machine import Pin` gives your code control of real metal pins. The simulator has no metal pins, so Snakie gives it a **simulated `machine` module** instead. `Pin` remembers whether it's on or off, `PWM` accepts your settings, and `ADC` (the thing that reads dials and sensors) returns a gently changing value — so a program that plots a "sensor" draws a moving line instead of a flat one.

The on-screen [instruments](../guides/instruments.md) work with the simulator the same way they work with a real board: your program sends little readings using the telemetry library, and Snakie draws them live. (Curious how that works? See [How Snakie talks to your board](how-snakie-talks-to-your-board.md).)

## Files live in memory

The simulated board has its own little filesystem, held in memory. You can save files to it, list them, and import them — exactly like a real board's storage. But because it's memory, it **resets when the simulator restarts**: reconnecting, or pressing **Stop** while a program is stuck in a tight loop, gives you a fresh, empty board — just like unplugging a real one and plugging it back in. Keep your programs saved in your project folder, not only on the simulated device.

## Why Stop sometimes restarts everything

The simulator runs in its own background worker, so even a `while True:` loop that never sleeps can't freeze Snakie's window. But a loop like that also never stops to listen — so when you press **Stop**, Snakie's only option is to shut the worker down and start a fresh interpreter. That's why a stubborn loop ends with a clean, empty REPL. (A real board does the same thing — Stop reboots the interpreter.)

## What the simulator can't do

Being honest is important, so here's what a pretend board can't give you:

- **No real electronics.** Nothing physically lights up, spins, or beeps. A sensor read returns simulated values, not the temperature of your room.
- **Timing isn't exact.** `time.sleep(0.5)` is close, but the simulator isn't a precise copy of a real chip's speed.
- **No Wi-Fi or Bluetooth.** Network code that needs real radio hardware won't work.

For everything else — learning Python, testing logic, watching the instruments, following the [built-in lessons](../get-started/first-steps.md#learn-inside-snakie) — the simulator is the fastest way to start, because there's nothing to plug in.

## Where you'll find it

The simulator is built into the **desktop app** and the **[web app](../get-started/web.md)** — on the web it's the device that's ready the moment the page loads, which is why Snakie works on iPads and school computers with no hardware at all.

Ready to move from pretend to real? [Connect a board](../guides/connect-board.md).
