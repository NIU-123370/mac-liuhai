<h1 align="center">
  <br>
  <img src="docs/app-icon.png" alt="mac-liuhai" width="160">
  <br>
  mac-liuhai
  <br>
</h1>

<p align="center">把 MacBook 刘海变成一个轻量的动态信息岛。</p>

mac-liuhai 是一个 macOS 菜单栏应用：音乐控制、播放可视化、日历与提醒、文件架、系统 HUD 替换、摄像头镜像、番茄钟，以及本机 Agent 会话状态，都集中在刘海里。

## 产品演示

[观看产品演示视频（31 秒）](docs/promo.mp4)

## 系统要求

- macOS 14 Sonoma 或更高版本
- Apple Silicon 或 Intel Mac
- 从源码构建需要 Xcode

## 功能

- 刘海展开、收起、悬停、拖拽和多屏支持
- Apple Music、Spotify 与 YouTube Music 播放控制和实时可视化
- 日历、提醒、电池、音量、亮度与系统 HUD
- 文件架与 AirDrop，摄像头镜像，番茄钟
- Agent 岛：读取本机 Codex 会话，并通过 hooks 接收 Claude Code / Qoder 状态

## 从源码构建

```sh
git clone https://github.com/NIU-123370/mac-liuhai.git
cd mac-liuhai
open macLiuhai.xcodeproj
```

在 Xcode 中选择 `macLiuhai` scheme 和 `My Mac` 后运行。也可以从 GitHub Actions 手动执行 **Fork Build**，下载构建出的 `mac-liuhai.app`。

命令行构建：

```sh
xcodebuild build \
  -project macLiuhai.xcodeproj \
  -scheme macLiuhai \
  -configuration Release \
  -destination "generic/platform=macOS"
```

## Agent 状态接入

Claude Code：

```sh
python3 scripts/agent-status/install_claude_hooks.py
```

Qoder：

```sh
python3 scripts/agent-status/install_qoder_hooks.py
```

安装后重启对应 IDE，再在 mac-liuhai 设置的 **Agents** 页勾选要显示的 Agent。详细边界、卸载方式和目录授权见 [docs/agent-island.md](docs/agent-island.md)。

## 验证

```sh
swiftc -swift-version 5 \
  macLiuhai/models/AgentSession.swift \
  macLiuhai/managers/AgentStatusReader.swift \
  tests/agent-status/main.swift -o /tmp/agent-status-tests
/tmp/agent-status-tests
python3 tests/agent-status/test_hooks.py
```

## 更新

当前构建不包含自动更新通道，也不会检查或安装旧项目的更新。

## 许可证

本项目以 **GNU GPL v3** 发布。完整许可证见 [LICENSE](LICENSE)，第三方依赖许可见 [THIRD_PARTY_LICENSES](THIRD_PARTY_LICENSES)，版权与修改声明见 [NOTICE](NOTICE)。
