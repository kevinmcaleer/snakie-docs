# robot.yml reference

`robot.yml` is the small text file that ties one Snakie project together. It remembers the board you chose, the parts you placed, the wires between them, and (for a robot) the 3-D model. This page lists every field so you know exactly what each one does.

You do not usually write this file by hand. Snakie writes it for you as you work in the [Board View](../guides/add-and-wire-parts.md) and [Robot View](../guides/robot-view.md). Because it is plain, readable YAML, it sits next to your code and version-controls cleanly.

!!! note "YAML"
    YAML is a simple text format that uses indentation (spaces) to show structure. Lines like `name: My Robot` are a *key* and a *value*.

## Where it lives

`robot.yml` is written in the folder your file browser is open on (the project root). It is the manifest for a **KRF** project ("Kev's Robot File") — a standard folder layout:

```text
my-robot/
├── robot.yml      # this file: wiring + the robot model
├── code/          # your MicroPython source
├── urdf/          # the .urdf model + meshes/
└── stl/           # 3D-printable files
```

## Top-level fields

| Field | Type | What it does |
| --- | --- | --- |
| `name` | text | Optional project name. |
| `description` | text | Optional free-text description. |
| `board` | text | The microcontroller board id (e.g. `pico2w`). |
| `boardX`, `boardY` | number | Where the board box sits on the canvas. |
| `parts` | list | The parts you placed (see below). |
| `connections` | list | The wires between pins (see below). |
| `robot` | section | Optional 3-D robot model (see below). |

!!! tip
    Every field except `parts` and `connections` is optional. An older wiring-only `robot.yml` with no `robot:` section still opens fine.

## `parts` — the placed parts

Each entry is one part dropped onto the canvas.

| Field | Type | What it does |
| --- | --- | --- |
| `id` | text | Unique name for this instance (e.g. `dist1`). Wires point at its pins as `"<id>.<Pin>"`. |
| `lib` | text | The library (folder) the part came from. |
| `part` | text | The part id inside that library. |
| `label` | text | Optional friendly name shown on the canvas. |
| `x`, `y` | number | Where the part sits on the canvas. |
| `rotation` | number | Turn on the breadboard, in degrees: `0`, `90`, `180` or `270`. |

## `connections` — the wires

Each entry is one wire joining two pins. A pin is written `"<partId>.<Pin>"`, or `"board.<Pin>"` for the microcontroller.

| Field | Type | What it does |
| --- | --- | --- |
| `id` | text | Unique id for the wire. |
| `from` | text | One end, e.g. `dist1.SDA`. |
| `to` | text | The other end, e.g. `board.GP4`. |
| `net` | text | `vcc`, `gnd` or `signal` — sets the default colour. |
| `color` | text | Optional colour override (any CSS colour). |

## `robot` — the 3-D model

This optional section links your design to a 3-D robot model. Snakie fills it in as you work in [Robot View](../guides/robot-view.md); to learn what it is *for*, see the [Robot View explanation](../explanation/robot-view.md).

| Field | Type | What it does |
| --- | --- | --- |
| `version` | number | The KRF schema version (currently `1`). |
| `urdf` | text | Path to the `.urdf` model file, relative to the project. |
| `baseLink` | text | The link chosen as the base (root) of the robot — everything hangs off it. |
| `servoJointMap` | list | Links a servo pin to a URDF joint, with angle calibration (see below). |
| `joints` | map | Per-joint `min`/`max` limit overrides. |
| `defaultPose` | map | Joint values applied when the model loads (degrees or mm). |
| `poses` | list | Saved named poses, each with a `name` and `values`. |
| `timeline` | section | A choreographed motion clip (see below). |
| `sequences` | list | Pose-to-pose sequences (walk cycles) built from saved poses (see below). |
| `controls` | list | Puppet controls — sliders that blend saved poses (see below). |
| `mirror` | list | Left↔right joint pairs for symmetric movement. |

### A `servoJointMap` entry

Tells Snakie which joint a servo drives, and how the servo's angle maps onto the joint.

| Field | Type | What it does |
| --- | --- | --- |
| `pin` | text | The board pin the servo is on (e.g. `GP0`). |
| `joint` | text | The URDF joint this servo moves. |
| `servoMin`, `servoMax` | number | Servo input range in degrees (default `0`…`180`). |
| `jointMin`, `jointMax` | number | Joint range it maps onto (degrees, or mm for a sliding joint). Both required. |
| `invert` | true/false | Reverse the mapping (servo min → joint max). |

### A `timeline` section

| Field | Type | What it does |
| --- | --- | --- |
| `duration` | number | Loop length in seconds. |
| `easing` | text | `linear` or `easeInOut` (how it moves between keyframes). |
| `loop` | true/false | Repeat the motion. |
| `fps` | number | Preview/export sample rate (default `20`). |
| `tracks` | list | One track per joint, each with `joint` and a list of `keys` (`{ t, value }`). |

### A `sequences` entry

A pose-to-pose sequence — a walk cycle or gesture chained from saved poses. (A `timeline` keyframes each joint by hand; a sequence just names the poses to move through.)

| Field | Type | What it does |
| --- | --- | --- |
| `name` | text | The sequence name. |
| `steps` | list | The ordered steps (see below). |
| `loop` | true/false | Repeat — the last step eases back to the first. |
| `fps` | number | Preview/export sample rate (default `20`). |

Each **step** names a saved pose and how long to ease into the *next* one:

| Field | Type | What it does |
| --- | --- | --- |
| `pose` | text | The saved pose this step is on (a `poses` entry's `name`). |
| `duration` | number | Seconds to transition to the next step's pose. |
| `easing` | text | `linear` or `easeInOut` (default `easeInOut`). |

### A `controls` entry

A puppet control — a named slider that smoothly blends two or more saved poses (e.g. frown → neutral → smile, or a stride).

| Field | Type | What it does |
| --- | --- | --- |
| `id` | text | Unique id for the control within the project. |
| `name` | text | The slider's label (e.g. `Look up / Down`). |
| `poses` | list | The saved-pose names to blend, in order (two or more). Dragging the slider 0 → 1 moves through them. |

## Annotated example

```yaml
name: Line Follower          # project name (optional)
board: pico2w                # the microcontroller
boardX: 40
boardY: 30
parts:
  - id: dist1                # unique instance id
    lib: snakie-basics       # library it came from
    part: vl53l0x            # part id in that library
    label: Distance          # friendly name (optional)
    x: 320
    y: 30
connections:
  - id: dist1.SDA__board.GP4
    from: dist1.SDA          # "<partId>.<Pin>"
    to: board.GP4            # "board.<Pin>" is the MCU
    net: signal              # vcc | gnd | signal
    color: '#4ea1ff'         # optional colour

robot:                       # optional 3-D model
  version: 1
  urdf: urdf/robot.urdf
  servoJointMap:
    - pin: GP0
      joint: shoulder
      servoMin: 0
      servoMax: 180
      jointMin: -90          # joint range (deg for a rotating joint)
      jointMax: 90
      invert: false
  defaultPose:
    shoulder: 0              # applied on load
  poses:
    - name: home
      values: { shoulder: 0 }
    - name: wave
      values: { shoulder: 60 }
  sequences:
    - name: greet          # move home -> wave -> home, looping
      loop: true
      steps:
        - { pose: home, duration: 0.4 }
        - { pose: wave, duration: 0.4 }
  controls:
    - id: ctl-1
      name: Wave amount    # a slider that blends home <-> wave
      poses: [home, wave]
```

!!! warning
    Field names are case-sensitive. Use `servoMin`, not `servomin`. If a field is malformed, Snakie safely ignores it rather than refusing to open the file — but the setting will not take effect.

## See also

- [Add and wire parts](../guides/add-and-wire-parts.md) — build the `parts` and `connections` on the canvas.
- [Robot View](../guides/robot-view.md) — where the `robot:` section is created.
- [Robot View, explained](../explanation/robot-view.md) — the ideas behind poses, joints and the timeline.
