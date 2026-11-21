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

## Install a package step by step

1. Open the **Packages** panel from the activity bar on the left edge.
2. Type the package name into the **search box**, for example `ssd1306`.
3. Find it in the **REGISTRY** list of results.
4. Click **INSTALL** next to it.

Snakie runs mip on your board and shows you a live log of what's happening. When it finishes, the package appears in the **INSTALLED** list, and you can `import` it in your code straight away.

!!! example "📸 Screenshot"
    _Show: the Packages panel with a search result and its INSTALL button, plus the INSTALLED list below._

```python
# After installing the ssd1306 package you can import it:
import ssd1306
# ...now set up your screen and draw to it.
```

!!! tip "No Wi-Fi? No problem"
    A plain Raspberry Pi Pico can't reach the internet on its own. Snakie handles this by downloading the package on your computer and copying the files to the board, so mip works on every board.

## See what's already on your board

The panel's **ON BOARD (/lib)** list shows every package that's really installed on the board right now — read straight from the board's `/lib` folder, with each package's version next to it.

- Click **Uninstall** to remove a package you no longer need.
- If the registry has a **newer version** of something on your board, Snakie offers an **Upgrade** button right there.

The list refreshes by itself whenever anything installs to the board — even from a different Snakie window.

## Find missing imports

Not sure which packages your project needs? Click **⌕ Scan imports**. Snakie reads every `.py` file in your project and lists any `import` that nothing satisfies — not built into the firmware, not on the board, and not one of your own files. Each missing one gets a one-click install button.

## Keep an eye on space

Boards have a small amount of storage, called **flash**. The Packages panel shows a **Flash storage used** meter so you can see how much room is left. If it fills up, remove packages you no longer need.

## Advanced options

Expand **Advanced options** if you want to:

- install from a `github:user/repo` package,
- use a **custom index URL** (a different place to fetch packages from), or
- choose whether existing files get overwritten.

Most of the time you won't need these, so feel free to skip them.

## Parts can install their own driver

Here's a lovely shortcut. When you add a part that needs a driver in the Board View, Snakie often offers to install it **for you**. A banner appears above the editor with a button to add the driver, and you don't have to search for anything.

!!! example "📸 Screenshot"
    _Show: the banner above the editor offering to install a part's driver._

To learn about adding parts and connecting them up, see [Add and wire parts](../guides/add-and-wire-parts.md).

!!! warning "Nothing happens?"
    If the INSTALL button is greyed out, your board probably isn't connected. Check the connection and try again. If an install fails, read the log message shown, it usually tells you what went wrong (for example, a name typed slightly wrong).

Once your driver is installed, you're ready to write code that talks to your new part. Have fun building!
