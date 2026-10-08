<div align="center">

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://cdn.jsdelivr.net/gh/wlmosv-png/TGAutoSign@master/docs/banner-dark.svg">
    <source media="(prefers-color-scheme: light)" srcset="https://cdn.jsdelivr.net/gh/wlmosv-png/TGAutoSign@master/docs/banner-light.svg">
    <img src="https://cdn.jsdelivr.net/gh/wlmosv-png/TGAutoSign@master/docs/banner-light.svg" alt="TGAutoSign" width="100%">
  </picture>
</p>

<p align="center"><b>中文</b> · <a href="https://github.com/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/blob/main/README.en.md">English</a></p>

**点一次，签一年。**  ·  *Tap once. Signed every day.*

在 Telegram 里点一下它的签到按钮 —— 之后再也不用管。

回调按钮、文本指令、群签到都支持；签到窗口、断网补签、多账号隔离、限流退避内置。
管理面板就在 Telegram 内 —— 任意聊天发 `/jmb`。

[![Latest Release](https://img.shields.io/github/v/release/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign?label=%E6%9C%80%E6%96%B0%E7%89%88%E6%9C%AC&labelColor=3d3d3d&color=8e44ad)](https://github.com/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/total?label=%E4%B8%8B%E8%BD%BD%E9%87%8F&labelColor=3d3d3d&color=8e44ad)](https://github.com/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/releases)
[![API](https://img.shields.io/badge/libxposed-API%20102-8e44ad?labelColor=3d3d3d)](https://github.com/LSPosed/LSPlant)
[![License](https://img.shields.io/badge/license-GPLv3-8e44ad?labelColor=3d3d3d)](https://github.com/wlmosv-png/TGAutoSign/blob/master/LICENSE)
[![Telegram Group](https://img.shields.io/badge/Telegram-Join%20Group-8e44ad?labelColor=3d3d3d&logo=telegram&logoColor=white)](https://t.me/+V2Oyu8pSubs4ZjE0)

**[下载最新版 APK](https://github.com/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/releases/latest)** · [源码仓库](https://github.com/wlmosv-png/TGAutoSign)

<sub>只从这两个地址下载。第三方站点的转载包请用下方指纹自行比对。</sub>

作者 **wlmosv** · 好用的话 [给源码仓库点个 Star](https://github.com/wlmosv-png/TGAutoSign)

</div>

---

### 本地运行 · Local by design

<sub>无需账号密码、不碰官方 API、数据全在设备上。</sub>

- **唯一联网行为**是每 12 小时一次的更新检查，可在设置中关闭，不携带任何签到数据
- 签到目标与已签状态存在 Telegram 进程的本地存储，**不离开设备**
- 模块**不申请**存储、通知、安装权限；自动化操作全部在设备侧完成，不经任何中转服务器


<details>
<summary><b>验证方式与签名指纹</b> · <i>Verify the build</i></summary>

<br>

官方 APK 签名证书 · *official signing certificate*

```
SHA-256  AF:55:24:CD:55:4A:E6:ED:E3:EC:27:47:C7:BE:D1:59
         B0:9B:C4:F6:A4:32:44:A6:8B:46:22:E9:46:32:25:C8
SHA-1    58:A2:B4:D3:F2:83:9A:92:7A:D4:0C:23:51:FE:43:AB:6F:D3:FB:C3
```

自己核对 · *check it yourself*

```sh
keytool -printcert -jarfile TGAutoSign-*.apk   # 比对上面的指纹
sha256sum TGAutoSign-*.apk                     # 比对 Release 里的 sha256sum.txt
```

全仓库只有 `update/UpdateChecker.java` 一个类发起网络连接，可直接审计。
指纹对应 2026-09 起使用的 release key；若将来更换密钥，会在 Release 说明中公告。

> ⚠️ **风险提示** · *Risk notice* — 任何 Telegram 自动化都存在账号被限制的可能。本模块采用客户端侧签到、随机时窗与退避策略，已尽可能平滑，但**不承诺零风险**。

</details>

---

## 界面一览 · Screenshots

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://cdn.jsdelivr.net/gh/wlmosv-png/TGAutoSign@master/docs/hero-dark.png">
    <source media="(prefers-color-scheme: light)" srcset="https://cdn.jsdelivr.net/gh/wlmosv-png/TGAutoSign@master/docs/hero-light.png">
    <img src="https://cdn.jsdelivr.net/gh/wlmosv-png/TGAutoSign@master/docs/hero-light.png" alt="TGAutoSign 界面一览" width="100%">
  </picture>
</p>

**主面板** · **目标列表** — 截图由模块自带的 `/jmb shots` 导出，非手工截屏；目标名已替换为占位文本。

**英文界面 · English UI** — 内置，无需设置，英文设备装上即是英文

同一页面的暗色 / 亮色对照

| 主面板 · 暗色 | 主面板 · 亮色 |
| --- | --- |
| ![主面板·暗色](https://cdn.jsdelivr.net/gh/wlmosv-png/TGAutoSign@master/docs/screenshots/shot-main-dark.png) | ![主面板·亮色](https://cdn.jsdelivr.net/gh/wlmosv-png/TGAutoSign@master/docs/screenshots/shot-main-light.png) |

| 目标列表 · 暗色 | 目标列表 · 亮色 |
| --- | --- |
| ![目标列表·暗色](https://cdn.jsdelivr.net/gh/wlmosv-png/TGAutoSign@master/docs/screenshots/shot-targets-dark.png) | ![目标列表·亮色](https://cdn.jsdelivr.net/gh/wlmosv-png/TGAutoSign@master/docs/screenshots/shot-targets-light.png) |

| 设置 · 暗色 | 设置 · 亮色 |
| --- | --- |
| ![设置·暗色](https://cdn.jsdelivr.net/gh/wlmosv-png/TGAutoSign@master/docs/screenshots/shot-settings-dark.png) | ![设置·亮色](https://cdn.jsdelivr.net/gh/wlmosv-png/TGAutoSign@master/docs/screenshots/shot-settings-light.png) |

## 它能做什么 · What it does

| 能力 · Capability | 说明 · Description |
| --- | --- |
| **点一次就学会** · **Tap once, it learns** | 在 bot 里点一下签到按钮，之后每天自动重放；按钮 data 变了也跟得上<br>*Tap the bot's button once and it replays daily — even when the callback data changes.* |
| **文本指令也行** · **Text commands too** | 填 bot ID + 指令（如 `/checkin`），到点自动发<br>*Set bot ID + command (e.g. `/checkin`); sent on schedule.* |
| **群 / 频道签到** · **Group & channel check-ins** | 群 ID 同样支持，回复判定按群内消息走<br>*Group IDs supported; replies are read from group messages.* |
| **时间你说了算** · **Your schedule** | 签到窗口 · 每目标随机时刻 · 错开间隔 · 补签截止 · 暂停一周<br>*Window · per-target random slots · spacing · make-up deadline · pause a week.* |
| **不硬刚风控** · **Rate-limit friendly** | 失败退避 5m→15m→45m→2h→4h · 尊重 `FLOOD_WAIT` · 断网自动补签<br>*Backoff on failure · waits out `FLOOD_WAIT` · catches up when back online.* |
| **不想签的挡得住** · **Block what you don't want** | 关键词 / 正则规则 · 整只 bot 排除 · 单个目标冻结<br>*Keyword / regex rules · block a whole bot · freeze a single target.* |
| **多账号互不干扰** · **Multi-account, isolated** | 目标与已签状态按账号隔离；可一键把目标复制到其它账号<br>*Targets and signed-state are per account; copy targets across accounts.* |
| **每天一条摘要** · **Daily summary** | 发到自己的收藏夹，不弹系统通知；连续失败 3 天额外告警<br>*One message to your Saved Messages; alert after 3 failing days.* |
| **中英双语界面** · **Bilingual UI** | 英文设备装上即英文；设置里可手动切换<br>*English out of the box on English devices; switchable in Settings.* |
| **数据全在本地** · **Local by design** | 仅更新检查联网，可关闭<br>*Only the update check goes online — and it can be turned off.* |

---

## 支持的客户端 · Supported clients

模块先按宿主包名判定，再按标志类能力兜底，命中才注入。

<sub>**要求**：已 root + LSPosed（libxposed **API 102** 及以上，见 LSPosed Manager → 设置 → 关于）。**不支持**：未 root 设备、Telegram X、独立服务器部署。</sub>
*Matched by host package first, then by flag classes as fallback — only injects on a match.*

| 客户端 · Client | 包名 · Package | 状态 · Status |
| --- | --- | --- |
| Telegram（Play / 默认渠道）| `org.telegram.messenger` | ✅ 12.10.4 实测 · *tested* |
| Telegram（官网直连版）| `org.telegram.messenger.web` | ✅ 静态核对 · *statically verified* |
| Nagram（NextAlone）| `xyz.nextalone.nagram` | ✅ 12.10.3 实测 · *tested* |
| Nagram XF | `fork.risin42.nagramx` | ✅ dec46b0 实测 · *tested* |
| ExteraLess | `com.exteraless.app` | ✅ 12.10.1 实测 · *tested* |
| Mercurygram | `it.belloworld.mercurygram` | ✅ 12.10.3.1 实测 · *tested* |
| Turrit | `org.telegram.group` | ✅ 1.9.0.4.2 静态核对 · *statically verified* |
| Nagram / NagramX / NagramNX | `nu.gpu.nagram` 等 | 白名单覆盖，未实测 · *whitelisted, untested* |
| 其它 Telegram-Android fork | 任意 | 标志类齐全即注入 · *injects if flags intact* |
| Telegram X | — | ❌ 不注入（换内核）· *not injected* |

> ⚠️ **作用域 · Scope**：LSPosed 里默认只勾了官方版。用第三方客户端，请把**对应客户端**也勾进模块作用域。
> *LSPosed enables only the official client by default. Using a third-party client? Tick **that** client in scope too.*

---

## 30 秒上手 · 30-second setup

| 步骤 · Step | 做什么 · Do this |
| --- | --- |
| **1** | 装 APK → LSPosed → **模块** 里启用 TGAutoSign<br>*Install the APK → LSPosed → **Modules** → enable TGAutoSign* |
| **2** | **作用域**里勾选你在用的 Telegram 客户端<br>*Tick your Telegram client in **Scope*** |
| **3** | 完全停掉 Telegram，再重新打开<br>*Fully stop Telegram, then reopen it* |
| **4** | 任意聊天发 `/jmb` → 到 bot 会话**点一次它的签到按钮**<br>*Send `/jmb` in any chat → tap the button once in the bot chat* |

> 完成。之后每天自动签，想看状态随时发 `/jmb`。
> *Done. It signs daily from then on — send `/jmb` anytime to check.*

---

## 常见问题 · FAQ

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

## 更新日志 · Changelog

### v1.6.4 (130) — 2026-10-08

**修复**：机器人发个「签到规则」都可能被判成签到成功 · 群里机器人回复了，模块却说没等到 · 群里别人签到，算到了你头上 · 群 ID 少写一个「100」，这个群就永远认不出 · 机器人说「次数已达上限」，被当成没签上 · 自己发的签到，跑到「未识别回复」里等你判断 · 待添加列表里，同一条内容越滚越长 · 被拦下的按钮直接消失，找不回来 · 群里聊到「签到」两个字也被收集 · 打开日志会闪一下 · 目标列表和统计页，最后一行永远看不到 · 「未识别回复」页点一下卡一下 · 待添加显示「1 个」，点进去有好几个 · Turrit 装上模块却不生效 · 机器人说「签到失败，详见规则」被判成无法判断 · 「不是签到成功」这种带否定的话会被判错 · 机器人说「已封禁/禁止参与」被当成无法判断 · 更新下载更稳了

**新增**：「未识别回复」页重做 · 机器人认不出的回复，可以教它 · 点按钮不再「点什么学什么」 · 确认新目标时，可以顺手记住「以后怎么办」 · 像签到的按钮直接学，其余才问你

### v1.6.3 (129) — 2026-10-05

**修复**：按钮学习失效（本版最重要）——类型判据大小写敏感 · 气泡内按钮的回调类在官方版里已不存在 · `/help` 是句空话 · 按钮点了没反应且零日志 · 群目标当天重发 13 次 · 群聊重复发送 / 未识别「今日用尽」 · 「请求发出」被当成「签到成功」 · 漏签根因：判定与落盘不同源 · 无限递归导致 Telegram 卡死（ANR） · 每日摘要永远发不出 · 文字冒出「1970-01-01」 · 列表「少一行」与「整块空白」 · 统计页静默丢条目、各处尺寸被裁 · 开关看起来全是关的 · 切 Tab 后面板消失（严重） · 易懂档日志顺序倒置、「首页有、日志页没有」 · 日历摘要连签虚高、今日状态不可达 · 代码通读发现的四类问题

**变更**：界面整体重做：从「到处是框」改为「靠底色分层」 · `termBorder` 本体改为忽略描边参数 · 按钮分四级 · 日间色调转暖，浅色模式改用实色分层 · 设置页：多卡折叠 → 顶部锚点条 + 单卡 · 条目操作菜单：分组卡片 + 唯一主操作 · 编辑目标：标签外置 + 模板 chip 按宽度自动折行 · 排除管理：改为 ①②③④ 四步工作流 · 最近动态：时间定宽左列 + 图标槽 + 单行截断 · 统计页重做 · 账号一览改版 · 主面板减法

**新增**：规则测试器 · Turrit 适配 · 外部通知 · `/help` 命令 · 教程全面重写 · 界面主题跟随修复

[完整更新日志 →](https://github.com/wlmosv-png/TGAutoSign/blob/master/CHANGELOG.md)

## 许可 · License

基于 **GPLv3** 开源，仅供个人学习与自有账号使用。
请遵守 Telegram 服务条款及各群组 / 机器人规则。

*Licensed under **GPLv3**. For personal use with your own accounts.
Please respect Telegram's Terms of Service and each group's / bot's rules.*

---

<p align="center"><sub>Made by wlmosv · <a href="https://github.com/wlmosv-png/TGAutoSign">点个 Star 是持续更新的动力</a></sub></p>
