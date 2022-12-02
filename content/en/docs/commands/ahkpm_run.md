---
title: ahkpm run
description: Run user-defined scripts from ahkpm.json
lead: Run user-defined scripts from ahkpm.json
menu:
  docs:
    parent: "commands"
toc: true
---
## Synopsis

This command allows running user-defined scripts located in `ahkpm.json` within
the `scripts` object.

For example, if there is a script `"greet": "echo Hi!"`, then running
`ahkpm run greet` would execute `echo Hi!`, resulting in the message `Hi!`
being printed to the terminal.

ahkpm scripts are useful for defining common commands for things like testing,
running builds, and starting programs.

## Usage

```text
ahkpm run <script>
```

## Examples

```text
ahkpm run build\nahkpm run test
```

