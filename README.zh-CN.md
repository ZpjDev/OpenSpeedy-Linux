<h1 align="center"> OpenSpeedy </h1>

<p align="center">
  <img style="margin:0 auto" width=100 height=100 src="https://github.com/user-attachments/assets/a82ceda2-9b7b-41e4-96dc-cd250c9bd3ff">
  </img>  
</p>

<p align="center">
  最好的开源游戏变速工具 — <strong>Linux 版</strong>
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

> **向原项目致敬**：本仓库是 [game1024/OpenSpeedy](https://github.com/game1024/OpenSpeedy) 的 Linux 适配 Fork，旨在继承原项目的设计理念和卓越贡献的同时，针对 Linux 环境（x86_64/x86）进行适配和优化。

## 🚀 功能特性

- **快速变速**：即时调节游戏速度，精确控制
- **现代化 UI**：基于 React + Tauri 2.0 构建，界面简洁直观
- **多进程支持**：支持原生 Linux 游戏、Steam Proton/Wine 游戏
- **跨架构支持**：同时支持 x86_64 和 x86 进程
- **无内核侵入**：Ring-3 级 Hook，不破坏系统内核
- **系统监控**：实时监控 CPU、内存和 GPU 使用情况
- **轻量级**：占用资源极少

## 📋 系统要求

- **操作系统**：Linux（推荐 x86_64）
- **桌面环境**：X11 或 Wayland
- **依赖库**：WebKit2GTK（大部分发行版包管理器会自动安装）

## 💾 安装方式

### 预编译版本

前往 [Releases](https://github.com/ZpjDev/OpenSpeedy-Linux/releases) 页面下载最新的 `.AppImage`、`.deb` 或 `.tar.gz` 包。

### 源码编译

1. **安装编译依赖**

   ```bash
   # Debian/Ubuntu
   sudo apt install build-essential libwebkit2gtk-4.1-dev libappindicator3-dev librsvg2-dev patchelf
   
   # Fedora/RHEL
   sudo dnf install webkit2gtk4.1-devel openssl-devel curl-devel sqlite-devel libappindicator-gtk3-devel librsvg2-devel
   
   # Arch Linux
   sudo pacman -S base-devel webkit2gtk-4.1 libsoup-2.4 librsvg
   ```

2. **安装 Rust 和 Node.js**

   - [Rust](https://rustup.rs/)（1.70+）
   - [Node.js](https://nodejs.org/)（v18+）

3. **克隆并编译**

   ```bash
   git clone https://github.com/ZpjDev/OpenSpeedy-Linux.git
   cd OpenSpeedy-Linux
   npm install
   npm run tauri build
   ```

   编译后的二进制文件位于 `src-tauri/target/release/bundle/`。

## 🛠️ 工作原理

OpenSpeedy Linux 版采用 **LD_PRELOAD 函数 Hook** 的方式拦截时间相关的系统调用。通过 Hook `nanosleep`、`clock_nanosleep`、`poll`、`select`、`epoll_wait` 等函数，实现对游戏时间流速的控制，而无需修改内核。

**通信架构：**
- 主 Tauri 应用通过 Unix Domain Socket（UDS）与 Bridge 通信
- Bridge 负责管理 Hook 注入和速度控制
- Hook 库（`libopenspeedy_hook.so`）拦截目标进程中的 libc 时间函数

## ⚠️ 已知限制

- **运行时注入**：当前版本不支持向已运行的进程注入。建议通过 OpenSpeedy 启动游戏以获得最佳体验。
- **Proton/Wine 游戏**：兼容性因游戏而异。部分依赖特定计时机制的游戏可能无法正常响应 Hook。
- **Wayland**：部分游戏在 Wayland 下的兼容性可能有所差异，具体取决于其图形栈实现。

## 🤝 参与贡献

欢迎提交 Issue 和 Pull Request！无论是 Bug 报告、功能建议还是代码贡献，我们都非常欢迎。

## 📄 开源协议

本项目采用 GNU General Public License v3.0（GPLv3）开源协议。详情请参阅 [LICENSE](LICENSE) 文件。

## 🙏 致谢

- **原始项目**：[OpenSpeedy](https://github.com/game1024/OpenSpeedy) by [Game1024](https://github.com/game1024) — 感谢其开创性设计与实现，为本 Linux 版提供了坚实基础。
- **框架支持**：[Tauri](https://tauri.app/)
- **界面设计**：[React](https://react.dev/) + [Ant Design](https://ant.design/)

<p align="center">
  Made with ❤️ by the OpenSpeedy community — Linux 版适配
</p>
