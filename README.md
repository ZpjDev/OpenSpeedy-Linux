<h1 align="center"> OpenSpeedy </h1>

<p align="center">
  <img style="margin:0 auto" width=100 height=100 src="https://github.com/user-attachments/assets/a82ceda2-9b7b-41e4-96dc-cd250c9bd3ff">
  </img>  
</p>

<p align="center">
  The Best Open-Source Game Speed Controller — <strong>Linux Edition</strong>
</p>

<p align="center">
  <img src="https://api.visitorbadge.io/api/visitors?path=ZpjDev.OpenSpeedy-Linux&countColor=%234ecdc4">
  <br/>
    
  <a href="https://github.com/ZpjDev/OpenSpeedy-Linux/stargazers">
    <img src="https://img.shields.io/github/stars/ZpjDev/OpenSpeedy-Linux?style=for-the-badge&color=yellow" alt="GitHub Stars">
  </a>

  <img src="https://img.shields.io/github/forks/ZpjDev/OpenSpeedy-Linux?style=for-the-badge&color=8a2be2" alt="GitHub Forks">

  <a href="https://github.com/ZpjDev/OpenSpeedy-Linux/issues">
    <img src="https://img.shields.io/github/issues-raw/ZpjDev/OpenSpeedy-Linux?style=for-the-badge&label=Issues&color=orange" alt="Github Issues">
  </a>
  <br/>  
  
  <a href="https://github.com/ZpjDev/OpenSpeedy-Linux/releases">
    <img src="https://img.shields.io/github/downloads/ZpjDev/OpenSpeedy-Linux/total?style=for-the-badge" alt="Downloads">
  </a>
  <a href="https://github.com/ZpjDev/OpenSpeedy-Linux/releases">
    <img src="https://img.shields.io/github/v/release/ZpjDev/OpenSpeedy-Linux?style=for-the-badge&color=brightgreen" alt="Version">
  </a>
  <a href="https://github.com/ZpjDev/OpenSpeedy-Linux/actions">
      <img src="https://img.shields.io/github/actions/workflow/status/ZpjDev/OpenSpeedy-Linux/build.yml?style=for-the-badge" alt="Github Action">
  </a>
  <a href="https://github.com/ZpjDev/OpenSpeedy-Linux">
    <img src="https://img.shields.io/badge/Platform-Linux-lightblue?style=for-the-badge" alt="Platform">
  </a>
  <br/>
  
  <img src="https://img.shields.io/badge/language-Rust%20%2B%20TypeScript-blue?style=for-the-badge">
  <img src="https://img.shields.io/badge/License-GPLv3-green.svg?style=for-the-badge">
</p>

<p align="center">
  🌐 <a href="https://github.com/ZpjDev/OpenSpeedy-Linux/blob/master/README.md">English</a> |
  <a href="https://github.com/ZpjDev/OpenSpeedy-Linux/blob/master/README.zh-CN.md">简体中文</a>
</p>

> **A tribute to the original project**: This repository is a Linux-adapted fork of [game1024/OpenSpeedy](https://github.com/game1024/OpenSpeedy) — honoring its design, philosophy, and effort while tailoring it for Linux environments (x86_64/x86).

## 🚀 Features

- **Quick Speed Adjustment**: Instantly change game speed with precision controls
- **Modern UI**: Clean, intuitive interface built with React + Tauri 2.0
- **Process Support**: Works with native Linux games, Steam Proton/Wine games
- **Cross-Architecture**: Supports both x86_64 and x86 processes
- **No Kernel Intrusion**: Ring-3 level hooking, does not tamper with the system kernel
- **System Monitoring**: Real-time CPU, memory, and GPU usage statistics
- **Lightweight**: Minimal resource footprint

## 📋 Requirements

- **OS**: Linux (x86_64 recommended)
- **Desktop Environment**: X11 or Wayland
- **Dependencies**: WebKit2GTK (installed automatically via most package managers)

## 💾 Installation

### Pre-built Binaries

Download the latest `.AppImage`, `.deb`, or `.tar.gz` from the [Releases](https://github.com/ZpjDev/OpenSpeedy-Linux/releases) page.

### Build from Source

1. **Install prerequisites**

   ```bash
   # Debian/Ubuntu
   sudo apt install build-essential libwebkit2gtk-4.1-dev libappindicator3-dev librsvg2-dev patchelf
   
   # Fedora/RHEL
   sudo dnf install webkit2gtk4.1-devel openssl-devel curl-devel sqlite-devel libappindicator-gtk3-devel librsvg2-devel
   
   # Arch Linux
   sudo pacman -S base-devel webkit2gtk-4.1 libsoup-2.4 librsvg
   ```

2. **Install Rust & Node.js**

   - [Rust](https://rustup.rs/) (1.70+)
   - [Node.js](https://nodejs.org/) (v18+)

3. **Clone and build**

   ```bash
   git clone https://github.com/ZpjDev/OpenSpeedy-Linux.git
   cd OpenSpeedy-Linux
   npm install
   npm run tauri build
   ```

   Built binaries will be in `src-tauri/target/release/bundle/`.

## 🛠️ How It Works

OpenSpeedy for Linux uses **LD_PRELOAD-based function hooking** to intercept time-related system calls. By hooking functions like `nanosleep`, `clock_nanosleep`, `poll`, `select`, and `epoll_wait`, it can effectively control the perceived speed of games without modifying the kernel.

**Communication Architecture:**
- Main Tauri app communicates with the bridge via Unix Domain Sockets (UDS)
- Bridge manages hook injection and speed control
- Hook library (`libopenspeedy_hook.so`) intercepts libc time functions in target processes

## ⚠️ Known Limitations

- **Runtime Injection**: Currently does not support injecting into already-running processes. For best results, launch games through OpenSpeedy.
- **Proton/Wine Games**: Compatibility varies by game. Games that heavily rely on certain timing mechanisms may behave differently.
- **Wayland**: Some games may have varying compatibility depending on their graphics stack and implementation.

## 🤝 Contributing

Contributions are welcome! Whether it's bug reports, feature requests, or code contributions, please feel free to open an issue or pull request.

## 📄 License

This project is licensed under the GNU General Public License v3.0 (GPLv3). See the [LICENSE](LICENSE) file for details.

## 🙏 Credits

- **Original Project**: [OpenSpeedy](https://github.com/game1024/OpenSpeedy) by [Game1024](https://github.com/game1024) — the original Windows version that inspired this Linux adaptation.
- **Framework**: [Tauri](https://tauri.app/)
- **UI**: [React](https://react.dev/) + [Ant Design](https://ant.design/)

<p align="center">
  Made with ❤️ by the OpenSpeedy community — adapted for Linux
</p>
