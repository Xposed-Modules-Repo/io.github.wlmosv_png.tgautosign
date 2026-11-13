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
| Telegram（Play / 默认渠道）| `org.telegram.messenger` | ✅ 13.1.1 实测 · **13.2.0 已适配** · *tested on 13.1.1; 13.2.0 adapted* |
| Telegram（官网直连版）| `org.telegram.messenger.web` | ✅ 实测 · **13.2.0 已适配** · *tested; 13.2.0 adapted* |
| Nagram（NextAlone）| `xyz.nextalone.nagram` | ✅ 12.10.3 实测 · *tested* |
| Nagram XF | `fork.risin42.nagramx` | ✅ 实测 · *tested* |
| ExteraLess | `com.exteraless.app` | ✅ 12.10.5 实测 · *tested* |
| Mercurygram | `it.belloworld.mercurygram` | ✅ 12.10.3.1 实测 · *tested* |
| Turrit | `org.telegram.group` | ✅ 1.9.0.4.2 实测 · *tested* |
| Nnngram（NextAlone）| `xyz.nextalone.nnngram` | ✅ 12.10.6 实测 · *tested* |
| AyuGram | `com.radolyn.ayugram` | ✅ 实测 · *tested* |
| Nagram / NagramX / NagramNX | `nu.gpu.nagram` 等 | ✅ 实测 · *tested* |
| 其它 Telegram-Android fork | 任意 | 标志类齐全即注入 · *injects if flags intact* |
| Telegram X | — | ❌ 不注入（换内核）· *not injected* |

**版本适配说明 · Version adaptation**：Telegram **13.2.0** 起 R8 不再保留 `org.telegram.messenger.*` 的类名（官方混淆规则删除了整包 keep），过去「按原名反射」的取数方式会整条失效。模块内置**宿主符号解析层**：旧版仍按原名直查（13.1.1 及更早、以及所有不混淆的第三方 fork 行为逐字不变），新版按结构指纹与版本映射解析，并对映射结果做结构校验 —— 校验不过就明确报「宿主版本未适配」并只保留 `/jmb` 命令与按钮学习，绝不假装适配成功。
*Since Telegram **13.2.0**, R8 no longer keeps `org.telegram.messenger.*` class names. The module ships a host-symbol resolution layer: legacy clients still resolve by original names (13.1.1 and older, plus all non-obfuscated forks, behave exactly as before); new builds resolve by structural fingerprints and a version map, and every mapped class is structurally verified. If verification fails the module reports "host version not supported" and keeps only the `/jmb` commands and button learning — it never fakes a successful adaptation.*

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

### v1.7.2 (172) — 2026-11-13

**新增**：宿主符号运行时自愈 · 符号解析失败时输出明确状态

**修复**：APK 条目未对齐导致 Android 11+ 拒绝安装 · 判定命中改取最强匹配，不再由词表顺序决定 · 文档类措辞不再吞掉明确结论 · 跨天状态泄漏导致目标被永久钉死 · 面板公告与额度判断的边界收紧

### v1.7.1 (171) — 2026-11-01

**修复**：目标固定时刻不再被全局窗口旁路 · 心跳不再绕过签到门禁 · 补签时段起点按目标时刻计算 · 面板公告不再被误判为签到失败 · 真失败句仍判失败

**新增**：手动撤销「今日已签」

**修复**：已有成功结论后，自动判定不再翻转它 · 已签目标不再进「未识别回复」池 · 撤销已签时同步清掉签到时刻 · 状态撕裂自愈 · 撤销动作全部留痕

**修复**：命令式重复提示现在直接判为已签

**界面**：撤销入口重做：一行一个「撤销」，点开再选 · 新增「已暂停」列表 —— 暂停不再等于消失 · 条目操作菜单显示真实状态 · 「标记为未签」也进了条目操作菜单

**工程**：补签判据新增目标维度重载 · 门禁补入触发策略测试 · 13 条真阳性用例

[完整更新日志 →](https://github.com/wlmosv-png/TGAutoSign/blob/master/CHANGELOG.md)

## 许可 · License

基于 **GPLv3** 开源，仅供个人学习与自有账号使用。
请遵守 Telegram 服务条款及各群组 / 机器人规则。

*Licensed under **GPLv3**. For personal use with your own accounts.
Please respect Telegram's Terms of Service and each group's / bot's rules.*

---

<p align="center"><sub>Made by wlmosv · <a href="https://github.com/wlmosv-png/TGAutoSign">点个 Star 是持续更新的动力</a></sub></p>
