# 🛡️ HaGeZi Blocklists (MRS Format) & Universal Mihomo Merge Engine

[![Automated Build](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/actions/workflows/build-mrs.yml/badge.svg)](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/actions)
[![Latest Release](https://img.shields.io/github/v/release/Erfan4700/HaGeZi_BlockLists_mrs_format?color=blue&label=Latest%20Release)](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/latest)
[![Last Commit](https://img.shields.io/github/last-commit/Erfan4700/HaGeZi_BlockLists_mrs_format/release?label=Last%20Rule%20Update&color=blueviolet)](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/commits/release)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

An enterprise-grade, automated ecosystem providing pre-compiled **Mihomo Rule-Set (`.mrs`)** binaries for [HaGeZi DNS Blocklists](https://github.com/hagezi/dns-blocklists), bundled with an advanced, production-tested **JavaScript Merge Script** (`clash-verge-merge.js`) engineered for anti-DNS leakage, regional bypass, and ad-blocking.

---

## 📱 Compatible GUI Clients (Prerequisites)

This repository and its companion script are specifically optimized for modern proxy clients powered by the **Mihomo (formerly Clash.Meta)** core:

* **[Clash Verge Rev](https://github.com/clash-verge-rev/clash-verge-rev)** *(Recommended — Windows, macOS, Linux)*
* **[Mihomo Party](https://github.com/mihomo-party-org/mihomo-party)** *(Windows, macOS, Linux)*
* **[Clash Nyanpasu](https://github.com/libnyanpasu/clash-nyanpasu)** *(Windows, macOS, Linux)*
* **[Flclash](https://github.com/chen08209/FlClash)** *(Cross-Platform)*
* Any client supporting Mihomo Core Rule-Providers.

---

## 📦 1. Available Pre-Compiled HaGeZi Tiers

Every blocklist is continuously synced with upstream changes, compiled using the native Mihomo binary engine, and distributed globally through jsDelivr CDN edges with automated cache-purge triggers:

| Tier | Format | Size | Target Profile | CDN URL |
| :--- | :---: | :---: | :--- | :--- |
| **Light** | `.mrs` | ![Light Size](https://img.shields.io/github/size/Erfan4700/HaGeZi_BlockLists_mrs_format/HageziLight.mrs?branch=release&label=&color=success) | Low-resource routers & minimal filtering | [CDN Link](https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziLight.mrs) |
| **Normal** | `.mrs` | ![Normal Size](https://img.shields.io/github/size/Erfan4700/HaGeZi_BlockLists_mrs_format/HageziNormal.mrs?branch=release&label=&color=success) | Everyday household ad & tracker protection | [CDN Link](https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziNormal.mrs) |
| **Pro** | `.mrs` | ![Pro Size](https://img.shields.io/github/size/Erfan4700/HaGeZi_BlockLists_mrs_format/HageziPro.mrs?branch=release&label=&color=blue) | **Balanced Standard:** Ads, trackers, and telemetry | [CDN Link](https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziPro.mrs) |
| **Pro++** | `.mrs` | ![ProPlus Size](https://img.shields.io/github/size/Erfan4700/HaGeZi_BlockLists_mrs_format/HageziProPlus.mrs?branch=release&label=&color=blue) | **Default:** Advanced tracking, telemetry & affiliate links | [CDN Link](https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziProPlus.mrs) |
| **Ultimate** | `.mrs` | ![Ultimate Size](https://img.shields.io/github/size/Erfan4700/HaGeZi_BlockLists_mrs_format/HageziUltimate.mrs?branch=release&label=&color=orange) | Paranoia mode (strict corporate-grade filtering) | [CDN Link](https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziUltimate.mrs) |
| **TIF** | `.mrs` | ![TIF Size](https://img.shields.io/github/size/Erfan4700/HaGeZi_BlockLists_mrs_format/HageziTIF.mrs?branch=release&label=&color=critical) | **Active Threat Defense:** Phishing, malware, botnets & miners | [CDN Link](https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziTIF.mrs) |

> 🔗 **Raw CDN Base URL:**  
> `https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/{TIER_NAME}.mrs`

---

## ⚙️ 2. The Universal Merge Script (`clash-verge-merge.js`)

Included directly in this repository is [`clash-verge-merge.js`](./clash-verge-merge.js), an engine designed to transform any raw subscription into a high-performance configuration:

* **Dual-Layer Filtering:** Combines HaGeZi MRS blocklists with **Chocolate4U** regional threat feeds.
* **Intelligent Regional Routing (Iran):** Complete `DIRECT` routing for national `.ir` domains, banking portals, payment gateways, ride-hailing services (Snapp/Tapsi), and localized IP-CIDRs/ASNs.
* **Leak-Proof DNS Design:** Implements `fake-ip` address mapping, bootstrap DNS protection, and isolated unpoisoned upstream resolvers (`nameserver-policy`).
* **Memory & Garbage Collection Optimization:** Uses immutable structures (`Object.freeze`), precompiled regular expressions, and avoids unnecessary runtime allocations.
* **QUIC Protocol Suspension:** Automatically drops `UDP/443` traffic to circumvent ISP packet loss, handshake delays, and bandwidth throttling.

### Quick In-Script Configuration Panel:
You can switch blocklist tiers or toggle features simply by editing the top lines of [`clash-verge-merge.js`](./clash-verge-merge.js):

```javascript
// 1. Select HaGeZi Tier: "light" | "normal" | "pro" | "proplus" | "ultimate"
const HAGEZI_TIER = "proplus";

// 2. Enable Real-Time Cyber Defense (Threat Intelligence Feeds)
const ENABLE_HAGEZI_TIF = true;

// 3. Enforce Strict SafeSearch (Google & Bing)
const ENABLE_SAFE_SEARCH = false;
```

---

## 📖 3. Setup & Installation Guide (Clash Verge Rev)

### Method A: Global Script (Recommended — Applies to all subscriptions)
1. Launch **Clash Verge Rev**.
2. Select the **Script** tab on the left-side navigation menu.
3. Click **New** (or Create Script).
4. Enter a descriptive title (e.g., `HaGeZi + Universal Bypass Engine`).
5. Copy the entire contents of [`clash-verge-merge.js`](./clash-verge-merge.js) and paste it into the editor.
6. Click **Save** and ensure the script switch is toggled **ON**.
7. Return to the **Profiles** tab and click **Refresh** (🔄) on your active subscription profile.

### Method B: Single Profile Extension
1. Open the **Profiles** tab.
2. Right-click your active profile and choose **Edit Rules / Script**.
3. Paste the contents of `clash-verge-merge.js` into the script configuration area and click **Save**.

---

## 🇮🇷 4. Regional Routing: Chocolate4U Integration

For domestic traffic segregation within Iran, this project integrates datasets maintained by the **[Chocolate4U/Iran-clash-rules](https://github.com/Chocolate4U/Iran-clash-rules)** initiative:

* `ir.mrs` & `ircidr.mrs`: Complete coverage of Iranian national infrastructure and CIDRs.
* `irasn.txt`: Autonomous System Number definitions for domestic telecommunications and datacenters.
* `ads.mrs`: Localized ad-blocking targeting domestic video portals, applications, and news sites.
* `malware-ip.mrs` & `phishing-ip.mrs`: Dedicated regional threat feeds.
* `geoip.metadb`: High-performance GeoIP databases specifically compiled for Mihomo.

---

## 🔄 5. Automated CI/CD Pipeline Architecture

```text
[HaGeZi Upstream Repository] (Monitored every 20 minutes)
              │
              ▼
    [GitHub Actions Runner] (Detects new Commit SHA)
              │
              ├─► Downloads latest Mihomo core binary
              ├─► Converts wildcard text lists to binary .mrs
              ├─► Performs file size validation (>10 KB sanity check)
              │
              ▼
         [Deployment]
              ├─► Pushes updated artifacts to 'release' branch
              ├─► Creates a timestamped GitHub Release with standalone assets
              └─► Sends automated purge requests to jsDelivr edge caches
```

---

## 🎖️ Credits & Acknowledgements

* **HaGeZi Blocklists:** Curated and maintained by [@hagezi](https://github.com/hagezi) at [hagezi/dns-blocklists](https://github.com/hagezi/dns-blocklists).
* **Iran Clash Rules:** Maintained by [@Chocolate4U](https://github.com/Chocolate4U) at [Chocolate4U/Iran-clash-rules](https://github.com/Chocolate4U/Iran-clash-rules).
* **Mihomo (Clash.Meta) Core:** Developed by the [@MetaCubeX](https://github.com/MetaCubeX) team at [MetaCubeX/mihomo](https://github.com/MetaCubeX/mihomo).

---

## 📄 License

This automation repository is distributed under the **MIT License**. Upstream blocklists and datasets belong to their respective maintainers.
