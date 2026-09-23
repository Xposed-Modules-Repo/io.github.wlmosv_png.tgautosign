<div align="center">

<img src="https://raw.githubusercontent.com/wlmosv-png/TGAutoSign/master/docs/banner.png" width="720" alt="TGAutoSign">

# TGAutoSign

**点一次，签一年。**  ·  *Tap once. Signed every day.*

在 Telegram 里点一下它的签到按钮 —— 之后再也不用管。

回调按钮、文本指令、群签到都支持；签到窗口、断网补签、多账号隔离、限流退避内置。
管理面板就在 Telegram 内 —— 任意聊天发 `/jmb`。

[![Latest Release](https://img.shields.io/github/v/release/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign?label=%E6%9C%80%E6%96%B0%E7%89%88%E6%9C%AC&color=blue)](https://github.com/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/total?label=%E4%B8%8B%E8%BD%BD%E9%87%8F&color=brightgreen)](https://github.com/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/releases)
[![API](https://img.shields.io/badge/libxposed-API%20102-8A2BE2)](https://github.com/LSPosed/LSPlant)
[![License](https://img.shields.io/badge/license-GPLv3-green)](LICENSE)

**⬇️ [下载最新版 APK](https://github.com/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/releases/latest)** · [源码仓库](https://github.com/wlmosv-png/TGAutoSign)

作者 **wlmosv** · 好用的话 [给源码仓库点个 Star ⭐](https://github.com/wlmosv-png/TGAutoSign)

</div>
<details open>
<summary><b>🇬🇧 English</b></summary>

**TGAutoSign** — Telegram daily auto check-in for LSPosed.
Tap the bot's check-in button **once**; it learns and repeats daily, automatically.
The control panel lives inside Telegram: send `/jmb` in any chat.

**Highlights**

- **Three ways to sign** — callback buttons · text commands · group/channel check-ins; one bot can hold several commands
- **Multi-account**, fully isolated (targets, signed state and retry backoff are per account)
- **Timing** — signing window · per-target schedule · minimum spacing · make-up deadline (23:00 default) · pause a target for a week
- **Reliability** — three-state reply parsing (success / already signed / failure) · failure rolls back and retries with backoff 5m → 15m → 45m → 2h → 4h · `FLOOD_WAIT` respected · offline make-up · 3-day failure alert · cross-client sync
- **Blocking** — line-based rules (matched against bot replies and button labels, `/…/` regex supported) · block a whole bot · freeze one target · network-learn hits need your confirmation
- **UI & data** — panel inside Telegram, all icons drawn in code, dark/light follows your Telegram theme, built-in log view with a one-tap diagnostic bundle, daily summary to your Saved Messages
- **100% local** — no server, no telemetry
- **English UI out of the box** — on English devices no setup is needed

**Supported clients**

| Client | Package | Status |
| --- | --- | --- |
| Telegram (Play / default) | `org.telegram.messenger` | ✅ tested on 12.10.3 |
| Telegram (direct APK) | `org.telegram.messenger.web` | ✅ statically verified |
| Nagram XF | `fork.risin42.nagramx` | ✅ tested |
| ExteraLess (ExteraGram fork) | `com.exteraless.app` | ✅ tested on 12.10.1 |
| Nagram / NagramX / NagramNX | `nu.gpu.nagram` etc. | whitelisted, not tested |
| Other Telegram-Android forks | any | injects if flag classes are intact |
| Telegram X | — | ❌ not injected (different core) |

> ⚠️ **Scope**: LSPosed enables only the official client by default. Using a third-party client? Tick **that** client in the module's scope as well.

**Install** — install the APK → enable in LSPosed → tick your Telegram client in scope → fully stop Telegram, reopen → send `/jmb` in any chat.
Requires **libxposed API 102+** and a rooted device.

**What this is not** — a convenience tool, not a bypass. It respects rate limits, waits out `FLOOD_WAIT`, backs off on failures, and never loops tightly. No exploit, no anti-detection logic.

</details>

---

## 📱 Screenshots / 界面一览

**English UI** — built in, no setup required
**英文界面** — 内置，无需设置

| Main panel | Main menu |
| --- | --- |
| ![Main panel](https://raw.githubusercontent.com/wlmosv-png/TGAutoSign/master/docs/screenshots/main-en-dark.jpg) | ![Main menu](https://raw.githubusercontent.com/wlmosv-png/TGAutoSign/master/docs/screenshots/menu-en-dark.jpg) |
| Targets | Settings |
| ![Targets](https://raw.githubusercontent.com/wlmosv-png/TGAutoSign/master/docs/screenshots/targets-en-dark.jpg) | ![Settings](https://raw.githubusercontent.com/wlmosv-png/TGAutoSign/master/docs/screenshots/settings-en-dark.jpg) |

<details>
<summary>中文界面（3 张）</summary>

| 暗色 · 主面板 | 暗色 · 主菜单 |
| --- | --- |
| ![主面板·暗色](https://raw.githubusercontent.com/wlmosv-png/TGAutoSign/master/docs/screenshots/main-dark.jpg) | ![主菜单·暗色](https://raw.githubusercontent.com/wlmosv-png/TGAutoSign/master/docs/screenshots/menu-dark.jpg) |
| 设置 | |
| ![设置](https://raw.githubusercontent.com/wlmosv-png/TGAutoSign/master/docs/screenshots/settings-light.jpg) | |

</details>

---

## ✨ 它能做什么

| | 能力 | 说明 |
|---|---|---|
| ⚡ | **点一次就学会** | 在 bot 里点一下签到按钮，之后每天自动重放；按钮 data 变了也跟得上 |
| 📝 | **文本指令也行** | 填 bot ID + 指令（如 `/checkin`），到点自动发 |
| 👥 | **群 / 频道签到** | 群 ID 同样支持，回复判定按群内消息走 |
| 🕐 | **时间你说了算** | 签到窗口 · 每目标随机时刻 · 错开间隔 · 补签截止 · 暂停一周 |
| 🛡️ | **不硬刚风控** | 失败自动退避 5m→15m→45m→2h→4h · 尊重 FLOOD_WAIT · 断网自动补签 |
| 🚫 | **不想签的挡得住** | 关键词 / 正则规则 · 整只 bot 排除 · 单个目标冻结 |
| 👤 | **多账号互不干扰** | 目标与已签状态按账号隔离；可一键把目标复制到其它账号 |
| 🔔 | **每天一条摘要** | 发到自己的收藏夹，不弹系统通知；连续失败 3 天额外告警 |
| 🌍 | **中英双语界面** | 英文设备装上即英文；设置里可手动切换 |
| 🔒 | **数据全在本地** | 无服务器、无遥测、无上报 |

---

## 🖥️ 支持的客户端

模块先按宿主包名判定，再按标志类能力兜底，命中才注入：

| 客户端 | 包名 | 状态 |
| --- | --- | --- |
| Telegram（Play / 默认渠道） | `org.telegram.messenger` | ✅ 12.10.3 回调签到实测 |
| Telegram（官网直连版） | `org.telegram.messenger.web` | ✅ 静态逐项核对 |
| Nagram XF | `fork.risin42.nagramx` | ✅ dec46b0 实测 |
| ExteraLess（ExteraGram fork） | `com.exteraless.app` | ✅ 12.10.1-feae791 实测 |
| Nagram / NagramX / NagramNX | `nu.gpu.nagram` 等 | 白名单覆盖，未实测 |
| 其它 Telegram-Android 系 fork | 任意包名 | 标志类齐全即注入 |
| Telegram X | — | ❌ 不注入（换内核，标志类不齐全） |

适配 Telegram **12.10.x** 全系，含 12.10.3。

> ⚠️ **作用域**：LSPosed 里默认只勾了官方版。用官网直连版 / Nagram XF 等第三方客户端，请把**对应客户端**也勾进模块作用域（`Hosts` 只决定「勾了之后注不注入」）。

---


---

## 🚀 30 秒上手

**1.** 装 APK → LSPosed → **模块** → 启用 **TGAutoSign**
**2.** **作用域**里勾选你在用的 Telegram 客户端
**3.** 完全停掉 Telegram，再重新打开
**4.** 任意聊天发 `/jmb` → 到 bot 会话**点一次它的签到按钮** → 完成

> 之后每天自动签。想看状态、改设置，随时发 `/jmb`。


---

## ❓ 常见问题

**Q：点了按钮没有添加？**

A：检查「设置 → 学习行为」里的自动学习开关；或直接 `/jmb` → 添加目标手动加。若仍不加，确认作用域已勾选、并完全停止 Telegram 重开。

**Q：机器人是点按钮不发文字的那种，能自动签吗？**

A：能。点一次按钮即学会（列表里带类型标记），之后每天自动重放。若按钮是打开网页或游戏类（无回调数据），不会误学。

**Q：官方版能用，第三方客户端用不了？**

A：模块已支持这些客户端（见支持矩阵），但作用域默认只勾了官方版 —— 到 LSPosed 里把对应客户端勾进模块作用域，再完全停止 Telegram 重开。

**Q：签到没生效怎么办？**

A：`/jmb` → 自诊断看反射锚点是否正常；运行日志查注入与签到记录；仍未解决就导出运行日志，附客户端名称与版本提 Issue。

**Q：怎么迁移到新手机 / 新账号？**

A：旧环境 `/jmb` → 导出配置；新环境把 json 放进 `Android/data/<客户端包名>/files/tgautosign/` 后导入。导入只合并不清空。

**Q：升级提示「与已安装应用签名不同」？**

A：装到了调试包。先卸载再装本页正式版；正式包之间可直接覆盖升级，签到数据不丢。

---

## 📜 更新日志

### v1.5.6 (119)

**新增**：三层黑名单（排除规则 / 排除的 bot / 目标冻结）· 排除管理独立入口 · 网络学习需确认 · 目标备注名 + @username · bot 矢量图标

**界面**：冻结 / 已排除 徽章标识，已排除条目虚化 · 对话框不再叠层

**修复**：官方版 / Nagram 按钮学习失效（改结构匹配 hook）· 回调签到前置命令后盲等导致面板过期 · 网络层学习 hash 字段崩溃 · 汇总通知提前发送

**兼容**：按钮点击方法按参数类型结构匹配，官方版与各 fork 通用 · 三客户端回调签到实测通过

> 自本版起仅对 `org.telegram.messenger`、`xyz.nextalone.nagram`、`com.exteraless.app` 三个客户端做主要维护。

### v1.5.5 (118)

**新增**

- 群 / 频道签到
- 签到结果通知（发到自己的收藏夹，不弹系统通知）
- 跨客户端同步目标与签到状态
- 补签截止 —— 补签与签到窗口解耦，当天不再提前作废
- 连续失败 3 天告警

**界面**

- 图标全部改为代码绘制，替换 26 种 emoji
- 主菜单加分类直达，取消二级「更多功能」页
- 教程重写，补齐通知、主题、暂停、重试上限说明

**修复**

- 手动发指令被误判为已签，导致自动签到跳过该目标
- bot 回「已签过」不落盘，日历不绿且心跳每 90 秒重发
- 群签到发出后收不到结果判定
- 日志只读当天文件，历史记录读不到
- 日志「回到最新」方向相反
- 定时器重复排队导致多目标叠加签到

**兼容**

- 对话框改为自绘，不再依赖宿主 `AlertDialog` API（12.10.3 已把方法名混淆）

### v1.5.4 (117)

- 定时签到：只在签到窗口内签；签到时间按钮选择，错开间隔可配
- 今日计划：每目标显示已签实际时刻 / 待签计划时刻
- 日志升级：按目标过滤、诊断包、加载更多、配色重做
- 界面：自绘终端卡片对话框、设置页分组、下次签到倒计时
- 修复：启动与面板补签遵守窗口；多目标随机间隔发送

---

## 🔗 下载渠道

| 渠道 | 地址 |
| --- | --- |
| **本页 Releases**（推荐） | [releases/latest](https://github.com/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/releases/latest) |
| 源码仓库 Releases | [wlmosv-png/TGAutoSign](https://github.com/wlmosv-png/TGAutoSign/releases) |
| 模块内直达 | Telegram 发 `/jmb` → 检查更新 |

> 同一版本两个仓库的 APK 逐字节一致（`sha256sum.txt` 附在 Release 里），签名始终是同一把 release key，覆盖安装不丢数据。

---

## ⚖️ 许可

基于 **GPLv3** 开源，仅供个人学习与自有账号使用。
请遵守 Telegram 服务条款及各群组 / 机器人规则。

---

<p align="center"><sub>Made by wlmosv · <a href="https://github.com/wlmosv-png/TGAutoSign">点个 Star ⭐ 是持续更新的动力</a></sub></p>
