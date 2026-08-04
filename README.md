# XLibre2

![Logo](assets/xlibre2-logo_512px.png)

A fork of the XLibre build of the X server.

This repository contains the packaging, build environment, and installer for XLibre2 on GNU Operating System / H-Linux.

Rather than distributing prebuilt binaries, this project provides a reproducible build system that compiles XLibre2 and 
its libinput driver directly from source, applies H-Linux integration modifications, packages the results, and installs 
them onto the running system.

Ultimately, the goal is to make rebuilding XLibre2 straightforward while keeping H-Linux modification and patches 
separate from upstream XLibre.

---

## Features

* Native H-Linux package generation
* Reproducible packaging
* Automated build and installation
* Integrated libinput build procedure
* ccache support for faster rebuilds

---

## Requirements

The build requires:

* GNU Operating System / H-Linux instance
* H-Linux human command layer
* H-Linux env library
* makepkg
* Meson
* Ninja
* GCC or Clang
* ccache
* All dependencies specified by the included PKGBUILDs

---

## Getting the code

```bash
> gh repo clone fpucore/xlibre2

> cd xlibre2
```

---

## Build & Install

```bash
> ./install.sh
```

The installer will automatically:

* Create clean build environment
* Stage override files
* Build the libinput driver
* Build XLibre2
* Generate native packages
* Install all packages seamlessly

---

## License

This project is licensed under the **MIT License**.
