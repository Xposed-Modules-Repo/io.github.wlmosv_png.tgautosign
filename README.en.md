<div align="center">

<img src="https://raw.githubusercontent.com/wlmosv-png/TGAutoSign/master/docs/banner.png" width="720" alt="TGAutoSign">

# TGAutoSign

<p align="center"><a href="https://github.com/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/blob/main/README.md">中文</a> · <b>English</b></p>

**Tap once. Signed every day.**

Tap the bot's check-in button in Telegram once — then never think about it again.
The control panel lives inside Telegram: send `/jmb` in any chat.

[![Latest Release](https://img.shields.io/github/v/release/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign?label=release&color=blue)](https://github.com/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/total?label=downloads&color=brightgreen)](https://github.com/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/releases/latest)
[![API](https://img.shields.io/badge/libxposed-API%20102-8A2BE2)](https://github.com/LSPosed/LSPlant)
[![License](https://img.shields.io/badge/license-GPLv3-green)](LICENSE)
[![Telegram Group](https://img.shields.io/badge/Telegram-Join%20Group-26A5E4?logo=telegram&logoColor=white)](https://t.me/+V2Oyu8pSubs4ZjE0)

**⬇️ [Download the latest APK](https://github.com/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/releases/latest)** · [Source repo](https://github.com/wlmosv-png/TGAutoSign) · [Changelog](https://github.com/wlmosv-png/TGAutoSign/blob/master/CHANGELOG.md)

by **wlmosv** · if it's useful, [star the source repo ⭐](https://github.com/wlmosv-png/TGAutoSign)

</div>

---

## 📱 Screenshots

**English UI** — built in on English devices, no setup required

| Main panel | Main menu |
| --- | --- |
| ![Main panel](https://raw.githubusercontent.com/wlmosv-png/TGAutoSign/master/docs/screenshots/main-en-dark.jpg) | ![Main menu](https://raw.githubusercontent.com/wlmosv-png/TGAutoSign/master/docs/screenshots/menu-en-dark.jpg) |
| Targets | Settings |
| ![Targets](https://raw.githubusercontent.com/wlmosv-png/TGAutoSign/master/docs/screenshots/targets-en-dark.jpg) | ![Settings](https://raw.githubusercontent.com/wlmosv-png/TGAutoSign/master/docs/screenshots/settings-en-dark.jpg) |

---

## ✨ What it does

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
- **100% local** — no server, no telemetry, nothing reported.

---

## 🖥️ Supported clients

The module matches by host package first, then falls back to flag-class capability — it only injects on a match.

| Client | Package | Status |
| --- | --- | --- |
| Telegram (Play / default) | `org.telegram.messenger` | ✅ tested on 12.10.4 |
| Telegram (direct APK) | `org.telegram.messenger.web` | ✅ statically verified |
| Nagram (NextAlone) | `xyz.nextalone.nagram` | ✅ tested on 12.10.3 |
| Nagram XF | `fork.risin42.nagramx` | ✅ tested (dec46b0) |
| ExteraLess (ExteraGram fork) | `com.exteraless.app` | ✅ tested on 12.10.1 |
| Nekogram | `tw.nekomimi.nekogram` | ✅ tested on 12.10.3 |
| Mercurygram | `it.belloworld.mercurygram` | ✅ tested on 12.10.3.1 |
| Nagram / NagramX / NagramNX | `nu.gpu.nagram` etc. | whitelisted, not tested |
| Other Telegram-Android forks | any | injects if flag classes are intact |
| Telegram X | — | ❌ not injected (different core) |

Adapted for the whole Telegram **12.10.x** line, including 12.10.4.

> ⚠️ **Scope**: LSPosed only enables the official client by default. If you use a third-party client, tick **that client** in the module's scope as well.

---

## 🚀 30-second setup

1. Install the APK → **LSPosed** → **Modules** → enable **TGAutoSign**
2. Tick your Telegram client under **Scope**
3. Fully stop Telegram, then reopen it
4. Send `/jmb` in any chat → go to the bot chat and **tap its check-in button once**

> Done — it signs daily from then on. Send `/jmb` anytime to check status or change settings.

---

## ❓ FAQ

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

## 📜 Changelog

### v1.6.0 (123) — 2026-09-26

**Architecture**: Account isolation moved from convention to structure · Six single-responsibility classes extracted from the core file · Pure logic is now unit-testable · Storage keys consolidated into a single source of truth · Flush policy made explicit

**Fixed**: Account crossover — all six paths now pin the account (important) · Out-of-range guard read another account's partition (important) · Failed targets were signed over and over (important) · Duplicate scheduling within one account (important) · Sign-in succeeded but was judged a failure and pushed back into backoff (important) · Panel waiting always timed out into the fallback (important) · Same class of bug, full sweep: three more places treated success as failure · The "pending" pool is now per-account, with automatic migration · The "pending" state was write-only: visible but unclickable (important) · Reply verdict could land on the wrong account (important) · Result tallying mixed accounts during sign-all · Clearing config left state behind, resurrecting it on re-add (important) · Clearing config wrongly deleted the per-account pending pool · Stale buttons caused an endless retry loop · Silent robots made the module wait out a timeout every day · Crash when saving in the settings screen · Opening "Logs" stuttered · Only the first startup line reached the log file · Tapping a bot button within 30 s of a cold start did nothing · The make-up window became all day when it crossed midnight · Configs synced from another client did not apply locally · Only the first of several bot buttons was learned · Chain ids in the log could repeat across accounts · Two instances ran in parallel after a hot reload · Numeric headings rendered as wrong glyphs in the startup log · Decorative text showed tofu boxes · The "pending" retry button used the wrong account

**New**: Detailed version info in logs and the diagnostics bundle · Host friendly names follow the UI language

**Tooling**: The in-repo build.sh was missing three gates · Unit assertions grew from 115 to 174 · The wiring checker listed a method that no longer existed

### v1.5.8 (121) — 2026-09-24

**Fixed**: Panels turned light — fixed · Theme logging now records every change · "Unrecognized bot reply" is no longer an error · A single tap is no longer processed twice · i18n gate whitelist hole closed, 18 historical missing translations fixed · The gate now catches "wrapped method used but not registered" · Background heartbeat throttles on demand — no more 45-second wakeups all night · Timed tasks no longer double-queue or get dropped · Panel-refresh triggers no longer duplicate the heartbeat send · A bot's numeric id was shown once and then never resolvable · "Already checked in today" replies are now recognized · "This is not a check-in result" no longer looks like a failure · Auto-verdict being off is no longer silent · Fresh installs could not learn targets by tapping a bot button (important) · Capture mode did not work on Nagram or the official client · Rejections reported the wrong reason · Account numbers in the UI were garbled (e.g. "account 10") · Log account prefixes went stale · Sign-in windows crossing midnight now actually work · Cross-client sync: accounts no longer shift · Rescheduled the timetable after receiving another client's config · In-flight validity window aligned with failure revocation (90 s → 30 min) · Cross-device sync throttling · Pre-release check for test markers

**New**: Verdict words became toggle-based · New "loose mode (accept anything)"

**Reliability**: Pure-logic unit tests added and wired into the build gate · Unrecognized bot replies are no longer silent · Exceptions on critical paths are no longer swallowed silently

**Diagnostics**: Diagnostics bundle gained learning and hook state · Diagnostics bundle header shows patch markers · Diagnostics bundle shows raw account field values

[Full changelog →](https://github.com/wlmosv-png/TGAutoSign/blob/master/CHANGELOG.md)

## 🔗 Download

| Channel | Where |
| --- | --- |
| **This page's Releases** (recommended) | [https://github.com/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/releases/latest](https://github.com/Xposed-Modules-Repo/io.github.wlmosv_png.tgautosign/releases/latest) |
| Source repo Releases | [https://github.com/wlmosv-png/TGAutoSign/releases](https://github.com/wlmosv-png/TGAutoSign/releases) |
| In-app | Telegram → send `/jmb` → Check for updates |

> Both repos ship byte-identical APKs (a `sha256sum.txt` is attached to each release). They are signed with the same release key, so installing over an older version keeps your data.

---

## ⚖️ License

Licensed under **GPLv3**. For personal use with your own accounts.
Please respect Telegram's Terms of Service and each group's / bot's rules.

---

<p align="center"><sub>Made by wlmosv · <a href="https://github.com/wlmosv-png/TGAutoSign">a ⭐ keeps it going</a></sub></p>
