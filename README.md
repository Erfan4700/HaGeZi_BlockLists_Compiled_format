# 🛡️ HaGeZi Blocklists (MRS Format) & Universal Mihomo Engine

[![Automated Build](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/actions/workflows/build-mrs.yml/badge.svg)](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/actions)
[![Latest Release](https://img.shields.io/github/v/release/Erfan4700/HaGeZi_BlockLists_mrs_format?color=blue&label=Latest%20Release)](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/latest)
[![Last Commit](https://img.shields.io/github/last-commit/Erfan4700/HaGeZi_BlockLists_mrs_format/release?label=Last%20Rule%20Update&color=blueviolet)](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/commits/release)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

High-performance, automated, pre-compiled **Mihomo Rule-Set (`.mrs`)** binaries for [HaGeZi DNS Blocklists](https://github.com/hagezi/dns-blocklists), bundled with an advanced **JavaScript Merge Script** (`clash-verge-merge.js`) for anti-DNS leakage, tracker blocking, and domestic bypass.

---

## 📱 Compatible GUI Clients (Prerequisites)

Optimized for clients powered by the modern **Mihomo (formerly Clash.Meta)** core:

* **[Clash Verge Rev](https://github.com/clash-verge-rev/clash-verge-rev)** *(Recommended — Windows, macOS, Linux)*
* **[Mihomo Party](https://github.com/mihomo-party-org/mihomo-party)** *(Windows, macOS, Linux)*
* **[Clash Nyanpasu](https://github.com/libnyanpasu/clash-nyanpasu)** *(Windows, macOS, Linux)*
* **[Flclash](https://github.com/chen08209/FlClash)** *(Cross-Platform)*

---

## 📦 1. Available Pre-Compiled HaGeZi Tiers

Continuously synced with upstream commits every **20 minutes**, compiled using the native Mihomo binary engine, and delivered via jsDelivr CDN edges with instant cache purging:

| Tier | Format | Size | Target Profile | CDN URL |
| :--- | :---: | :---: | :--- | :--- |
| **Light** | `.mrs` | ![Light Size](https://img.shields.io/github/size/Erfan4700/HaGeZi_BlockLists_mrs_format/HageziLight.mrs?branch=release&label=&color=success) | Low-resource routers & minimal filtering | [CDN Link](https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziLight.mrs) |
| **Normal** | `.mrs` | ![Normal Size](https://img.shields.io/github/size/Erfan4700/HaGeZi_BlockLists_mrs_format/HageziNormal.mrs?branch=release&label=&color=success) | Everyday household ad & tracker protection | [CDN Link](https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziNormal.mrs) |
| **Pro** | `.mrs` | ![Pro Size](https://img.shields.io/github/size/Erfan4700/HaGeZi_BlockLists_mrs_format/HageziPro.mrs?branch=release&label=&color=blue) | **Balanced Standard:** Ads, trackers, and telemetry | [CDN Link](https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziPro.mrs) |
| **Pro++** | `.mrs` | ![ProPlus Size](https://img.shields.io/github/size/Erfan4700/HaGeZi_BlockLists_mrs_format/HageziProPlus.mrs?branch=release&label=&color=blue) | **Default:** Advanced tracking, telemetry & affiliate links | [CDN Link](https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziProPlus.mrs) |
| **Ultimate** | `.mrs` | ![Ultimate Size](https://img.shields.io/github/size/Erfan4700/HaGeZi_BlockLists_mrs_format/HageziUltimate.mrs?branch=release&label=&color=orange) | Paranoia mode (strict corporate-grade filtering) | [CDN Link](https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziUltimate.mrs) |
| **TIF** | `.mrs` | ![TIF Size](https://img.shields.io/github/size/Erfan4700/HaGeZi_BlockLists_mrs_format/HageziTIF.mrs?branch=release&label=&color=critical) | **Active Threat Defense:** Phishing, malware, botnets & miners | [CDN Link](https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziTIF.mrs) |

---

## ⚙️ 2. The Universal Merge Script (`clash-verge-merge.js`)

Included directly in this repository is [`clash-verge-merge.js`](./clash-verge-merge.js), an engine designed to transform any raw subscription into a high-performance configuration:

* **Dual-Layer Filtering:** Integrates HaGeZi MRS blocklists with domestic Iranian routing.
* **Leak-Proof DNS Design:** Implements `fake-ip` address mapping and isolated unpoisoned upstream resolvers.
* **Memory Optimization:** Uses immutable structures (`Object.freeze`) and precompiled regexes to eliminate runtime GC lag.
* **QUIC Protocol Drop:** Drops `UDP/443` traffic to circumvent ISP packet loss and throttling.

👉 **[View the Complete Script Here (`clash-verge-merge.js`)](./clash-verge-merge.js)**

---

## 📖 3. Setup & Installation (Clash Verge Rev)

1. Open **Clash Verge Rev**.
2. Select the **Script** tab on the left-side navigation menu.
3. Click **New** and name it `Universal Bypass Engine`.
4. Copy the entire contents of [`clash-verge-merge.js`](./clash-verge-merge.js) and paste it into the editor.
5. Click **Save** and ensure the switch is toggled **ON**.
6. Switch to the **Profiles** tab and click **Refresh** (🔄) on your active profile.

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
