<div align="center">

<img src="https://raw.githubusercontent.com/wlmosv-png/TGAutoSign/master/docs/banner.png" width="720" alt="TGAutoSign">

# TGAutoSign

<p align="center"><b>中文</b> · <a href="https://github.com/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/blob/main/README.en.md">English</a></p>

**点一次，签一年。**  ·  *Tap once. Signed every day.*

在 Telegram 里点一下它的签到按钮 —— 之后再也不用管。

回调按钮、文本指令、群签到都支持；签到窗口、断网补签、多账号隔离、限流退避内置。
管理面板就在 Telegram 内 —— 任意聊天发 `/jmb`。

[![Latest Release](https://img.shields.io/github/v/release/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign?label=%E6%9C%80%E6%96%B0%E7%89%88%E6%9C%AC&color=blue)](https://github.com/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/total?label=%E4%B8%8B%E8%BD%BD%E9%87%8F&color=brightgreen)](https://github.com/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/releases)
[![API](https://img.shields.io/badge/libxposed-API%20102-8A2BE2)](https://github.com/LSPosed/LSPlant)
[![License](https://img.shields.io/badge/license-GPLv3-green)](LICENSE)
[![Telegram Group](https://img.shields.io/badge/Telegram-Join%20Group-26A5E4?logo=telegram&logoColor=white)](https://t.me/+V2Oyu8pSubs4ZjE0)

**⬇️ [下载最新版 APK](https://github.com/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/releases/latest)** · [源码仓库](https://github.com/wlmosv-png/TGAutoSign)

作者 **wlmosv** · 好用的话 [给源码仓库点个 Star ⭐](https://github.com/wlmosv-png/TGAutoSign)

</div>

---

## 📱 界面一览 · Screenshots

**英文界面 · English UI** — 内置，无需设置 · *built in, no setup required*

| Main panel | Main menu |
| --- | --- |
| ![Main panel](https://raw.githubusercontent.com/wlmosv-png/TGAutoSign/master/docs/screenshots/main-en-dark.jpg) | ![Main menu](https://raw.githubusercontent.com/wlmosv-png/TGAutoSign/master/docs/screenshots/menu-en-dark.jpg) |
| Targets | Settings |
| ![Targets](https://raw.githubusercontent.com/wlmosv-png/TGAutoSign/master/docs/screenshots/targets-en-dark.jpg) | ![Settings](https://raw.githubusercontent.com/wlmosv-png/TGAutoSign/master/docs/screenshots/settings-en-dark.jpg) |


**中文界面 · Chinese UI**

| 暗色 · 主面板 | 暗色 · 主菜单 |
| --- | --- |
| ![主面板·暗色](https://raw.githubusercontent.com/wlmosv-png/TGAutoSign/master/docs/screenshots/main-dark.jpg) | ![主菜单·暗色](https://raw.githubusercontent.com/wlmosv-png/TGAutoSign/master/docs/screenshots/menu-dark.jpg) |
| 设置 | |
| ![设置](https://raw.githubusercontent.com/wlmosv-png/TGAutoSign/master/docs/screenshots/settings-light.jpg) | |


---

## ✨ 它能做什么 · What it does

| | 能力 · Capability | 说明 · Description |
|---|---|---|
| ⚡ | **点一次就学会** · **Tap once, it learns** | 在 bot 里点一下签到按钮，之后每天自动重放；按钮 data 变了也跟得上<br>*Tap the bot's button once and it replays daily — even when the callback data changes.* |
| 📝 | **文本指令也行** · **Text commands too** | 填 bot ID + 指令（如 `/checkin`），到点自动发<br>*Set bot ID + command (e.g. `/checkin`); sent on schedule.* |
| 👥 | **群 / 频道签到** · **Group & channel check-ins** | 群 ID 同样支持，回复判定按群内消息走<br>*Group IDs supported; replies are read from group messages.* |
| 🕐 | **时间你说了算** · **Your schedule** | 签到窗口 · 每目标随机时刻 · 错开间隔 · 补签截止 · 暂停一周<br>*Window · per-target random slots · spacing · make-up deadline · pause a week.* |
| 🛡️ | **不硬刚风控** · **Rate-limit friendly** | 失败退避 5m→15m→45m→2h→4h · 尊重 `FLOOD_WAIT` · 断网自动补签<br>*Backoff on failure · waits out `FLOOD_WAIT` · catches up when back online.* |
| 🚫 | **不想签的挡得住** · **Block what you don't want** | 关键词 / 正则规则 · 整只 bot 排除 · 单个目标冻结<br>*Keyword / regex rules · block a whole bot · freeze a single target.* |
| 👤 | **多账号互不干扰** · **Multi-account, isolated** | 目标与已签状态按账号隔离；可一键把目标复制到其它账号<br>*Targets and signed-state are per account; copy targets across accounts.* |
| 🔔 | **每天一条摘要** · **Daily summary** | 发到自己的收藏夹，不弹系统通知；连续失败 3 天额外告警<br>*One message to your Saved Messages; alert after 3 failing days.* |
| 🌍 | **中英双语界面** · **Bilingual UI** | 英文设备装上即英文；设置里可手动切换<br>*English out of the box on English devices; switchable in Settings.* |
| 🔒 | **数据全在本地** · **100% local** | 无服务器、无遥测、无上报<br>*No server, no telemetry.* |

---

## 🖥️ 支持的客户端 · Supported clients

模块先按宿主包名判定，再按标志类能力兜底，命中才注入。
*Matched by host package first, then by flag classes as fallback — only injects on a match.*

| 客户端 · Client | 包名 · Package | 状态 · Status |
| --- | --- | --- |
| Telegram（Play / 默认渠道）| `org.telegram.messenger` | ✅ 12.10.3 实测 · *tested* |
| Telegram（官网直连版）| `org.telegram.messenger.web` | ✅ 静态核对 · *statically verified* |
| Nagram XF | `fork.risin42.nagramx` | ✅ dec46b0 实测 · *tested* |
| ExteraLess | `com.exteraless.app` | ✅ 12.10.1 实测 · *tested* |
| Nagram / NagramX / NagramNX | `nu.gpu.nagram` 等 | 白名单覆盖，未实测 · *whitelisted, untested* |
| 其它 Telegram-Android fork | 任意 | 标志类齐全即注入 · *injects if flags intact* |
| Telegram X | — | ❌ 不注入（换内核）· *not injected* |

> ⚠️ **作用域 · Scope**：LSPosed 里默认只勾了官方版。用第三方客户端，请把**对应客户端**也勾进模块作用域。
> *LSPosed enables only the official client by default. Using a third-party client? Tick **that** client in scope too.*

---


---

## 🚀 30 秒上手 · 30-second setup

| 步骤 · Step | 做什么 · Do this |
| --- | --- |
| **1** | 装 APK → LSPosed → **模块** 里启用 TGAutoSign<br>*Install the APK → LSPosed → **Modules** → enable TGAutoSign* |
| **2** | **作用域**里勾选你在用的 Telegram 客户端<br>*Tick your Telegram client in **Scope*** |
| **3** | 完全停掉 Telegram，再重新打开<br>*Fully stop Telegram, then reopen it* |
| **4** | 任意聊天发 `/jmb` → 到 bot 会话**点一次它的签到按钮**<br>*Send `/jmb` in any chat → tap the button once in the bot chat* |

> 完成。之后每天自动签，想看状态随时发 `/jmb`。
> *Done. It signs daily from then on — send `/jmb` anytime to check.*

---

## ❓ 常见问题 · FAQ

**Q：点了按钮没有添加 / Tapped the button but nothing was added**

检查「设置 → 学习行为」里的自动学习开关；或 `/jmb` → 添加目标手动加。若仍不加，确认作用域已勾选、并完全停止 Telegram 重开。

*Check the auto-learn switch under Settings → Learning, or add the target manually via `/jmb` → Add target. If it still won't add, make sure the scope is ticked and fully restart Telegram.*

**Q：机器人是点按钮不发文字的那种 / The bot uses buttons, not text**

能。点一次按钮即学会（列表里带类型标记），之后每天自动重放。若按钮是打开网页或游戏类（无回调数据），不会误学。

*Yes. Tapping once teaches it (the list shows a type badge) and it replays daily. Buttons that only open a web page or game (no callback data) are never mis-learned.*

**Q：官方版能用，第三方客户端用不了 / Works on the official client but not a third-party one**

模块已支持这些客户端（见支持矩阵），但作用域默认只勾了官方版 —— 到 LSPosed 里把对应客户端勾进模块作用域，再完全停止 Telegram 重开。

*Those clients are supported (see the matrix), but scope only includes the official client by default — tick your client in LSPosed, then fully restart Telegram.*

**Q：签到没生效怎么办 / Signing isn't working**

`/jmb` → 自诊断看反射锚点是否正常；运行日志查注入与签到记录；仍未解决就导出运行日志，附客户端名称与版本提 Issue。

*Run `/jmb` → Self-check to verify the reflection anchors, then inspect the log view. Still stuck? Export the log with your client name and version and open an issue.*

**Q：怎么迁移到新手机 / 新账号 / Migrating to a new phone or account**

旧环境 `/jmb` → 导出配置；新环境把 json 放进 `Android/data/<客户端包名>/files/tgautosign/` 后导入。导入只合并不清空。

*On the old device: `/jmb` → Export. On the new one: drop the json into `Android/data/<client package>/files/tgautosign/` and import. Import merges, never wipes.*

**Q：升级提示「与已安装应用签名不同」/ "Signature mismatch" when updating**

装到了调试包。先卸载再装本页正式版；正式包之间可直接覆盖升级，签到数据不丢。

*You installed a debug build. Uninstall it, then install the official APK from here. Official builds upgrade over each other in place — your data is kept.*

---

## 📜 更新日志 · Changelog

### v1.5.8 (121) — 2026-09-23

**修复**：新装用户点 bot 按钮学不会目标（重要） · 捕获模式在 Nagram \/ 官方版上无效 · 拒绝原因被谎报 · 日志账号前缀过期

**诊断**：诊断包新增学习与 hook 状态 · 诊断包头部显示补丁标记

### v1.5.7 (120) — 2026-09-23

**新增**：界面全面国际化（英文） · 多账号数据隔离修复

**修复**：签到倒计时混排 · 署名残缺 · 诊断页整块未译 · 弹窗按钮与分享标题未译 · 日志页筛选与空态未译 · 进度条永远走不满 · 「排除的 bot」没有真正生效 · 冻结条目视觉不一致

[完整更新日志 →](https://github.com/wlmosv-png/TGAutoSign/blob/master/CHANGELOG.md)

## 🔗 下载渠道 · Download

| 渠道 · Channel | 地址 · Where |
| --- | --- |
| **本页 Releases**（推荐）· *recommended* | [releases/latest](https://github.com/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/releases/latest) |
| 源码仓库 Releases · *source repo* | [wlmosv-png/TGAutoSign](https://github.com/wlmosv-png/TGAutoSign/releases) |
| 模块内直达 · *in-app* | Telegram 发 ` /jmb ` → 检查更新 |

> 同一版本两个仓库的 APK 逐字节一致（`sha256sum.txt` 附在 Release 里），
> 签名始终是同一把 release key，覆盖安装不丢数据。
> *Both repos ship byte-identical APKs (with `sha256sum.txt`), signed by the same release key — installing over keeps your data.*

---

## ⚖️ 许可 · License

基于 **GPLv3** 开源，仅供个人学习与自有账号使用。
请遵守 Telegram 服务条款及各群组 / 机器人规则。

*Licensed under **GPLv3**. For personal use with your own accounts.
Please respect Telegram's Terms of Service and each group's / bot's rules.*

---

<p align="center"><sub>Made by wlmosv · <a href="https://github.com/wlmosv-png/TGAutoSign">点个 Star ⭐ 是持续更新的动力</a></sub></p>
