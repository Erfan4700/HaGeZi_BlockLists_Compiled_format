# 🛡️ HaGeZi Blocklists (MRS Format) & Universal Mihomo Engine

[![Automated Build](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/actions/workflows/build-mrs.yml/badge.svg)](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/actions)
[![Latest Release](https://img.shields.io/github/v/release/Erfan4700/HaGeZi_BlockLists_mrs_format?color=blue&label=Latest%20Release)](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/latest)
[![Last Commit](https://img.shields.io/github/last-commit/Erfan4700/HaGeZi_BlockLists_mrs_format/release?label=Last%20Rule%20Update&color=blueviolet)](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/commits/release)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

High-performance, automated, pre-compiled **Mihomo Rule-Set (`.mrs`)** binaries for [HaGeZi DNS Blocklists](https://github.com/hagezi/dns-blocklists), bundled with an advanced **JavaScript Merge Script** (`clash-verge-merge.js`) for anti-DNS leakage, tracker blocking, and domestic bypass.

---

## 📦 Available Pre-Compiled HaGeZi Rulesets

Continuously synced with upstream commits every **20 minutes**, compiled using the native Mihomo binary engine, and delivered via jsDelivr CDN edges with instant cache purging:

### 1. General & Security Tiers
| Tier | Format | Size | Target Profile | CDN URL |
| :--- | :---: | :---: | :--- | :--- |
| **Light** | `.mrs` | ![Light Size](https://img.shields.io/github/size/Erfan4700/HaGeZi_BlockLists_mrs_format/HageziLight.mrs?branch=release&label=&color=success) | Low-resource routers & minimal filtering | [CDN Link](https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziLight.mrs) |
| **Normal** | `.mrs` | ![Normal Size](https://img.shields.io/github/size/Erfan4700/HaGeZi_BlockLists_mrs_format/HageziNormal.mrs?branch=release&label=&color=success) | Everyday household ad & tracker protection | [CDN Link](https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziNormal.mrs) |
| **Pro** | `.mrs` | ![Pro Size](https://img.shields.io/github/size/Erfan4700/HaGeZi_BlockLists_mrs_format/HageziPro.mrs?branch=release&label=&color=blue) | **Balanced Standard:** Ads, trackers, and telemetry | [CDN Link](https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziPro.mrs) |
| **Pro++** | `.mrs` | ![ProPlus Size](https://img.shields.io/github/size/Erfan4700/HaGeZi_BlockLists_mrs_format/HageziProPlus.mrs?branch=release&label=&color=blue) | **Default:** Advanced tracking, telemetry & affiliate links | [CDN Link](https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziProPlus.mrs) |
| **Ultimate** | `.mrs` | ![Ultimate Size](https://img.shields.io/github/size/Erfan4700/HaGeZi_BlockLists_mrs_format/HageziUltimate.mrs?branch=release&label=&color=orange) | Paranoia mode (strict corporate-grade filtering) | [CDN Link](https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziUltimate.mrs) |
| **TIF** | `.mrs` | ![TIF Size](https://img.shields.io/github/size/Erfan4700/HaGeZi_BlockLists_mrs_format/HageziTIF.mrs?branch=release&label=&color=critical) | **Active Threat Defense:** Phishing, malware, botnets & miners | [CDN Link](https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziTIF.mrs) |
| **DynDNS** | `.mrs` | ![DynDNS Size](https://img.shields.io/github/size/Erfan4700/HaGeZi_BlockLists_mrs_format/HageziDynDNS.mrs?branch=release&label=&color=critical) | Block dynamic DNS domains utilized by malware & C2 servers | [CDN Link](https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziDynDNS.mrs) |

### 2. Native Hardware & OS Tracker Protection
| Target OS | Format | Live Size | Protection Scope | Fast CDN URL |
| :--- | :---: | :---: | :--- | :--- |
| **Windows** | `.mrs` | ![Windows Size](https://img.shields.io/github/size/Erfan4700/HaGeZi_BlockLists_mrs_format/HageziWindows.mrs?branch=release&label=&color=blue) | Complete Windows 10/11 & Office diagnostic telemetry block | [CDN Link](https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziWindows.mrs) |
| **Apple** | `.mrs` | ![Apple Size](https://img.shields.io/github/size/Erfan4700/HaGeZi_BlockLists_mrs_format/HageziApple.mrs?branch=release&label=&color=blue) | Blocks Apple diagnostic metrics, analytics & crash reporters | [CDN Link](https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziApple.mrs) |
| **Xiaomi** | `.mrs` | ![Xiaomi Size](https://img.shields.io/github/size/Erfan4700/HaGeZi_BlockLists_mrs_format/HageziXiaomi.mrs?branch=release&label=&color=orange) | Neutralizes MIUI/HyperOS aggressive system analytics | [CDN Link](https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziXiaomi.mrs) |
| **Android** | `.mrs` | ![Android Size](https://img.shields.io/github/size/Erfan4700/HaGeZi_BlockLists_mrs_format/HageziAndroid.mrs?branch=release&label=&color=success) | Blocks Samsung & OEM native device telemetry | [CDN Link](https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziAndroid.mrs) |

### 3. Specialized Filtering (Parental Control & Anti-Gambling)
| Target | Format | Live Size | Protection Scope | Fast CDN URL |
| :--- | :---: | :---: | :--- | :--- |
| **Gambling** | `.mrs` | ![Gambling Size](https://img.shields.io/github/size/Erfan4700/HaGeZi_BlockLists_mrs_format/HageziGambling.mrs?branch=release&label=&color=critical) | Comprehensive international gambling, casino, and betting block | [CDN Link](https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziGambling.mrs) |
| **NSFW** | `.mrs` | ![NSFW Size](https://img.shields.io/github/size/Erfan4700/HaGeZi_BlockLists_mrs_format/HageziNSFW.mrs?branch=release&label=&color=critical) | Worldwide adult content and pornography blocklist | [CDN Link](https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziNSFW.mrs) |

---

## ⚙️ The Universal Merge Script (`clash-verge-merge.js`)

Included directly in this repository is [`clash-verge-merge.js`](./clash-verge-merge.js), an engine designed to coordinate both global and regional protections into a zero-leak profile.

👉 **[View the Complete Script Here (`clash-verge-merge.js`)](./clash-verge-merge.js)**

---

## 🌐 The Complete Ecosystem (Related Projects)

This repository is part of a two-pillar, self-hosted routing & security suite for Mihomo / Clash:

* 🛡️ **Global Defense (This Repo):** **[HaGeZi_BlockLists_mrs_format](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format)** — Automated, pre-compiled binary `.mrs` versions of HaGeZi DNS blocklists (Adblock, Telemetry, and Threat Intelligence Feeds).
* 🇮🇷 **Regional Engine:** **[Iran_Clash_Rules_mrs_format](https://github.com/Erfan4700/Iran_Clash_Rules_mrs_format)** — Optimized Iranian domestic routing, collapsed RIPE CIDRs, and payment gateway safety layers.
* ⚡ **Unified Driver:** [`clash-verge-merge.js`](./clash-verge-merge.js) — The master integration script combining both repositories into a zero-leak Clash profile.

---

## 🎖️ Credits & Acknowledgements

* **HaGeZi Blocklists:** Curated and maintained by [@hagezi](https://github.com/hagezi) at [hagezi/dns-blocklists](https://github.com/hagezi/dns-blocklists).
* **Mihomo (Clash.Meta) Core:** Developed by the [@MetaCubeX](https://github.com/MetaCubeX) team at [MetaCubeX/mihomo](https://github.com/MetaCubeX/mihomo).

---

## 📄 License

Distributed under the **MIT License**. Upstream blocklists and datasets belong to their respective maintainers.
