---
title: ahkpm include
description: Gets the "Include" statement needed to use a package
lead: Gets the "Include" statement needed to use a package
menu:
  docs:
    parent: "commands"
toc: true
---
## Synopsis

Given the name of an installed package, this command will print the "Include"
statement needed to use the package in an AutoHotkey script. If the package does
not provide that information, or if the package is not installed, it will say
so.

Including the `-f` or `--file` flag means that rather than printing the
"Include" statement, it will be prepended to the top of the specified file.

## Usage

```text
ahkpm include <package> [flags]
```

## Examples

```text
ahkpm include gh:joshuacc/fake-package
ahkpm include --file my-script.ahk gh:joshuacc/fake-package
```

## Options

- `--file`, `-f`: The file to add the "Include" statement to
