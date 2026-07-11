# The snakie module

`snakie` is a small on-board module you import the **hardware** classes from. It gives you one clear, friendly name for the things you *drive* — servos, buzzers, LEDs — so your board code reads well and never clashes with someone else's module.

```python
from snakie import Servo, Buzzer, Led, Pin, PWM
```

For a walkthrough of using these to pose a robot, see [Bind servos and animate](../guides/motion-studio.md).

## What it is

`snakie` simply **re-exports** the hardware classes from Snakie's on-board runtime, `instruments`. So `snakie.Servo` *is* `instruments.Servo` — the very same object, just under a tidier name. Nothing is removed: `import instruments` still works exactly as before.

The split is by job:

| Import from | For |
| --- | --- |
| `snakie` | The **hardware** you wire up — `Servo`, `Buzzer`, `Led`, and the raw `Pin` / `PWM`. |
| `instruments` | The **measurement** helpers that *watch* your program — `scope()`, `meter()`, `plot()` (see the [telemetry API](telemetry-api.md)). |

!!! warning "Why not `from servo import Servo`?"
    Some MicroPython builds (for example Pimoroni's) ship their **own** frozen `servo` module, whose `Servo(pin)` takes a pin *number*, not a `PWM`. A frozen module wins over a file on the board, so `from servo import Servo` can quietly grab the wrong class — you then see `TypeError: can't convert PWM to int`. Importing from **`snakie`** sidesteps the clash entirely.

## Getting it onto your board

`snakie.py` is installed to `/lib/snakie.py` **automatically**, right next to `instruments.py`, whenever you install or update the on-board library — the one-click banner in the app does both (see the [Instruments guide](../guides/instruments.md#1-install-the-library-one-click)). If you ever update Snakie, take the "library update" banner so the board picks up the latest copy.

## Servo

Drives a hobby servo (SG90 and friends). Hand it a `PWM` you made yourself — the code then reads *pin → PWM → Servo*:

```python
from snakie import Servo, Pin, PWM

base = Servo(PWM(Pin(0)), pin=0)   # a servo on GP0
base.angle(90)                     # centre it
```

`Servo(pwm=None, freq=50, min_us=500, max_us=2500, pin=None)`

| Method | What it does |
| --- | --- |
| `angle(deg)` | Move to `deg` (0–180). |
| `set_pin(n)` | (Re)attach the PWM on GPIO `n` at 50 Hz. |
| `detach()` | Release the servo — stops holding torque (quells buzz at an end stop). |

!!! tip "Pass `pin=` so the model follows"
    Giving `pin=n` makes every `angle()` also emit `SNK SERVO <pin> <deg>` telemetry. Snakie maps that to the joint the servo is [bound to](robot-yml.md#a-servojointmap-entry), so the **3-D model and the Poses bench move with the real servo**. You can also pass a bare pin (`Servo(pin=0)`) and Snakie builds the `PWM` for you.

## Buzzer

Plays tones on a piezo buzzer.

```python
from snakie import Buzzer, Pin, PWM

beeper = Buzzer(PWM(Pin(5)))
beeper.tone(880, 120)              # 880 Hz for 120 ms
```

`Buzzer(pwm=None)`

| Method | What it does |
| --- | --- |
| `tone(freq, ms)` | Play a single tone (`freq` Hz for `ms` milliseconds). |
| `play_seq([(freq, ms), ...])` | Play a list of notes in order (a `freq` of `0` is a silent rest). |
| `stop()` | Silence any current tone. |
| `set_volume(level)` | Set loudness from `0`…`1`. |
| `set_pin(n)` | (Re)target the buzzer's GPIO. |

## Led

Drives a plain, dimmable, or RGB LED.

```python
from snakie import Led

status = Led(pin=25)               # the Pico's on-board LED
status.set(True)
status.pwm(0.3)                    # 30 % brightness
```

`Led(pin=None, pwm=None, rgb=None)`

| Method | What it does |
| --- | --- |
| `set(on)` | Turn the LED on (`True`) or off (`False`). |
| `pwm(level)` | Dim it — brightness `0`…`1`. |
| `rgb(r, g, b)` | Set three colour channels, each `0`…`255`. |

## Pin and PWM

`Pin` and `PWM` are re-exported straight from MicroPython's `machine`, so you can build your own and pass them in:

```python
from snakie import PWM, Pin, Servo

signal = PWM(Pin(0))               # the GP0 signal
base = Servo(signal, pin=0)
```

## See also

- [Use the instruments](../guides/instruments.md) — the reading instruments and the **Poses bench**.
- [Bind servos and animate](../guides/motion-studio.md) — connect a servo to a joint and drive it live.
- [Instrument telemetry API](telemetry-api.md) — `scope()`, `meter()`, `plot()` and the readers.
- [robot.yml reference](robot-yml.md) — where a servo's pin ↔ joint calibration is stored.
