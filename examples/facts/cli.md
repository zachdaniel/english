# CLI conventions

The program is invoked as `todo <command> [args...]`.

- Success exits with status `0`; any user-facing error exits non-zero.
- Normal output goes to stdout. Errors go to stderr, prefixed with `error: `.
- The usage message lists every command in this form:

  ```
  usage: todo <command>

    add <text>   add a new task
    list         list all tasks
    done <id>    mark a task as done
  ```

- Task ids are shown to the user as `#<id>`, e.g. `#3`.
- A done task is shown with `[x]` and a not-done task with `[ ]`, so a listed
  line looks like `#3 [ ] buy milk`.
