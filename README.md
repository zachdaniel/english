# english

This is a joke, I vibe coded it because I thought it was funny.

---

A programming language whose compiler is Claude.

You write programs in **plain English**: just a folder of markdown files (or a
single one). The "compile" step is one line — it hands the markdown to Claude's
built-in `/goal` with a prompt:

```sh
claude -p "/goal <compile the markdown at PATH into code, then link the prose to it...>"
```

Claude reads the prose, follows the markdown links between the files to the
**facts** that ground them, and emits real source code in whatever target
language the program asked for — then edits the markdown in place, linking each
line of prose to the code that realizes it. The source files become a **semantic
graph** linking prose → facts → generated code, in both directions.

The entire toolchain is one bash script. The intelligence is Claude.

## Install

```sh
git clone <this repo> && cd english
./bin/english install          # symlinks the script onto your PATH (~/.local/bin)
```

## Use

```sh
english build examples/todo.md     # compile a single file
english build examples/            # compile a whole folder of markdown
english build                      # compile everything under .
```

## A program

A program is just a folder of markdown. The prose is the program; ordinary
markdown links point to the other `.md` files in the folder that ground its
behavior — there's nothing special about those files, they're just markdown that
something links to. Optional YAML frontmatter gives build hints — `target` and
`out` — but both are inferred if you leave them out.

```markdown
---
target: elixir
out: build/
---

# Todo

A small command-line todo list. Its behavior is grounded by
[how tasks are stored](storage.md) and the [CLI conventions](cli.md).

When the user runs `todo add "buy milk"`, append a new task with that text...
```

## What you get

For `todo.md`, compilation produces:

- **`build/`** — real, runnable source in the target language. Each generated
  file carries a header comment linking back to the program and the facts it
  implements.
- **Your markdown, annotated in place** — the compiler edits the original `.md`
  files, leaving the prose intact but linking each phrase to the code that
  realizes it (`... appends a [new task](build/lib/todo/store.ex) ...`). The
  source files themselves become the semantic graph: trace any line of generated
  code back to the English that asked for it, and any sentence of English forward
  to the code that satisfies it. Re-running the build updates the links in place.

## How it works

There is only `bin/english`. Its `build` command resolves the path, builds a
prompt describing the compile contract (read corpus → follow links → generate
code → link the prose to it in place), and runs `claude -p "/goal <prompt>"`.
That's the whole compiler. `/goal` is Claude Code's built-in "work toward this
until it's done" command; we just give it the program as the goal.

`target` can be anything — `elixir`, `python`, `typescript`, a shell script.
The language English compiles *to* is up to each program.
