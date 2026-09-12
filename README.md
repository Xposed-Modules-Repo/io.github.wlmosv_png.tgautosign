<div align="center">

# TGAutoSign · Telegram 自动签到

**Telegram 每日自动签到 Xposed 模块** · *Telegram auto check-in module for LSPosed / libxposed*

发 `/jmb` 管理一切：自动学习签到目标、每日一签、断网自动补、内置更新与迁移。支持官方版 / 官网直连版 / Nagram XF 等 Telegram-Android 系客户端。

[![Latest Release](https://img.shields.io/github/v/release/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign?label=%E6%9C%80%E6%96%B0%E7%89%88%E6%9C%AC&color=blue)](https://github.com/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/total?label=%E4%B8%8B%E8%BD%BD%E9%87%8F&color=brightgreen)](https://github.com/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/releases)
[![API](https://img.shields.io/badge/libxposed-API%20102-8A2BE2)](https://github.com/LSPosed/LSPlant)
[![License](https://img.shields.io/badge/license-GPLv3-green)](LICENSE)

**⬇️ [下载最新版 APK](https://github.com/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/releases/latest)** · [全部版本](https://github.com/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/releases) · [源码仓库](https://github.com/wlmosv-png/TGAutoSign)

作者 **wlmosv** · 觉得好用的话 [给源码仓库点个 Star ⭐](https://github.com/wlmosv-png/TGAutoSign) 就是更新的动力

</div>

---

## ✨ 特性

- **Telegram 内管理界面**：任意聊天发 `/jmb`，弹出管理菜单（目标列表 / 添加 / 删除 / 立即签到 / 全部签到 / 运行日志 / 设置 / 检查更新 / 导出配置 / 导入配置 / 导出运行日志），无需独立 App
- **自动学习**：点一次 bot 的签到按钮即自动记录（仅当按钮文案包含已配置关键词时添加）；网络层同步识别签到指令（仅 bot、含关键词）
- **回调按钮签到（v1.3.0+）**：bot 用 inline 回调按钮（点击不发文本消息、只弹气泡或改卡片）也能自动签到——点一次按钮即学习，之后每天自动重放回调
- **一个 bot 多条指令（v1.3.0+）**：同一 bot 的不同签到指令、文本与回调按钮可并存，各自独立签到、独立状态、独立重试
- **全账号签到（v1.3.0+）**：`/jmb → 🌐 签全部账号` 一次跑完所有已激活账号，各账号目标集与数据完全隔离
- **每日一签**：每天只签一次，成功即停；打开 Telegram 发现已全部签过会提示「今天已经签到过了 ✅」
- **断网补签**：启动 / 定时(30min) / 打开聊天 / 网络恢复 自动补签，每天每目标最多 5 次（新的一天自动重置计数）
- **回复语义判定**：bot 回复含「失败 / 请先 / 已过期…」→ 自动撤销已签并指数退避重试（5m→15m→45m→2h→4h）；限流 420/FLOOD_WAIT 尊重服务器给出的等待秒数
- **多账号感知**：切换账号自动重载目标，数据按账号隔离，互不覆盖
- **多客户端（v1.2.2+）**：官方版 / 官网直连版 / Telegram-Android 系第三方 fork 均可注入，详见下方支持矩阵
- **内置检查更新（v1.2.1+）**：启动静默检查（12 小时冷却）；`/jmb → 🔄 检查更新` 可强制查看版本、更新说明与大小，一键下载到系统「下载」目录后交给系统安装器确认
- **配置导出 / 导入（v1.2.1+）**：签到目标、关键词、重试上限、当天签到状态存成 json；换账号 / 换手机不用重新学习目标；导入只合并不清空
- **日志导出（v1.2.3+）**：`/jmb → 🧾 导出运行日志` 写到系统「下载」目录，方便反馈问题
- **纯本地**：无服务器、无遥测，数据仅存于本机 SharedPreferences

---

## 🖥️ 支持的客户端

模块先按宿主包名判定，再按标志类能力兜底，命中才注入：

| 客户端 | 包名 | 状态 |
| --- | --- | --- |
| Telegram（Play / 默认渠道） | `org.telegram.messenger` | ✅ 长期实测 |
| Telegram（官网直连版） | `org.telegram.messenger.web` | ✅ 12.10.1 静态逐项核对（issue #1） |
| Nagram XF | `fork.risin42.nagramx` | ✅ 12.10.1-dec46b0 静态核对 + 真机实测通过（issue #2） |
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
   - 弹 `✅ 已添加新签到目标: xxx` → 文本指令型；弹 `✅ 已添加回调签到目标: xxx` → 回调按钮型（v1.3.0+）
2. 或发 `/jmb` → **➕ 添加目标**，手动填 bot ID + 签到指令（同一 bot 可加多条）
3. 之后每天全自动签到

### 管理菜单（/jmb）

| 菜单 | 功能 |
| --- | --- |
| 📋 目标列表 | 查看所有目标、今日状态与上次签到时间（显示 bot 用户名，🔘 标记为回调型） |
| ➕ 添加目标 | 手动填 bot ID + 指令，立即签到（同一 bot 可加多条指令） |
| 🗑 删除目标 | 按条目移除 |
| 🚀 立即签到 | 手动触发一轮签到；多目标时可一键全部签到 |
| 🌐 签全部账号 | 一次为所有已激活账号各签一轮（v1.3.0+） |
| 📄 运行日志 | 最近 200 行运行日志 |
| ⚙️ 设置 | 学习关键词 / 每日重试上限 |
| 🔄 检查更新 | 强制检查版本，发现新版可一键下载安装 |
| 📤 导出配置 | 目标与设置存成 json，换账号不用重学 |
| 📥 导入配置 | 读最新导出文件，只合并不清空 |
| 🧾 导出运行日志 | 写出到系统「下载」目录，便于反馈问题 |

---

## 🛎️ Toast 含义

| Toast | 含义 |
| --- | --- |
| `TGAutoSign 注入成功: ...` | 模块已注入，正常工作 |
| `✅ 已添加新签到目标: xxx` | 记住了文本指令型签到 |
| `✅ 已添加回调签到目标: xxx` | 记住了回调按钮型签到（v1.3.0+） |
| `✅ 签到成功: xxx` | 该目标今日签到已完成 |
| `⚠️ 签到失败，稍后自动重试` | 网络/服务端异常，会自动补 |
| `TGAutoSign 有新版本 vX.X.X` | 静默检查发现新版，去 /jmb 查看 |
| `今天已经签到过了 ✅` | 全部目标今日已签，无需重复 |

---

## ❓ FAQ

**Q：点了按钮没有添加？**
A：按钮文案必须包含「设置」里配置的关键词（默认含 签到/打卡/checkin 等），不含关键词的按钮一律不添加；确认作用域勾选后完全停止 Telegram 重开。

**Q：机器人是点按钮不发文字的那种（inline 回调按钮），能自动签吗？**
A：能，v1.3.0 起支持。点一次该按钮即自动学习（列表里带 🔘 标记），之后每天自动重放回调完成签到。若按钮是打开网页或游戏类（无回调数据），不会误学。

**Q：一个 bot 有两条签到指令（比如「签到」和「签到2」）怎么办？**
A：v1.3.0 起同一 bot 可登记多条目标，各自独立签到与重试；点按钮学习和手动添加都按条目区分。

**Q：官方版能用，官网直连版 / Nagram XF 用不了？**
A：模块已支持这些客户端（见支持矩阵），但作用域默认只勾了官方版——到 LSPosed 里把对应客户端勾进模块作用域，再完全停止 Telegram 重开。

**Q：多账号会互相干扰吗？**
A：不会。目标、已签状态、重试全部按账号隔离；需要一次跑完所有号请用 `🌐 签全部账号`。

**Q：在电脑端签过，手机会重复签吗？**
A：手机模块只能感知手机端行为，以手机端为准。

**Q：如何清除已学习的目标？**
A：发 `/jmb` → 🗑 删除目标，点选条目移除即可。

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

已知限制（TG 12.10.x）：`MessagesController.processUpdate` 已改名 `processUpdateArray`，v1.2.3 起按前缀 hook，新版宿主可正常命中；若你的宿主仍显示 0 命中告警，请把日志发我。

---

## 📜 更新日志

### v1.3.0（2026-09-11）—— 回调按钮 + 多指令 + 全账号

- ➕ **回调按钮（inline button）自动签到**：点一次按钮学习，之后每天自动重放回调
- ➕ **同一 bot 多条目标并存**：不同指令 / 文本+回调混合，各自独立状态与重试
- ➕ **`/jmb → 🌐 签全部账号`**：遍历所有已激活账号，各用各的目标集
- 🔧 签到请求失败的「已签」标记现在会正确撤销，退避重试真正生效
- 🧪 数据格式向后兼容：v1.2.x 的目标与已签状态原样保留，覆盖安装即可

### v1.2.3（2026-09-10）—— 签到可靠性修复

- 🔧 修复：重试计数跨天不重置（此前用完当日上限后目标永久停签）
- 🔧 修复：签到请求失败后「已签」标记未撤销，退避重试实际不生效
- 🔧 修复：FLOOD_WAIT 尊重服务器要求的等待秒数，不再固定 60 秒空转
- 🔧 修复：`processUpdate` 改名 `processUpdateArray` 后回复语义判定失效（TG 12.10.1+）
- ➕ 新增：🧾 导出运行日志；目标列表显示 bot 用户名与上次签到时间；🚀 一键全部签到

### v1.2.2（2026-09-10）—— 多客户端支持

- ➕ 新增 `Hosts` 宿主判定：官方版 / 官网直连版 / Nagram XF 白名单 + 标志类能力探测
- 📋 运行日志标注宿主与命中方式

### v1.2.1（2026-09-08）

- ➕ 内置检查更新（12 小时冷却 + 手动强查 + 一键下载安装）
- ➕ `/jmb → 📤 导出配置 / 📥 导入配置`
- 🔒 签名信息改为环境变量注入，仓库不再留存口令

### v1.2.0（2026-09-08）

- 🔧 修复签到不发送：`getInputPeer` 反射参数类型错误
- 🔑 按钮学习增加关键词过滤
- 🧩 适配 Telegram 12.10.1

完整变更见 [源码仓库 CHANGELOG](https://github.com/wlmosv-png/TGAutoSign/blob/master/CHANGELOG.md)。

---

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
