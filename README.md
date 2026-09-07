<div align="center">
> **TGAutoSign** · Telegram 每日自动签到模块

# TGAutoSign · Telegram 每日自动签到

**让签到机器人自动打卡，每天只签一次，断网自动补。**

`Xposed` · `LSPosed` · `libxposed API 102`

[![Version](https://img.shields.io/badge/version-v1.0.0-blue?style=flat-square)](https://github.com/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/releases)
[![API](https://img.shields.io/badge/libxposed-API%20102-8A2BE2?style=flat-square)](https://github.com/LSPosed/LSPlant)
[![License](https://img.shields.io/badge/license-GPLv3-green?style=flat-square)](LICENSE)

作者：**wlmosv** · [源码仓库](https://github.com/wlmosv-png/TGAutoSign)

</div>

---

## ✨ 特性

- **自动学习**：手动点一次机器人的签到按钮，模块自动记住「机器人 + 签到指令」，无需任何配置
- **每日一签**：每天只签一次，签到请求发出成功即判定完成，**当天绝不再发**
- **已签提示**：打开 Telegram 发现今天已全部签过 → 提示「今天已经签到过了 ✅」
- **断网补签**：失败/断网自动重试，网络恢复立即补签，每天每目标最多 5 次
- **多目标**：支持多个签到机器人同时托管，每个目标独立记录，互不干扰
- **纯本地**：无服务器、无遥测，数据仅存于本机 SharedPreferences

---

## 🧠 工作原理（为什么不用猜指令）

不同机器人的签到指令五花八门（`📅 签到`、`/qd`、`/checkin`…），模块 **不猜不匹配文本**，而是：

1. **观察真实网络请求**：按钮点击最终都会变成一条真实消息请求（`TL_messages_sendMessage`），模块在 `ConnectionsManager.sendRequest` 处 Hook；
2. **自动识别**：当 **未登记** 的机器人（`user.bot == true`）收到一条 **≤20 字符的短指令**，判定为"又一个签到按钮"，自动加入目标；
3. 之后每天向每个目标发送其各自的签到指令。

---

## 📲 安装

1. 需要 **LSPosed / Vector**（API ≥ 102）环境，且设备已 Root
2. 安装 APK（本模块**无界面**，安装后不需要打开）
3. LSPosed 管理器 → **模块** → 启用 **TGAutoSign**
4. **作用域勾选 `Telegram（org.telegram.messenger）`**
5. 完全关闭 Telegram 后重新打开
6. 看到 Toast **「TGAutoSign 注入成功: org.telegram.messenger」** → 注入完成 ✅

> 仅支持官方 Telegram。第三方客户端（Nekogram 等）以及 iOS 版不受影响。

---

## 🚀 使用（三步上手）

1. **重启 Telegram**（模块加载，此时还不认识任何目标）
2. 打开签到机器人的聊天页，**手动点一次签到按钮**
   - 屏幕弹出 `✅ 已添加新签到目标: xxx` → 学习成功
   - 部分按钮网络层也会自动识别，弹出 `✅ 已自动添加新签到目标`
3. 把所有要签到的机器人各点一次，之后全自动

---

## 🛎️ Toast 含义

| Toast | 含义 |
|---|---|
| `TGAutoSign 注入成功: ...` | 模块已注入，正常工作 |
| `✅ 已添加新签到目标: xxx` | 记住了一个新机器人及指令 |
| `✅ 签到成功: xxx` | 该目标今日签到请求已发出 |
| `⚠️ 签到失败，稍后自动重试` | 网络/服务端异常，会自动补 |
| `今天已经签到过了 ✅` | 全部目标今日已签，无需重复 |

---

## ❓ FAQ

**Q：点了按钮没有添加 Toast？**
A：确认作用域勾选后**完全杀掉 Telegram 重开**；再看 LSPosed 日志里 `TGAutoSignModule` 标签的输出。若机器人按钮打开的是网页（WebApp）而非发送消息，则不属于可自动识别范围。

**Q：在电脑端签过，手机会重复签吗？**
A：手机模块只能感知手机端行为。若常在电脑端签到，建议该机器人也保存在手机端，或接受"以手机端为准"。

**Q：如何清除已学习的目标？**
A：在 LSPosed 中停用模块，或清除 Telegram 应用数据；也可在设置里清除模块偏好（`tg_autosign_gen`）。

**Q：为什么有时候不弹"签到成功"？**
A：签到指令已发出即标记成功（防止重复打扰机器人），只有网络失败才回弹失败提示。

---

## 📜 更新日志

### v2.0.0（2026-09-08）— 界面版

- App 界面：主页状态卡（注入检测 / 今日已签进度）、目标列表（改指令 / 重置 / 删除 / 手动签到）、实时日志页、设置页（关键词 / 重试上限 / 通知开关）
- 手动添加目标：填 bot ID + 指令，立即入列并触发签到
- 签到结果走系统通知栏；桌面小组件显示今日进度
- 模块与 App 跨进程通信改广播桥（此前文件共享、ContentProvider 都跨不过包权限），App 现在能实时看到注入状态和全部运行数据
- 旧版学习数据自动迁移，不用重新学
- 详细经过见源码仓库 [CHANGELOG](https://github.com/wlmosv-png/TGAutoSign/blob/master/CHANGELOG.md)

### v1.1.0（2026-09-08）— 稳定性与成功率增强

- **回调型按钮识别**（`TL_messages_getBotCallbackAnswer`）：识别 callback_data 型签到机器人并明确提示，不再静默漏签
- **Bot 回复语义判定**（hook `MessagesController.processUpdate`）：回复含失败关键词（失败/请先/无法/已过期…）→ 自动撤销已签标记并退避重试
- **错误分类**：永久错误（PEER_ID_INVALID 等）当日放弃；420/FLOOD_WAIT 限流 60s 后重试且不占次数
- **指数退避**：失败后 5min → 15min → 45min → 2h → 4h 放宽重试
- **账号切换感知**：切换账号自动重载目标列表
- **启动补签 10s**：等 MTProto 连接就绪，减少首发失败
- **双触发去重**：修复 sendRequest 多重载导致日志 ×2 的问题
- **学习关键词补全**：`/qd,/qiandao,/sign`

### v1.0.0（2026-09-07）

- 首个公开版本
- 自动学习签到目标（UI 点击 + 网络层双通道）
- 每日一签、成功即停、已签提示
- 断网补签：网络恢复 / 打开聊天 / 30 分钟兜底轮询

---

## ⚖️ 许可

本项目基于 **GPLv3** 许可开源，仅供个人学习与自有账号使用。
请遵守 Telegram 服务条款及各群组/机器人规则。

---

<p align="center"><sub>Made with ❤️ by wlmosv</sub></p>