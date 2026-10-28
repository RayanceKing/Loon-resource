# Loon-resource

<p align="center">
  <strong>面向 Loon 的配置与插件资源。</strong>
</p>

<p align="center">
  提供一份可直接导入的 Loon 配置，包含 DNS、节点筛选、策略组等常用设置；<br />
  同时收录用于增强 The Intro Database 数据访问能力的 Loon 插件。
</p>

<p align="center">
  <a href="https://www.nsloon.com/openloon/import?sub=https%3A%2F%2Fraw.githubusercontent.com%2FRayanceKing%2FLoon-plugins%2Fmain%2Fconfig%2FLoonKit.lcf">
    一键导入 Loon 配置
  </a>
</p>

<p align="center">
  <a href="https://raw.githubusercontent.com/RayanceKing/Loon-plugins/main/config/LoonKit.lcf">获取配置地址</a> ·
  <a href="#快速开始">快速开始</a> ·
  <a href="#插件">插件</a>
</p>

> 本项目是社区资源，与 Loon 官方无关。节点、订阅、API Key 和其他个人配置需要自行准备。

## 功能概览

**基础网络配置** — 提供双栈网络、DNS、DoH、DNS 劫持和常用绕过规则等设置，可作为个人 Loon 配置的基础模板。

**节点筛选与策略组** — 按地区、用途和订阅信息筛选节点，并提供 `Proxy`、`Auto`、`Fallback` 等策略组，方便手动选路或自动选择可用节点。

**TIDB 增强插件** — 通过为 The Intro Database API 请求添加个人 `Authorization`，让已上传但尚未审核通过的片头片尾数据可以用于个人场景。

## 快速开始

1. **备份配置**：首次导入前，先在 Loon 中导出现有配置，并保存自己的节点订阅。
2. **导入配置**：在已安装 Loon 的 iPhone 或 iPad 上用 Safari 打开上方「一键导入 Loon 配置」；也可以进入 **配置 → 所有配置文件 → ＋ → 从链接导入**，粘贴[配置地址](https://raw.githubusercontent.com/RayanceKing/Loon-plugins/main/config/LoonKit.lcf)。
3. **添加节点**：导入后，在 `[Proxy]` 或 `[Remote Proxy]` 中添加自己的节点和订阅，再根据需要调整策略组。
4. **选择策略**：在 Loon 的策略页面中，为不同服务选择 `DIRECT`、`Proxy`、`Auto` 或 `Fallback`。

> [!IMPORTANT]
> 配置文件不包含任何个人节点或订阅。使用「全覆盖更新」前请确认已经备份；该操作可能替换现有节点、订阅和本地设置。

## 配置说明

### DNS

- 默认提供普通 DNS 与 DoH 配置。
- `hijack-dns = *:53` 用于接管常规 UDP/53 DNS 请求，不包含应用内置的 DoH/DoT 请求。
- DNS、IPv6、TUN 和 UDP 行为会受到当前网络环境及 Loon 版本影响，遇到解析或连接问题时请结合请求记录排查。

### 节点筛选

配置内置常用的节点筛选规则，包括中国香港、中国台湾、日本、新加坡、美国、游戏节点和全球节点。`Auto` 与 `Fallback` 默认使用全部订阅节点，你可以按自己的订阅命名方式修改 `Auto_Filter` 和 `Fallback_Filter`。

## 插件

### TIDB 增强

文件：[plugins/TIDB增强.lpx](./plugins/TIDB增强.lpx)

该插件为 `api.theintrodb.org` 的媒体请求添加 `Authorization` 请求头，用于访问自己上传的、尚未通过审核的片头片尾数据。

安装步骤：

1. 下载 [TIDB增强.lpx](./plugins/TIDB增强.lpx)。
2. 在 Loon 的插件页面中导入该文件并启用。
3. 在插件参数中填入自己的 **TIDB API Key**，不要把 Key 写入仓库或分享给他人。
4. 按 Loon 提示为 `api.theintrodb.org` 配置并启用 MitM；如果已有相关 MitM 配置，请直接复用。

> 插件只会在请求中使用你提供的 Key，不提供或代管 TIDB 账号、API Key 和上传内容。请遵守 The Intro Database 的服务条款与接口限制。

## 常见问题

<details>
<summary><strong>导入后没有可用节点？</strong></summary>

本项目不会内置或分发节点。请在 `[Proxy]` 或 `[Remote Proxy]` 中添加自己的节点或订阅，并检查策略组当前选择的线路。

</details>

<details>
<summary><strong>点击导入后没有打开 Loon？</strong></summary>

请确认设备已安装 Loon，并使用 Safari 打开导入链接。也可以在 **配置 → 所有配置文件 → ＋ → 从链接导入** 中手动粘贴[配置地址](https://raw.githubusercontent.com/RayanceKing/Loon-plugins/main/config/LoonKit.lcf)。

</details>

<details>
<summary><strong>TIDB 插件没有生效？</strong></summary>

请检查插件是否已启用、API Key 是否填写正确，并确认 Loon 已为 `api.theintrodb.org` 启用 MitM。建议同时查看 Loon 请求记录，确认请求是否命中插件规则。

</details>

<details>
<summary><strong>配置更新会覆盖我的设置吗？</strong></summary>

托管配置的更新行为取决于 Loon 的更新选项。更新前请始终备份配置；对于节点、订阅和本地策略等个人内容，建议保留独立副本。

</details>

## 目录结构

```text
.
├── config/
│   └── LoonKit.lcf       # Loon 主配置
├── plugins/
│   └── TIDB增强.lpx      # The Intro Database 增强插件
├── LICENSE
└── README.md
```

## 免责声明与许可

本项目仅提供配置模板和插件规则，不保证节点、DNS、第三方 API 或网络服务的持续可用性。请自行评估配置风险，并对个人数据、API Key 及订阅链接负责。

项目以 [AGPL-3.0](./LICENSE) 授权。使用第三方服务时，请同时遵守其服务条款、接口限制和相关法律法规。

<sub><a href="https://github.com/RayanceKing/Loon-plugins/issues">Issues</a> · <a href="./LICENSE">AGPL-3.0</a></sub>
