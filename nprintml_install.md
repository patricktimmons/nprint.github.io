---
title: Installation
has_children: false
parent: nPrintML
grand_parent: The nPrint Project
nav_order: 1
---

# Installation

### Dependencies

Python versions 3.6 through 3.8 are supported.

You might check what versions of Python are installed on your system, _e.g._:

    ls -1 /usr/bin/python*

As needed, consult your package manager or [python.org](https://python.org/).

Depending on your situation, consider [pyenv](https://github.com/pyenv/pyenv) for easy installation and management of arbitrary versions of Python.

nprintML further requires nPrint (see below).

### Installation

nprintML itself is available for download from the [Python Package Index (PyPI)](https://pypi.org/project/nprintml/) and via `pip`:

    python -m pip install nprintml

This downloads, builds and installs the `nprintml` console command. If you're happy to manage your Python (virtual) environment, you're all set with the above.

That said, installation of this command via a tool such as [pipx](https://pipxproject.github.io/pipx/) is strongly encouraged. pipx will ensure that nprintML is installed into its own virtual environment, such that its third-party libraries do not conflict with any others installed on your system.

(Note that nPrint and nprintML are unrelated to the PyPI distribution named "nprint.")

### Post-installation

nprintML depends on the nPrint command, which may be installed separately.

For quick-and-easy satisfaction of this requirement, nprintML supplies the bootstrapping command `nprint-install`, which is made available to your environment with nprintML installed. This command will inspect its execution environment and attempt to retrieve, compile and install nPrint with the most appropriate defaults:

    nprint-install

nPrint may thereby be installed system-globally, to the user environment, to the (virtual) environment to which nprintML was installed, or to a specified path prefix. Consult the command's `--help` for more information.

`nprint-install` is identically available through its Python module (no different from `pip` above):

    python -m nprintml.net.install

### Further set-up

nprintML leverages [AutoGluon](https://auto.gluon.ai/) to manage AutoML. However, it _does not_ by default install additional libraries required for **all** models supported by AutoGluon. If you wish to test these models, you will need to install their requirements manually.

AutoGluon will itself note which models it is unable to generate – and how to satisfy their requirements – during operation.

For more information, consult the [AutoGluon documentation](https://auto.gluon.ai/).
