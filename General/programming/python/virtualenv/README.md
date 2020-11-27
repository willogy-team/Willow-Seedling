# Python Virtual Environment

| **Author(s)** | Vi Pham|
| :------------ | :-------------------------------------------------------------------------------------------- |
| **Reviewer(s)** | Quang Tran |
| **Start Date** | Nov 27th, 2020 |
| **Topic(s)** | General Techniques |
| **Status**       | In Progress |

# Index
- Introduction
- Motivation
- Virtual Enviroments on Linux
- Managing Packages with pip

## Introduction

A cooperatively isolated runtime environment that allows Python users and applications to install and upgrade Python distribution packages without interfering with the behaviour of other Python applications running on the same system.

## Motivation

Python applications will often use packages and modules that don’t come as part of the standard library. Applications will sometimes need a specific version of a library, because the application may require that a particular bug has been fixed or the application may be written using an obsolete version of the library’s interface.

This means it may not be possible for one Python installation to meet the requirements of every application. If application A needs version 1.0 of a particular module but application B needs version 2.0, then the requirements are in conflict and installing either version 1.0 or 2.0 will leave one application unable to run.

The solution for this problem is to create a **virtual environment**, a self-contained directory tree that contains a Python installation for a particular version of Python, plus a number of additional packages.

Different applications can then use different virtual environments. To resolve the earlier example of conflicting requirements, application A can have its own virtual environment with version 1.0 installed while application B has another virtual environment with version 2.0. If application B requires a library be upgraded to version 3.0, this will not affect application A’s environment.

## Virtual Enviroments on Linux

### The tool to create isolated Python environmens

`virtualenv` module will help you. Since Python `3.3`, a subset of it has been integrated into the standard library under the `venv` module. The `venv` module does not offer all features of this library, to name just a few more prominent:
- is slower (by not having the `app-data` seed method),
- is not as extendable,
- cannot create virtual environments for arbitrarily installed python versions (and automatically discover these),
- is not upgrade-able via `pip`,
- does not have as rich programmatic API (describe virtual environments without creating them).

Install `virtualenv`:
```
$ python -m pip install --user virtualenv
```

### Create a virtual environment

When you switch projects, you can simply create a new virtual environment and not have to worry about breaking the packages installed in the other environments. It is always recommended to use a virtual environment while developing Python applications.

To create a virtual environment, go to your project’s directory and run command line.
```
$ python -m virtualenv <virtual_environment_name>
```

### Activate a virtual environment

Before you can start installing or using packages in your virtual environment you’ll need to **activate** it. Activating a virtual environment will put the virtual environment-specific `python` and `pip` executables into your shell’s `PATH`.

```
$ source <virtual_environment_name>/bin/activate
```

### Leave the virtual environment

If you want to switch projects or otherwise leave your virtual environment, simply run:

```
(env) $ deactivate
```

## Managing Packages with pip

### What is `pip`?

A program help you install, upgrade, and remove packages. By default [pip](https://pypi.org/) will install packages from the Python Package Index.

### Search

You can browse the Python Package Index by going to it in your web browser, or you can use pip’s limited search feature:
```
(env) $ pip search <query>
```
```
(env) $ pip search virtualenv
virtualenv-switcher (0.1.1)            - Virtualenv switcher.
virtualenv-api (2.1.18)                - An API for virtualenv/pip
virtualenv-commands (0.2.3)            - Additional commands for virtualenv.
virtualenv-clone (0.5.4)               - script to clone virtualenvs.
virtualenv-tools3 (2.0.4)              - A set of tools for virtualenv
virtualenv-tools (1.0)                 - A set of tools for virtualenv
pytest-virtualenv (1.7.0)              - Virtualenv fixture for py.test
virtualenv-mgr (1.0.4)                 - Tool to manage your virtualenvs
...
```

### Install

You can install the latest version of a package by specifying a package’s name:
```
(env) $  python -m pip install <package_name>

```
```
(env) $  python -m pip install numpy
Collecting numpy
  Downloading numpy-1.19.4-cp37-cp37m-manylinux2010_x86_64.whl (14.5 MB)
     |████████████████████████████████| 14.5 MB 2.8 MB/s 
Installing collected packages: numpy
Successfully installed numpy-1.19.4
```

You can also install a specific version of a package by giving the package name followed by `==` and the version number:
```
(env) $  python -m pip install <package_name>==<version>

```
```
(env) $ python -m pip install numpy==1.17.2
Collecting numpy==1.17.2
  Downloading numpy-1.17.2-cp37-cp37m-manylinux1_x86_64.whl (20.3 MB)
     |████████████████████████████████| 20.3 MB 3.2 MB/s 
Installing collected packages: numpy
  Attempting uninstall: numpy
    Found existing installation: numpy 1.19.4
    Uninstalling numpy-1.19.4:
      Successfully uninstalled numpy-1.19.4
Successfully installed numpy-1.17.2
``` 

If you re-run this command, `pip` will notice that the requested version is already installed and do nothing. You can supply a different version number to get that version, or you can `run pip install --upgrade` to upgrade the package to the latest version:
```
(env) $ python -m pip install --upgrade <package_name>
```
```
(env) $ python -m pip install --upgrade numpy
Collecting numpy
  Using cached numpy-1.19.4-cp37-cp37m-manylinux2010_x86_64.whl (14.5 MB)
Installing collected packages: numpy
  Attempting uninstall: numpy
    Found existing installation: numpy 1.17.2
    Uninstalling numpy-1.17.2:
      Successfully uninstalled numpy-1.17.2
Successfully installed numpy-1.19.4
```

### Uninstall

You can uninstall package.
```
(env) $ pip uninstall <package_name>
```
```
(env) $ pip uninstall numpy
Found existing installation: numpy 1.19.4
Uninstalling numpy-1.19.4:
  Would remove:
    /home/env/bin/f2py
    /home/env/bin/f2py3
    /home/env/bin/f2py3.7
    /home/env/lib/python3.7/site-packages/numpy-1.19.4.dist-info/*
    /home/env/lib/python3.7/site-packages/numpy.libs/libgfortran-2e0d59d6.so.5.0.0
    /home/env/lib/python3.7/site-packages/numpy.libs/libopenblasp-r0-ae94cfde.3.9.dev.so
    /home/env/lib/python3.7/site-packages/numpy.libs/libquadmath-2d0c479f.so.0.0.0
    /home/env/lib/python3.7/site-packages/numpy.libs/libz-eb09ad1d.so.1.2.3
    /home/env/lib/python3.7/site-packages/numpy/*
Proceed (y/n)? y
  Successfully uninstalled numpy-1.19.4
```

### Show

You want to view information about a particular package:
```
(env) $ pip show <package_name>
```
```
(env) $ pip show numpy
Name: numpy
Version: 1.17.2
Summary: NumPy is the fundamental package for array computing with Python.
Home-page: https://www.numpy.org
Author: Travis E. Oliphant et al.
Author-email: None
License: BSD
Location: /home/env/lib/python3.7/site-packages
Requires: 
Required-by: 
```

### List

You can see all of the packages installed in the virtual environment:
```
(env) $ pip list
Package         Version
--------------- -------
cachetools      4.1.1
google-auth     1.23.0
numpy           1.17.2
pandas          1.1.4
pip             20.2.4
pyasn1          0.4.8
pyasn1-modules  0.2.8
python-dateutil 2.8.1
pytz            2020.4
rsa             4.6
setuptools      50.3.2
six             1.15.0
wheel           0.35.1
```
### Freeze

You can make a similar list of the installed packages, but the output uses the format that pip `install` expects. A common convention is to put this list in a `requirements.txt` file:
```
(env) $ pip freeze > requirements.txt
(env) $ cat requirements.txt
cachetools==4.1.1
google-auth==1.23.0
numpy==1.17.2
pandas==1.1.4
pyasn1==0.4.8
pyasn1-modules==0.2.8
python-dateutil==2.8.1
pytz==2020.4
rsa==4.6
six==1.15.0
```
The `requirements.txt` can then be committed to version control and shipped as part of an application. Users can then install all the necessary packages with `install -r`:
```
(env) $ python -m pip install -r requirements.txt
```

# References

- [1] [Installing packages using pip and virtual environments](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)
- [2] [Virtual Environment Wrapper](https://www.bogotobogo.com/python/python_virtualenv_virtualenvwrapper.php)
