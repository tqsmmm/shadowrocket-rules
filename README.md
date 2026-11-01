# shadowrocket-rules

个人专属的 **Shadowrocket（小火箭）** 高性能策略分流配置，深度对齐 [mihomo-tauri-proxy](https://github.com/tqsmmm/mihomo-tauri-proxy) 的日常使用与开发工作流习惯。

精简冗余的流媒体规则，聚焦于 **AI 生产力、DevOps 基础设施、社媒沟通与常用生态**，搭配各地区延迟自动测速选优（`url-test`）。

---

## 🚀 快速导入

在 iOS 端打开 **Shadowrocket**：
1. 进入底部导航栏 **配置**；
2. 点击右上角 **`+`** 添加远程配置；
3. 在 **URL** 输入框粘贴以下订阅地址（二选一）：

### 官方 Raw 直连地址
```text
https://raw.githubusercontent.com/tqsmmm/shadowrocket-rules/main/lazy_group.conf
```

### 国内镜像加速地址（推荐国内网络直接拉取）
```text
https://ghproxy.net/https://raw.githubusercontent.com/tqsmmm/shadowrocket-rules/main/lazy_group.conf
```

4. 点击 **下载** 并选中该配置即可生效。

---

## 🎯 核心分流设计

| 策略分组 | 覆盖服务 / 规则 | 默认行为 |
| :--- | :--- | :--- |
| **OpenAI** | ChatGPT、OpenAI API、`oaistatic.com`、`oaiusercontent.com` | 手动选择 / 节点自选（优先美/日/新） |
| **Anthropic** | Claude 网页端及 API（`anthropic.com`、`claude.ai`） | 手动选择 / 节点自选（优先美/日/新） |
| **Gemini** | Google Gemini、Antigravity (AGY)、DeepMind、CloudCode | 手动选择 / 节点自选（优先美/日/新） |
| **Cursor** | Cursor IDE、`cursor.com`、`cursor.sh`、`todesktop.com` | 独立代理通道 |
| **xAI** | x.ai、Grok API 及网页端 | 独立代理通道 |
| **GitHub** | GitHub 代码仓库、CDN、Raw 资源、Assets、Gist | 强制走代理（彻底避免直连超时或 Push/Clone 失败） |
| **DevOps** | Docker Hub、Cloudflare API / CDN 节点 | 代理 / 直连切换 |
| **Telegram** | Telegram 客户端与 Web 通讯 | 代理自选 |
| **Discord** | Discord 客户端及网关 | 代理自选 |
| **YouTube** | YouTube 视频与流媒体数据 | 代理自选 |
| **Google** | Google 搜索与海外常用谷歌服务 | 代理自选 |
| **Binance** | 币安交易所 Web & API | 专属优选代理 |
| **苹果 / 微软** | Apple 全家桶服务、微软生态服务 | 默认直连 `DIRECT`（可手动切代理） |
| **哔哩哔哩** | Bilibili 客户端与网页 | 默认直连 `DIRECT`（支持港台节点换区） |
| **国内应用** | 微信、百度、网易云、知乎、小红书、抖音等 | 直连 `DIRECT` |
| **全局兜底** | 局域网、中国大陆 IP（`GEOIP,CN`）直连，其余流量兜底走代理 | `FINAL,PROXY` |

---

## ⚡ 地区自动测速选优

配置内内置各地区 `url-test` 节点池（每 10 分钟自动发起健康检查与延迟测试，自动切换到最低延迟节点）：
- 🇭🇰 **香港节点**
- 🇹🇼 **台湾节点**
- 🇯🇵 **日本节点**
- 🇸🇬 **新加坡节点**
- 🇰🇷 **韩国节点**
- 🇺🇸 **美国节点**

---

## 🛡️ 网络与安全配置

- **DoH / 加密 DNS**：集成阿里与腾讯 DoH（`https://dns.alidns.com/dns-query`、`https://doh.pub/dns-query`），2 秒超时自动回退到系统 DNS。
- **WebRTC 防泄露**：内置 STUN 伪造响应（`1.1.1.1` / `::1`），防止通过 WebRTC 协议泄露本地及真实外网 IP。
- **QUIC 优化**：针对代理流量屏蔽 UDP 443（QUIC），强制回退到 HTTP/2，杜绝国内运营商针对国际 UDP 限速与丢包造成的卡顿。
- **DNS 劫持防护**：强制重定向硬编码的 `8.8.8.8` / `8.8.4.4`。

---

## 🔄 配置同步与更新

当在 GitHub 仓库修改或更新规则后，在 Shadowrocket 的 **配置** 列表找到该配置，左滑点击 **从 URL 更新** 即可拉取最新配置。

