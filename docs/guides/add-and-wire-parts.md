# Add and wire up parts

Snakie can draw your whole circuit, not just your board. This page shows you how to drop a part — like a sensor — next to your microcontroller and connect their pins with wires.

!!! note "New word: part"
    A **part** is anything you plug into your board — a sensor, a button, a motor driver, a screen. Snakie keeps a whole [Parts Library](../explanation/parts-library.md) of them.

## Before you start

- Open a project folder in Snakie.
- Open the **Board View** window, which has the wiring canvas.
- Have the **Parts** panel handy — it lists every part you have installed.

If a part you want is not there yet, you can [browse and install one from the community library](../explanation/parts-library.md), or [make your own](make-a-part.md).

## Step 1 — Pick a canvas

Snakie gives you two ways to look at the same circuit:

| Canvas | Looks like | Wires are… |
| --- | --- | --- |
| **Breadboard** | Your real parts on paper | Curvy "noodle" wires you draw by hand |
| **Schematic** | Tidy labelled blocks | Neat right-angle lines, routed for you |

Pick whichever feels friendlier. Your work is the same in both.

## Step 2 — Drag a part onto the canvas

1. Find your part in the docked **Parts** panel.
2. **Drag** it out and **drop** it onto the canvas, near your microcontroller.
3. The part appears at real size, drawn just as it was authored.

!!! tip
    You can drop as many parts as you like. Move a part any time by dragging its body.

!!! example "📸 Screenshot"
    _Show: a distance sensor being dragged from the Parts panel onto the breadboard beside a Pico._

## Step 3 — Wire the pins together

Now connect the pins — the little metal legs that carry signals.

1. Click a pin on one part.
2. Click a pin on the other part (or on your board).
3. A wire joins them.

Snakie **colours wires by their job** so your circuit is easy to read:

- **Red** — power (the "+" that feeds the part).
- **White** — ground (the "−" the part shares with your board).
- **Colour** — everything else (signals). You can pick the colour you like.

In **Breadboard** mode the wires are soft node-RED-style noodles. In **Schematic** mode Snakie draws tidy straight lines and bends them around your parts automatically.

!!! note "Pins your code uses light up"
    Snakie reads your Python and **highlights the pins your code actually uses**. That makes it easy to check you wired the right leg. For example, this uses the onboard LED:

    ```python
    from machine import Pin
    import time

    led = Pin("LED", Pin.OUT)
    while True:
        led.toggle()
        time.sleep(0.5)
    ```

## Step 4 — Let a part bring its driver (optional)

Some parts need a small helper file on the board to work — called a **driver**. If a part you placed needs one, Snakie shows a gentle banner offering to **install the driver** for you. Nothing is copied to your board until you click it, and you need a board connected.

Prefer to do it yourself? See [Install packages](install-packages.md).

## Step 5 — Your design is saved

Your parts and wires are stored in a **`robot.yml`** file in your project. That means your whole circuit travels with your code — open the project later and it is all still there.

See [The robot.yml file](../reference/robot-yml.md) for what is inside, and [The parts.yml file](../reference/parts-yml.md) for how each part describes its pins.

!!! tip "Next steps"
    - Want a part that does not exist yet? [Make a part](make-a-part.md).
    - Curious how the library works? Read [about the Parts Library](../explanation/parts-library.md).
