---
title: "Versions"
description: "How versions work in ahkpm"
lead: >
  How versions are treated is key to understanding any package manager, and
  ahkpm is no different.
date: 2022-11-24T15:11:49-05:00
lastmod: 2022-11-24T15:11:49-05:00
draft: false
images: []
menu:
  docs:
    parent: "concepts"
weight: 10
toc: true
---

ahkpm supports four types of versions.

- Semantic versions such as `1.2.3`
- Tag versions such as `tag:beta`
- Branch versions such as `branch:develop`
- Commit versions such as `commit:badcce14f8e828cda4d8ac404a12448700de1441`

In addition, ahkpm supports the use of semantic version ranges rather than exact
versions, but that is the subject of a separate article.

<!-- TODO: Add link to version range article -->

If you're familiar with git, you've probably noticed that three of those version
types map directly to concepts in git. In fact, because ahkpm uses git as the
storage mechanism for packages, every version type maps to something in git,
even semantic versions.

<!-- TODO: If you're not familiar with git, see the git article -->

## Semantic versions

### Semantic versioning in general

The general concept of semantic versions is relatively simple. Semantic
versioning is the convention of versioning software (especially libraries)
by using three dot-separated numbers (e.g. `1.16.3`), where each of those
numbers represents a certain type of information.

The first number is the "major" version. The second is the "**minor**" version.
And the third is called the "patch" version.

In other words, `<major>.<minor>.<patch>`.

Each of those numbers represents a change from the previous version. For example,
suppose we have a newly released library that starts out at version `1.0.0`
(the usual place to start).

If we find and fix a minor bug and publish a new version, semantic versioning
specifies that we should increment the **patch** version, resulting in `1.0.1`.

If we add a new feature in a way that doesn't break any existing
usage of the library, semantic versioning specifies that we should increment
the **minor** version, as well as reset the patch version to zero, resulting in
`1.1.0`

If we change the behavior of the library in a way that breaks code using the
current version, then according to semantic versioning, we should increment the
**major** version, as well as reset the minor and patch versions to zero,
resulting in `2.0.0`.

Based on these three rules, it becomes relatively simple to tell whether a new
version of a package is likely to break our code if we update. Thanks to these
rules, it becomes possible to use version ranges to specify what versions of
libraries are acceptable for us to use.

<!-- TODO: Add link to version range article -->

Semantic versioning does have a few more rules, but these cover the vast
majority of cases.

<aside class="alert alert-info">

For more details on semantic versioning, see [the official spec](https://semver.org).

</aside>

### Semantic versions in ahkpm

As mentioned previously, every type of version in ahkpm maps back to a concept
in git. And semantic versions in particular map to tags.

Of course, not every git tag is a valid semantic version, but ahkpm when ahkpm
attempts to find a semantic version, it does so by looking up the tags on the
package's git repository.

For example, if I attempt to install `github.com/joshuacc/simple-http` at
version `1.0.0`, ahkpm will check to see if that git repository has a tag
matching `1.0.0`. If it does, then the source code associated with that tag
is what will be installed.

Whenever possible, specifying your desired version using a semantic version
or semantic version range is preferred, because it leads to the greatest level
of stability when making updates.

If you have specified an exact version number for a package, running
`ahkpm update <packageName>` will have no effect. To get a new version you will
need to run `ahkpm install` with a new version specifier.

## Tag versions

Of course, you may want to install a package from a particular tag that isn't
a valid semantic version. For example, you might want to install the code from
tag `build-2022-12-25`. To specify that version, all you need to do is write it
as `tag:build-2022-12-25`.

Running `ahkpm update <packageName>` on a package using a tag version has no
effect. To get a new version you will need to run `ahkpm install` with a new
version specifier.

## Commit versions

Commit versions work similarly to tag versions, but allow referencing specific
commit IDs by using the `commit:` prefix. For example:
`commit:badcce14f8e828cda4d8ac404a12448700de1441`.

Running `ahkpm update <packageName>` on a package using a commit version has no
effect. To get a new version you will need to run `ahkpm install` with a new
version specifier.

## Branch versions

Branch versions also work similarly, but use the `branch:` prefix. For example:
`branch:beta`.

However, unlike exact semantic versions, tag versions, and commit version,
if you use a branch version, running `ahkpm update <packageName>` will result
in getting the latest code on that branch. And because it has no mechanism
for checking the compatibility of the package's code, it may result in breakage.

As a result, using branch versions is not recommended unless you are very
closely monitory the packages changes on this branch. However, it can be very
useful if you are.
