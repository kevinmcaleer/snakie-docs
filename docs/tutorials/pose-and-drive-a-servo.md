# Pose and drive a servo

In this tutorial you'll take one servo from a wire on a breadboard all the way to a moving 3-D model — and then to a real, moving motor. You'll bind the servo to a joint, save a couple of poses, and drive it live from the **Poses bench**, watching both the on-screen robot and the physical servo move together.

We'll keep it to **one servo** so every step stays clear. Once you've done it once, adding more is just more of the same.

!!! tip "New here?"
    This tutorial assumes you already have a simple robot with at least one joint. If you don't, build one first with the [First robot tutorial](first-robot.md) — it takes about ten minutes — then come back here.

## What you'll need

- A microcontroller board, such as a **Raspberry Pi Pico**.
- One **hobby servo** (an SG90 is perfect — small, cheap, and 3-pin).
- Three jumper wires to connect the servo's signal, power and ground.

A *servo* is a little motor that turns to an **angle** you ask for (0° to 180°), rather than just spinning. That makes it ideal for a robot joint.

## 1. Place and wire the servo

1. Open the **Board View**.
2. From the Parts Library, drop an **SG90** onto the canvas.
3. Wire it up:
    - the servo's **Signal** pin to **GP0** on your board,
    - its **V+** (power) to a power pin,
    - its **GND** (ground) to a ground pin.

The **signal wire** is the important one for Snakie: it's how Snakie knows *which GPIO* drives this servo. (A *GPIO* is a numbered pin on your board — GP0, GP1, and so on.) Power and ground just keep the servo alive.

!!! example "📸 Screenshot"
    _Show: an SG90 on the Board View canvas with its Signal wire running to GP0, plus power and ground._

## 2. Bind the servo to a joint

Now tell Snakie which joint this servo should move.

1. Switch to the **Robot View**.
2. In the **Build panel** on the left, open the **Servos** section. Your GP0 servo is listed there.
3. Pick the **joint** it should drive from the dropdown next to it.

That's the whole idea of *binding*: the servo on GP0 is now tied to one joint of your 3-D robot, so moving one moves the other.

!!! example "📸 Screenshot"
    _Show: the Build panel's Servos section, with the GP0 servo's joint dropdown open._

## 3. Calibrate and fix the direction

Click the servo to open its **dialog**. Here you can tune how the servo's angle maps onto the joint:

- **Servo range** — the servo angles you'll use (0–180° by default).
- **Joint range** — the joint values those angles map onto (degrees for a turning joint).
- **Invert** — a tick-box that flips the direction.

Try moving the joint. If the **3-D model turns the opposite way** to what you expect, just tick **Invert** — the model will immediately turn the right way. Invert only flips the *model* to match your real servo; it doesn't change the servo's own wiring.

!!! tip
    Don't worry about getting the ranges perfect now. The defaults (servo 0–180 → the joint's limits) work fine for a first pass, and you can always come back.

## 4. Save two poses

A *pose* is a saved snapshot of where your joints sit. Let's save two so we have something to jump between.

1. Drag the joint's **slider** to a resting position.
2. Save it as a pose named **`home`**.
3. Drag the slider to a reaching position.
4. Save that one as **`reach`**.

You now have two named poses stored in your project.

## 5. Test it with the Poses bench

The **Poses** instrument is a live test bench for your servos — and here's the lovely part: it moves the 3-D model **without any program running**.

1. Open the **Poses** instrument from the instrument dock.
2. **Drag its slider** for the GP0 servo — the 3-D model moves with it.
3. **Press the `home` or `reach` button** — the model glides straight to that pose.

!!! example "📸 Screenshot"
    _Show: the Poses instrument with a per-servo slider and the `home` / `reach` pose buttons, next to the 3-D model in a pose._

So far, only the on-screen model is moving. Let's make the **real servo** move too.

## 6. Drive the real servo

The Poses bench already sends its slider and pose changes to your board — a tiny program just needs to *apply* them to the hardware. Create a new file, paste this in, and press **Run**:

```python
import instruments as inst
from snakie import Servo, Pin, PWM
import time

servo = Servo(PWM(Pin(0)), pin=0)   # your servo on GP0

inst.start()                        # open Snakie's control channel
inst.control.on(
    "servos",
    lambda p: inst.servos_command(p, factory=lambda pin: servo if pin == 0 else inst.servo_on(pin)),
)

print("Listening — drag the Pose bench slider or press a pose.")
while True:
    inst.control.poll()             # apply each slider / pose change to the servo
    time.sleep_ms(20)
```

With this running, go back to the **Poses** instrument and drag the slider or press **`home`** / **`reach`** — the physical servo now follows along, and the 3-D model moves too.

Here's what the program does:

- `inst.start()` opens Snakie's **control channel** — the path the Poses bench uses to send commands.
- `inst.control.poll()`, called every loop, reads any waiting slider/pose change and drives the servo. It never interrupts your program, so the loop keeps running smoothly.
- We import the servo from **`snakie`**, not `servo` — `from snakie import Servo` gives you Snakie's own servo class and avoids clashing with a `servo` module that some board firmwares already ship. (See the [`snakie` module reference](../reference/snakie-module.md).)

!!! note
    The `pin=0` you passed to `Servo` is what lets the moving servo report its position back to Snakie, so the 3-D model mirrors the real hardware.

## Where next

- [Build your first robot](first-robot.md) — if you skipped ahead, this is where the robot and joint come from.
- [Choreograph motion (Motion Studio)](../guides/motion-studio.md) — chain poses into sequences and blend them with sliders.
- [Use the instruments](../guides/instruments.md) — the rest of Snakie's live on-screen tools.
- [The `snakie` module](../reference/snakie-module.md) — the friendly hardware imports: `Servo`, `Buzzer`, `Led`, `Pin`, `PWM`.
