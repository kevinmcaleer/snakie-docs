# How Snakie talks to your board

This page explains, in a friendly way, the clever trick that lets Snakie do so much over a single USB cable: run your code, manage your files, and feed the live instruments, all at the same time.

## Two little words: serial and REPL

Before we start, here are the two words you'll keep hearing.

- **Serial** is a way of sending information down a wire one tiny piece at a time, like beads on a string. Your USB cable carries a serial connection between your computer and your board.
- **REPL** stands for Read–Eval–Print Loop. It's just MicroPython's friendly prompt: you type a line, it reads it, runs it, prints the answer, and waits for the next line. It's the same prompt you see in Snakie's [interactive shell](../guides/instruments.md).

So "talking over serial to the REPL" simply means: your computer types things to MicroPython down the USB cable, and MicroPython types its answers back.

## The one-cable magic trick: raw REPL

Here's the neat part. That friendly prompt is lovely for a human, but a bit chatty for a program. It prints banners, echoes what you typed, and adds decoration. When Snakie wants to do a job precisely, it switches MicroPython into a quieter mode called the **raw REPL**.

Think of it like this:

- The **friendly REPL** is talking out loud in a room.
- The **raw REPL** is passing tidy notes back and forth. No chit-chat, no echo, just "here's some code, run it, give me the result."

!!! note "Where the raw REPL comes from"
    The raw REPL is built into MicroPython itself, not into Snakie. Snakie flips into it by sending a special control character, then flips back out when it's done. You don't have to do anything.

Because the raw REPL can run *any* Python on the board, Snakie can use it for more than just running your program:

- **Run your code** — Snakie hands your whole file to the board and shows you what it prints.
- **Read and write files** — to save a file to the board, Snakie quietly runs a little bit of Python that opens the file and writes your text into it. To list your files, it runs Python that lists them. That's how the [device file browser](../guides/manage-files.md) works, over the very same cable.

!!! tip "Stop and reset"
    When you press Stop and nothing is running, Snakie also gives the board a gentle **soft reset**, so it starts fresh and clean, ready for your next Run.

## How the instruments listen in

The Oscilloscope, Multimeter, and Plotter feel like they're plugged into the board separately, but they're not. They share the exact same USB serial connection.

The trick is a tiny helper library that Snakie can install on your board with one click. Your program calls small functions from it — like `scope()`, `meter()`, and `plot()` — to send out little readings as it runs:

```python
from machine import Pin
import time

led = Pin("LED", Pin.OUT)

while True:
    led.toggle()
    time.sleep(0.5)
```

Add a telemetry call inside your loop and those readings stream back up the cable, where Snakie catches them and draws them on the instruments — live.

!!! example "📸 Screenshot"
    _Show: a program running on the left while the Plotter and Multimeter update in real time on the right._

The important word here is **non-invasive**. The instruments only read the little messages your program chooses to send. They don't interrupt it, slow it down, or change what it does. Your program stays in charge; the instruments just watch and draw.

## The big picture

One USB cable. One serial connection. One built-in MicroPython prompt. From that single link, Snakie runs your code, looks after your files, and powers the live instruments — all by politely talking to your board in the language it already speaks.

Ready to try it? Start by learning how to [connect your board](../guides/connect-board.md).
