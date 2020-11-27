# Python Virtual Environment

| **Author(s)** | Vi Pham|
| :------------ | :-------------------------------------------------------------------------------------------- |
| **Reviewer(s)** | Quang Tran |
| **Start Date** | Nov 27th, 2020 |
| **Topic(s)** | General Techniques |
| **Status**       | In Progress |

## Introduction

A cooperatively isolated runtime environment that allows Python users and applications to install and upgrade Python distribution packages without interfering with the behaviour of other Python applications running on the same system.

## Motivation

Python applications will often use packages and modules that don’t come as part of the standard library. Applications will sometimes need a specific version of a library, because the application may require that a particular bug has been fixed or the application may be written using an obsolete version of the library’s interface.

This means it may not be possible for one Python installation to meet the requirements of every application. If application A needs version 1.0 of a particular module but application B needs version 2.0, then the requirements are in conflict and installing either version 1.0 or 2.0 will leave one application unable to run.

The solution for this problem is to create a **virtual environment**, a self-contained directory tree that contains a Python installation for a particular version of Python, plus a number of additional packages.

Different applications can then use different virtual environments. To resolve the earlier example of conflicting requirements, application A can have its own virtual environment with version 1.0 installed while application B has another virtual environment with version 2.0. If application B requires a library be upgraded to version 3.0, this will not affect application A’s environment.

## Create Virtual Enviroments on Linux

### The tool to create isolated Python environmens

`virtualenv` module will help you. Since Python `3.3`, a subset of it has been integrated into the standard library under the `venv` module. The `venv` module does not offer all features of this library, to name just a few more prominent:
- is slower (by not having the `app-data` seed method),
- is not as extendable,
- cannot create virtual environments for arbitrarily installed python versions (and automatically discover these),
- is not upgrade-able via [pip](pip),
- does not have as rich programmatic API (describe virtual environments without creating them).

Install `virtualenv`:
```
$ python -m pip install --user virtualenv
```

### Create a virtual environment

When you switch projects, you can simply create a new virtual environment and not have to worry about breaking the packages installed in the other environments. It is always recommended to use a virtual environment while developing Python applications.

To create a virtual environment, go to your project’s directory and run command line.
```
python -m virtualenv <virtual_environment_name>
```

### Activate a virtual environment

Before you can start installing or using packages in your virtual environment you’ll need to **activate** it. Activating a virtual environment will put the virtual environment-specific `python` and `pip` executables into your shell’s `PATH`.

```
$ source <virtual_environment_name>/bin/activate
```

### Leave the virtual environment

If you want to switch projects or otherwise leave your virtual environment, simply run:

```
$ deactivate
```

## References


- [1] [Installing packages using pip and virtual environments](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)
- [2] [Virtual Environment Wrapper](https://www.bogotobogo.com/python/python_virtualenv_virtualenvwrapper.php)
