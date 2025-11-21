---
layout: onboarding
title: Setup
---

# Setup

The majority of these steps involve use of the terminal. For Windows users, you should install Windows Terminal and in the settings, set Windows PowerShell as the default profile. You can download it at the link below:

## Installing Development Tools

Please open the terminal application provided by your operating system and create a new folder called .qkrt in your home directory. This will create a hidden folder that we will use to isolate some of our tools. The commands to do this are as follows:

    cd ~
    mkdir .qkrt

Proceed to follow the steps below corresponding to your operating system.

### Windows 10
### Linux
### MacOS

1. Download and install Homebrew by running the following commands:

        /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
        brew update
    Make brew a system-usable command:

        echo >> ~/.zprofile
        echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
        eval "$(/opt/homebrew/bin/brew shellenv)"

2. Use Homebrew to install most of the necessary tools (this could take awhile):

        # install general tools
        brew install git

        # install ARM (target device) toolchain and tools
        brew tap osx-cross/arm
        brew install arm-gcc-bin
        brew install openocd --HEAD

        # install host gcc compiler and boost lib for tests
        brew install boost gcc@11 cmake

3. Install Python 3.8 and Pip3 using the installer here:

    [Python 3.8 MacOS PKG](https://www.python.org/ftp/python/3.8.0/python-3.8.0-macosx10.9.pkg)

    Continue through the installer leaving all options default.

    Ceate a symlink called python that links to the `python3.8` binary created by the installer. You can do this by running the following command:

        sudo ln -s $(which python3.8) $(dirname $(which python3))/python

    Verify that the python and pip3 commands work for Python 3.8 by opening a new terminal and then running the following commands:

        python --version
        pip3 --version

4. Install Pipenv 2023.2.20 using Pip3:

        pip3 install pipenv==2023.3.20

    Verify that you’ve successfully installed Pipenv by running the following command:

        pipenv --version

## Testing the Development Enviroment

 Open a terminal and change your working directory to some project folder (e.g. I keep my QKRT related projects in ~/dev/qkrt). Use Git to recursively clone the Tank Drive Tutorial starter code onto your machine.

    cd some/project/folder
    git clone --recursive https://gitlab.com/aruw/controls/aruw-edu.git tank-drive

Change directory into tank-drive and open Visual Studio Code using the following commands:

    cd tank-drive
    code .

Visual Studio Code may ask you if you would like to install the recommended extensions. I have listed them below for you to install:

![VS Code Extensions](/assets/images/setup/setup_vs_extensions.webp "VS Code Extensions")

Press Ctrl+Shft+P (or Cmd+Shift+P on macOS) to open Visual Studio Code’s Command Pallete and search for the “Tasks: Run Task” command:


## Setting up Development Environment

## Flashing and Debugging Using J-Link

## Testing Code
