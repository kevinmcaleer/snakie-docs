# Flash firmware

A brand-new board often arrives empty. This page shows you how to put MicroPython onto it using Snakie's built-in flasher, so your board is ready to run your code.

!!! note "What is firmware?"
    **Firmware** is the base software that lives on the board itself. MicroPython *is* the firmware here — it is the program that lets your board understand Python. Learn more in [What is MicroPython?](../explanation/what-is-micropython.md).

!!! warning "Flashing replaces what is on the board"
    Flashing installs fresh firmware over the top of whatever is already there. Any MicroPython files you saved on the board can be wiped, so copy anything you want to keep to your computer first.

## Open the flasher

Click the **⚡ Flash firmware** button on the right of the status bar (the strip along the bottom of the window).

Snakie looks for connected boards automatically. Press **⟳ Detect** at any time to scan again after you plug a board in.

!!! example "📸 Screenshot"
    _Show: the Flash firmware dialog with a detected board and the Board type dropdown open._

## 1. Pick your board

Choose your board from the **Board type** list:

| Board | How it flashes |
| --- | --- |
| RP2040 / Pico (UF2) | Copies a `.uf2` file to a special drive |
| ESP32 / ESP8266 (esptool) | Flashes over the serial (USB) port |
| BBC micro:bit (.hex) | Copies a `.hex` file to the micro:bit drive |

Not sure your board is in the list? See [Supported boards](../reference/supported-boards.md).

## 2. Choose the firmware

Pick where the firmware comes from:

- **Download from MicroPython.org** — choose a **Family → Model → Variant → Version** and Snakie fetches the correct file for you. This is the easy choice.
- **Local file** — browse to a firmware file you already downloaded (`.uf2`, `.bin` or `.hex`).

## 3. Flash it

=== "Raspberry Pi Pico / RP2040"

    1. Unplug the board.
    2. Hold down the **BOOTSEL** button while you plug it back in, then let go.
    3. A drive called `RPI-RP2` appears — pick it in the dialog.
    4. Press **Flash**. Snakie copies the file across and the board reboots into MicroPython.

=== "ESP32 / ESP8266"

    1. Pick the **serial port** for your board.
    2. Leave the **flash offset** as filled in.
    3. Press **Flash**.

    !!! note "esptool needed"
        ESP boards flash with a helper called `esptool`. If the dialog says it is missing, install it once from a terminal:
        ```bash
        pip install esptool
        ```

=== "micro:bit"

    1. Pick the `MICROBIT` drive.
    2. Press **Flash**.

    !!! warning
        If you see a `MAINTENANCE` drive instead, unplug and replug **without** holding the reset button. Flashing in maintenance mode can break the board, so Snakie will not let you.

A progress bar and a live log show each step. When it finishes, press **Done**.

## Try it out

Now [connect to your board](connect-board.md), open the shell, and toggle the onboard LED to check MicroPython is running:

```python
from machine import Pin
import time

led = Pin("LED", Pin.OUT)
while True:
    led.toggle()
    time.sleep(0.5)
```

The light should blink on and off. 🎉

## Keeping firmware up to date

When a board is connected, Snakie can tell you if a newer MicroPython is available and offer to update it from the same **⚡** button. You can switch this on or off in **Settings ▸ Editor ▸ Firmware updates**.

!!! tip
    You only need to flash firmware once (or when you want a newer version). After that, just [connect](connect-board.md) and start coding.
