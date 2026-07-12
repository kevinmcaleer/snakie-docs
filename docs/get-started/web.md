# Snakie in your browser

You don't have to install anything to use Snakie. **[app.snakie.org](https://app.snakie.org)**
is the whole editor, running right in your web browser — perfect for
**Chromebooks**, school computers, or just trying Snakie in ten seconds.

[Open Snakie online :material-open-in-new:](https://app.snakie.org){ .md-button .md-button--primary }

## What you can do online

- ✍️ **Write and run MicroPython** on a built-in **simulated device** — no board
  needed. `from machine import Pin`, `print(...)`, loops and `while True:` all work.
- 🔭 Watch the on-screen **instruments** (oscilloscope, multimeter, plotter, and
  more) animate from your running program.
- 🧩 Open the **Board View**, drop in parts from the Standard Library, and see your
  wiring drawn out.
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
    The simulator and editor work in any modern browser. **Opening a folder** to
    edit files on your computer needs a **Chromium-based** browser (Chrome, Edge,
    or a Chromebook's browser). Safari and Firefox can still use everything else.

## Where your work is saved

- Files you **Open Folder** live on *your computer* — Snakie reads and writes them
  directly, so nothing is uploaded anywhere. Your browser remembers the folder
  between visits (you may click once to grant access again).
- The **simulated device** keeps its files in memory only. They reset when you
  reconnect, or when you press **Stop** on a running program — exactly like
  unplugging and re-plugging a board.

## Online vs. the desktop app

The web version has almost everything. A few things need the desktop app for now:

- Talking to a **real board** over USB.
- **Flashing** MicroPython firmware onto a board.
- Installing packages from the network (`mip`).

Connecting real boards from the browser (over Web Serial) is on the roadmap. Until
then, for hardware work, [install the desktop app](install.md) — it's free for
macOS, Windows and Linux.

!!! tip "Bookmark it"
    Add **[app.snakie.org](https://app.snakie.org)** to your bookmarks or home
    screen so it's always one click away.
