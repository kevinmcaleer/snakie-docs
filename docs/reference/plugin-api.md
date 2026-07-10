# Plugin API

This page lists what a Snakie plugin can do. A plugin is a small **Python** program that adds new powers to the editor, like a command button or a live code checker.

Want a step-by-step walkthrough instead? See [Write a plugin](../guides/write-a-plugin.md). This page is the quick reference you come back to.

## How a plugin works

Snakie starts a little Python helper in the background. That helper finds your plugins, loads them, and lets them talk to the editor. You write normal Python and import the `snakie` toolkit (the "SDK", short for *software development kit* — a set of ready-made helpers).

```python
from snakie import plugin, Context, message, edit

@plugin.command("hello", "Say hello")
def hello(ctx: Context):
    return message("info", f"Editing {ctx.file.name}")
```

!!! note
    Plugins need **Python 3** on your computer. If Snakie can't find it, the **Plugins** view shows a friendly prompt instead, and the rest of the app keeps working.

## Where plugins live

Snakie looks for plugins in three places:

| Place | Example |
| --- | --- |
| A single file in your plugins folder | `~/.snakie/plugins/my_plugin.py` |
| A folder (package) in your plugins folder | `~/.snakie/plugins/my_plugin/__init__.py` |
| An installed package that declares a `snakie.plugins` entry point | in the package's `pyproject.toml` |

Snakie also loads its own bundled example plugins, so the Plugins view works right away.

## Register things

You add features with **decorators** (a decorator is the `@` line written just above a function).

| Decorator | What it registers | Handler shape |
| --- | --- | --- |
| `@plugin.command(id, title)` | A command with a **Run** button in the Plugins view. `id` is unique; `title` is what you see. | `(ctx: Context)` |
| `@plugin.linter(name)` | A **linter** — a checker that runs as you type and draws squiggles under problems. | `(ctx: Context) -> list of diagnostics` |

## What your handler receives: `Context`

Every command and linter is handed a `Context` describing the current editor state.

| Field | Meaning |
| --- | --- |
| `ctx.file.path` | Full path of the active file |
| `ctx.file.name` | Just the file name |
| `ctx.file.source` | Where the file is: `"local"` (your computer) or `"device"` (the board) |
| `ctx.file.content` | The file's text |
| `ctx.selection` | The highlighted text, or `None`. Has `start_line`, `start_column`, `end_line`, `end_column`, `text` |

## What your handler returns

Return one helper, a list of them, or `None` (nothing happens). A plain string is treated as an info message.

| Helper | What it does |
| --- | --- |
| `message(level, text)` | Shows a notice in the Plugins panel. `level` is `"info"`, `"warning"` or `"error"`. |
| `edit(new_content)` | Replaces the whole active file with `new_content`. The file is marked unsaved, so save as usual. |
| `status(text, *, tooltip=None, href=None, priority=0)` | Shows a message in the status bar at the bottom. `href` makes it a clickable link; when two plugins post, the higher `priority` wins. |
| `diagnostic(line, message, *, severity="warning", column=None, end_line=None, end_column=None, source="snakie", fixes=None)` | A problem marker. From a command it appears as a notice; from a linter it becomes an editor squiggle. |
| `fix(title, new_text, *, line=None, column=None, end_line=None, end_column=None)` | A quick-fix (the lightbulb suggestion) attached to a diagnostic. |

!!! note "Coordinates start at 1"
    Every line and column number is **1-based** — the first line is line `1`, not `0`.

## Linters and quick-fixes

A linter runs on its own while you edit — you don't press anything.

```python
import re
from snakie import plugin, Context, diagnostic, fix

@plugin.linter("todo-finder")
def lint(ctx: Context):
    out = []
    for i, line in enumerate(ctx.file.content.splitlines()):
        if "# TODO" in line:
            out.append(diagnostic(i + 1, "Unfinished TODO", severity="info"))
    return out
```

How it behaves:

- Snakie waits about **400 milliseconds** after you stop typing, then runs your linter. It never runs on every keystroke.
- Each diagnostic becomes a coloured squiggle in the editor.
- A diagnostic with `fixes` also shows a **lightbulb**; clicking a fix edits the file for you.
- If Python isn't available, linting quietly does nothing.

!!! tip
    A `fix` always targets a range. Leave the range out and it replaces the diagnostic's own spot. There is no "replace the whole file" fix, so aim at the exact text you flagged.

## Running and reloading

1. Open the **Plugins** view from the activity bar (the puzzle-piece icon).
2. Open the file you want to act on — commands run against the **active file**.
3. Press **Run** next to a command.

Added or changed a plugin? Press **Reload** in the Plugins view to pick it up.

!!! warning "Plugins run real code"
    A plugin is ordinary Python that runs as you, with your permissions. Only install plugins you trust. Keep commands quick — slow work blocks the plugin helper. Anything you `print` goes to Snakie's log, so it won't break the connection.

Ready to build one? Head to [Write a plugin](../guides/write-a-plugin.md).

!!! example "📸 Screenshot"
    _Show: the Plugins view listing a plugin with its commands and Run buttons, next to an open editor file._
