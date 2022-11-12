---
title: ahkpm version
description: Bumps the version in `ahkpm.json`.
lead: Bumps the version in `ahkpm.json`.
menu:
  docs:
    parent: "commands"
toc: true
---
## Synopsis

Bumps the version in `ahkpm.json`, making version updates easier than manually
working out the version number and editing the file.

`ahkpm version` should be called with a valid semantic version (such as `1.2.3`),
or with one of `major`, `minor`, `patch`. In the second case, the existing 
version will be incremented by 1 in the specified field.

For example, if you are on version `1.2.3` and run `ahkpm version major`,
your `ahkpm.json` will be updated to `2.0.0`.

Running `ahkpm version 3.3.3` will update `ahkpm.json` to have exactly `3.3.3`.

## Usage

```text
ahkpm version [<newversion> | major | minor | patch] [flags]
```

## Examples

```text
ahkpm version major
```

## Options

- `--message`, `-m`: Custom git commit and tag message
