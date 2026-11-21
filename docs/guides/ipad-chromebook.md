# Use Snakie on an iPad or Chromebook

You don't need a laptop with an install button to use Snakie. The web app at **[app.snakie.org](https://app.snakie.org)** runs happily on the two most common classroom devices — Chromebooks and iPads. This page tells you exactly what works on each, and how to set them up.

If you haven't met the web app yet, start with [Snakie in your browser](../get-started/web.md).

## On a Chromebook

Chromebooks get the **full** Snakie web experience:

- ✍️ Write and run code on the built-in [simulator](../explanation/simulator.md) — no hardware needed.
- 🔌 Plug in a **real board** (like a Raspberry Pi Pico) over USB and program it — the Chromebook's browser supports the Web Serial connection Snakie needs. See [the steps here](../get-started/web.md#connect-a-real-board-over-usb).
- 📦 Install packages, use the instruments, open the Board View and Robot View.

!!! tip "Pin it to the shelf"
    In the browser's address bar, look for the **install** icon. Installing puts
    Snakie on the ChromeOS shelf with its own icon and window — and it keeps
    working offline, because the simulator doesn't need the internet.

!!! note "For teachers and school admins"
    You can pre-approve Snakie's USB access in the Google Admin console so
    students never see a permission prompt — the policy name and a ready-made
    example are in [Snakie in your browser](../get-started/web.md#connect-a-real-board-over-usb).

## On an iPad

Open **[app.snakie.org](https://app.snakie.org)** in Safari and you can:

- ✍️ Write and run MicroPython on the **simulator** — the full editor, REPL and instruments.
- 📁 Keep your work in a **Projects folder**. iPads don't let websites open folders on the device, so Snakie gives you a Projects folder stored safely **inside the browser** instead. Tap **Open Folder** and it's just there — no dialog — and your files are waiting for you next time you visit.
- 🤖 Build robots: **New robot** works too, creating a real `robot.urdf` in your Projects folder that survives reloads.
- 👆 Wire up circuits **by touch** in the Board View: tap a part to see its pin labels, drag wires with a finger, and pinch to zoom. See [Use the Board View](board-view.md#use-it-by-touch).

!!! tip "Add it to your Home Screen"
    In Safari, tap the **Share** button, then **Add to Home Screen**. Snakie gets
    its own icon and opens full-screen, like a real app.

!!! warning "Your files live in the browser"
    On an iPad, the Projects folder is stored in Safari's website storage.
    That's real, persistent storage — but **clearing website data deletes it**.
    For work you care about, save a copy somewhere else too (for example with
    [Git](version-control.md), or by pasting important code into a note).

### What an iPad can't do

Being honest: Safari on iPadOS has no Web Serial, so an iPad **can't talk to a real board** over USB, and it can't [flash firmware](flash-firmware.md) either. The simulator is the whole show — which is still plenty for learning Python, the instruments, the Board View and the Robot View.

## Which device for which job?

| I want to… | Chromebook | iPad |
| --- | --- | --- |
| Learn Python on the simulator | ✅ | ✅ |
| Use the instruments and Board View | ✅ | ✅ |
| Build robots in the 3-D Robot View | ✅ | ✅ |
| Program a real board over USB | ✅ | ❌ |
| Flash MicroPython firmware | ❌ (needs the [desktop app](../get-started/install.md)) | ❌ |

## Where to go next

- [Snakie in your browser](../get-started/web.md) — everything about the web app.
- [How the simulator works](../explanation/simulator.md) — what the pretend board really is.
- [Your first steps](../get-started/first-steps.md) — a tour of the Snakie window.
