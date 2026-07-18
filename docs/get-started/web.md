# Snakie in your browser

You don't have to install anything to use Snakie. **[app.snakie.org](https://app.snakie.org)**
is the whole editor, running right in your web browser — perfect for
**Chromebooks**, **iPads**, school computers, or just trying Snakie in ten seconds.

[Open Snakie online :material-open-in-new:](https://app.snakie.org){ .md-button .md-button--primary }

## What you can do online

- ✍️ **Write and run MicroPython** on a built-in **simulated device** — no board
  needed. `from machine import Pin`, `print(...)`, loops and `while True:` all work.
- 🔭 Watch the on-screen **instruments** (oscilloscope, multimeter, plotter, and
  more) animate from your running program.
- 🧩 Open the **Board View**, drop in parts from the Standard Library, and see your
  wiring drawn out. The board icon in the toolbar pops it out into its **own browser
  window**, just like on the desktop.
- 📦 **Install packages** from the [Packages panel](../guides/install-packages.md) —
  drivers and modules install to the board's `/lib`, on real boards and on the
  simulator.
- 🤖 Build and pose robots in the **3-D Robot View** — run a servo program and watch
  the model move.
- 📂 **Open a real folder** on your computer and edit + save files straight to disk.

The simulator is the same MicroPython that runs on a real board, so your code
behaves the way it will on hardware — you just don't need the hardware to start.

## Connecting to Snakie online

Just open **[app.snakie.org](https://app.snakie.org)** and click **Connect** on the
*Simulated device (offline)* — it's ready to run code immediately. Press **New file**,
type a program, and press **Run**.

!!! note "Which browser?"
    The simulator and editor work in any modern browser. **Connecting a real
    board** needs a **Chromium-based** browser (Chrome, Edge, or a Chromebook's
    browser). Safari and Firefox can still use everything else — on an iPad,
    Snakie even gives you a built-in **Projects** folder so your work is saved
    between visits. See [Snakie on an iPad or Chromebook](../guides/ipad-chromebook.md).

!!! tip "Install it like an app"
    app.snakie.org is a **PWA** (a web page that can behave like an installed
    app). In Chrome or Edge, look for the **install** icon in the address bar —
    Snakie then gets its own window and icon, and keeps working even when you're
    offline (the simulator doesn't need the internet).

## Connect a real board over USB

On a Chromium browser you can plug a **real** MicroPython board (a Raspberry Pi
Pico, an ESP32, and friends) into USB and use it just like the simulator — the
REPL, **Run**/**Stop**, the device file tree, package installs and the instruments
all work over the board.

1. Plug the board in.
2. In the port dropdown (top of the shell) choose **＋ Connect a USB board** and
   pick your board in the browser's chooser. Boards you've allowed before appear
   in the list directly next time.
3. Press **Connect**. Write code, press **Run** — it runs on the real board.

!!! tip "Chromebooks in a classroom"
    School admins can pre-approve Snakie so students get **no permission prompt**,
    via the Google Admin console policy
    [`SerialAllowUsbDevicesForUrls`](https://chromeenterprise.google/policies/#SerialAllowUsbDevicesForUrls).
    Example (Pico + the common bridge chips):

    ```json
    [{ "urls": ["https://app.snakie.org"], "devices": [
      { "vendor_id": 11914 },   // Raspberry Pi (Pico / RP2040)
      { "vendor_id": 12346 },   // Espressif (native-USB ESP32-S2/S3)
      { "vendor_id": 4292  },   // Silicon Labs CP210x bridge
      { "vendor_id": 6790  },   // WCH CH340 bridge
      { "vendor_id": 1027  }    // FTDI bridge
    ]}]
    ```

## Where your work is saved

- Files you **Open Folder** live on *your computer* — Snakie reads and writes them
  directly, so nothing is uploaded anywhere. Your browser remembers the folder
  between visits (you may click once to grant access again).
- On an **iPad** (which has no folder picker), **Open Folder** gives you a
  **Projects** folder stored safely inside the browser instead. It's there again
  every time you come back. More in
  [Snakie on an iPad or Chromebook](../guides/ipad-chromebook.md).
- The **simulated device** keeps its files in memory only. They reset when you
  reconnect, or when you press **Stop** on a running program — exactly like
  unplugging and re-plugging a board.

## Online vs. the desktop app

The web version has almost everything — including talking to a real board (above)
and installing packages. One thing still needs the desktop app:

- **Flashing** MicroPython firmware onto a blank board.

For that, [install the desktop app](install.md) — it's free for macOS, Windows
and Linux.

!!! tip "Bookmark it"
    Add **[app.snakie.org](https://app.snakie.org)** to your bookmarks or home
    screen so it's always one click away.
