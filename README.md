# network-monitor · Homebrew 安装

采集网卡的上传、下载速度和累计流量，查看每天或指定时段的统计与趋势图。
适用于 macOS 14 及以上版本，支持 Apple Silicon 和 Intel。

## 按操作系统下载

| 操作系统 | 下载 |
| --- | --- |
| macOS 14+ | [![下载 Apple Silicon（ARM64）版](https://img.shields.io/badge/tar.gz-Apple%20Silicon-000000.svg?logo=apple&logoColor=white)](https://github.com/Verdient/network-monitor/releases/download/v0.1.0/network-monitor-0.1.0-macos-arm64.tar.gz)<br>[![下载 Intel（x86_64）版](https://img.shields.io/badge/tar.gz-Intel%20x64-00A9E0.svg?logo=apple&logoColor=white)](https://github.com/Verdient/network-monitor/releases/download/v0.1.0/network-monitor-0.1.0-macos-x86_64.tar.gz) |

可使用同一版本的 [SHA256SUMS](https://github.com/Verdient/network-monitor/releases/download/v0.1.0/SHA256SUMS) 校验下载文件。
完整更新记录：[ChangeLog](https://github.com/Verdient/network-monitor/blob/main/CHANGELOG.md)。

## 安装并开始使用

先安装 [Homebrew](https://brew.sh/)，然后运行：

```bash
brew install Verdient/tap/network-monitor
network-monitor --version
brew services start network-monitor
```

启动后等待几秒，查看今天的网速统计：

```bash
network-monitor stats
```

默认每秒采集一次，使用默认路由网卡，按系统时区统计当天数据。

## 常用查询

```bash
# 指定网卡
network-monitor stats -i en0

# 查询指定日期，包含开始时间，不包含结束时间
network-monitor stats --start 2026-11-18 --end 2026-11-19

# 按北京时间查询当天的数据
network-monitor stats --tz Asia/Shanghai

# 只看统计表
network-monitor stats --no-chart
```

将 `en0` 换成实际网卡名，可用 `ifconfig -l` 查看。
如果同时采集多张网卡，使用 `-i` 选择要查询的一张。

## 设置采集网卡

打开配置文件：

```bash
nano "$(brew --prefix)/etc/network-monitor/config.ini"
```

保留已有的 `database` 路径，在 `[monitor]` 中设置网卡与采样间隔：

```ini
[monitor]
interface = en0, en1
interval = 1

[stats]
timezone = Asia/Shanghai
```

多张网卡用逗号分隔；不设置 `interface` 时采集默认路由网卡。
`interval` 单位为秒，最小为 1；不设置 `timezone` 时使用系统时区。
`--count`、`--start/--end` 和图表选项通过命令行指定，不写入配置。

修改后重启采集：

```bash
brew services restart network-monitor
```

## 管理服务

```bash
brew services info network-monitor      # 查看状态
brew services restart network-monitor   # 重启
brew services stop network-monitor      # 停止并取消登录后启动
```

## 数据和日志在哪里

| 内容 | 位置 |
| --- | --- |
| 配置 | `$(brew --prefix)/etc/network-monitor/config.ini` |
| 数据库 | `$(brew --prefix)/var/lib/network-monitor/network-monitor.db` |
| 日志 | `$(brew --prefix)/var/log/network-monitor/` |

历史数据持续保留。出现“暂无采样数据”时，先用 `brew services info network-monitor`
确认服务状态，再检查查询的网卡和日期。

## 更新与卸载

更新到新版本：

```bash
brew update
brew upgrade network-monitor
brew services restart network-monitor
```

卸载：

```bash
brew services stop network-monitor
brew uninstall network-monitor
```

卸载会保留配置和历史数据。

## 更多用法

```bash
network-monitor -h
network-monitor stats -h
```

多网卡临时采集、指定数据库和更多查询方式见 [完整使用说明](https://github.com/Verdient/network-monitor#readme)。
问题与建议请提交到 [Issues](https://github.com/Verdient/network-monitor/issues)。
本仓库使用 [0BSD 许可证](LICENSE)。
