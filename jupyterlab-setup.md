---
layout: page
---

## Windows, MacOS and Linux

The operating system on your computer both provides an interface between programs on your computer and it's physical machinery (the "hardware") and also provides a range of programs for user interaction. For our purposes some of the most important of these are the "terminal" and "shell" interfaces. The choice of programs that you use will different depending on the operating system that you are using but in all cases we will be using "command line" interfaces to the computer. A command line interface (CLI) allows interaction with the computer using commands typed as text. These commands are interpreted by a shell program (and we will be using the "bash" shell) and this shell program is itself run inside a graphical environment called a "terminal".

The name "terminal" comes from the days when the interface to a computer was a physical terminal and its (typically black) screen and (typically green) text were all that a user saw. Now that we are using computers with graphical user interfaces (GUIs), the terminal is only one of many programs that we will have open on our desktop at any one time.

### Windows Setup for WSL2

We will not be using Windows directly but rather using Ubuntu Linux installed in Windows Subsystem for Linux. Follow [these instructions](https://ubuntu.com/tutorials/install-ubuntu-on-wsl2-on-windows-11-with-gui-support#1-overview) to install Ubuntu on Windows 10 or Windows 11.

Once you have set up Ubuntu on WSL2, install the [Windows Terminal](https://apps.microsoft.com/store/detail/windows-terminal/9N0DX20HK701) app from the Microsoft Store.

## Setup a Python environment

A video walkthrough of this tutorial is available [here](https://drive.google.com/file/d/18cuBa-6CtHugl-lB5JDkd6tVLCLg1zM8/view?usp=drive_link).

In the next steps, Ubuntu on WSL2 will be treated the same as a native Ubuntu Linux install. MacOS is, however, slightly different.

To install a Python environment, download and install [Mambaforge](https://github.com/conda-forge/miniforge#mambaforge). Download the installer using either `wget` or `curl` and choose the installer that you want using these rules:

1. If you are on Ubuntu, download [Mambaforge-Linux-x86_64](https://github.com/conda-forge/miniforge/releases/latest/download/Mambaforge-Linux-x86_64.sh)

2. If you are on MacOS and you are *not* using a Mac with a M1 or M2 chip, download [Mambaforge-MacOSX-x86_64](https://github.com/conda-forge/miniforge/releases/latest/download/Mambaforge-MacOSX-x86_64.sh)

3. If you are on MacOS and you are using a M1 or M2 Mac, download [Mambaforge-MacOSX-arm64](https://github.com/conda-forge/miniforge/releases/latest/download/Mambaforge-MacOSX-arm64.sh)

The steps that we will be following are:

1. Download the Mambaforge installer
2. Install Python using Mambaforge
3. Setup your Python package environment
4. Install JupyterLab
5. Download and install JupyterLab Desktop

The commands to use must be run in your terminal. If you are on MacOS, find the Terminal in the Utils section of Applications. For Ubuntu and Windows, you can press the Windows key (the one with 4 squares) and type "terminal" to start the Terminal. 

### Download the Mambaforge installer

In all of these examples, ensure that you are using the download link (i.e. URL) that is correct for your computer and operating system.

To download using `wget` type:

```bash
wget -c https://github.com/conda-forge/miniforge/releases/latest/download/Mambaforge-Linux-x86_64.sh
```

and with `curl` type:

```bash
curl -OLC - https://github.com/conda-forge/miniforge/releases/latest/download/Mambaforge-Linux-x86_64.sh
```

In both cases, you need to press Enter after typing the command.

### Install Python using Mambaforge

Run the command below, replacing the `Mambaforge-Linux-x86_64.sh` with the name of the Mambaforge installer that you downloaded.

```bash
bash Mambaforge-Linux-x86_64.sh -b
```

Adding `-b` to this command means that the installer won't ask you any questions and instead will choose default answers. It also means that you agree to the license terms of the Mambaforge software that can be found [here](https://github.com/conda-forge/miniforge/blob/main/LICENSE).

### Setup your Python package environment

After the Mambaforge installer completes, you need to exit the Terminal and re-open it. This will ensure that your Python environment is active for the next steps. If your Python environment is active your prompt (the text on the left of your terminal) should contain the text '(base)`. Now run:

```bash
conda config --add channels defaults
conda config --add channels bioconda
conda config --add channels conda-forge
conda config --set channel_priority strict
```

The commands in this step set up the "channels", i.e. sources of packages, for the conda package management system that underlies our Python environment.

### Install JupyterLab

With package management correctly configured, we now can create a "jupyterlab environment". This will contain Python and the JupyterLab and notebook environment we need to use in our Python learning.

Run this command:

```bash
mamba create -n jupyterlab -y jupyterlab
```

This downloads all the software we need (the `-y` tells the system to not ask us to confirm the download) using `mamba`. [Mamba](https://github.com/mamba-org/mamba) is a fast package manager for conda packages (and conda is the package manager for our Python environment). While the Python programming language is named after the [Monty Python](https://en.wikipedia.org/wiki/Monty_Python) comedy group, many people have used snake-names for Python-related software. (And if you want to see more snakes, look [here](https://commons.wikimedia.org/wiki/Category:Serpentes_sex#/media/File:Snakes_having_Sex.jpg))

### Install JupyterLab Desktop

To make it easier to start JupyterLab sessions, our final setup step is to install the JupyterLab Desktop. Once again, we will need different packages depending on your computer and operating system setup.

#### Installing on Ubuntu (including Ubuntu on WSL2)

Download the installer with:

```bash
wget -c https://github.com/jupyterlab/jupyterlab-desktop/releases/latest/download/JupyterLab-Setup-Debian.deb
```

and install with

```bash
sudo dpkg -i JupyterLab-Setup-Debian.deb
```

This command will ask you for your password. Enter your Ubuntu user password. (`sudo` which stands for `superuser do` runs commands as the administrator of your computer).

#### Installing on MacOS

For M1 or M2 Macs, download and install [JupyterLab-Setup-macOS-arm64.dmg](https://github.com/jupyterlab/jupyterlab-desktop/releases/latest/download/JupyterLab-Setup-macOS-arm64.dmg) and for non-M1/M2 Macs, download and install [JupyterLab-Setup-macOS-x86.dmg](https://github.com/jupyterlab/jupyterlab-desktop/releases/latest/download/JupyterLab-Setup-macOS-x86.dmg).

### Starting the Jupyter Desktop environment

To test that everything works, run the `jlab` command. You should get a screen like that shown below:

<img alt="Screenshot of JupyterLab Desktop" style="border-style: solid; width: 100%" src="/img/jlab.png" />

There should not be any warning about "Python environment not found".

