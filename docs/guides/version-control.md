# Save your work with Git

This page shows you how to save snapshots of your project with Snakie's built-in Git panel, so you can always go back if something breaks.

## What is Git?

Git is a *version control* system — a tool that saves snapshots of your project as you work. Each snapshot is called a **commit**. If a change goes wrong, you can look back at what you had before and get it back. Think of it like a save point in a game.

!!! tip "Why bother?"
    Every maker breaks their code sometimes. Git means a broken experiment is never scary — your last working version is always safe.

## Open the Source Control panel

Snakie has a Source Control panel, much like the one in VS Code.

1. Click **Source Control** in the activity bar down the side of the window.
2. The panel follows the folder you have open in **Files**. If you have not opened a folder yet, open one first (see [Browse and manage your files](./manage-files.md)).
3. If that folder is not a Git project yet, use the option to start (initialise) one. That creates a hidden history for the folder.

!!! example "📸 Screenshot"
    _Show: the Source Control panel with the branch name at the top and a list of changed files._

## Make your first commit

Once you have edited and saved a file, Snakie lists what has changed. Files are grouped so they are easy to read:

| Group | What it means |
| --- | --- |
| **Changes** | Files you have edited since the last snapshot. |
| **Untracked** | Brand-new files Git has not seen before. |
| **Staged Changes** | Files you have picked to go into the next commit. |

To save a snapshot:

1. Click a file to see its **diff** — a coloured view where green lines were added and red lines were removed.
2. (Optional) Use the small **stage** (＋) button to choose exactly which files go in, or skip this and let the commit include everything.
3. Type a short **message** in the box saying what you changed, like `got the LED blinking`.
4. Click **Commit**.

That's it — your snapshot is saved.

!!! tip "Good commit messages"
    Write what you did, not how. `add button to start the robot` is perfect. Commit **small and often**.

## Undo a change

Made a mess in one file? Each changed file has a **discard** (⨯) button. It puts that file back to how it was at your last commit. This is exactly what version control is for.

!!! warning
    Discarding throws away your latest edits to that file for good. Only use it when you are sure you want the older version back.

## Branches, Push and Pull

A **branch** lets you try a new idea without touching your working code. Use the branch dropdown at the top of the panel to switch branches or make a new one.

If your project is linked to an online copy (like on GitHub):

- **Push** (↑) sends your commits up to the online copy.
- **Pull** (↓) brings down changes from there.
- The small **↑ / ↓ numbers** show how many commits you are ahead of or behind the online copy.

!!! note
    Snakie uses the `git` already installed on your computer, and everything runs on your own machine. Files stored **on your board** are not part of Git — keep your source code in a local folder so every change gets saved.

Now go and build something bold. Git has your back.
