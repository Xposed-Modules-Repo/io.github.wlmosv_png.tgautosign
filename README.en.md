<div align="center">

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://cdn.jsdelivr.net/gh/wlmosv-png/TGAutoSign@master/docs/banner-dark.svg">
    <source media="(prefers-color-scheme: light)" srcset="https://cdn.jsdelivr.net/gh/wlmosv-png/TGAutoSign@master/docs/banner-light.svg">
    <img src="https://cdn.jsdelivr.net/gh/wlmosv-png/TGAutoSign@master/docs/banner-light.svg" alt="TGAutoSign" width="100%">
  </picture>
</p>

<p align="center"><a href="https://github.com/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/blob/main/README.md">中文</a> · <b>English</b></p>

**Tap once. Signed every day.**

Tap the bot's check-in button in Telegram once — then never think about it again.
The control panel lives inside Telegram: send `/jmb` in any chat.

[![Latest Release](https://img.shields.io/github/v/release/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign?label=release&color=8e44ad)](https://github.com/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/total?label=downloads&color=8e44ad)](https://github.com/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/releases/latest)
[![API](https://img.shields.io/badge/libxposed-API%20102-8e44ad?labelColor=3d3d3d)](https://github.com/LSPosed/LSPlant)
[![License](https://img.shields.io/badge/license-GPLv3-8e44ad?labelColor=3d3d3d)](https://github.com/wlmosv-png/TGAutoSign/blob/master/LICENSE)
[![Telegram Group](https://img.shields.io/badge/Telegram-Join%20Group-8e44ad?labelColor=3d3d3d&logo=telegram&logoColor=white)](https://t.me/+V2Oyu8pSubs4ZjE0)

**[Download the latest APK](https://github.com/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/releases/latest)** · [Source repo](https://github.com/wlmosv-png/TGAutoSign)

<sub>Download only from these two sources. For repacked builds elsewhere, compare the fingerprint below.</sub> · [Changelog](https://github.com/wlmosv-png/TGAutoSign/blob/master/CHANGELOG.md)

by **wlmosv** · if it's useful, [star the source repo](https://github.com/wlmosv-png/TGAutoSign)

</div>

---

### Local by design

<sub>No account credentials, no official API, no data leaving your device.</sub>

- The **only outbound call** is an update check every 12 hours — it can be disabled, and it carries no sign-in data
- Targets and signed-state live in Telegram's local storage; they **never leave the device**
- The module requests **no** storage, notification or install permissions; all automation happens on-device, with no relay server


<details>
<summary><b>Verify the build</b></summary>

<br>

Official signing certificate

```
SHA-256  AF:55:24:CD:55:4A:E6:ED:E3:EC:27:47:C7:BE:D1:59
         B0:9B:C4:F6:A4:32:44:A6:8B:46:22:E9:46:32:25:C8
SHA-1    58:A2:B4:D3:F2:83:9A:92:7A:D4:0C:23:51:FE:43:AB:6F:D3:FB:C3
```

Check it yourself

```sh
keytool -printcert -jarfile TGAutoSign-*.apk   # compare against the fingerprint above
sha256sum TGAutoSign-*.apk                     # compare against sha256sum.txt in the release
```

Exactly one class opens a connection — `update/UpdateChecker.java` — so you can audit it.
The fingerprint corresponds to the release key in use since September 2026; any key rotation will be announced in the release notes.

> ⚠️ **Risk notice** — any Telegram automation carries some risk of account restriction. This module uses client-side check-ins, randomised slots and backoff, and is deliberately gentle, but **makes no zero-risk claim**.

</details>

---

## Screenshots

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://cdn.jsdelivr.net/gh/wlmosv-png/TGAutoSign@master/docs/hero-dark.png">
    <source media="(prefers-color-scheme: light)" srcset="https://cdn.jsdelivr.net/gh/wlmosv-png/TGAutoSign@master/docs/hero-light.png">
    <img src="https://cdn.jsdelivr.net/gh/wlmosv-png/TGAutoSign@master/docs/hero-light.png" alt="TGAutoSign UI overview" width="100%">
  </picture>
</p>

**Main panel** · **Targets** — exported by the module's own `/jmb shots`, not captured by hand; target names are replaced with placeholders.

**English UI** — built in on English devices, no setup required

Each page shown in dark / light

| Main panel · Dark | Main panel · Light |
| --- | --- |
| ![Main panel·Dark](https://cdn.jsdelivr.net/gh/wlmosv-png/TGAutoSign@master/docs/screenshots/shot-main-dark.png) | ![Main panel·Light](https://cdn.jsdelivr.net/gh/wlmosv-png/TGAutoSign@master/docs/screenshots/shot-main-light.png) |

| Targets · Dark | Targets · Light |
| --- | --- |
| ![Targets·Dark](https://cdn.jsdelivr.net/gh/wlmosv-png/TGAutoSign@master/docs/screenshots/shot-targets-dark.png) | ![Targets·Light](https://cdn.jsdelivr.net/gh/wlmosv-png/TGAutoSign@master/docs/screenshots/shot-targets-light.png) |

| Settings · Dark | Settings · Light |
| --- | --- |
| ![Settings·Dark](https://cdn.jsdelivr.net/gh/wlmosv-png/TGAutoSign@master/docs/screenshots/shot-settings-dark.png) | ![Settings·Light](https://cdn.jsdelivr.net/gh/wlmosv-png/TGAutoSign@master/docs/screenshots/shot-settings-light.png) |

## What it does

- **Tap once, it learns** — tap the bot's check-in button once and it replays daily, automatically. It keeps up even when the button's callback data changes.
- **Text commands too** — set a bot ID plus a command (e.g. `/checkin`) and it sends on schedule.
- **Group & channel check-ins** — group IDs are supported; replies are read from group messages.
- **Your schedule** — signing window · per-target random slots · minimum spacing · make-up deadline (23:00 by default) · pause a target for a week.
- **Rate-limit friendly** — on failure it backs off 5m → 15m → 45m → 2h → 4h, waits out `FLOOD_WAIT` exactly as the server asks, and catches up when the network returns.
- **Block what you don't want** — keyword / regex rules (matched against bot replies and button labels) · block a whole bot · freeze a single target. Network-learned hits wait for your confirmation.
- **Multi-account, fully isolated** — targets and signed-state are kept per account; targets can be copied across accounts.
- **Daily summary** — one message a day to your own Saved Messages (no system notifications); an extra alert after 3 consecutive failing days.
- **Cross-client sync** — the official client and third-party clients share targets and signed state.
- **Bilingual UI** — English out of the box on English devices; switchable in Settings.
- **Local by design** — no server, no telemetry; the update check is the only outbound call and can be disabled.

---

## Supported clients

The module matches by host package first, then falls back to flag-class capability — it only injects on a match.

<sub>**Requires** root + LSPosed (libxposed **API 102** or newer — see LSPosed Manager → Settings → About). **Not supported**: non-root devices, Telegram X, standalone server deployment.</sub>

| Client | Package | Status |
| --- | --- | --- |
| Telegram (Play / default) | `org.telegram.messenger` | ✅ tested on 13.0.1 |
| Telegram (direct APK) | `org.telegram.messenger.web` | ✅ tested |
| Nagram (NextAlone) | `xyz.nextalone.nagram` | ✅ tested on 12.10.3 |
| Nagram XF | `fork.risin42.nagramx` | ✅ tested |
| ExteraLess (ExteraGram fork) | `com.exteraless.app` | ✅ tested on 12.10.5 |
| Mercurygram | `it.belloworld.mercurygram` | ✅ tested on 12.10.3.1 |
| Turrit | `org.telegram.group` | ✅ tested on 1.9.0.4.2 |
| Nnngram (NextAlone) | `xyz.nextalone.nnngram` | ✅ tested on 12.10.6 |
| AyuGram | `com.radolyn.ayugram` | ✅ tested |
| Nagram / NagramX / NagramNX | `nu.gpu.nagram` etc. | ✅ tested |
| Other Telegram-Android forks | any | injects if flag classes are intact |
| Telegram X | — | ❌ not injected (different core) |

Adapted for the whole Telegram **12.10.x / 13.0.x** line.

> ⚠️ **Scope**: LSPosed only enables the official client by default. If you use a third-party client, tick **that client** in the module's scope as well.

---

## 30-second setup

1. Install the APK → **LSPosed** → **Modules** → enable **TGAutoSign**
2. Tick your Telegram client under **Scope**
3. Fully stop Telegram, then reopen it
4. Send `/jmb` in any chat → go to the bot chat and **tap its check-in button once**

> Done — it signs daily from then on. Send `/jmb` anytime to check status or change settings.

---

## FAQ

**Tapped the button but nothing was added**

Check the auto-learn switch under Settings → Learning, or add the target manually via `/jmb` → Add target. If it still won't add, make sure the scope is ticked and fully restart Telegram.

**The bot uses buttons instead of text — does that work?**

Yes. Tapping once teaches it (the list shows a type badge) and it replays daily. Buttons that merely open a web page or a game (no callback data) are never mis-learned.

**It works on the official client but not my third-party one**

Those clients are supported (see the matrix above), but scope only includes the official client by default. Tick your client in LSPosed, then fully restart Telegram.

**Signing isn't working — what do I do?**

Run `/jmb` → **Self-check** to verify the reflection anchors, then check the built-in log view for injection and signing records. Still stuck? Export the log together with your client name and version, and open an issue.

**How do I migrate to a new phone or account?**

On the old device: `/jmb` → **Export**. On the new one, drop the json into `Android/data/<client package>/files/tgautosign/` and import it. Import merges — it never wipes.

**Update says "signature mismatch"**

You installed a debug build. Uninstall it, then install the official APK from this page. Official builds upgrade over each other in place, and your data is kept.

---

## 更新日志 · Changelog

### v1.6.9 (135) — 2026-10-28

**Fixed**: Signed status is written only from the bot's explicit reply. · The conclusion inside a reply takes precedence. · Ads, menus, help text and account panels do not count as sign-in results. · Genuine results are no longer discarded as advertisements. · Verdicts and list display now agree. · Image and sticker replies do not produce a sign-in result. · The Saved Messages digest switch is evaluated per account. · The unrecognized-replies page renders long lists without blocking the UI. · Make-up sign-ins follow the configured schedule window in scheduled mode. · Learned words apply at the level they are configured. · Targets can be added even when the bot is missing from local chat data.

**New**: Added: a fixed sign-in time for individual targets. · Added: sign-in sound. · Added: target names are filled in automatically. · Added: startup daily summary.

### v1.6.7 (133) — 2026-10-17

**New**: Link self-check. · Second, independent message entry point. · Dice / animated emoji check-in. · Emoji check-in panel. · Unified chat picker. · Accept @username directly. · Command reference. · Capture mode switch. · Separate switch for Saved Messages digest. · Statistics page expansion. · Reworked check-in centre. · Account health badge. · Handbook.

**Fixed**: Fixed replies that were received but never judged. · Fixed misreading the answer from callback responses. · Fixed "sent" marker lingering after repeated stale-button failures. · Fixed stale "sent" marker persisting after a successful check-in. · Image-only replies no longer reported as unreadable. · Command menus no longer treated as results. · Fixed the last row of the target list being unreachable. · Fixed all targets appearing stuck with an absurd elapsed time. · Fixed self-sent commands being learned as new candidates. · Fixed the whole panel closing after using the chat picker. · Fixed misleading timer log wording. · Fixed pure-emoji commands not being learned in groups. · Removed redundant toast when adding a target. · Loose mode no longer accepts replies for targets not sent today.

**Improved**: Unified handling for abnormal states. · Unified "needs attention" criteria. · Manual triggers no longer blocked incorrectly. · Cross-account copy. · Multi-account reply attribution. · UI consistency. · Fixed missing feedback for single-account signing and inflated progress denominators. · Copy and prompts.

[Full changelog →](https://github.com/wlmosv-png/TGAutoSign/blob/master/CHANGELOG.md)

## License

Licensed under **GPLv3**. For personal use with your own accounts.
Please respect Telegram's Terms of Service and each group's / bot's rules.

---

<p align="center"><sub>Made by wlmosv · <a href="https://github.com/wlmosv-png/TGAutoSign">a star keeps it going</a></sub></p>
