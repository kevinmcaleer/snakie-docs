# Make your own part

Snakie comes with lots of parts, but sometimes you want one that isn't there yet. The visual **Part Editor** lets you draw your own part — its shape, its pins, its holes and buttons — with no code required. A **part** is just a small building block, like a sensor or a motor driver, that you can drop into your projects.

When you finish, your part joins your own library and can be wired up like any other. To learn how to place and wire it, see [Add and wire parts](add-and-wire-parts.md).

!!! example "📸 Screenshot"
    _Show: the Part Editor with a board outline, a row of pins along one edge, and the tool buttons down the side._

## Open the Part Editor

You author parts from the **Parts** panel.

1. Open the Parts panel.
2. Choose to create a new part. This opens the Part Editor.
3. Give your part a name in its details.

Your new part is saved into your own parts library, so it stays separate from the built-in ones.

## Set the shape and size

Every part starts as a simple board outline (a rectangle).

- Set the **width** and **height** so it matches your real part in millimetres (mm). A millimetre is a tiny unit — a small sensor might be around 16 mm wide.
- Use the **shape tool** if you want a custom outline. You can drag the corner points, and click an edge to add a new point.
- You can even upload a photo of the real board onto the PCB layer to trace over.

!!! tip
    Turn on the **grid** and everything **snaps to a 2.54 mm grid**. That spacing is the standard gap between header pins, so your pins line up neatly with a breadboard.

## Add pins

Pins are the legs that carry power and signals.

1. Pick the **Add pin** tool and click on the board where the pin goes.
2. Select the pin to open its inspector.
3. Give it a **name** (like `SDA` or `GP0`), a **type**, and any **capabilities**.

**Pin types** tell Snakie what the pin does:

| Type | Meaning |
|------|---------|
| Power | Sends power in (like 3V3 or VCC) |
| Ground | The 0 V return path (GND) |
| IO | A general input/output pin |
| Other | Anything else |

**Capabilities** are extra skills a pin has. Tick any that apply:

| Capability | What it means |
|------------|---------------|
| Digital | On/off signals |
| PWM | "Dimming" signals, e.g. for LED brightness or motor speed |
| ADC | Reads changing voltages, e.g. from a dial |
| I²C, SPI, UART | Ways two chips talk to each other |

You can also choose a **pad shape** for how each pin looks: **Square**, **Round**, **Castellated** (a half-hole on the edge of the board), or **Header**.

## Add holes and buttons

- Use the **mounting hole** tool to add screw holes. Pins can't sit inside a hole.
- Use the **push-button** tool to add a clickable button.
- There are quick buttons for handy extras too, like an onboard **LED** or a **QWIIC / STEMMA QT** connector.

## Check both views

At the top you can flip between two views:

- **Breadboard** — the life-like picture of your part, as it really looks.
- **Schematic** — the tidy symbol version used in circuit diagrams.

Switch to Schematic to see the **Schematic symbol** preview and make sure your pins are labelled clearly.

!!! example "📸 Screenshot"
    _Show: the Breadboard and Schematic tabs side by side, with the same part in both styles._

## Save your part

When you're happy, choose **Save**. Snakie writes your part as a folder containing a human-readable `parts.yml` file — the recipe that describes every pin, hole and shape. You never have to edit it by hand, but if you're curious, see [The parts.yml file](../reference/parts-yml.md).

!!! note
    Because a part is just a folder, it's easy to share with friends. To understand how parts and libraries fit together, read [About the Parts Library](../explanation/parts-library.md).

Well done — you've made a reusable part you can wire into any project!
