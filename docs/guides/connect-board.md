# Connect to your board

This page shows you how to link Snakie to a MicroPython board so you can run your code on it. MicroPython is a small version of Python that runs on tiny computer chips like the Raspberry Pi Pico.

You only need two things: your board and a USB cable.

## Step 1: Plug the board in

Connect your board to your computer with a USB cable.

!!! warning "Use a *data* cable, not a charge-only one"
    Some USB cables can only carry power, not data. If your computer never notices the board, a charge-only cable is the most common reason. Swap it for one you know can move files.

When the board is plugged in, your computer sees it as a **serial port** — a named channel that Snakie uses to talk to the board.

## Step 2: Choose the serial port

Near the shell (the terminal panel at the bottom of Snakie) there is a small drop-down list of serial ports.

1. Open the drop-down.
2. Pick your board. Each entry shows the port name, and often the maker's name too, so you can tell which one is your board.

!!! tip "Not sure which one is yours?"
    Unplug the board, open the list, then plug it back in and press the refresh button (**⟳**) next to the drop-down. The entry that appears is your board.

## Step 3: Press Connect

Click the **Connect** button. The button shows **Connecting…** for a moment, then changes to **Disconnect** once you are linked.

## How you know it worked

Look at the **status bar** — the thin strip along the very bottom of the window. When you are connected it shows a coloured dot and a label like:

```
● Connected · /dev/ttyACM0
```

The name after the dot is your board's port, so it may look different on your computer. When you are not connected, it simply reads **Disconnected**.

!!! example "📸 Screenshot"
    _Show: the status bar reading "Connected" with a green dot and the board's port name._

Now you are ready to [run your code and stop it](run-and-stop.md).

!!! tip "No board yet?"
    You can still explore Snakie. Pick the **offline** device in the port list to try things out without any hardware. The status bar will say **offline** so you always know it is not a real board.

## Troubleshooting

Connecting almost always just works, but here is what to try if it doesn't.

| What you see | What to try |
| --- | --- |
| Your board is not in the list | Check the cable is a **data** cable, try a different USB port, then press the refresh (**⟳**) button. On some computers a **driver** may be needed for the board's USB chip — check your board maker's guide. |
| Connect fails or says the port is **busy** | Another program is probably holding the port. Close tools like Thonny, `mpremote`, or any serial monitor, then try again. |
| It connects but nothing works, or you see odd characters | Your board may not have MicroPython on it yet. See [Flash firmware](flash-firmware.md) to install it first. |

!!! note "Want to know what's happening under the hood?"
    Curious how Snakie chats with the chip over that serial port? Read [How Snakie talks to your board](../explanation/how-snakie-talks-to-your-board.md).
