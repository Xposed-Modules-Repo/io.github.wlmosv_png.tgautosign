<div align="center">

# TGAutoSign · Telegram 自动签到

Telegram 每日自动签到 Xposed 模块：自动发送签到指令或重放回调按钮，断网自动补签，支持官方版 / 官网直连版 / Nagram XF 等多客户端，全部管理在客户端内发 `/jmb` 完成。

[![Latest Release](https://img.shields.io/github/v/release/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign?label=%E6%9C%80%E6%96%B0%E7%89%88%E6%9C%AC&color=blue)](https://github.com/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/total?label=%E4%B8%8B%E8%BD%BD%E9%87%8F&color=brightgreen)](https://github.com/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/releases)
[![API](https://img.shields.io/badge/libxposed-API%20102-8A2BE2)](https://github.com/LSPosed/LSPlant)
[![License](https://img.shields.io/badge/license-GPLv3-green)](LICENSE)

**⬇️ [下载最新版 APK](https://github.com/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/releases/latest)** · [全部版本](https://github.com/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/releases) · [源码仓库](https://github.com/wlmosv-png/TGAutoSign)

作者 **wlmosv** · 觉得好用的话 [给源码仓库点个 Star ⭐](https://github.com/wlmosv-png/TGAutoSign) 就是更新的动力

</div>

---

## 📱 界面一览

| 暗色 · 主面板 | 日间 · 主面板 |
| --- | --- |
| ![暗色主面板](https://raw.githubusercontent.com/wlmosv-png/TGAutoSign/master/docs/screenshots/main-dark.jpg) | ![日间主面板](https://raw.githubusercontent.com/wlmosv-png/TGAutoSign/master/docs/screenshots/main-light.jpg) |
| 自诊断 | 使用教程 |
| ![自诊断](https://raw.githubusercontent.com/wlmosv-png/TGAutoSign/master/docs/screenshots/diagnose-dark.jpg) | ![使用教程](https://raw.githubusercontent.com/wlmosv-png/TGAutoSign/master/docs/screenshots/tutorial-light.jpg) |

---

## ✨ 特性

### 🧭 签到核心

- **每日一签**：每天只签一次，成功即停；打开 Telegram 发现已全部签过会提示「今天已经签到过了 ✅」
- **断网补签**：启动 / 定时(30min) / 打开聊天 / 网络恢复 自动补签，每天每目标最多 5 次（新的一天自动重置计数）
- **回复语义判定**：bot 回复含「失败 / 请先 / 已过期…」→ 撤销已签并按 5m→15m→45m→2h→4h 指数退避重试；限流 420/FLOOD_WAIT 尊重等待秒数
- **自动学习（默认关闭）**：可在设置打开「点一下按钮即加入」；即便开启，默认也只收录文案命中关键词的按钮，杜绝误加。网络层同步识别签到指令（仅 bot、含关键词）
- **回调按钮签到（v1.3.1 起）**：inline 回调按钮（点击不发文本、只改卡片）也能自动签到，点一次即学习、之后每天自动重放
- **Live Panel 实时面板引擎（v1.5.0）**：持续跟踪 bot 最新面板，重放前按「data 精确 > 文本一致 > 最近点击」自适应匹配最新 msg_id；一次性按钮被点废后自动拉新面板重试
- **一个 bot 多条指令（v1.3.0+）**：同一 bot 的不同签到指令、文本与回调按钮可并存，各自独立签到、独立状态、独立重试
- **全账号签到（v1.3.0+）**：`/jmb → 🌐 签全部账号` 一次跑完所有已激活账号，各账号目标集与数据完全隔离
- **多账号感知**：切换账号自动重载目标，数据按账号隔离，互不覆盖

### 🛡️ 可靠性

- **防风控保护（v1.5.0）**：bot 不回执 15 分钟长退避 + 当日上限 2 次；单账号每日动作上限；目标可暂停一周；签到动作带随机间隔
- **多客户端（v1.2.2+）**：官方版 / 官网直连版 / Telegram-Android 系第三方 fork 均可注入，详见下方支持矩阵
- **作用域自动申请（v1.4.3+）**：已知 Telegram 客户端自动申请进作用域，系统通知一键确认；换手机 / 出新 fork / 重装客户端不再手动翻列表
- **纯本地**：无服务器、无遥测，数据仅存于本机 SharedPreferences

### 🛠️ 体验

- **Telegram 内管理界面**：任意聊天发 `/jmb`，弹出管理菜单（目标列表 / 添加 / 删除 / 立即签到 / 全部签到 / 运行日志 / 设置 / 检查更新 / 导出配置 / 导入配置 / 导出运行日志），无需独立 App
- **回调可控化（v1.4.0）**：🔘 捕获列出按钮点选绑定（不受关键词限制）；目标可带前置命令序列；🔬 调试台 / 🧪 测试 即时看 bot 返回；🔁 旧回调一键重绑
- **跨账号复制目标（v1.4.2+）**：一键把当前账号的签到目标同步给其它账号，同 bot 同指令自动跳过并报告跳过数
- **运行日志（v1.4.2 重做）**：错误 / 警告 / 成功 / 普通 / 调试 五级；支持搜索、按级别筛选、正序倒序切换、长按单行复制、一键清空；日志同时落盘（约 1.3MB 上限，自动轮转）
- **内置检查更新（v1.2.1+）**：启动静默检查（12 小时冷却）；`/jmb → 🔄 检查更新` 可强制查看版本、更新说明与大小，一键下载到系统「下载」目录后交给系统安装器确认
- **配置导出 / 导入（v1.2.1+）**：签到目标、关键词、重试上限、当天签到状态存成 json；换账号 / 换手机不用重新学习目标；导入只合并不清空
- **日志导出（v1.2.3+）**：`/jmb → 🧾 导出运行日志` 写到系统「下载」目录，方便反馈问题

---
## 🖥️ 支持的客户端

适配 Telegram **12.10.x** 全系（含 12.10.3，对话框自动兼容）。模块先按宿主包名判定，再按标志类能力兜底，命中才注入：

| 客户端 | 包名 | 状态 |
| --- | --- | --- |
| Telegram（Play / 默认渠道） | `org.telegram.messenger` | ✅ 长期实测 |
| Telegram（官网直连版） | `org.telegram.messenger.web` | ✅ 12.10.1 静态逐项核对（issue #1） |
| Nagram XF | `fork.risin42.nagramx` | ✅ dec46b0 实测 · 30dcd6c 构建暂不兼容 |
| ExteraLess（ExteraGram fork） | `com.exteraless.app` | ✅ 12.10.1-feae791 实测 |
| Nagram / NagramX / NagramNX | `nu.gpu.nagram` 等 | 白名单覆盖，未实测 |
| 其它 Telegram-Android 系 fork | 任意包名 | 能力探测：标志类齐全即注入 |
| Telegram X | — | ❌ 不注入（换内核，标志类不齐全） |

> ⚠️ **作用域**：LSPosed 里默认只勾了官方版。用官网直连版 / Nagram XF 等第三方客户端，请在 LSPosed 中把**对应客户端**也勾进模块作用域（`Hosts` 只决定「勾了之后注不注入」）。

---

## 📲 安装

1. 需要 **Xposed 环境（libxposed API 102+）**、设备已 Root
2. 点上方 **⬇️ 下载最新版** 安装 APK（老用户**直接覆盖安装**，签到数据不丢）
3. LSPosed 模块管理器 → **模块** → 启用 **TGAutoSign**
4. 作用域勾选你实际在用的 Telegram 客户端（见上方支持矩阵）
5. 完全停止 Telegram 后重新打开，任意聊天发 `/jmb` 即可管理

---

## 🚀 使用

1. 在签到机器人的聊天里，手动**点一次签到按钮**（按钮文案需包含「设置」里配置的关键词）
   - 弹 `✅ 已添加新签到目标: xxx` → 文本指令型；弹 `✅ 已添加回调签到目标: xxx` → 回调按钮型（v1.3.1）
2. 或发 `/jmb` → **➕ 添加目标**，手动填 bot ID + 签到指令（同一 bot 可加多条）
3. 之后每天全自动签到

### 管理菜单（/jmb）

| 菜单 | 功能 |
| --- | --- |
| 📋 目标列表 | 查看所有目标、今日状态与上次签到时间（显示 bot 用户名，🔘 标记为回调型） |
| ➕ 添加目标 | 文本指令（bot ID + 指令）或 🔘 捕获回调按钮（点选绑定，可多个） |
| 🗑 删除目标 | 按条目移除 |
| 🚀 立即签到 | 手动触发一轮签到；多目标时可一键全部签到 |
| 🌐 签全部账号 | 一次为所有已激活账号各签一轮（v1.3.0+） |
| 📄 运行日志 | 五级日志，支持搜索 / 筛选 / 复制 / 清空；落盘约 1.3MB 自动轮转 |
| ⚙️ 设置 | 关键词 / 重试上限 / 自动学习与关键词过滤开关 / 全局唤醒命令 |
| 🔄 检查更新 | 强制检查版本，发现新版可一键下载安装 |
| 📤 导出配置 | 目标与设置存成 json，换账号不用重学 |
| 📥 导入配置 | 列出候选备份，选「合并」或「覆盖」，不认识的键不写入 |
| 🧾 导出运行日志 | 写出到系统「下载」目录，便于反馈问题 |
| 🔬 回调调试台 | 列出当前面板全部按钮，点任意一个即时发一次并看返回 |
| 📖 使用教程 | 分节说明，首次自动弹一次 |
| 🩺 自诊断 | 反射锚点是否正常，排查第三方客户端 |
| 🧹 清空所有配置 | 跨全部账号彻底清除，仅保留设置 |

---

## 🛎️ Toast 含义

| Toast | 含义 |
| --- | --- |
| `TGAutoSign 注入成功: ...` | 模块已注入，正常工作 |
| `✅ 已添加新签到目标: xxx` | 记住了文本指令型签到 |
| `✅ 已添加回调签到目标: xxx` | 记住了回调按钮型签到（v1.3.1） |
| `✅ 签到成功: xxx` | 该目标今日签到已完成 |
| `⚠️ 签到失败，稍后自动重试` | 网络/服务端异常，会自动补 |
| `TGAutoSign 有新版本 vX.X.X` | 静默检查发现新版，去 /jmb 查看 |
| `今天已经签到过了 ✅` | 全部目标今日已签，无需重复 |

---

## ❓ FAQ

**Q：点了按钮没有添加？**
A：v1.4.0 起「点一下即自动加入」默认关闭（防误加）。请用 `/jmb` → ➕ 添加目标 → 🔘 捕获回调 / ⌨️ 文本指令 手动加，或在设置里打开「自动学习」。若已开仍不加：检查是否命中关键词、作用域是否勾选、并完全停止 Telegram 重开。

**Q：机器人是点按钮不发文字的那种（inline 回调按钮），能自动签吗？**
A：能，v1.3.1 起支持。点一次该按钮即自动学习（列表里带 🔘 标记），之后每天自动重放回调完成签到。若按钮是打开网页或游戏类（无回调数据），不会误学。

**Q：一个 bot 有两条签到指令（比如「签到」和「签到2」）怎么办？**
A：v1.3.0 起同一 bot 可登记多条目标，各自独立签到与重试；点按钮学习和手动添加都按条目区分。

**Q：官方版能用，官网直连版 / Nagram XF 用不了？**
A：模块已支持这些客户端（见支持矩阵），但作用域默认只勾了官方版——到 LSPosed 里把对应客户端勾进模块作用域，再完全停止 Telegram 重开。

**Q：多账号会互相干扰吗？**
A：不会。目标、已签状态、重试全部按账号隔离；需要一次跑完所有号请用 `🌐 签全部账号`。

**Q：在电脑端签过，手机会重复签吗？**
A：手机模块只能感知手机端行为，以手机端为准。

**Q：如何清除已学习的目标？**
A：`/jmb` → 🗑 删除目标逐条移除；删不干净时用 `/jmb` → 🧹 清空所有配置（跨全部账号彻底清、重开 TG 不再复活）。

**Q：换手机 / 换账号怎么迁移？**
A：旧环境 `/jmb → 📤 导出配置`；新环境把 json 放进 `Android/data/org.telegram.messenger/files/tgautosign/` 后 `/jmb → 📥 导入配置`。导入只合并不清空。

**Q：检查更新没反应？**
A：静默检查有 12 小时冷却，请用 `/jmb → 🔄 检查更新` 手动强制查；用户侧网络到 GitHub 不通时检查/下载会失败，可手动到本页 Release 下载。

**Q：升级提示「与已安装应用签名不同」？**
A：说明装到了调试包。请先卸载再装本页正式版；正式包之间可直接覆盖升级，签到数据不丢。

---

## 🐞 反馈与问题提交

用 `[新建 Issue](https://github.com/wlmosv-png/TGAutoSign/issues)` 提交，请务必带两样东西：
1. `/jmb → 📄 运行日志`（或 `🧾 导出运行日志` 生成的 txt）
2. 客户端名称与版本（如 Nagram XF 12.10.1-dec46b0）

v1.5.0 起 `processUpdate*` 首参容器解包，面板采集与回复语义判定链路已恢复生效；若你的宿主仍显示 0 命中告警，请把日志发我。
Nagram XF `30dcd6c` 构建存在兼容问题（注入后启动无响应），暂不注入；`dec46b0` 及更早构建正常。
Telegram 12.10.3 起对话框自动降级为主题化系统框（功能不受影响）。

---

## 📜 更新日志

### v1.5.2 (115) —— 签到时间窗 + 连续签到日历 + 界面体验升级

- 🕐 **每日签到窗口**：设置可配（如 08:00-10:00），窗口外自动跳过、窗口内准点补签（秒级排程 + 随机偏移防风控）
- 📅 **连续签到日历**：首页显示连续天数 + 最近 14 天打卡格子（绿=已签），旧记录自动兼容
- 📚 **预设模板**：主菜单新增，常用签到指令一键添加（bot ID / 指令可改）
- ✨ **界面体验升级**：面板开启动效（顶部扫光、命令行打字机、光标闪烁、状态呼吸灯、内容渐进显现）、标题字符动态效果、按钮按压反馈；15 秒内重复打开秒开
- 🧱 主菜单改双排网格；修复新版 Telegram 主面板无法滚动
- 🔌 兼容 Telegram 12.10.3；新增 ExteraLess 第三方支持（见支持矩阵）

### v1.5.1 (114) —— 界面主题化 + 更新判定修复

- 🎨 终端风色板主题化：日间模式 = 浅灰蓝卡片 + 深色文字 + 高对比描边，暗色配色不变；深浅色判定跟随 TG 主题开关
- 🔧 修复「永远显示可更新」：版本号统一到 114 / 1.5.1（build.gradle / UpdateChecker / module.prop 三处同步 + 构建守卫）

<details>
<summary>📦 历史版本（9 个）</summary>

### v1.5.0 (113) —— 回调协议修复 + 实时面板引擎

- 🔴 修复 `TL_messages_getBotCallbackAnswer` 缺 `flags` 位 → 全 bot 回调 `DATA_INVALID`（协议层根因）
- 🔴 `processUpdate*` 首参容器解包 → 面板采集 + 回复语义判定链路恢复生效
- ➕ Live Panel 实时面板引擎：自适应匹配最新面板，一次性按钮自动拉面板重试
- ➕ 可靠性：bot 不回执 15 分钟长退避 + 每日上限；单账号每日动作上限；目标可暂停一周
- 🎨 终端风深色界面：实时日志卡、快捷命令行、`/jmb log`、`/jmb update`

### v1.4.3 (112) —— 作用域自动申请 + 自诊断

- ➕ 已知 Telegram 客户端自动申请进作用域，系统通知一键确认
- 🩺 自诊断逐项判定：三个标志类缺失时直接报名字、写明跳过原因
- 🔧 延续 1.4.2 修复收口

### v1.4.2 (111) —— 调度修正 + 运行日志重做

- 🔧 修复同一天退避/重试上限失效、「签全部账号」只签第一个、账号切换状态串号、线程安全与僵尸目标
- ➕ 跨账号复制目标、五级运行日志（搜索/筛选/落盘轮转）、导入配置重做

### v1.4.0 —— 回调可控化大改版

- ➕ 回调捕获 / 绑定 / 调试台 / 测试 / 前置命令 / 重绑全套；自动学习默认关闭防误加
- 🔧 删除配置彻底化 + 🧹 清空所有配置；卡片化界面 + 使用教程 + 自诊断

### v1.3.0 —— 回调按钮 + 多指令 + 全账号

- ➕ 回调按钮自动签到、同一 bot 多目标并存、`🌐 签全部账号`
- 🔧 已签标记正确撤销、退避重试生效；数据格式向后兼容

### v1.2.3 —— 签到可靠性修复

- 🔧 重试跨天不重置、失败后已签未撤销、FLOOD_WAIT 尊重等待秒数、processUpdate 改名适配
- ➕ 导出运行日志、一键全部签到、目标列表显示 bot 用户名

### v1.2.2 —— 多客户端支持

- ➕ 官方版 / 官网直连版 / Nagram XF 白名单 + 标志类能力探测

### v1.2.1

- ➕ 内置检查更新（12 小时冷却 + 手动强查）、配置导入导出
- 🔒 签名信息改为环境变量注入

### v1.2.0

- 🔧 修复签到不发送（getInputPeer 反射参数类型）、关键词过滤、适配 TG 12.10.1

</details>

完整变更见 [源码仓库 CHANGELOG](https://github.com/wlmosv-png/TGAutoSign/blob/master/CHANGELOG.md)。

---
-

## 🔗 下载渠道

| 渠道 | 地址 | 说明 |
| --- | --- | --- |
| **本页 Releases**（推荐） | [releases/latest](https://github.com/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/releases/latest) | 模块仓库镜像，模块内检查更新第一跳 |
| 源码仓库 Releases | [wlmosv-png/TGAutoSign](https://github.com/wlmosv-png/TGAutoSign/releases) | 同一份 APK，兜底通道 |
| 模块内直达 | Telegram 发 `/jmb` → 🔄 检查更新 | 自动列出新版并下载到「下载」目录 |

> 同一版本两个仓库的 APK 逐字节一致（`sha256sum.txt` 附在 Release 里），签名始终是同一把 release key，覆盖安装不丢数据。

---

## ⚖️ 许可

本项目基于 **GPLv3** 许可开源，仅供个人学习与自有账号使用。
请遵守 Telegram 服务条款及各群组/机器人规则。

---

<p align="center"><sub>Made with ❤️ by wlmosv · <a href="https://github.com/wlmosv-png/TGAutoSign">点个 Star ⭐ 是持续更新的动力</a></sub></p>
