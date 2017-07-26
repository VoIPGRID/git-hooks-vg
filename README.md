**git-hooks** - A tool to manage project and user Git hooks for multiple git repositories.

git-hooks lets hooks be installed inside git repositories and users home directory.
When a hook is called by `git`, git-hooks will check each of these locations for the hooks to run.


Install
=======

Just download the `git-hooks` executable found in the root of this repository to a directory of your
choice and ensure that it is added to your `PATH` environment variable so `git-hooks` can be run.

**A quick note on git subcommands**: When you type `git hooks` git actually looks for an
executable called `git-hooks`. This is done automatically, so although we're directly invoking
the executable (`git-hooks`) in the examples below, you can also use `git hooks` interchangably, since
git will invoke `git-hooks` in the background when you run `git hooks`.

For the latest master version, and assuming you want to put the executable in `/usr/local/bin/`:
```
$ curl -o /usr/local/bin/git-hooks https://raw.githubusercontent.com/wearespindle/git-hooks/master/git-hooks
$ chmod +x /usr/local/bin/git-hooks
```

Run `git-hooks --install` in a git project to tell it to use git-hooks hooks.  You can run
`git-hooks --uninstall` at any time to revert to your previous hooks.  (These are usually the
default hooks, which do nothing.)


Overview
========

Hooks are powerful and useful.  Some common hooks include:

- Spell check the commit message.
- Verify that the code builds.
- Verify that any new files contain a copyright with the current year in it.

Hooks can be very project-specific such as:

- Verify that the project still builds
- Verify that autotests matching the modified files still pass with no errors.
- Pre-populate the commit message with a "standard" format.
- Verify that any new code follows a "standard" coding style.

Or very person-specific hooks, such as:

- Don't allow a `push` to a remote repository after 1AM, in case I break something and will be asleep.
- Don't allow a commit between 9-5 for projects in `~/personal/`, as I shouldn't be working on them during work hours.

For more details about the different hooks available to you, check out:

	   http://www.kernel.org/pub/software/scm/git/docs/githooks.html



Locations
=========

git-hooks provide a way to manage and share your hooks using three locations:

 - **User hooks**, installed in `~/.git_hooks/`
 - **Project hooks**, installed in `git_hooks/` or `.githooks/` in a project.


Listing hooks
=============

When `git-hooks` is run without arguments, it lists all hooks installed on your system.  It will run the hooks with the `--about` argument to generate the description shown.

Check out the hooks in `contrib/` for some examples.


Creating hooks
==============

To keep things organized, git-hooks looks for scripts in **sub-directories** named after the git hook name.  For example, this project has the following `pre-commit` script in the following location:

	   git_hooks/pre-commit/bsd
