# Install a package

Some parts need a little extra code, called a **driver**, before your board knows how to talk to them. This page shows you how to add one using Snakie's **Packages** panel.

## What is a package?

A **package** (also called a **library**) is a bundle of ready-made MicroPython code that someone else has written and shared. Instead of writing everything yourself, you install their package and just `import` it.

**mip** is MicroPython's built-in package installer. Snakie runs it on your board for you, so you never have to type install commands by hand.

!!! note "When would you need one?"
    A **sensor** is a part that measures something, like distance or temperature. Many sensors, such as an OLED screen (`ssd1306`) or a distance sensor, need their own driver package before they will work. If your code says `import ssd1306` but you never installed it, the board will complain that it can't find the module.

## Before you start

You need a connected board — a real one **or the simulator**. If you haven't done that yet, follow [Connect a board](connect-board.md) first. Installing writes files to the board, so it must be awake and connected.

!!! note "Works everywhere"
    The Packages panel works on the desktop app, on real boards connected over
    USB in the [web app](../get-started/web.md), and on the built-in simulator.

## The two tabs

Open the **Packages** panel from the activity bar on the left edge. It has two tabs, named for what you're there to do:

| Tab | What's in it |
| --- | --- |
| **Get libraries** | Everything you can **add** to your board: the package search, the **Popular libraries** list, **⌕ Scan imports**, and **Snakie drivers** (Snakie's own drivers for the parts and instruments it knows). |
| **On this board** | Everything that's **already there**: how full the board is, the libraries you've installed (with **Uninstall** and **Upgrade**), and every module your code can import. |

You can start an install, switch tab to look at something, and come back. The install keeps going.

## Install a package step by step

1. Open the **Packages** panel and stay on the **Get libraries** tab.
2. Type the package name into the **Search packages…** box, for example `ssd1306`, and press **Search**.
3. Find it in the **Search results** list. (Before you search, the list shows **Popular libraries** instead.)
4. Click **Install** on its row.

Snakie runs mip on your board and shows you a live log of what's happening. When it finishes, the row says **INSTALLED**, the library shows up on the **On this board** tab, and you can `import` it in your code straight away.

!!! example "📸 Screenshot"
    _Show: the Get libraries tab with a search result and its Install button._

```python
# After installing the ssd1306 package you can import it:
import ssd1306
# ...now set up your screen and draw to it.
```

!!! tip "No Wi-Fi? No problem"
    A plain Raspberry Pi Pico can't reach the internet on its own. Snakie handles this by downloading the package on your computer and copying the files to the board, so mip works on every board.

!!! note "No board connected yet?"
    You can still search and browse everything. To install, connect a board (or the simulator) first. The panel tells you so, and hovering **Install** says *Connect a board first*.

## Snakie drivers

Further down **Get libraries** is **Snakie drivers**: drivers Snakie ships for the parts and instruments it supports, grouped by the instrument each one powers. Install only the ones your project needs. Snakie shows the drivers that match what your board runs: MicroPython ones, or CircuitPython ones from the Adafruit CircuitPython Library Bundle on a CircuitPython board.

A driver that's already part of the board's firmware is marked **BUILT IN**, so there's nothing to install.

## See what's already on your board

Switch to the **On this board** tab. Its **Installed libraries (/lib)** list shows every library that's really on the board right now, read straight from the board's `/lib` folder, with each one's version next to it.

- Click **Uninstall** to remove a library you no longer need.
- If the index has a **newer version** of something on your board, an **Upgrade** button appears right there.

Below that is every module your code can import, including the ones built into the firmware.

The list refreshes by itself whenever anything installs to the board, even from a different Snakie window.

## Find missing imports

Not sure which packages your project needs? With a board connected and a project folder open, click **⌕ Scan imports** on the **Get libraries** tab. Snakie reads every `.py` file in your project and lists any `import` that nothing satisfies: not built into the firmware, not on the board, and not one of your own files. Each missing one gets a **+ name** button that installs it. If nothing is missing, you'll see **All imports satisfied ✓**.

## Keep an eye on space

Boards have a small amount of storage, called **flash**. The **On this board** tab shows a **Board storage** meter so you can see how much room is left. If it fills up, remove packages you no longer need.

## Advanced options

Expand **Advanced options** if you want to:

- install from a `github:user/repo` package,
- use a **custom index URL** (a different place to fetch packages from), or
- choose whether existing files get overwritten.

Most of the time you won't need these, so feel free to skip them.

## Parts can install their own driver

Here's a lovely shortcut. When a part in your project needs a driver, an amber **Drivers** chip appears beside **Find** in the Code workspace. Tap it and a card opens over your code listing each driver, with **Install drivers** and **Show parts**. You don't have to search for anything.

If no board is connected when you press **Install drivers**, Snakie asks you to connect one and installs the drivers as soon as the board arrives.

!!! example "📸 Screenshot"
    _Show: the amber Drivers chip beside Find, with its card open over the code._

To learn about adding parts and connecting them up, see [Add and wire parts](../guides/add-and-wire-parts.md).

!!! warning "Install didn't work?"
    If an install fails, the row's button changes to **RETRY**. Read the log message shown first: it usually tells you what went wrong (for example, a name typed slightly wrong).

Once your driver is installed, you're ready to write code that talks to your new part. Have fun building!
