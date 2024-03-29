---
title: "Introduction"
description: "An introduction to using ahkpm"
lead: >
  AutoHotkey is a powerful language for scripting automations on Windows, but
  finding, downloading, and using AutoHotkey libraries manually is painful.
  That's where ahkpm comes in.
draft: false
images: []
menu:
  docs:
    parent: "overview"
weight: 1
toc: true
---

## ahkpm is a package manager

The name ahkpm stands for "AutoHotkey Package Manager."
But what is a package manager?

A package manager is a tool used to find, download, install, and update
libraries and scripts. And it makes the overall process both easier and more
reliable than doing all that work by hand.

There are, however, a few things you need to learn in order to use it
effectively.

<mark class="fs-6">Already familiar with package managers? You can skip directly to
the [quick start guide](/quick-start).</mark>

## What is a package?

A "package" in the context of ahkpm means the source code for an AutoHotkey
library or script that is meant to be downloaded and used by others, typically
by importing it into your script with an `#Include`.
That can be something as simple as a few functions for working with strings,
or as complex as a web browser driver.
You can find examples on the [packages page](/packages).

<aside class="alert alert-info">
  <p>In order to follow along with the rest of the introduction, you will need
  the latest version of ahkpm. Please download and install it before continuing.</p>
  <a download class="btn btn-small btn-secondary" href="{{<download-latest-msi-url>}}">Download ahkpm</a>
</aside>

## Setting up your project to use ahkpm

To use ahkpm for your script or other project, open up a command prompt and
navigate to the folder where you are keeping your script's source code.
For example, `cd c:\my-project`.

Once in that folder, run the command `ahkpm init` to initialize ahkpm within
your project. You will be prompted with several questions about your project.
If you aren't sure about the answer, just go with the default.

Once you answer all the questions, you'll be presented with a final prompt
asking you to confirm that everything looks correct. Answer "Y" and you will
find a new file named `ahkpm.json` in your project folder.

The file will look similar to this.

```jsonc
{
  "version": "0.0.1",
  "description": "A brief description of what the package does",
  "repository": "github.com/user/my-project",
  "website": "example.com",
  "license": "MIT",
  "issueTracker": "github.com/user/my-project/issues",
  "author": {
    "name": "joshuacc",
    "email": "",
    "website": "joshuaclanton.dev"
  },
  "dependencies": {}
}
```

For our purposes in this introduction, the most important part is the line that
lists `"dependencies": {}`. What that means is that while we have set up ahkpm
within this project, we have not yet installed anything.

<aside class="alert alert-info">

  ##### Why is it called `dependencies`?

  Any time your script uses functionality from a package you've installed,
  it **depends on** that package (and that version) in order to work.
  In programming, something that you depend on is called a dependency.

</aside>

## Installing a package

Now that your project is set up with ahkpm, we can use it to install a package.
For this example, let's suppose we want to make an http request to a url and
then display the response.

Looking over the [packages page](/packages) we can see that there is a library
called `gh:joshuacc/simple-http` that appears to do what we need. (In ahkpm, `gh:`
is a shorthand for `github.com/`)

To install it we run the command `ahkpm install gh:joshuacc/simple-http`.
After a moment you should see a message indicating that it was installed
successfully.

If we look at `ahkpm.json` again, we'll see that the file has changed.
Now `dependencies` is no longer an empty object, but contains something similar
to the following:

```jsonc
{
  // Omitting others for brevity
  "dependencies": {
    "github.com/joshuacc/simple-http": "^1.0.0"
  }
}
```

Now ahkpm knows that this project depends on `github.com/joshuacc/simple-http`,
and that the version needs to match `^1.0.0`, which translates to
"at least `1.0.0`, but less than `2.0.0`."

<!-- For more information, see the versions, semver, and semver ranges pages -->

There is also a new file called `ahkpm.lock`. The contents and purpose of that
file are beyond the scope of this introduction, but **`ahkpm.lock` should not be
either edited or deleted.**

The third thing that has changed is that within your project folder there is a
new folder called `ahkpm-modules`. That folder is where the package's source
code is actually saved so that you can use it within your AutoHotkey scripts.

<mark class="fs-6">If you are storing your project in git, you should add `ahkpm-modules` to
your `.gitignore` file.</mark>

## Using a package

Now that we've installed the package, it's time to use it. We can do so by
typing `ahkpm include gh:joshuacc/simple-http` at the command line.

The command will output an `#Include` directive which we can paste into our script.
So let's do so.

```autohotkey
; my-script.ahk

; The #Include directive we got from the command line
#Include, %A_ScriptDir%\ahkpm-modules\github.com\joshuacc\simple-http\simple-http.ahk
```

Next we consult the package's documentation by visiting it's GitHub page to
learn how to use it. Fortunately it's fairly simple, so we add a couple more
lines of code till we have the following.

```autohotkey
; my-script.ahk

; The #Include directive we got from the command line
#Include, %A_ScriptDir%\ahkpm-modules\github.com\joshuacc\simple-http\simple-http.ahk

; Create a new instance
http := new SimpleHTTP()

; Get some user profile data to display
profileData := http.get("https://api.github.com/users/joshuacc")

; Open a dialog box to display the profile data
MsgBox, , "The Profile", %profileData%,
```

After running the script with AutoHotkey, you should see a dialog box with a
big blob of JSON describing the GitHub user profile of joshuacc. (That's me!)

<div class="alert alert-success">

  #### Package installed!

  You've installed your first package with ahkpm. That's enough to be useful,
  but it's in the ongoing maintenance that ahkpm really saves time.

</div>

## Updating a package

Suppose that the package we are using is updated with either new features or
bug fixes. If we had manually downloaded this code, then in order to get those
new features and fixes, we'd need to do the following:

1. Visit the website for the package
2. Check to see if there are any changes since we originally downloaded it.
   (Hopefully the authors keep good records!)
3. Manually download the updated version
4. Manually verify that the changes are compatible with our existing script

But with ahkpm, we run one simple command to do most of that work:

- `ahkpm update gh:joshuacc/simple-http`

This automatically checks to see if there are new versions of the package which
match the version range in `ahkpm.json`. In this case it is, `^1.0.0`, which
means "at least `1.0.0` and less than `2.0.0`." If there is a new matching
version, ahkpm will automatically download it.

And thanks to the fact that our version range doesn't allow going all the way up
to `2.0.0`, we can be fairly confident that updating won't break anything.

<aside class="alert alert-info">

#### About versions and ranges

ahkpm primarily relies on a versioning scheme called semantic versioning, which
is widely used in software development. Any time a package changes in a way that
is not backwards-compatible, it bumps the major version (the first number).

This means that updating is much safer than it would be otherwise, and can be
mostly (or entirely) automated. For more, see the documentation on
[versions in ahkpm][versions].

</aside>

#### What about updating further?

You may be wondering, "What about if I actually do want to update to a version
outside of that range?"

That is also easy to do. You would just run a command like the following:

- `ahkpm install gh:joshuacc/simple-http@2`.

The `@2` specifies that you want to install the latest version within the
`2.x.x` range. Assuming that there is a matching version available, ahkpm will
install it for you.


## You did it!

In this introduction, you've learned:

<div class="list-unstyled">

- ✅ What packages and package managers are
- ✅ How to set up your project to use ahkpm
- ✅ How to install a package for your project
- ✅ How to use a package in your AutoHotkey scripts
- ✅ How to update a package to get the latest features and bug fixes

</div>

**You're all set to start using ahkpm on your projects and save a ton of time
going forward.**

<!-- TODO: Link to concepts -->

[versions]:/docs/concepts/versions/
