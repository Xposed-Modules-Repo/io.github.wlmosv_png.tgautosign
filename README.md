<div align="center">

# TGAutoSign · Telegram 自动签到

在 Telegram 里点一次签到按钮，之后每天替你签。

回调按钮、文本指令、群签到都支持；签到窗口、断网补签、多账号隔离、限流退避内置。
管理面板就在 Telegram 内 —— 任意聊天发 `/jmb`。

[![Latest Release](https://img.shields.io/github/v/release/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign?label=%E6%9C%80%E6%96%B0%E7%89%88%E6%9C%AC&color=blue)](https://github.com/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/total?label=%E4%B8%8B%E8%BD%BD%E9%87%8F&color=brightgreen)](https://github.com/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/releases)
[![API](https://img.shields.io/badge/libxposed-API%20102-8A2BE2)](https://github.com/LSPosed/LSPlant)
[![License](https://img.shields.io/badge/license-GPLv3-green)](LICENSE)

**⬇️ [下载最新版 APK](https://github.com/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/releases/latest)** · [源码仓库](https://github.com/wlmosv-png/TGAutoSign)

作者 **wlmosv** · 好用的话 [给源码仓库点个 Star ⭐](https://github.com/wlmosv-png/TGAutoSign)

</div>

---

## 📱 界面一览

| 主面板（暗色） | 主菜单（日间） |
| --- | --- |
| ![主面板](https://raw.githubusercontent.com/wlmosv-png/TGAutoSign/master/docs/screenshots/main-dark.jpg) | ![主菜单](https://raw.githubusercontent.com/wlmosv-png/TGAutoSign/master/docs/screenshots/main-light.jpg) |
| 设置 | 目标过滤 |
| ![设置](https://raw.githubusercontent.com/wlmosv-png/TGAutoSign/master/docs/screenshots/settings-dark.jpg) | ![目标过滤](https://raw.githubusercontent.com/wlmosv-png/TGAutoSign/master/docs/screenshots/filter-dark.jpg) |

---

## ✨ 特性

**签到方式**

- **回调按钮**：去 bot 会话点一次签到按钮即学会，之后每天自动重放。按钮 data 每次变化也跟得上
- **文本指令**：填 bot ID + 指令（如 `/checkin`），到点自动发
- **群 / 频道**：群 ID（形如 `-1001234567890`）同样支持，回复判定按群内消息走
- **一个 bot 多条指令**：不同签到指令、文本与回调可并存，各自独立签到与重试
- **多账号**：目标与已签状态按账号隔离；可一键把目标复制到其它账号

**时间控制**

- **签到窗口**：只在窗口内动作，窗口外零请求。适合固定时段签、其余时间安静
- **时刻表**：窗口按目标数均分，各目标取随机时刻、互不重叠
- **错开间隔**：设 N 分钟则相邻目标至少隔 N 分钟再随机，防风控节奏自己定
- **补签截止**：窗口结束后仍会补到该时刻（默认 23:00），当天不会提前作废
- **暂停**：单个目标可暂停一周，到期自动恢复

**可靠性**

- **回复三态判定**：成功 / 已签过 / 失败。失败撤销已签，按 5m→15m→45m→2h→4h 退避重试
- **限流尊重**：遇到 FLOOD_WAIT 按服务器给的秒数等待
- **断网补签**：启动 / 定时 / 打开聊天 / 网络恢复都会补
- **连续失败告警**：同一目标连续 3 天失败告警一次，避免以为签上了其实没有
- **跨客户端同步**：官方版与第三方客户端之间同步目标与签到状态，任一端签的都算数

**界面与数据**

- **管理界面在 Telegram 内**：任意聊天发 `/jmb`，无独立 App、无桌面组件
- **图标全部代码绘制**：不依赖系统 emoji，各机型渲染一致
- **深浅色跟随 TG 主题**，也可在设置里强制日间 / 夜间
- **运行日志**：五级配色、最新在上、按目标筛选、一键诊断包
- **通知**：每天一条签到摘要发到自己的收藏夹，不弹系统通知
- **全部本地存储**：无服务器、无遥测

---

## 🖥️ 支持的客户端

模块先按宿主包名判定，再按标志类能力兜底，命中才注入：

| 客户端 | 包名 | 状态 |
| --- | --- | --- |
| Telegram（Play / 默认渠道） | `org.telegram.messenger` | ✅ 长期实测 |
| Telegram（官网直连版） | `org.telegram.messenger.web` | ✅ 静态逐项核对 |
| Nagram XF | `fork.risin42.nagramx` | ✅ dec46b0 实测 |
| ExteraLess（ExteraGram fork） | `com.exteraless.app` | ✅ 12.10.1-feae791 实测 |
| Nagram / NagramX / NagramNX | `nu.gpu.nagram` 等 | 白名单覆盖，未实测 |
| 其它 Telegram-Android 系 fork | 任意包名 | 标志类齐全即注入 |
| Telegram X | — | ❌ 不注入（换内核，标志类不齐全） |

适配 Telegram **12.10.x** 全系，含 12.10.3。

> ⚠️ **作用域**：LSPosed 里默认只勾了官方版。用官网直连版 / Nagram XF 等第三方客户端，请把**对应客户端**也勾进模块作用域（`Hosts` 只决定「勾了之后注不注入」）。

---

## 📲 安装

1. 需要 **Xposed 环境（libxposed API 102+）**、设备已 Root
2. 点上方 **⬇️ 下载最新版** 安装 APK（老用户直接覆盖安装，签到数据不丢）
3. LSPosed 模块管理器 → **模块** → 启用 **TGAutoSign**
4. 作用域勾选你在用的 Telegram 客户端
5. 完全停止 Telegram 后重新打开，任意聊天发 `/jmb`

---

## 🚀 使用

**最快上手**：到签到 bot 的会话里手动点一次它的签到按钮 → 模块自动记住目标 → 之后每天全自动。

也可以发 `/jmb` 打开面板手动添加：

| 入口 | 用途 |
| --- | --- |
| 目标列表 | 查看全部目标、今日状态、上次签到时间 |
| 添加目标 | 文本指令 / 回调按钮捕获 / 群频道，三种方式 |
| 立即签到 | 手动触发一轮 |
| 运行日志 | 查注入与签到记录，一键复制诊断包 |
| 设置 | 签到窗口、错开间隔、补签、通知、主题、学习行为 |
| 使用教程 | 面板内分节说明 |

面板底部「全部功能」是分类直达：目标 / 数据 / 系统 / 帮助 / 维护 —— 横向滑动点一下进对应分组。

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
