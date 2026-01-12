## Introduction

[`ng2nlm`](https://github.com/davep/ng2nlm) is a simple command line tool
designed to turn a [Norton
Guide](https://en.wikipedia.org/wiki/Norton_Guides) file into a single
[Markdown](https://en.wikipedia.org/wiki/Markdown) file that can be uploaded
to Google's [NotebookLM](https://notebooklm.google.com/) (or presumably used
with other LLM tools for similar purposes).

It's probably fair to say that it's "opinionated" in that I wrote this to
serve my specific purpose; but where possible I've attempted to make it
generic and configurable.

## Installing

`ng2nlm` is a Python application and [is distributed via
PyPI](https://pypi.org/project/ng2nlm/). It can be installed with tools such
as [pipx](https://pipx.pypa.io/stable/):

```sh
pipx install ng2nlm
```

or [`uv`](https://docs.astral.sh/uv/):

```sh
uv tool install ng2nlm
```

Also, if you do have uv installed, you can simply use
[`uvx`](https://docs.astral.sh/uv/guides/tools/):

```sh
uvx ng2nlm
```

to run `ng2nlm`.

## Command line options

The command is called `ng2nlm` and all command line options can be found
with:

```sh
ng2nlm --help
```

giving output like this:

```bash exec="on" result="text"
ng2nlm --help
```

The key options are:

### `-g`, `--guide`

This tells `ng2nlm` the name of the guide to convert.

### `-s`, `---source`

This tells `ng2nlm` the name of the source file to create (the name of the
file that you will use as a source for NotebookLM). If `--source` isn't
supplied then the name of the guide minus its extension, plus an `.md`
extension, is assumed.

### `-a`, `--additional-instructions`

This switch lets you provide some optional additional instructions to
include at the top of the generated file. By default `ng2nlm` adds some
instructions for the LLM to help and encourage it to "comprehend" the
content of the file; using this switch you can add instructions specific to
the guide you're generating the file for.

!!! note

    This switch serves two purposes: if the value passed to the switch
    matches the name of a file in your filesystem, the content of that file
    will be read and used; otherwise the value given to the switch will be used.

### `-i`, `--instructions`

This switch is similar to the one above, but it lets you overwrite the
instructions that are built into `ng2nlm`.

## Examples

Create a NotebookLM source from a Norton Guide:

```sh
ng2nlm --guide ~/Documents/NGs/C52G01B.ng
```

This will read the contents of `C52G01B.ng` and create `C52G01B.md` in the
current working directory.

On the other hand, if you wanted to create the notebook source in a
different location and with a different name:

```sh
ng2nlm --guide ~/Documents/NGs/C52G01B.ng --source ~/sources/clipper52.md
```

To add a simple additional instruction when creating the output:

```sh
ng2nlm --guide mrdebug.ng --additional-instructions "Remember dark black is the best black"
```

or to do the same but pull the additional instruction from a file:

```sh
ng2nlm --guide mrdebug.ng --additional-instructions ~/.llm/rules.md
```

## Getting help

If you need some help using `ng2nlm`, or have ideas for improvements, please
feel free to drop by [the
discussions](https://github.com/davep/ng2nlm/discussions) and ask or
suggest. If you believe you've found a bug please feel free to [raise an
issue](https://github.com/davep/ng2nlm/issues).

[//]: # (index.md ends here)
