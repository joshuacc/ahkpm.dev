---
title: ahkpm
description: The root command for the ahkpm CLI
lead: The root command for the ahkpm CLI
menu:
  docs:
    parent: "commands"
toc: true
---
## Synopsis

ahkpm is a package manager for AutoHotkey. This root command provides access
to all of the subcommands which install, update, and manage your AutoHotkey
packages.

## Usage

```text
ahkpm [command]
ahkpm [flags]
```

## Available subcommands

- `cache`: Manipulates the packages cache
- `include`: Gets the "Include" statement needed to use a package
- `init`: Interactively create an ahkpm.json file in the current directory
- `install`: Installs specified package(s). If none, reinstalls all packages in ahkpm.json.
- `list`: List all installed packages and their versions
- `run`: Run user-defined scripts from ahkpm.json
- `search`: Searches GitHub for packages matching the specified query
- `test`: Runs the `test` script from ahkpm.json if it exists
- `update`: Update package(s) to the latest version allowed by ahkpm.json
- `version`: Bumps the version in `ahkpm.json`.

## Options

- `--ahk-version`, `-a`: Display the version of AutoHotkey
- `--version`, `-v`: Display the version of ahkpm
