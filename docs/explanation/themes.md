# Themes and skins

Snakie is designed to feel like a real gadget on your desk, not just another window full of buttons. This page tells the story behind that look, and why we made it feel so tactile.

## What "skeuomorph" means

**Skeuomorph** is a big word for a simple idea: a design that looks like a real, physical material or object.

When something is skeuomorphic, a button looks like a button you could actually press, and a panel looks like it is made from real stuff — metal, paper, glass or felt. Your brain already knows how those things behave in the real world, so the software feels familiar before you have learned a single menu.

!!! example "📸 Screenshot"
    _Show: the Snakie editor in the light skeuomorph skin, with the brushed-metal top bar, ruled-paper editor and green console visible together._

## The materials of Snakie

Snakie has its own little world of textures. You will spot the same materials all over the app:

| Part of Snakie | What it looks like |
| --- | --- |
| The top bar and edges | Brushed metal, like a real instrument panel |
| The knobs and switches | Shiny brass, the kind you want to twist |
| The code editor | Warm, ruled paper — like a notebook page |
| The version-control panel | Soft green felt |
| The shell (REPL) | Recessed dark glass with a glowing green "phosphor" screen, like an old lab display |

Using the same materials everywhere keeps things calm and consistent. Once you learn what a brass knob does in one place, you know what it does everywhere.

!!! note "What is a REPL?"
    The REPL (say it "repple") is the live shell where you type one line of MicroPython and the board answers straight away. In Snakie it looks like a glowing green screen.

## Light and dark

Snakie ships with two matching skins, and you can flip between them whenever you like:

- **Skeuomorph (light)** — the default. Warm parchment, cream paper and daylight brass. Friendly and bright.
- **Dark** — the very same materials, dressed in a darker palette. Dark brushed metal, deep-slate paper and the same glowing green screen.

They are twins, not strangers. Every panel, knob and screen has a light version and a dark version, so nothing looks out of place when you switch.

!!! tip "Try both"
    There is no "right" one. Pick the skin that is kindest to your eyes today. Working late? Dark mode is gentle. Sunny room? Light mode pops.

## Why a friendly, tactile look helps

Learning to code can feel a bit scary at first. A cold, grey grid of tools does not help. A warm, tactile look does three quiet, helpful things:

1. **It invites you in.** Something that looks like a fun instrument feels safe to poke at and explore.
2. **It borrows what you already know.** Real-world knobs, paper and screens need no explaining. That leaves more of your brain free for the actual coding.
3. **It makes tinkering joyful.** MicroPython is about making lights blink and robots move. Your editor should feel just as playful as the projects you build with it.

Here is the kind of small, happy project Snakie is built for — blinking the onboard LED on a Raspberry Pi Pico:

```python
from machine import Pin
import time

led = Pin("LED", Pin.OUT)

while True:
    led.toggle()
    time.sleep(0.5)
```

## Ready to switch?

Now you know the *why*. When you want the *how* — the exact steps to change your skin and flip between light and dark — head over to the how-to guide.

[Change your theme and skin →](../guides/themes.md)
