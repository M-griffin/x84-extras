# x84-extras

Add-ons, projects, active systems, etc. for x/84

- [BBS List](bbs-list.md)
- [Extra scripts](scripts.md)
- [Miscellaneous](misc.md)

# Contributing

We strongly encourage community involvement. The entire point of this repository is
to give SysOps and developers a resource that links together community contributions
separate from the main x/84 project. That being said, here are a few guidelines
that will assist you with *smoothly* integrating your project with `x84-extras`:

## Keep it neat and tidy

If you want to make modifications to this repository's Markdown files, please be sure
to keep them in line with the current style:

- Lists are to maintain alphabetical order
  - Discard articles like 'The' for simplicity
- The BBS list should have each column filled in for each table row
  - Non-standard ports should be specified in the BBS list
  - Standard ports can use the check mark
  - Missing ports should use an `X` to denote their absence

## Please host your project in its own repo

This repository is intended to be something of a *phone book*; we don't store, nor do
we maintain responsibility for the projects we link to. We are just acting as a
centralized collection of links to x/84-related projects.

So, if you want your project to be in our list, create a GitHub repository for it. We
would prefer if each project is stored in its own repository, rather than storing
a collection of unrelated scripts in the same repository. This will make it far easier
for people to stay up to date with and focus their interest on particular scripts
and resources rather than having to muddle their way through a blob of scripts, art,
torrents, Dockerfiles, and the like.

We are not opposed to linking to repositories off of GitHub (like those on BitBucket),
and we have no qualms with linking to FTP directories, static pages, and such; but we
always prefer GitHub repositories to keep the community homogenous in terms of
workflow and collaboration.

## Please provide instructions and documentation for your project

To make it easier for people to pick up your project and use it/integrate it with their
x/84 system, please be sure to provide ample documentation for the installation,
configuration, and usage of your project (if these apply).

**Required:**

- If integrating your script requires modifying another script, be as specific as
  possible
- If your project has Python dependencies that are not included in x/84 by default,
  include a pip-friendly `requirements.txt` file with *specific versions* for each
  module (do not use version ranges or fail to include version numbers)

**Suggested:**

- When providing examples of source code, use syntax-highlighted code blocks
- Please create self-contained mods that can be used as *git submodules*
- Please allow for customization of your scripts through `default.ini` settings as much
  as possible

## Self-contained mods as git submodules

The idea here is that eventually, we can standardize on a way to pull new mods into an
x/84 system. If they're all hosted in git repositories, the simplest and most efficient
way to accomplish that is to use *git submodules*. Each project repository is
self-contained, and unless configured via `default.ini` settings to do otherwise, uses
relative paths to load all of its resources (such as art files). See the
[Rumors](https://github.com/x84-extras/rumors) script for an example of this.

The Rumors mod can be added to a system and maintained independently as either a *clone*
or a *submodule*:

### Clone

First, the repository is cloned into a subdirectory of the system's `scriptpath`:

    $ cd /path/to/x84/scripts
    $ git clone https://github.com/x84-extras/rumors

Then, `main.py` is modified to add a menu entry for loading the `rumors.py` script:

```python
gosub('rumors/rumors')
```

### Submodule

First, the x/84 `scriptpath` must itself be a git repository (though it does not need
to be linked to an external source like GitHub):

    $ cd /path/to/x84/scripts
    $ git init .

Next, the Rumors mod is added to the `scriptpath` repo as a *submodule*:

    $ git submodule add https://github.com/x84-extras/rumors rumors

Finally, just like with the *clone* method, we modify main.py to load the `rumors.py`
script:

```python
gosub('rumors/rumors')
```

### Keeping mods up to date

In the case of the *clone* scenario, you must do the following for *each and every mod*:

    $ cd /path/to/x84/scripts
    $ cd modulename
    $ git pull

However, with *submodules*, you can act on them recursively:

    $ cd /path/to/x84/scripts
    $ git submodule update --init --remote --recursive

# Licensing

You may use any license you see fit for your project. However, you must understand that
by including a link to your project, we are not incorporating your project into
`x84-extras`--merely pointing to a resource--and so we are not bound by any viral
clauses in the license you have chosen (such as the GPL).

Many of the `x84-extras` scripts use the MIT license, as does x/84 itself.
