
<div align="center">

# 🛡️ HaGeZi Blocklists (Native Mihomo MRS Format)
### High-Performance Binary DNS Blocklists & Automated Upstream Engine

[![Build Status](https://img.shields.io/github/actions/workflow/status/Erfan4700/HaGeZi_BlockLists_mrs_format/build-mrs.yml?branch=main&label=CI%2FCD%20Build&style=flat-square&logo=github-actions&logoColor=white)](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/actions)
[![CDN Delivery](https://img.shields.io/badge/CDN-jsDelivr%20Active-orange?style=flat-square&logo=jsdelivr&logoColor=white)](https://www.jsdelivr.com/)
[![Upstream Sync](https://img.shields.io/badge/Sync%20Cadence-20%20Minutes-blue?style=flat-square&logo=git&logoColor=white)](#-automated-cicd-pipeline)
[![Format](https://img.shields.io/badge/Format-Binary%20MRS%20(Domain)-blueviolet?style=flat-square&logo=webassembly&logoColor=white)](#-why-mihomo-rule-set-mrs)
[![License: MIT](https://img.shields.io/badge/License-MIT-emerald?style=flat-square)](LICENSE)

Automated, pre-compiled **Mihomo Rule-Set (`.mrs`)** binaries generated directly from [HaGeZi's DNS Blocklists](https://github.com/hagezi/dns-blocklists). Optimized for minimal memory overhead, instant cold-starts, and zero-leak deployment on Mihomo (Clash.Meta) environments.

[Ruleset Catalog](#-ruleset-catalog) • [Why MRS?](#-why-mihomo-rule-set-mrs) • [Client Setup](#-client-integration) • [Ecosystem](#-the-unified-ecosystem)

</div>

---

## 📐 Pipeline Architecture

Upstream feeds are ingested every 20 minutes, validated, and converted into binary bytecode through an automated CI/CD pipeline:

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                       UPSTREAM HAGEZI REPOSITORIES                          │
├─────────────────────┬──────────────────────┬────────────────────────────────┤
│    Standard Tiers   │  Threat Feeds (TIF)  │ OS Telemetry & Content Filters │
│ (Light -> Ultimate) │ (Malware / C2 / DNS) │ (Apple, MS, Xiaomi, Gambling)  │
└──────────┬──────────┴──────────┬───────────┴───────────────┬────────────────┘
           │                     │                           │
           ▼                     ▼                           ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                     AUTOMATED GITHUB ACTIONS RUNNER                         │
├─────────────────────────────────────────────────────────────────────────────┤
│  • Upstream commit verification & differential change detection             │
│  • Rule syntax validation and duplicate pruning                             │
│  • Binary compilation via native Mihomo engine:                             │
│    `./mihomo convert-ruleset domain text input.txt output.mrs`              │
└──────────────────────────────────────┬──────────────────────────────────────┘
                                       │
                                       ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                    GLOBAL EDGE DISTRIBUTION (jsDelivr CDN)                  │
├─────────────────────────────────────────────────────────────────────────────┤
│  • Pushed directly to dedicated `release` branch                            │
│  • Automated edge cache purge via jsDelivr API                              │
│  • Sub-millisecond binary downloads worldwide                               │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## ⚡ Why Mihomo Rule-Set (`.mrs`)?

Standard plain-text or YAML domain lists require significant runtime parsing, which introduces latency and memory spikes on constrained devices.

* **Memory-Mapped I/O (mmap):** Mihomo loads `.mrs` files as pre-structured binary trees directly into memory, reducing initial parsing time to near **0 ms**.
* **RAM Optimization:** Decreases client memory usage by **up to 80%** compared to traditional YAML or classical text lists, making it ideal for home routers, embedded boards, and mobile devices.
* **Deterministic Matching:** Structured binary lookups provide consistent sub-millisecond route resolution, avoiding regex backtracking bottlenecks during high packet throughput.

---

## 📦 Ruleset Catalog

All binaries are compiled under the `domain` behavior and served globally through jsDelivr edges.

### 1. General Adblocking & Security Tiers

| Tier Name | Scope & Target Profile | CDN Endpoint |
| :--- | :--- | :--- |
| **Light** | Basic ad and tracker blocking for low-memory routers and legacy hardware. | [Get `HageziLight.mrs`](https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziLight.mrs) |
| **Normal** | Balanced daily protection against common consumer ads and tracking endpoints. | [Get `HageziNormal.mrs`](https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziNormal.mrs) |
| **Pro** | **Recommended Standard:** Comprehensive ad, tracking, metrics, and telemetry blocking. | [Get `HageziPro.mrs`](https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziPro.mrs) |
| **Pro++** | **Default Engine Tier:** Extended coverage including marketing affiliates, trackers, and telemetry. | [Get `HageziProPlus.mrs`](https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziProPlus.mrs) |
| **Ultimate** | Maximum protection tier designed for zero-tolerance security profiles. | [Get `HageziUltimate.mrs`](https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziUltimate.mrs) |
| **TIF** | **Threat Intelligence Feeds:** Blocks active malware, ransomware, botnet C2s, phishing, and miners. | [Get `HageziTIF.mrs`](https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziTIF.mrs) |
| **DynDNS** | Blocks public Dynamic DNS provider domains used by evasive trojans and command-and-control nodes. | [Get `HageziDynDNS.mrs`](https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziDynDNS.mrs) |

### 2. Native OS & Hardware Telemetry

| Target System | Scope & Description | CDN Endpoint |
| :--- | :--- | :--- |
| **Windows** | Blocks diagnostic tracking, Cortana telemetry, telemetry reporting, and Office metrics. | [Get `HageziWindows.mrs`](https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziWindows.mrs) |
| **Apple** | Neutralizes analytics, diagnostic loggers, and background metrics on iOS and macOS. | [Get `HageziApple.mrs`](https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziApple.mrs) |
| **Xiaomi** | Strips tracking, ad injection services, and system analytics across MIUI and HyperOS. | [Get `HageziXiaomi.mrs`](https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziXiaomi.mrs) |
| **Android** | Blocks analytics, crash telemetry, and OEM-level reporting (Samsung, Huawei, etc.). | [Get `HageziAndroid.mrs`](https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziAndroid.mrs) |

### 3. Content Filtering & Parental Control

| Target Scope | Protection Focus | CDN Endpoint |
| :--- | :--- | :--- |
| **Gambling** | Global online casinos, unlicensed betting networks, sportsbooks, and lottery providers. | [Get `HageziGambling.mrs`](https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziGambling.mrs) |
| **NSFW** | International adult entertainment, pornography networks, and explicit media domains. | [Get `HageziNSFW.mrs`](https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziNSFW.mrs) |

---

## 🚀 Client Integration

### Method 1: Universal JavaScript Merge Driver (Recommended)

Use our pre-configured master script [`clash-verge-merge.js`](./clash-verge-merge.js) for **Clash Verge Rev**, **Mihomo Party**, and **FlClash**.

* **Dynamic Toggles:** Toggle individual protection layers (TIF, OS Telemetry, DynDNS, NSFW, Gambling).
* **Multi-Tier Switching:** Switch between `light`, `normal`, `pro`, `proplus`, and `ultimate` using a single variable.
* **Leak-Proof DNS:** Sets up hardened DoH over proxy tunnels with zero Geo-Database memory overhead.

👉 **[View Master Integration Script (`clash-verge-merge.js`)](./clash-verge-merge.js)**

---

### Method 2: Declarative `config.yaml` Setup

Add providers directly to your custom Mihomo configuration:

```yaml
rule-providers:
  # General Protection (Choose Preferred Tier)
  hagezi-proplus:
    type: http
    behavior: domain
    format: mrs
    url: "https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziProPlus.mrs"
    path: ./ruleset/HageziProPlus.mrs
    interval: 86400

  # Active Cyber Defense
  hagezi-tif:
    type: http
    behavior: domain
    format: mrs
    url: "https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziTIF.mrs"
    path: ./ruleset/HageziTIF.mrs
    interval: 43200

  # Hardware Telemetry (Example: Windows)
  hagezi-windows:
    type: http
    behavior: domain
    format: mrs
    url: "https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziWindows.mrs"
    path: ./ruleset/HageziWindows.mrs
    interval: 86400

rules:
  # Threat mitigation must precede routing rules
  - RULE-SET,hagezi-tif,REJECT
  - RULE-SET,hagezi-proplus,REJECT
  - RULE-SET,hagezi-windows,REJECT

  # Standard Routing Follow-through
  - GEOIP,private,DIRECT,no-resolve
  - MATCH,PROXY
```

---

## 🌐 The Unified Ecosystem

This repository acts as the global security layer within a two-pillar Mihomo networking ecosystem:

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                          UNIFIED CLIENT RUNTIME                             │
├──────────────────────────────────────┬──────────────────────────────────────┤
│  🛡️ GLOBAL LAYER (This Repo)         │  🇮🇷 REGIONAL LAYER (Iran Suite)       │
│  HaGeZi_BlockLists_mrs_format        │  Iran_Clash_Rules_mrs_format         │
│  ----------------------------------  │  ----------------------------------  │
│  • Global Ad & Tracker Blocking      │  • Domestic Split-Tunneling (.ir)    │
│  • Threat Intelligence Feeds (TIF)   │  • RIPE Prefix-Folded CIDRs          │
│  • Native Hardware OS Telemetry      │  • Domestic Payment Safeguards       │
│  • Worldwide Gambling & NSFW Filter  │  • Native Android Package Rules      │
└──────────────────────────────────────┴──────────────────────────────────────┘
                                       ▲
                                       │
                        ⚡ Driven by `clash-verge-merge.js`
```

* 🛡️ **Global Layer (This Repo):** [HaGeZi_BlockLists_mrs_format](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format)
* 🇮🇷 **Regional Layer:** [Iran_Clash_Rules_mrs_format](https://github.com/Erfan4700/Iran_Clash_Rules_mrs_format)
* ⚡ **Unified Driver:** [`clash-verge-merge.js`](./clash-verge-merge.js)

---

## 🎖️ Upstream Attribution & Credits

* **Blocklist Upstream:** Curated by [@hagezi](https://github.com/hagezi) at [hagezi/dns-blocklists](https://github.com/hagezi/dns-blocklists).
* **Binary Engine:** Maintained by the [@MetaCubeX](https://github.com/MetaCubeX) team at [MetaCubeX/mihomo](https://github.com/MetaCubeX/mihomo).

---

## 📄 License

This build automation suite is released under the **[MIT License](LICENSE)**. Upstream blocklist definitions remain the intellectual property of their original authors.
