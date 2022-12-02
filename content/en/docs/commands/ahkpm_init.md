---
title: ahkpm init
description: Interactively create an ahkpm.json file in the current directory
lead: Interactively create an ahkpm.json file in the current directory
menu:
  docs:
    parent: "commands"
toc: true
---
## Synopsis

Interactively creates an ahkpm.json file in the current directory so that you
can install AutoHotkey packages and use them within your AutoHotkey scripts.

Running `ahkpm init` will prompt you for information about your package and
create an `ahkpm.json` file in the current directory.

## Usage

```text
ahkpm init [flags]
```

## Options

- `--defaults`, `-d`: Create an ahkpm.json file with default values. No prompts.
