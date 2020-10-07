# Quantum Mechanical Keyboard Firmware

[![Current Version](https://img.shields.io/github/tag/qmk/qmk_firmware.svg)](https://github.com/qmk/qmk_firmware/tags)
[![Build Status](https://travis-ci.org/qmk/qmk_firmware.svg?branch=master)](https://travis-ci.org/qmk/qmk_firmware)
[![Discord](https://img.shields.io/discord/440868230475677696.svg)](https://discord.gg/Uq7gcHh)
[![Docs Status](https://img.shields.io/badge/docs-ready-orange.svg)](https://docs.qmk.fm)
[![GitHub contributors](https://img.shields.io/github/contributors/qmk/qmk_firmware.svg)](https://github.com/qmk/qmk_firmware/pulse/monthly)
[![GitHub forks](https://img.shields.io/github/forks/qmk/qmk_firmware.svg?style=social&label=Fork)](https://github.com/qmk/qmk_firmware/)

This is a fork of Drop's version of qmk firmware for use with a Drop Alt High Profile


Based on the [tmk\_keyboard firmware](https://github.com/tmk/tmk_keyboard).

## Documentation

* [See the official documentation on docs.qmk.fm](https://docs.qmk.fm)

The docs are powered by [Docsify](https://docsify.js.org/) and hosted on [GitHub](/docs/). You can request changes by making a fork and [pull request](https://github.com/qmk/qmk_firmware/pulls), or by clicking the "Edit Document" link at the bottom of any page.

## Official Website

[qmk.fm](https://qmk.fm) is the official website of QMK, where you can find links to this page, the documentation, and the keyboards supported by QMK.

## QMK setup on Windows 10 using WSL

To run QMK under Windows using the Windows Subsystem for Linux with Fish-Shell, follow these steps:

* do a `sudo apt install git python3 python3-pip`
* add to path via `set -Ua fish_user_paths $HOME/.local/bin`
* install qmk: `python3 -m pip install --user qmk`
* clone repository: `cd $HOME && git clone https://github.com/0x4a/qmk_firmware.git`
* if you do `qmk setup` there will be some packages missing, so do: `sudo apt install gcc-avr avrdude gcc-arm-none-eabi dfu-util` first
* the `dfu-programmer` won't work because USB support is missing in WSL, so I just symlinked dfu-util to dfu-programmer with `sudo ln -s /usr/bin/dfu-util /usr/bin/dfu-programmer`. Yes, that will not *work* how it is intended, but it satisfies qmk's check for dfu-programmer. As we will never use it, and flash via [mdloader](https://github.com/Massdrop/mdloader/releases) instead, that should not be a problem. Just remember to not use dfu-programmer or try to flash the board from WSL. As an alternative you could install dfu-programmer for Windows and symlink that executable to `/usr/bin/dfu-programmer` instead. That should run from WSL giving you a working dfu-programmer - but I could not get it to run in Windows, so I opted for the easy way out ;-) 
* voila: run `qmk setup` and after it finishes successfully, you can build the default keymap with `qmk compile -kb massdrop/alt -km default` without error
