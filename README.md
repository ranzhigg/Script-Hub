<div align="center">

<a href="https://github.com/ranzhigg/Script-Hub">
  <img src="assets/readme-banner.svg" alt="Script Hub" width="880">
</a>

# Script Hub

### 规则集 · 重写 · 脚本转换
### Rule Sets · Rewrites · Script Conversion

一个面向代理工具生态的转换与适配工具箱，把不同客户端的配置、脚本和规则集转换成更适合你当前环境的格式。
<br>
An adapter toolkit for the proxy-app ecosystem — convert rules, rewrites and scripts into the format your client actually needs.

<p>
  <a href="https://script.hub"><img src="https://img.shields.io/badge/在线体验-试试看-6C63FF?style=for-the-badge&logo=googlechrome&logoColor=white" alt="Try Script Hub"></a>
  <a href="https://github.com/ranzhigg/Script-Hub/wiki"><img src="https://img.shields.io/badge/文档-Documentation-00B894?style=for-the-badge&logo=readthedocs&logoColor=white" alt="Documentation"></a>
  <a href="https://github.com/ranzhigg/Script-Hub/blob/main/LICENSE"><img src="https://img.shields.io/badge/License-GPL--3.0-F39C12?style=for-the-badge&logo=gnu&logoColor=white" alt="GPL-3.0 License"></a>
  <a href="https://github.com/ranzhigg/Script-Hub"><img src="https://img.shields.io/github/stars/ranzhigg/Script-Hub?style=for-the-badge&logo=github&label=Stars" alt="GitHub stars"></a>
</p>

<p>
  <a href="#快速开始--quick-start">快速开始</a> ·
  <a href="#支持范围--support-matrix">支持范围</a> ·
  <a href="#loon-script-v2-beta">Loon Script v2</a> ·
  <a href="#社区--community">社区</a>
</p>

</div>

> [!NOTE]
> 这是 `ranzhigg/Script-Hub` 的社区维护分支，基于 [Script-Hub-Org/Script-Hub](https://github.com/Script-Hub-Org/Script-Hub) 持续同步与改进。This is a community-maintained fork that stays close to the upstream project.

## 项目简介 · About

Script Hub 的目标很简单：**让配置迁移不再成为折腾的瓶颈**。你可以把 QX、Surge、Loon、Shadowrocket、Clash 等生态中的规则、重写、模块、插件或脚本，转换为其他客户端能够理解的格式，再按需修改参数、检查兼容性并快速导入。

Script Hub keeps configuration migration practical: convert rules, rewrites, modules, plugins and scripts across the QX, Surge, Loon, Shadowrocket and Clash ecosystems, then adjust arguments, review compatibility and import the result with minimal friction.

## 为什么选择 Script Hub · Why Script Hub

| 能力 | What it gives you |
| --- | --- |
| 🔁 **跨客户端转换** | One source, multiple targets — reduce repetitive manual edits. |
| 🧩 **参数可编辑** | Modify `argument` values and advanced text without downloading a remote module first. |
| 🛡️ **兼容性提示** | Unsupported semantics are reported instead of being silently discarded. |
| ⚡ **快速导入** | Generate installable links for compatible clients and keep the workflow in one place. |
| 🧪 **Beta 先行验证** | Test newer Loon Script v2 capabilities while keeping the stable line independent. |

## 支持范围 · Support Matrix

| 输入 / Source | 输出 / Targets | 说明 / Notes |
| --- | --- | --- |
| QX Rewrite | Surge · Shadowrocket · Loon · Stash | 常用重写规则跨端转换 / Cross-client rewrite conversion |
| Surge Module | Loon · Stash | 模块内容与参数适配 / Module and argument adaptation |
| Loon Plugin | Surge · Shadowrocket · Stash | 插件结构转换 / Plugin conversion |
| Loon Script v2 **(Beta)** | Surge · Egern · Shadowrocket · Stash · Loon | 保留 Loon 原生 v2 语法 / Preserve native Loon v2 syntax |
| QX · Surge · Loon · Shadowrocket · Clash 规则集 | Surge · Shadowrocket · Stash · Loon | 规则集解析与目标格式输出 / Rule-set parsing and serialization |
| QX Script | Surge Script | 兼容性转换 / Compatibility conversion |
| 纯文本 / Plain text | 参数修改 · 高级操作 | 适合远程模块的轻量调整 / Lightweight remote-content editing |

支持的目标客户端包括 **Surge、Loon、Shadowrocket、Stash、Egern、LanceX**；具体能力以目标客户端的语法边界和转换提示为准。

## 核心功能 · Features

- 🧭 **一站式转换**：选择输入类型和目标类型，生成可直接使用的配置结果。
- 🛠️ **高级操作**：编辑任意文本、修改参数，适配需要自定义 `argument` 的远程模块。
- 📦 **快速导入**：支持 Shadowrocket、Loon、Stash 等客户端的导入入口。
- 🧱 **规则集处理**：将常见规则集转换为不同客户端可识别的格式。
- 🧬 **脚本适配**：将可表达的脚本逻辑映射到目标客户端；目标不支持时保留诊断信息。
- 🌐 **自托管**：支持本地预览、Node.js 服务和 Docker 部署，适合个人或团队维护。

## Loon Script v2 (Beta)

Beta 版本支持 Loon 3.5.1+ Script v2 的 `request`、`response`、`cron`、`network-changed` 和 `generic` 触发器，并将可映射的 `timeout`、`enable`、`requires_body`、`binary_body_mode` 与脚本参数带到目标格式。

The Beta parser supports Loon 3.5.1+ Script v2 triggers — `request`, `response`, `cron`, `network-changed` and `generic` — together with representable timeouts, enable states, body flags and script arguments.

兼容性边界：WASM、加密逻辑和脚本正文不会被解密或改写；无法等价表达的条件或参数会给出提示，不会静默丢失。Beta 解析器也避免使用旧版 iOS JavaScriptCore 不支持的正则后行断言，改善 iOS 15/部分 iOS 16 环境的启动兼容性。

Compatibility boundary: WASM, encrypted logic and script bodies are not decrypted or rewritten. When a target cannot express a source feature, Script Hub reports it instead of silently dropping it. The Beta parser also avoids RegExp lookbehind so older iOS JavaScriptCore environments can start normally.

### 本地验证 · Local validation

```bash
npm run test:loon-v2
```

## 快速开始 · Quick Start

### 在线使用 · Use online

1. 打开 [Script Hub](https://script.hub)。
2. 选择输入格式、目标客户端和转换模式。
3. 粘贴远程链接或文本，生成结果后按客户端提示导入。

1. Open [Script Hub](https://script.hub).
2. Choose the source format, target client and conversion mode.
3. Paste a URL or text, generate the result and import it using the client-specific action.

### 本地预览 · Run locally

```bash
git clone https://github.com/ranzhigg/Script-Hub.git
cd Script-Hub
pnpm install
pnpm preview
```

生产服务可使用 `pnpm service` 启动；Docker 用户可以直接使用仓库内的 `Dockerfile` 构建部署。
For a service process, use `pnpm service`; Docker users can build from the included `Dockerfile`.

### 文档与生态 · Docs & ecosystem

- 📖 [使用文档 / Documentation](https://github.com/ranzhigg/Script-Hub/wiki)
- 🧰 [Surge 模块工具 / Surge module tools](https://github.com/Script-Hub-Org/Script-Hub/wiki/%E7%9B%B8%E5%85%B3%E7%94%9F%E6%80%81:-Surge-%E6%A8%A1%E5%9D%97%E5%B7%A5%E5%85%B7)
- 🖥️ [全服务器版（测试中）/ Full-server edition (testing)](https://github.com/Script-Hub-Org/Script-Hub/wiki/%E5%85%A8%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%89%88(%E6%B5%8B%E8%AF%95%E4%B8%AD))

## 社区 · Community

欢迎反馈转换结果、兼容性问题和使用建议。Please share conversion results, compatibility reports and ideas:

- 👥 群组 / Groups: [张佩服](https://t.me/zhangpeifu) · [折腾啥](https://t.me/zhetengsha_group)
- 📢 频道 / Channels: [张佩服](https://t.me/h5683577) · [折腾啥](https://t.me/zhetengsha)
- 🐛 问题反馈 / Issues: [GitHub Issues](https://github.com/ranzhigg/Script-Hub/issues)

## 致谢 · Acknowledgements

感谢所有上游项目、脚本作者和社区贡献者。特别感谢 [_@Chavy_](https://github.com/chavyleung) 的 [Env.js](https://github.com/chavyleung/scripts)、[_@KOP-XIAO_](https://github.com/KOP-XIAO) 的 [resource-parser.js](https://github.com/KOP-XIAO/Quantumult/raw/master/Scripts/resource-parser.js)，以及参与 Script Hub 前端、解析器和图标生态建设的每一位贡献者。

Thanks to the upstream projects, script authors and community contributors who make this ecosystem possible. See the original project history for the complete acknowledgement list.

## 许可证 · License

本项目基于 [GNU General Public License v3.0](LICENSE) 发布。
Released under the [GNU General Public License v3.0](LICENSE).

<div align="center">

<sub>Made for people who enjoy making their tools fit just right. ✨</sub>

</div>
