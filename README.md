# Verdient Homebrew Tap

Homebrew formulae for [Verdient/network-monitor](https://github.com/Verdient/network-monitor).

macOS 14+ 可直接安装：

```bash
brew install Verdient/tap/network-monitor
network-monitor --version
brew services start network-monitor
network-monitor stats
```

支持 Apple Silicon 和 Intel。

当前版本：[v0.1.0](https://github.com/Verdient/network-monitor/releases/tag/v0.1.0)。
配方中的 SHA-256 与 GitHub Release 的真实归档一致，两种架构均经过 Brew 安装测试。

- 配置：`$(brew --prefix)/etc/network-monitor/config.ini`
- 数据：`$(brew --prefix)/var/lib/network-monitor/network-monitor.db`
- 修改配置后：`brew services restart network-monitor`
- 停止采集：`brew services stop network-monitor`

本仓库的配方使用 [0BSD](LICENSE) 许可证，二进制依赖遵循各自许可证。
