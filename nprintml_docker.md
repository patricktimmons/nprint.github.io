---
title: Docker Demo Image
has_children: false
parent: nPrintml
grand_parent: The nPrint Project
nav_order: 3
---

# Docker Demo Image

A Docker container demo is provided for each nPrintML release to aid prospective users in trying out the tool.

Note: The container is intended for users of as-yet-unsupported platforms and users of atypically-configured systems. nPrintML _should_ install easily for most users, as described in the [preceding section](#set-up); and, for day-to-day use, it is **strongly recommended** that nPrintML be installed _without_ virtualization. nPrintML users requiring support in installing the tool should consult [the project's homepage](https://nprint.github.io/nprintml.html) and then consider [reaching out for help](https://github.com/nprint/nprintML/issues/new/choose). Users of unsupported platforms should consider creating a [feature request](https://github.com/nprint/nprintML/issues/new/choose) or a [pull request](https://github.com/nprint/nprintML/pulls).

## Dependencies

The container demo requires [Docker](https://www.docker.com/).

### Usage

The container entrypoint is the `nprintml` command, and as such takes the same arguments:

    docker run [...] ghcr.io/nprint/nprintml ...

Note, however, that any argument references to the host filesystem must be mapped to the container filesystem. For this reason, the `nprintml-docker` script is recommended.

#### Demo script

The `nprintml-docker` script is the recommended interface to the container demo. Argument references to the host filesystem are mapped and rewritten for the container filesystem; outputs are written to the host filesystem and given user ownership, _etc._

`nprintml-docker` requires Python v3.6 or greater.

The script is available for download from the [nPrintML repository](https://raw.githubusercontent.com/nprint/nprintML/main/image/nprintml-docker). It may be placed anywhere on your system, and made executable or invoked with either `python` or `python3`.

A reasonable installation of the script (globally) might include the following:

    DEST="/usr/local/bin"

    curl --output-dir="$DEST" -O https://raw.githubusercontent.com/nprint/nprintML/main/image/nprintml-docker

    chmod +x "$DEST"/nprintml-docker

The script should then be available for execution, even without reference to its full path, (so long as `DEST` above is itself in your environment's `PATH`):

    nprintml-docker ...

Note: In the above example, the script is installed to the system _globally_. This will likely require `root` permission &ndash; _e.g._ `sudo curl …` and `sudo chmod …`.

Alternatively, set a different `DEST`. The script may be placed wherever you have write access &ndash; including user directories which are also commonly placed on `PATH`: `$HOME/.local/bin`, `$HOME/bin`, _etc._

If `DEST` is not on `PATH`, the script may be invoked via its full download path, _e.g._:

    ~/Downloads/nprintml-docker ...

And if the script is not made executable, it may be invoked via any available `python` (v3.6+):

    python ~/Downloads/nprintml-docker ...

##### Environment variables

The script's interface is forwarded to `nprintml` within the demo container. The script itself may be configured via the following environment variables.

| Name | Values | Description |
| ---- | ------ | ----------- |
| `NPRINTML_DOCKER_CHOWN` | `0`, `1`\* | Outputs owned by `root` are given user ownership via `chown` (`1`) |
| `NPRINTML_DOCKER_DEBUG` | `0`\*, `1` | Enable debug-level logging to standard output (`1`) |
| `NPRINTML_DOCKER_REMOVE` | `0`, `1`\* | Container is removed after each run (`1`) |
| `NPRINTML_DOCKER_REPOSITORY` | (repository: `ghcr.io/nprint/nprintml`\*) | nPrintML repository of image |
| `NPRINTML_DOCKER_VERSION` | (version: `latest`\*) | nPrintML image version tag |

\* `default value`
