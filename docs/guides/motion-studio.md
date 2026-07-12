# Bind servos and animate (Motion Studio)

Once your robot has joints, Motion Studio is where you bring it to life: connect a real servo to a joint, save poses, chain them into movements, and test the whole thing live. This guide walks through every step.

A *servo* is a small motor that turns to an exact angle. A *joint* is the connection between two parts of your 3-D robot. Motion Studio ties the two together, so turning the servo turns the matching joint on screen — and, when you run your code, the real robot moves too.

!!! tip "New here?"
    Build a robot first with the [Robot View guide](robot-view.md), then come back here to make it move. To understand the ideas behind joints and poses, see [How the Robot View works](../explanation/robot-view.md).

## Bind a servo to a joint

*Binding* means telling Snakie "this servo drives that joint." Once bound, a running program's servo movements move the matching joint in the 3-D model. You can bind from either view — both write the same `servoJointMap` in your `robot.yml`, so they stay in step.

**First, wire the servo's signal.** A servo has three wires; the **signal** wire is the one that carries the angle. In the [Board View](add-and-wire-parts.md), run that signal wire to a numbered **GPIO** pin (a general-purpose pin, like `GP0`). Power and ground don't count — Snakie picks the numbered pin as the servo's signal.

!!! note "The pin comes from the wire, not your code"
    Snakie reads which GPIO a servo uses from **how you wired it**, not from your Python. A line like `PWM(Pin(0))` in your code doesn't set the binding — the wire to `GP0` does.

**Then bind it, either way:**

- **In the Board View** — click the placed servo. Its inspector shows a **"drives joint"** picker. Choose the joint it should move.
- **In the Robot View** — the Build panel on the left has a **Servos** section that lists every wired servo, each with a joint picker. Pick the joint there.

!!! example "📸 Screenshot"
    _Show: a servo selected on the breadboard with its "drives joint" picker open, and the same binding appearing in the Robot View's Servos list._

## Calibrate and invert

A fresh binding assumes the servo sweeps `0…180°` onto the joint's full range. To fine-tune it, open the servo's dialog: **Robot View → Build panel → Servos → click the servo**. You can set:

- **Servo (°)** — the servo's own min and max angle.
- **Joint range** — the joint values those map onto (degrees for a turning joint, millimetres for a sliding one).
- **Invert** — a checkbox that reverses the mapping, so the servo's minimum drives the joint's maximum.

!!! tip "Model turning the wrong way?"
    If the 3-D model rotates the **opposite** way to your real servo on one joint, open that servo's dialog and tick **Invert**. It flips the model to match the hardware — it doesn't change which way the physical servo turns (that's set by how the horn is fitted).

## Save a pose

A *pose* is a named snapshot of where every joint is — like "home", "wave" or "crouch".

1. Pose the robot by dragging the **joint sliders** until it looks right.
2. Give the pose a **name** and save it.

Saved poses become the building blocks for everything below, and each one shows up as a quick button in the Poses bench.

!!! example "📸 Screenshot"
    _Show: an arm posed with the joint sliders, with a "Save pose" field named "wave"._

## Test live with the Poses bench

The **Poses bench** is an on-screen instrument (a little tool in the dock) built for trying things out. It lists every bound servo as a **slider**, and every saved pose as a **button**.

- Drag a **slider** to nudge one servo.
- Press a **pose button** to send the whole robot to that pose — it **eases** there smoothly rather than snapping.

Here's the nice part: the Poses bench drives the **on-screen 3-D model live with no program running at all**. And when a program *is* running to service the servos (see [Drive the real servos](#drive-the-real-servos) below), the same sliders and buttons move the real hardware too.

!!! tip
    The Poses bench sits alongside the Oscilloscope, Multimeter and Plotter. See [Use the instruments](instruments.md) for how to open and dock instruments.

## Chain poses into a sequence

A *sequence* is a movement built from your saved poses played one after another — a wave, a nod, or a walk cycle.

1. Add poses to the sequence in the order they should play.
2. Give each **step** a **duration** (how long to take getting there) and an **easing** (`linear` for steady, `easeInOut` for a natural glide).
3. Turn on **loop** to repeat it forever, or leave it off to play once.

Press play to preview the sequence against the 3-D model, or scrub back and forth to check each step.

!!! example "📸 Screenshot"
    _Show: a "walk" sequence of four pose steps, each with a duration, playing against the model._

## Blend poses with a puppet control

A *puppet control* is a single **slider you make** that smoothly blends two or more poses. Instead of jumping between poses, you dial anywhere in between.

- Two poses — the slider fades from one to the other (say, a shoulder down → up).
- Three or more — it blends through them in order (for example **frown → neutral → smile**, or a left → middle → right stride).

Dragging the control moves the model live, so it's perfect for expressive, hand-driven motion.

## Drive the real servos

The 3-D model follows the Poses bench and controls on its own — you don't need anything running to see the model move. To move the **real** servos, run a small program on the board that listens for those changes and applies them:

```python
import instruments as inst
from snakie import Servo, Pin, PWM
import time

servos = {n: Servo(PWM(Pin(n)), pin=n) for n in (0, 1, 2, 3)}
inst.start()                                   # opens the control channel
inst.control.on("servos",
    lambda p: inst.servos_command(p, factory=lambda pin: servos.get(pin) or inst.servo_on(pin)))
while True:
    inst.control.poll()                        # apply each slider / pose change
    time.sleep_ms(20)
```

- `servos = {…}` makes one servo per pin `GP0…GP3` once, so a pin isn't re-created on every move. `pin=n` lets each servo report its angle back, so the 3-D model stays in sync too.
- `inst.start()` opens the **control channel** — the quiet back-channel Snakie uses to send commands without interrupting your program.
- `inst.control.on("servos", …)` points incoming slider/pose commands at *your* servos.
- `inst.control.poll()` inside the loop applies whatever the Poses bench last sent.

!!! note
    The control channel is non-invasive, so this loop keeps running while you drag sliders and press pose buttons — the real servos follow along in real time.

## Export to plain MicroPython

When you're happy, Snakie can **export** the motion as clean, readable MicroPython you own and can edit. Each servo is set up in the natural `pin → PWM → Servo` order, named after the joint it drives:

```python
base_servo = PWM(Pin(0))
base = Servo(base_servo, pin=0)
```

The `pin=0` keeps the servo reporting its angle, so even the exported code still moves the 3-D model when you run it back inside Snakie.

!!! question "Does the export carry my joint limits back into the code?"
    Yes. The exported angles are **already clamped to your calibration**: Snakie maps
    each joint value through the servo's range and the joint's `min`/`max` before it
    writes the number, so the code can't command a servo past a limit you set — you
    catch bad ranges (and the collisions they cause) in the 3-D model *before* they
    reach hardware.

    The limit **values** themselves live in your project's
    [`robot.yml` → `servoJointMap`](../reference/robot-yml.md#a-servojointmap-entry)
    — `jointMin`/`jointMax`, `servoMin`/`servoMax` and `invert` — the single source of
    truth that both the Board View and Robot View write, so the calibration stays with
    the project. When Motion Studio writes your poses into a MicroPython file it also
    records them in a managed `SNAKIE_SERVOS` block that it reads back, so the whole
    binding round-trips.

## See also

- [Build a robot in 3-D](robot-view.md) — make the parts and joints Motion Studio animates.
- [Use the instruments](instruments.md) — open and dock the Poses bench alongside the other instruments.
- [robot.yml reference](../reference/robot-yml.md) — the `servoJointMap`, `poses`, `sequences` and `controls` fields behind the scenes.
- [The `snakie` module](../reference/snakie-module.md) — `from snakie import Servo, …` for hand-written robot code.
- [Pose and drive a servo](../tutorials/pose-and-drive-a-servo.md) — a step-by-step first project.
