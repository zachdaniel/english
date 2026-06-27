# How tasks are stored

Tasks live in a single newline-delimited JSON file at `~/.todo/tasks.json`.
Create the directory and file on first use if they do not exist.

Each task is a JSON object on its own line:

- `id` — a positive integer, assigned sequentially starting at 1. Ids are never
  reused, even after a task is deleted. The next id is one greater than the
  largest id ever seen, not the current count.
- `text` — the task description, exactly as the user typed it.
- `done` — a boolean, `false` when the task is created.

Reading the store means reading every line and parsing each as a task. Writing
the store means rewriting the whole file. The store is the single source of
truth; never cache it across commands.
