# parts.yml reference

Every part in the Snakie Parts Library is a folder with one `parts.yml` file inside it. That file describes the part — its name, its pins, and how to draw it. This page lists every field you can put in it.

A *part* is a piece of hardware, like a sensor or a motor driver. *YAML* is a simple text format that uses `key: value` lines.

!!! tip "You rarely type this by hand"
    The visual **Part Editor** writes `parts.yml` for you. This page is here for when you want to read, tweak, or understand a part file. To make a part step by step, see [Make a part](../guides/make-a-part.md). For the bigger picture, see [The Parts Library](../explanation/parts-library.md).

Only `id`, `name`, and at least one `headers` entry are required. Everything else is optional.

!!! example "📸 Screenshot"
    _Show: a `parts.yml` file open in the editor next to the part it draws in the Board View._

## Catalogue fields (the header)

These describe the part in the library and let people search for it.

| Field | What it is |
| ----- | ---------- |
| `id` | A unique name inside its library. It is also the part's folder name (e.g. `vl53l0x`). **Required.** |
| `name` | The friendly display name (e.g. `VL53L0X ToF`). **Required.** |
| `description` | One short line about the part. |
| `manufacturer` | Who makes it (e.g. `Pimoroni`, `Raspberry Pi`). |
| `partNumber` | The maker's part number (e.g. `SC0918`). |
| `family` | The category (e.g. `Sensor`, `Microcontroller`, `Motor Driver`). |
| `tags` | A list of words to help searching (e.g. `[i2c, distance]`). |
| `package` | How it mounts: `THT` (through-hole) or `SMD` (surface-mount). |
| `pinSpacing` | The gap between pins in millimetres. The common header value is `2.54`. |
| `voltage` | Working voltage as free text (e.g. `3.3V`). |
| `properties` | Your own extra spec rows as `key: value` pairs. |
| `version` | The part's own version number, like `1.0.0`. Used to spot updates. |

## Shape and size fields

These control how the board is drawn.

| Field | What it is |
| ----- | ---------- |
| `dimensions` | The real size in millimetres, written `{ width: 25, height: 11 }`. |
| `aspect` | Width divided by height — sets the drawn proportions. |
| `pcbColor` | The board colour (any CSS colour, e.g. `'#101820'`). |
| `polygon` | An outline for non-rectangular boards: a list of `{ x, y }` points from `0` to `1`. Leave it out for a plain rounded rectangle. |
| `shape` | The outline kind: `rect` (default) or `polygon`. |

## Pins

Pins are grouped into **headers**. Each header is a row of pins along one edge.

```yaml
headers:
  - edge: bottom          # left | right | top | bottom
    pins:
      - { name: VIN, type: pwr, number: 1 }
      - { name: SDA, type: io,  number: 3, gpio: 4, capabilities: [i2c, digital] }
```

Each pin can have these fields:

| Pin field | What it is |
| --------- | ---------- |
| `name` | The pin's signal name (e.g. `GP0`, `SDA`, `VBUS`). **Required.** |
| `label` | Different text to print, if it differs from `name`. |
| `type` | The pin's job: `pwr` (power), `gnd` (ground), `io` (a usable GPIO), or `other`. |
| `number` | The physical pin number printed on the board, if any. |
| `gpio` | The GPIO number this pin uses. Snakie matches it to `Pin(n)` in your code. `io` pins only. |
| `capabilities` | What an `io` pin can do (a list): `digital`, `pwm`, `adc`, `i2c`, `spi`, `uart`. |
| `shape` | How the pad looks: `round`, `square`, `castellated`, or `header`. |
| `x` / `y` | Exact spot on the board, from `0` to `1`. Set by the editor's free placement. |

!!! note "io pins carry the extras"
    `gpio` and `capabilities` only matter on `io` pins. Snakie ignores them on power and ground pins.

## Holes, shapes, and labels

| Field | What it is |
| ----- | ---------- |
| `mountingHoles` | Screw holes. Each is `{ x, y, diameter }` — position `0`–`1` and diameter in mm. |
| `shapes` | Drawn components: a list of `rect`, `circle`, or `polygon` shapes with `fill`, `stroke`, and a position. |
| `labels` | Free text placed on the board: `{ text, x, y }`, with optional `fontSize`. |

## Assets and drivers

| Field | What it is |
| ----- | ---------- |
| `image` | The filename of a board photo in the same folder (e.g. `image.png`). |
| `help` | The filename of a small Markdown help file (e.g. `help.md`) shown when the part is used. |
| `drivers` | MicroPython files the part needs on the board. Each has `source`, `target`, and an optional `label`. |
| `mesh` | A 3-D model file (STL) in the folder for the [Robot View](../explanation/parts-library.md), e.g. `model.stl`. |
| `meshUnits` | The mesh's units so it loads at the right size: `mm` or `m`. |

## A full annotated example

```yaml
id: vl53l0x                       # unique; also the folder name
name: VL53L0X ToF                 # display name
description: Time-of-flight distance sensor
manufacturer: STMicroelectronics
family: Sensor
partNumber: VL53L0X
tags: [i2c, distance, tof]
package: SMD                      # THT | SMD
pinSpacing: 2.54                  # header gap, millimetres
voltage: 2.8–5V
version: 1.0.0                    # this part's version

# --- shape & size ---
pcbColor: '#101820'
aspect: 1.3
dimensions: { width: 25, height: 11 }

# --- pins ---
headers:
  - edge: bottom                  # left | right | top | bottom
    pins:
      - { name: VIN, type: pwr, number: 1 }
      - { name: GND, type: gnd, number: 2 }
      - { name: SCL, type: io, number: 3, gpio: 5, capabilities: [i2c, digital], shape: castellated }
      - { name: SDA, type: io, number: 4, gpio: 4, capabilities: [i2c, digital], shape: castellated }

# --- holes, shapes, labels ---
mountingHoles:
  - { x: 0.1, y: 0.5, diameter: 2 }
labels:
  - { text: XSHUT, x: 0.8, y: 0.5 }

# --- assets & drivers ---
image: image.png                  # a photo in this folder
help: help.md                     # optional help notes
drivers:
  - { source: github:org/repo/vl53l0x.py, target: lib, label: VL53L0X driver }
```

!!! warning "One typo won't break everything"
    If a `parts.yml` is malformed, Snakie skips just that part and still loads the rest of the library. Check spelling and indentation if a part goes missing.

## See also

- [Make a part](../guides/make-a-part.md) — build one visually, step by step.
- [The Parts Library](../explanation/parts-library.md) — how libraries and sharing work.
