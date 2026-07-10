# The Parts Library

The Parts Library is where Snakie keeps all the little hardware pieces you can add to your projects — sensors, motor drivers, boards and more. This page explains the idea behind it, so you understand *why* it works the way it does.

## What is a "part"?

A **part** is Snakie's word for one real-world component. A distance sensor is a part. A motor driver is a part. Your microcontroller board is a part too.

Each part is just a small **folder** on your computer. Inside that folder is a text file called `parts.yml` that describes the component in plain, readable words: its name, how big it is, and what each of its pins does.

!!! example "Inside a part folder"
    ```
    vl53l0x/
      parts.yml        # the description (readable text)
      vl53l0x.py       # an optional driver for the board
      image.png        # an optional picture
    ```

> **YAML** is a simple text format for storing information as a list of `name: value` lines. You can open it and read it like a note.

A part folder can also carry a **driver** (a small MicroPython file the board needs to talk to the component), a help page, or a 3-D **mesh** for the Robot View. Because everything lives in one folder, a part is easy to copy, share or back up.

## Libraries hold many parts

Parts are grouped into **libraries**. A library is a folder full of part folders, with a `library.yml` file naming it. You can have as many libraries as you like — one from Pimoroni, one from a friend, and your very own **My Parts** library for the components you make yourself.

## Sharing through a registry

The best bit is that parts are **community-shared**. Snakie keeps a master list — called the **registry** — of approved libraries that live on GitHub. From inside Snakie you can browse that list, **install** a library with a click, and later **update** it when someone improves a part.

Each part and library carries a version number, so Snakie can tell you "a newer version is available" and fetch it for you.

## Why this design is nice

This "small folders of readable text" idea has some lovely benefits:

- **Open** — nothing is hidden. You can open any `parts.yml` and read exactly what a part is.
- **Fixable** — if a pin is wrong, you can edit one line and fix it yourself.
- **Shareable** — copy a folder to a friend, or send a change back to the registry so everyone gets it.
- **Sturdy** — if one part has a typo, Snakie just skips that part and keeps loading the rest.

!!! tip
    Because parts are plain text in folders, they work beautifully with Git version control. You can track changes to a part just like you track changes to your code.

!!! example "📸 Screenshot"
    _Show: the Parts Library panel with several libraries listed and one part's footprint previewed._

## Where to go next

- To place parts on a canvas and wire them to your board, see [Add and wire parts](../guides/add-and-wire-parts.md).
- To build your own part from scratch, see [Make a part](../guides/make-a-part.md).
- For every field you can use in a part file, see the [`parts.yml` reference](../reference/parts-yml.md).
