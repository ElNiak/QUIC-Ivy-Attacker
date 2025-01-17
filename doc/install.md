---
layout: page
title: Installing IVy
---

There are two ways to install ivy:

1. [Install from source](#source)
2. [Install a binary release](#binary)

<a name="source"></a> Installing from source
--------------------------------------------

1. [Install from source on Linux](#linuxnotes)
3. [Install from source on Mac](#macnotes)


<a name="source"></a> Installing a binary release
--------------------------------------------

1. [Install from source on Linux](#linuxbinary)


<a name="linuxnotes"></a> Installation from source on Linux
===========================================================

This describes the steps need to install IVy on Ubuntu 20.04. This may
also work on other Debian-based distributions.

### Prerequisites

    $ sudo apt-get install python3.10 python3.10-pip g++ cmake python3.10-ply python3.10-pygraphviz git python3.10-tk tix pkg-config libssl-dev libreadline-dev

### Install IVy

Get the source like this:

    $ git clone --recurse-submodules https://github.com/kenmcmil/ivy.git
    $ cd ivy

Build the submodules like this (it takes a while):

    $ python3.10 build_submodules.py

Install into your local Python like this:

    $ sudo python3.10 setup.py install

If you want to run from the source tree for development purposes, do
this instead:

    $ sudo python3.10 setup.py develop

Optionally, build the experimental Ivy v2.0 compiler:

    $ python build_v2_compiler.py

### Run

Run Ivy on an example, like this:

    $ cd doc/examples
    $ ivy client_server_example.ivy

Or, if you only want to use Ivy on the command line, test it like this:

    $ ivy_check trace=true doc/examples/client_server_example_new.ivy
    
Ivy should print out a counterexample trace.

### Emacs mode

An emacs major mode for Ivy is available in `lib/emacs/ivy-mode.el`. Put this file
somewhere in your emacs load path and add the following code to your
`.emacs`:

    (add-to-list 'auto-mode-alist '("\\.ivy\\'" . ivy-mode))
    (autoload 'ivy-mode  "ivy-mode.el" "Major mode for editing Ivy code" t nil)

    
<a name="macnotes"></a> Installation from source on MacOS
=========================================================

Install using MacPorts
----------------------

These instructions have not been tested on recent MacOS versions.

1. Install Xcode from App Store
2. Install Xcode command line tools

        $ xcode-select --install

3. Install Xserver

    - [https://www.xquartz.org](https://www.xquartz.org)

4. Macports

        $ sudo xcodebuild -license

   Install Macports from [https://www.macports.org/install.php](https://www.macports.org/install.php). Select
   the version matching the macOS version running on your
   machine.

        $ sudo port install python310 py310-pip graphviz tix py310-tkinter git cmake openssl
        $ sudo port select --set python3.10 python310
        $ sudo port select --set pip3 pip310
        
5. Install Ivy:

        $ git clone --recurse-submodules https://github.com/kenmcmil/ivy.git
        $ cd ivy

    Build the submodules like this (it takes a while):

        $ python3.10 build_submodules.py

    Install into your local Python like this

        $ sudo python3.10 setup.py install
        $ sudo ln -s /opt/local/Library/Frameworks/Python.framework/Versions/3.10/bin/ivy* /opt/local/bin

    The second command may not be necessary, but works around a bug in
    the python setup tools installed by macports.

    If you want to run from the source tree for development purposes, do
    this instead:

        $ sudo python setup.py develop
        $ sudo ln -s /opt/local/Library/Frameworks/Python.framework/Versions/3.10/bin/ivy* /opt/local/bin


6. Running a test

        $ cd doc/examples
        $ ivy_check diagnose=true client_server_example_new.ivy

    This should fire up a GUI.



<a name="binary"></a> Binary releases
--------------------

Ivy is released as a Python package in the PyPI repository. I

### <a name="linuxbinary"> Install binary release on Linux

    $ sudo apt-get install python3.10 python3.10-pip g++ cmake python3.10-ply python3.10-pygraphviz git python3.10-tk tix pkg-config libssl-dev libreadline-dev
    $ sudo pip3 install ms-ivy

Note, if you omit `sudo` in the second command, Ivy will be installed
into `~\.local\bin`, which is probably not what you want, so be
careful.

This does not install the documentation and example files. You can get
these from github like this (see the directory `ivy/doc`):

    $ sudo apt-get install git
    $ git clone https://github.com/kenmcmil/ivy.git

### <a name="macbinary"> Install binary release on Mac

Mac binary distributions are not yet available.

 
