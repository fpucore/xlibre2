![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)
![Build Status](https://img.shields.io/badge/build-passing-brightgreen)
![Version](https://img.shields.io/badge/version-26.8.0-blue)
![Platform](https://img.shields.io/badge/platform-H--Linux-lightgrey)
![Maintenance](https://img.shields.io/badge/maintained%20by-fpucore-orange)

# XLibre2 - A better X Server 🖥️✨

![Logo](assets/xlibre2-logo_512px.png)

> **A modern, reproducible build of the X server**  
> *A fork of the XLibre build with H-Linux integration*

This repository contains the packaging, build environment, and installer for XLibre2 on GNU Operating System / H-Linux.

Rather than distributing prebuilt binaries, this project provides a **reproducible build system** that compiles XLibre2 and its libinput driver directly from source, applies H-Linux integration modifications, packages the results, and installs them onto the running system.

Ultimately, the goal is to make rebuilding XLibre2 straightforward while keeping H-Linux modification and patches separate from upstream XLibre.

---

## 🚀 Features

* **Native H-Linux package generation** 📦
* **Reproducible packaging** 🔁
* **Automated build and installation** ⚙️
* **Integrated libinput build procedure** 🖱️
* **ccache support for faster rebuilds** ⚡

---

## 📋 Requirements

The build requires:

* GNU Operating System / H-Linux instance 🐧
* H-Linux human command layer 💻
* H-Linux env library 🔧
* NLP 🧠
* makepkg 📦
* Meson 🏗️
* Ninja 🥷
* GCC or Clang ⚙️
* ccache 💾
* All dependencies specified by the included PKGBUILDs

---

## 📥 Getting the code

```bash
> gh repo clone fpucore/xlibre2

> cd xlibre2
```

---

## 🔨 Build & Install

```bash
> ./install.sh
```

The installer will automatically:

* Create clean build environment 🧹
* Stage override files 📂
* Build the libinput driver 🖱️
* Build XLibre2 🖥️
* Generate native packages 📦
* Install all packages seamlessly 🚀

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📄 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

* Thanks to the XLibre project for the foundation
* H-Linux community for integration support
* All contributors who help improve this project

*Built with ❤️ for the H-Linux ecosystem*