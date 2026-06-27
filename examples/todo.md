# Todo

A small command-line todo list, run as an escript called `todo`. Its behavior is
grounded by two other files in this folder: [how tasks are stored](storage.md)
and the [CLI conventions](cli.md) it follows.

## Adding a task

When the user runs `todo add "buy milk"`, append a new task with that text to
the store. New tasks start out not done. Print the id of the task that was added.

## Listing tasks

When the user runs `todo list`, print every task, one per line, in the order
they were added. Show its id, whether it is done, and its text.

## Completing a task

When the user runs `todo done <id>`, mark the task with that id as done. If no
task has that id, tell the user and exit with a non-zero status.

## Anything else

For any other command, or no command at all, print a short usage message
following the CLI conventions and exit with a non-zero status.
