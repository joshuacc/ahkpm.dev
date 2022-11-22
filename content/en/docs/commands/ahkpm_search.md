---
title: ahkpm search
description: Searches GitHub for packages matching the specified query
lead: Searches GitHub for packages matching the specified query
menu:
  docs:
    parent: "commands"
toc: true
---
## Synopsis

Searches GitHub for any ahkpm packages which match the specified query. The
search is limited to GitHub repositories in the `ahkpm-package` topic.

So `ahkpm search testing` will return any GitHub repositories that both match
"testing" and are tagged with `ahkpm-package`.

If no search terms are specified, it will provide an unfiltered list of ahkpm
packages.

## Usage

```text
ahkpm search <searchTerm>...
```

