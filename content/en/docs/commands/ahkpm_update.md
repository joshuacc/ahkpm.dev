---
title: ahkpm update
lead: "Update package(s) to the latest version allowed by ahkpm.json"
menu:
  docs:
    parent: "commands"
toc: true
---
## Synopsis

Updates package(s) to the latest version allowed by ahkpm.json.

For example, if you have a dependency on `github.com/user/repo` with version
`branch:main`, running `ahkpm update github.com/user/repo` will update the
package to the latest commit on the main branch.

You may also use package name shorthands, such as `gh:user/repo`.

```
ahkpm update <packageName>... [flags]
```

## Examples

```
ahkpm update github.com/joshuacc/mock-ahkpm-package-a
```

## Options

```
  -h, --help   help for update
```

## See also:

* [ahkpm](ahkpm.md)	 - The package manager for AutoHotkey

