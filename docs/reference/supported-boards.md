# Supported boards

Snakie knows about lots of MicroPython boards. This page lists the ones it can **draw** in the Board View and the ones it can **flash** with fresh MicroPython firmware.

!!! note "Two different lists"
    A board is a small computer you can program (a "microcontroller"). Snakie can do two things with boards:

    - **Draw** a picture of the exact board in the [Board View](../guides/board-view.md).
    - **Flash** (install) MicroPython onto a board — see [Flash firmware](../guides/flash-firmware.md).

    These are separate lists, so a board might be on one and not the other.

## Boards the Board View can draw

The Board View reads your code, finds the pins you use, and draws them on a life-like picture of the real board. Most of these board pictures come from the **Standard [Parts Library](../explanation/parts-library.md)** that ships with Snakie — every microcontroller part in the library is also a board the Board View can draw.

| Board | Chip | Good to know |
|-------|------|--------------|
| Raspberry Pi Pico 2 W | RP2350 | The default board. Has Wi‑Fi; the onboard light is `Pin("LED")`. |
| Raspberry Pi Pico W | RP2040 | The original Pico with Wi‑Fi; onboard light is `Pin("LED")`. |
| Raspberry Pi Pico | RP2040 | The original Pico; onboard light is `Pin(25)`. |
| Pimoroni Pico Plus 2 | RP2350 | Same shape as a Pico, but with a USB‑C socket and extra memory. |
| Pimoroni Tiny 2040 | RP2040 | A very small board with pads down its two long edges and an RGB light. |
| Pimoroni Tiny 2350 | RP2350 | Like the Tiny 2040, with the newer RP2350 chip. |
| Pimoroni Motor 2040 | RP2040 | A board made for driving four DC motors. |
| Pimoroni Servo 2040 | RP2040 | A board made for driving up to 18 servos. |
| Seeed Studio XIAO RP2040 | RP2040 | Thumbnail-sized board with a USB‑C socket. |
| Seeed Studio XIAO RP2350 | RP2350 | The XIAO with the newer RP2350 chip. |
| Adafruit Feather RP2040 | RP2040 | Feather-shaped board with battery charging built in. |
| Adafruit Feather ESP32‑S3 | ESP32‑S3 | A Feather with Wi‑Fi and Bluetooth. |
| Adafruit Feather nRF52840 Express | nRF52840 | A Feather with Bluetooth. |
| Adafruit ItsyBitsy RP2040 | RP2040 | A small, thin RP2040 board. |
| Adafruit QT Py RP2040 | RP2040 | A thumb-sized board with a STEMMA QT socket. |
| ESP32 DevKit | ESP32 | The common 30‑pin ESP32‑WROOM‑32 dev board. |
| ESP32‑12F | ESP32 | Another common ESP32 dev board. |

!!! tip "Not on the list? Make your own"
    You can add any board yourself with the **Part Editor** or the visual **Board Creator** — see [Make your own part](../guides/make-a-part.md). Your board then appears in the Board View just like the built-in ones, and you can share it with friends too.

The Board View can also try to guess your board from the message a board prints when it starts up, so the right picture often appears on its own.

## Boards Snakie can flash

Flashing means copying a fresh copy of MicroPython onto a board. Snakie shows a built-in catalog (a big list) of official MicroPython builds, so you do not have to hunt for a file on the internet. You pick your board, pick a version, and Snakie does the rest.

The catalog covers three big families of boards:

| Family | Example chips | Firmware file |
|--------|---------------|---------------|
| Raspberry Pi RP2 | RP2040, RP2350 (Pico, Pico W, Pico 2, Pico 2 W, and many more) | `.uf2` |
| Espressif ESP | ESP32, ESP32‑S2/S3, ESP32‑C2/C3/C5/C6, ESP32‑P4, ESP8266 | `.bin` |
| BBC micro:bit | micro:bit v1 and v2 | `.hex` |

!!! note "It is a live list"
    The flashing catalog is downloaded when you open the flash window, so the exact boards and versions can grow over time. You will need an internet connection the first time to fetch it.

Because Snakie uses the official MicroPython builds, hundreds of boards are flashable — far more than the ones drawn in the Board View. For a full catalogue of every board with an official MicroPython build, see the repo file `docs/micropython-boards.md`.

!!! warning "Match the file to your board"
    Always choose the build that matches your exact board and chip. Flashing the wrong file can stop a board working until you flash the right one. When in doubt, pick the entry with your board's name in it.

## What next?

- Ready to install MicroPython? Head to [Flash firmware](../guides/flash-firmware.md).
- Want to see your pins come alive? Open the [Board View](../guides/board-view.md).
