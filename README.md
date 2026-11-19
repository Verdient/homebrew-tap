# Verdient Homebrew Tap

Homebrew formulae for [Verdient/network-monitor](https://github.com/Verdient/network-monitor).

首次版本正在准备。`Formula/network-monitor.rb` 会在源码仓库的 Release 构建与验证完成后加入。

发布完成后，macOS 14+ 可使用：

```bash
brew install Verdient/tap/network-monitor
network-monitor --version
brew services start network-monitor
network-monitor stats
```

支持 Apple Silicon 和 Intel。

- 配置：`$(brew --prefix)/etc/network-monitor/config.ini`
- 数据：`$(brew --prefix)/var/lib/network-monitor/network-monitor.db`
- 修改配置后：`brew services restart network-monitor`
- 停止采集：`brew services stop network-monitor`

本仓库的配方使用 [0BSD](LICENSE) 许可证，二进制依赖遵循各自许可证。
