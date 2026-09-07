<div align="center">

# TGAutoSign · Telegram 自动签到

**发 `/jmb` 管理一切：自动学习签到目标、每日一签、断网自动补。**

`Xposed` · `libxposed API 102`

[![Version](https://img.shields.io/badge/version-v1.2.0-blue?style=flat-square)](https://github.com/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/releases)
[![API](https://img.shields.io/badge/libxposed-API%20102-8A2BE2?style=flat-square)](https://github.com/LSPosed/LSPlant)
[![License](https://img.shields.io/badge/license-GPLv3-green?style=flat-square)](LICENSE)

作者：**wlmosv** · [源码仓库](https://github.com/wlmosv-png/TGAutoSign)

</div>

---

## ✨ 特性

- **Telegram 内管理界面**：任意聊天发 `/jmb`，弹出管理菜单（目标列表 / 添加 / 删除 / 立即签到 / 运行日志 / 设置），无需独立 App
- **自动学习**：点一次 bot 的签到按钮即自动记录（仅当按钮文案包含已配置关键词时添加）；网络层同步识别签到指令（仅 bot、含关键词）
- **每日一签**：每天只签一次，成功即停；打开 Telegram 发现已全部签过会提示「今天已经签到过了 ✅」
- **断网补签**：启动 / 定时(30min) / 打开聊天 / 网络恢复 自动补签，每天每目标最多 5 次
- **回复语义判定**：bot 回复含「失败 / 请先 / 已过期…」→ 自动撤销已签并指数退避重试（5m→15m→45m→2h→4h）；限流 420/FLOOD_WAIT 单独处理
- **多账号感知**：切换账号自动重载目标，数据按账号隔离
- **纯本地**：无服务器、无遥测，数据仅存于本机 SharedPreferences

---

## 📲 安装

1. 需要 **Xposed 环境（API 102+）**、设备已 Root
2. 安装本页 Release 中的 APK
3. Xposed 模块管理器 → **模块** → 启用 **TGAutoSign**
4. **作用域勾选 `Telegram（org.telegram.messenger）`**
5. 完全停止 Telegram 后重新打开

---

## 🚀 使用

1. 在签到机器人的聊天里，手动**点一次签到按钮**（按钮文案需包含「设置」里配置的关键词）
   - 弹出 `✅ 已添加新签到目标: xxx` → 学习成功
2. 或发 `/jmb` → **添加目标**，手动填 bot ID + 签到指令
3. 之后每天全自动签到

### 管理菜单（/jmb）

| 菜单 | 功能 |
|---|---|
| 📋 目标列表 | 查看所有目标与今日状态 |
| ➕ 添加目标 | 手动填 bot ID + 指令，立即签到 |
| 🗑 删除目标 | 移除不想自动签的 bot |
| 🚀 立即签到 | 手动触发一轮签到 |
| 📄 运行日志 | 最近 200 行运行日志 |
| ⚙️ 设置 | 关键词 / 每日重试上限 |

---

## 🛎️ Toast 含义

| Toast | 含义 |
|---|---|
| `TGAutoSign 注入成功: ...` | 模块已注入，正常工作 |
| `✅ 已添加新签到目标: xxx` | 记住了一个新机器人及指令 |
| `✅ 签到成功: xxx` | 该目标今日签到已完成 |
| `⚠️ 签到失败，稍后自动重试` | 网络/服务端异常，会自动补 |
| `今天已经签到过了 ✅` | 全部目标今日已签，无需重复 |

---

## ❓ FAQ

**Q：点了按钮没有添加？**
A：按钮文案必须包含「设置」里配置的关键词（默认含 签到/打卡/checkin 等），不含关键词的按钮一律不添加；确认作用域勾选后完全停止 Telegram 重开。

**Q：在电脑端签过，手机会重复签吗？**
A：手机模块只能感知手机端行为，以手机端为准。

**Q：如何清除已学习的目标？**
A：发 `/jmb` → 删除目标，点选移除即可。

---

## 📜 更新日志

### v1.2.0（2026-09-08）

- 🔧 修复签到不发送：`getInputPeer` 反射参数类型错误，此前手动 / 自动签到均静默失败
- 🔑 按钮学习增加关键词过滤：不含关键词的按钮一律不添加
- 🧩 适配 Telegram 12.10.1：按钮文案优先走 `getText()`，兼容新版按钮结构
- ➕ 设置页补全「保存」按钮

---

## ⚖️ 许可

本项目基于 **GPLv3** 许可开源，仅供个人学习与自有账号使用。
请遵守 Telegram 服务条款及各群组/机器人规则。

---

<p align="center"><sub>Made with ❤️ by wlmosv</sub></p>
