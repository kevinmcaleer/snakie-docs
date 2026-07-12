# Welcome to Snakie 🐍

**Snakie is a friendly app for writing code that runs on tiny computers.**

Those tiny computers are called **microcontrollers** — little boards like the
Raspberry Pi Pico. You plug one into your computer with a USB cable, write some
[MicroPython](explanation/what-is-micropython.md) code in Snakie, press **Run**,
and watch your board do things: blink a light, spin a motor, read a sensor.

Snakie also does some things most code editors can't:

- 🔭 It **draws a picture of your board** and shows which pins your code is using.
- 📟 It has on-screen **instruments** — an oscilloscope, a multimeter and a plotter —
  that show live readings from your program.
- 🧩 It has a **Parts Library** so you can drop in sensors and motors and wire them up.
- 🤖 It has a **3-D Robot View** where you can build a robot from parts and pose it.

!!! tip "See Snakie in action"
    [Watch two Snakie demos and read Kev's full feature tour on
    KevsRobots](https://www.kevsrobots.com/blog/what-if-building-robots-with-code-was-actually-easy.html).
    It shows the live instruments, Board View and drag-a-part workflow on real
    hardware, plus practical gotchas that are easier to understand on video.

It runs on **Windows, macOS and Linux** (including the Raspberry Pi) — or right in
your **web browser** at **[app.snakie.org](https://app.snakie.org)**, with nothing to
install ([more on the online version](get-started/web.md)).

<div class="grid cards" markdown>

-   :material-web: **Try it in your browser**

    ---

    No install needed — the whole editor + simulator runs online. Great on a
    Chromebook.

    [:octicons-arrow-right-24: Open app.snakie.org](https://app.snakie.org)

-   :material-download: **New here? Start here**

    ---

    Install Snakie and run your very first program.

    [:octicons-arrow-right-24: Install Snakie](get-started/install.md)

-   :material-school: **Tutorials**

    ---

    Step-by-step lessons. Great if you like to learn by doing.

    [:octicons-arrow-right-24: Start learning](tutorials/index.md)

-   :material-wrench: **How-to guides**

    ---

    Short recipes for a specific task, like "connect to my board".

    [:octicons-arrow-right-24: Find a recipe](guides/index.md)

-   :material-book-open-variant: **Reference**

    ---

    The details: keyboard shortcuts, file formats and APIs.

    [:octicons-arrow-right-24: Look something up](reference/index.md)

-   :material-lightbulb-on: **Explanation**

    ---

    The "why" and "how it works" behind Snakie's features.

    [:octicons-arrow-right-24: Understand Snakie](explanation/index.md)

-   :material-github: **Snakie is open source**

    ---

    The app lives on GitHub. Downloads are on the Releases page.

    [:octicons-arrow-right-24: Get the app](https://github.com/kevinmcaleer/Snakie/releases/latest)

</div>

## How these docs are organised

We follow a plan called **[Diátaxis](https://diataxis.fr/)** that splits docs into
four kinds, so you can find the right help fast:

| If you want to… | Go to |
| --- | --- |
| **Learn** by following along | [Tutorials](tutorials/index.md) |
| **Do** one specific thing | [How-to guides](guides/index.md) |
| **Look up** a fact or format | [Reference](reference/index.md) |
| **Understand** how something works | [Explanation](explanation/index.md) |

!!! tip "Never used a microcontroller before?"
    That's totally fine — Snakie is a great place to start. Read
    [What is MicroPython?](explanation/what-is-micropython.md) for a gentle
    introduction, then jump into [Blink an LED](tutorials/blink.md).
