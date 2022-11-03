---
title: "Introduction"
description: "An introduction to using ahkpm"
lead: >
  AutoHotkey is a powerful tool for scripting automations on Windows, but
  manually managing dependencies for your scripts is painful.
  ahkpm brings modern package management to AutoHotkey,
  making it easier than ever to automate away the drudgery.
date: 2020-10-06T08:48:57+00:00
lastmod: 2020-10-06T08:48:57+00:00
draft: false
images: []
menu:
  docs:
    parent: "overview"
weight: 100
toc: true
---

## Installation

To install ahkpm:

1. Go to the [releases][releases] page and find the most recent version.
2. Download the `ahkpm-{version}.msi` file.
3. Open it on your Windows machine to launch the ahkpm installer.

## Basic usage

1. Open the command line and navigate to the directory which will contain your AutoHotKey script.
2. Run `ahkpm init` and answer the prompts to create an `ahkpm.json` file
3. Run `ahkpm install <package>@<version>`
   - The package can be any github repository in the form: `github.com/user/repo`
   - The version can be any of the following:
     - A valid [semantic version][semver] such as `1.0.0`
     - The prefix `tag:` followed by the name of a tag in the package's repository, such as `tag:beta2`
     - The prefix `branch:` followed by the name of a branch in the package's repository, such as `branch:main`
     - The prefix `commit:` followed by the hash of a commit in the package's repository, such as `commit:badcce14f8e828cda4d8ac404a12448700de1441`
     - Omitting the version is not yet supported
4. Add `#Include, %A_ScriptDir%` to the top of your script to set the current directory as the context for subsequent includes
5. Add `#Include, ahkpm-modules\github.com\user\repo\main-file.ahk` to your script
6. You can now use the package's functionality within your AutoHotKey script!

## Current limitations

ahkpm is being actively developed, but it is still a young project.
As a result it has the following limitations.

- It only supports hosting and downloading of packages on GitHub, though other git hosts will be supported in the future.
- It doesn't (yet) support specifying version ranges as you can in npm and other package managers.
- The lockfile only guides installations [when top-level dependencies haven't changed](https://github.com/joshuacc/ahkpm/issues/75).

If you'd like to help remedy these limitations, consider [contributing][github]!

[semver]:https://semver.org/
[releases]:https://github.com/joshuacc/ahkpm/releases
[github]:https://github.com/joshuacc/
