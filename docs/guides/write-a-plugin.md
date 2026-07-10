# Write a plugin

Snakie can grow new powers, and *you* can be the one who adds them. A **plugin** is a small piece of Python code that teaches Snakie a new trick. This page shows you how to build your very first one.

## What is a plugin?

A plugin is a tiny **Python program** (Python is the coding language Snakie's plugins are written in) that adds a new command or a new checker to the editor.

Snakie starts a little helper called the **plugin host**, finds your plugin, and lets you run it against the file you're editing. Your plugin can:

- show a **message** (a small notice), or
- **edit** the open file (change its text), or
- add **squiggles** (coloured underlines that point out problems), sometimes with a one-click fix.

!!! note "You need Python"
    Plugins run in Python, so you need **Python 3** installed on your computer. If Snakie can't find it, the **Plugins** view shows you a friendly message telling you what to do. Snakie also ships with a copy of the plugin kit built in, so the Plugins view works right away.

## Where plugins live

Snakie looks for your plugins in a special folder in your home directory:

```text
~/.snakie/plugins/
```

You can write a plugin in two shapes:

| Shape | Where the file goes |
| --- | --- |
| Single file | `~/.snakie/plugins/my_plugin.py` |
| Folder (package) | `~/.snakie/plugins/my_plugin/__init__.py` |

Both work the same way. A folder is handy once your plugin grows past one file.

## Make your first plugin

Let's build a plugin with two commands: one that says hello, and one that shouts your file in UPPERCASE.

1. Create the folder `~/.snakie/plugins/my_plugin/`.
2. Inside it, make a file called `__init__.py`.
3. Paste in this code:

    ```python
    from snakie import plugin, Context, message, edit

    @plugin.command("hello", "Say hello")
    def hello(ctx: Context):
        # ctx.file has .path, .name, .source and .content
        return message("info", f"Editing {ctx.file.name}")

    @plugin.command("upper", "Uppercase the file")
    def upper(ctx: Context):
        return edit(ctx.file.content.upper())
    ```

Here's what the pieces mean:

- `@plugin.command("hello", "Say hello")` registers a command. The first word is its **id** (must be unique). The second is the **title** you'll see in Snakie.
- `ctx` (short for *context*) is what your command is given to work with. `ctx.file.name` is the file's name, and `ctx.file.content` is all its text.
- `message("info", ...)` shows a small notice. `edit(...)` replaces the file's text with something new.

!!! tip
    There's a ready-made copy of this in the Snakie repo at `examples/plugins/hello/__init__.py`. Copy it as a starting point.

## Run your plugin in Snakie

1. Open the **Plugins** view from the activity bar (the puzzle-piece icon on the side).
2. Open the file you want to change. Commands always act on the file you're looking at.
3. Press **Run** next to your command. A `message` shows up as a notice; an `edit` changes your open file (then just save it like normal).

!!! note "Just added or changed a plugin?"
    Press **Reload** in the Plugins view. That restarts the helper and picks up your new code.

## Checkers that run as you type

A **linter** is a checker that runs on its own while you type and draws squiggles under problems, sometimes with a lightbulb quick-fix. You register one with `@plugin.linter(...)` instead of `@plugin.command(...)`. The example plugin `examples/plugins/lint_demo/__init__.py` flags trailing spaces and `# TODO` notes, and is a great next step.

## Stay safe

!!! warning "Only install plugins you trust"
    A plugin is real Python code that runs **as you**, so it can do anything you can do on your computer. Only add plugins you wrote or that come from someone you trust.

## Where to go next

You've made a plugin! To see the full list of things a plugin can do — every command, checker, message level, and quick-fix helper — read the [Plugin API reference](../reference/plugin-api.md).

!!! example "📸 Screenshot"
    _Show: the Plugins view with a custom plugin listed and its Run button highlighted._
