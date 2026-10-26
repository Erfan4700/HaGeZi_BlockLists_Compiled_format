---
<div align="center">

# 🛡️ HaGeZi Universal Cyber Defense & Ruleset Suite
### Enterprise Automated Multi-Platform Binary Rule-Sets & Threat Feeds for Mihomo, Sing-box & Core Proxies

[![Automated Build Pipeline](https://img.shields.io/github/actions/workflow/status/Erfan4700/HaGeZi_BlockLists_mrs_format/build.yml?branch=main&label=Build%20Pipeline&style=flat-square&logo=github-actions&logoColor=white)](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/actions)
[![Direct Release](https://img.shields.io/badge/Release-GitHub%20Direct%20(Zero--Cache)-blue?style=flat-square&logo=github&logoColor=white)](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/latest)
[![Edge CDN Active](https://img.shields.io/badge/CDN-jsDelivr%20Purged-orange?style=flat-square&logo=jsdelivr&logoColor=white)](https://fastly.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/)
[![Upstream Synced](https://img.shields.io/badge/Upstream-HaGeZi%20Feeds-purple?style=flat-square&logo=adguard&logoColor=white)](https://github.com/hagezi/dns-blocklists)
[![Formats](https://img.shields.io/badge/Formats-MRS%20%7C%20SRS%20%7C%20GeoIP-emerald?style=flat-square&logo=shield&logoColor=white)](#-ruleset-catalog--distribution-endpoints)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow?style=flat-square)](LICENSE)

An automated high-throughput binary compilation pipeline and cyber defense engine generating pre-compiled **Mihomo (`.mrs`)**, **Sing-box (`.srs`)**, and custom **GeoIP (`.dat`)** rule-sets directly from HaGeZi's authoritative blocklists and NRD threat intelligence. Optimized for zero runtime parsing overhead, deterministic Radix-Tree lookups, and minimal memory consumption across enterprise gateways, open-source routers, and mobile environments.

[Architecture](#-pipeline--runtime-architecture) • [Client Matrix](#-multi-platform-client-matrix) • [Catalog & Endpoints](#-ruleset-catalog--distribution-endpoints) • [Client Setup](#-client--platform-integration) • [Upstream Attributions](#-telemetry-sources--upstream-attribution) • [Ecosystem](#-the-unified-two-pillar-ecosystem)

</div>

---

## 🌐 Multi-Platform Client Matrix

This repository acts as an authoritative, single source of truth, compiling upstream feeds into native runtime formats:

| Platform / Client Application | Target Core Engine | Native Binary Rule-Set | Legacy / Complementary |
| :--- | :--- | :---: | :---: |
| **Clash Verge Rev, Mihomo Party, FlClash** | Mihomo / Clash.Meta | **`.mrs`** (Native Radix Tree) | `config.yaml` / Providers |
| **Sing-box, Hiddify, NekoBox, Karing, Box4Magisk** | Sing-box Core (v1.8+) | **`.srs`** (Compiled Protobuf Binary) | Headless Rule-Set JSON |
| **Xray / V2Ray Gateways & Mihomo DNS Engine** | GeoIP / MMDB Engines | **`hagezi-geoip.dat`** | GeoIP Rule Matching |
| **Self-Hosted Infrastructure / Air-Gapped Mirrors**| All Client Runtimes | **`all-rulesets.tar.gz`** (Full Bundle) | Offline Local Assets |

---

## 📐 Pipeline & Runtime Architecture

Upstream blocklists and freshly observed domains are monitored continuously. When an upstream commit SHA changes, rules are normalized, deduplicated, and concurrently converted into native bytecode binaries:

```text
┌────────────────────────────────────────────────────────────────────────────────────────────────────────┐
│                                      UPSTREAM HAGEZI REPOSITORIES                                      │
├──────────────────────────────┬──────────────────────────────┬──────────────────────────────────────────┤
│        Standard Tiers        │     Threat Feeds (TIF)       │       OS Telemetry, DGA, Bypass & IP     │
│     (Light -> Ultimate)      │    (Malware / C2 / Scam)     │       (Apple, MS, Xiaomi, DoH, TLDs)     │
└──────────────┬───────────────┴──────────────┬───────────────┴────────────────────┬─────────────────────┘
               │                              │                                    │
               ▼                              ▼                                    ▼
┌────────────────────────────────────────────────────────────────────────────────────────────────────────┐
│                                   AUTOMATED GITHUB ACTIONS RUNNER                                      │
├────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ • Differential SHA verification & rule hygiene (deduplication, syntax normalization, prefix pruning)   │
│ • Concurrent Dual-Engine Binary Compilation:                                                           │
│   ├─ Mihomo Engine   ➔ `./mihomo convert-ruleset [domain|ipcidr] text <in> <out.mrs>`                  │
│   └─ Sing-box Engine ➔ `sing-box rule-set compile <in.json> -o <out.srs>`                              │
│ • Geo-Data Generation: Packaged `hagezi-geoip.dat` & consolidated `all-rulesets.tar.gz`                │
└───────────────────────────────────────────────────┬────────────────────────────────────────────────────┘
                                                    │
                         ┌──────────────────────────┴──────────────────────────┐
                         ▼                                                     ▼
┌─────────────────────────────────────────────────┐   ┌─────────────────────────────────────────────────┐
│            OFFICIAL GITHUB RELEASES             │   │            GLOBAL EDGE DISTRIBUTION             │
├─────────────────────────────────────────────────┤   ├─────────────────────────────────────────────────┤
│ • Rolling `latest` release tag                  │   │ • Committed to active `release` branch          │
│ • Over 90 pre-compiled binary assets            │   │ • Automated jsDelivr edge purge cache           │
│ • Direct permanent zero-latency download URLs   │   │ • Resilient failover mirrors                    │
└─────────────────────────────────────────────────┘   └─────────────────────────────────────────────────┘
```

### ⚡ Why Binary Rule-Sets (`.mrs` & `.srs`)?

Standard plain-text or YAML domain lists require significant runtime parsing, causing high latency, CPU load, and memory spikes on routers and mobile devices.

* **Memory-Mapped I/O (mmap):** Rule sets load directly as pre-structured radix trees into memory with **0 ms cold-start latency**.
* **RAM Optimization:** Binary engines reduce RAM utilization by **up to 80%** compared to traditional YAML or text lists.
* **Deterministic Matching:** Binary lookups execute sub-millisecond packet routing without regex backtracking bottlenecks during gigabit-speed traffic.

---

## 🛡️ Cyber Threat Mitigation & Whitelist Integrity

* **Tiered Multi-Layered Protection:** Tailor filtering from lightweight home setups (`HageziLight`) to zero-compromise hardening (`HageziUltimate`).
* **Active Threat Feeds (`HageziTIF`):** Blocks malicious command-and-control (C2) servers, trojans, ransomware callbacks, malware distributions, and zero-day threats.
* **High-Entropy DGA Suppression (`HageziDGA`):** Defends against domain generation algorithms used by modular malware to evade standard DNS filters.
* **Encrypted Bypass Neutralization (`HageziBypass`):** Restricts unmonitored DoH/DoT endpoints and circumvention proxies to maintain centralized network policies.
* **Native OS Telemetry Insulation:** Hardened shields for Windows, Apple, Samsung, Xiaomi, Huawei, Roku, and IoT smart TVs.

---

## 📦 Ruleset Catalog & Distribution Endpoints

All release assets are rebuilt continuously upon upstream commits and distributed via both zero-cache GitHub direct links and purged jsDelivr edge mirrors:

* **Direct GitHub Releases URL (Recommended - Real-time & Zero Cache Lag):**  
  `https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/`
* **Edge CDN URL (Failover):**  
  `https://fastly.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/`

### 0. Complete Archive & GeoIP Database
| Asset Name | Type | Scope / Description | Direct GitHub Download |
| :--- | :---: | :--- | :---: |
| **`all-rulesets.tar.gz`** | `archive` | Complete bundle containing all `.mrs` and `.srs` compiled assets | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/all-rulesets.tar.gz) |
| **`hagezi-geoip.dat`** | `dat` | Binary GeoIP database compiled from HaGeZi threat telemetry | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/hagezi-geoip.dat) |

---

### 1. Multi Tiers (General Ad & Tracker Protection)
*Select exactly **one** primary tier matching your device profile and tolerance for false positives.*

| List Name | Behavior | Scope & Recommended Profile | Action | Supported Formats |
| :--- | :---: | :--- | :---: | :---: |
| **`HageziLight`** | `domain` | Basic protection for legacy hardware and low-RAM devices | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziLight.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziLight.srs) |
| **`HageziNormal`** | `domain` | Balanced protection against consumer ads and baseline trackers | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNormal.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNormal.srs) |
| **`HageziPro`** | `domain` | **Recommended:** Thorough defense against trackers, metrics, and ads | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziPro.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziPro.srs) |
| **`HageziProPlus`** | `domain` | **Advanced:** Aggressive blocker for users with whitelist access | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziProPlus.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziProPlus.srs) |
| **`HageziUltimate`** | `domain` | **Maximum:** Strict privacy lockdown; may break non-standard sites | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziUltimate.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziUltimate.srs) |

#### Size-Optimized Mini Editions (Top 1M/10M Domains Only)

| List Name | Behavior | Scope & Recommended Profile | Action | Supported Formats |
| :--- | :---: | :--- | :---: | :---: |
| **`HageziProMini`** | `domain` | Size-optimized Pro edition for mobile and embedded routers | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziProMini.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziProMini.srs) |
| **`HageziProPlusMini`** | `domain` | Compact Pro++ edition for memory-limited environments | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziProPlusMini.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziProPlusMini.srs) |
| **`HageziUltimateMini`**| `domain` | Compact Ultimate edition for high-security embedded gateways | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziUltimateMini.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziUltimateMini.srs) |

---

### 2. Threat Intelligence Feeds (TIF & Active Cyber Defense)

| List Name | Behavior | Specific Scope | Action | Supported Formats |
| :--- | :---: | :--- | :---: | :---: |
| **`HageziTIF`** | `domain` | **Full Threat Feed:** Active malware, ransomware, botnets, and C2s | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziTIF.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziTIF.srs) |
| **`HageziTIFMedium`** | `domain` | Core high-impact cyber threat intelligence | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziTIFMedium.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziTIFMedium.srs) |
| **`HageziTIFMini`** | `domain` | Compact threat defense for memory-constrained clients | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziTIFMini.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziTIFMini.srs) |
| **`HageziFake`** | `domain` | Phishing clones, fraudulent webshops, and scam portals | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziFake.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziFake.srs) |
| **`HageziPopUpAds`** | `domain` | Intrusive pop-ups, coercive redirects, and browser hijacks | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziPopUpAds.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziPopUpAds.srs) |
| **`HageziDynDNS`** | `domain` | Dynamic DNS endpoints leveraged by polymorphic trojans | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziDynDNS.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziDynDNS.srs) |
| **`HageziBadwareHoster`**| `domain` | Hosting providers harboring malware and malicious scripts | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziBadwareHoster.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziBadwareHoster.srs) |
| **`HageziSpamTLDs`** | `domain` | High-abuse top-level domains (`.top`, `.shop`, `.cfd`, etc.) | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziSpamTLDs.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziSpamTLDs.srs) |
| **`HageziSpamTLDsAllow`**| `domain` | Whitelist for certified legitimate services on spam TLDs | `DIRECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziSpamTLDsAllow.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziSpamTLDsAllow.srs) |

---

### 3. High-Entropy & Domain Generation Algorithms (DGA)

| List Name | Behavior | Scope & Retention Period | Action | Supported Formats |
| :--- | :---: | :--- | :---: | :---: |
| **`HageziDGA7`** | `domain` | Algorithmic DGA domains active in the last 7 days | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziDGA7.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziDGA7.srs) |
| **`HageziDGA14`** | `domain` | Algorithmic DGA domains active in the last 14 days | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziDGA14.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziDGA14.srs) |

---

### 4. Bypass Prevention & Network Integrity

| List Name | Behavior | Scope & Protection Focus | Action | Supported Formats |
| :--- | :---: | :--- | :---: | :---: |
| **`HageziBypassAll`** | `domain` | Blocks external DoH/DoT/DoQ, commercial VPNs, and proxies | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziBypassAll.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziBypassAll.srs) |
| **`HageziBypassDoH`** | `domain` | Restricts evasive standalone public DoH endpoints | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziBypassDoH.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziBypassDoH.srs) |

---

### 5. Content Filtering & Parental Safeguards

| List Name | Behavior | Category / Purpose | Action | Supported Formats |
| :--- | :---: | :--- | :---: | :---: |
| **`HageziGambling`** | `domain` | Comprehensive online gambling, bookmakers, and casinos | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziGambling.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziGambling.srs) |
| **`HageziGamblingMedium`**| `domain` | Medium-tier gambling filter covering major operations | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziGamblingMedium.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziGamblingMedium.srs) |
| **`HageziGamblingMini`**| `domain` | Compact gambling filter for limited devices | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziGamblingMini.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziGamblingMini.srs) |
| **`HageziNSFW`** | `domain` | Adult content, pornography, and sexually explicit services | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNSFW.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNSFW.srs) |
| **`HageziSocial`** | `domain` | Social networks (Facebook, TikTok, Instagram, X/Twitter) | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziSocial.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziSocial.srs) |
| **`HageziAntiPiracy`** | `domain` | Warez, illicit streaming portals, and torrent indexes | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziAntiPiracy.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziAntiPiracy.srs) |
| **`HageziURLShortener`**| `domain` | Link shorteners masking destinations and trackers | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziURLShortener.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziURLShortener.srs) |
| **`HageziNoSafeSearch`**| `domain` | Search engines lacking enforced SafeSearch modes | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNoSafeSearch.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNoSafeSearch.srs) |

---

### 6. Native Hardware & OS Telemetry

| List Name | Behavior | Operating System / OEM Target | Action | Supported Formats |
| :--- | :---: | :--- | :---: | :---: |
| **`HageziNativeMicrosoft`** | `domain` | Windows diagnostics, telemetry beacons, and Office metrics | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeMicrosoft.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeMicrosoft.srs) |
| **`HageziNativeApple`** | `domain` | Analytics, crash loggers, and metrics across iOS / macOS | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeApple.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeApple.srs) |
| **`HageziNativeSamsung`** | `domain` | Tracking, telemetry, and OEM-level reporting on Samsung devices | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeSamsung.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeSamsung.srs) |
| **`HageziNativeXiaomi`** | `domain` | Analytics and ad-service telemetry across MIUI / HyperOS | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeXiaomi.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeXiaomi.srs) |
| **`HageziNativeHuawei`** | `domain` | Hardware telemetry endpoints on EMUI / HarmonyOS | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeHuawei.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeHuawei.srs) |
| **`HageziNativeOppoRealme`** | `domain` | Telemetry on ColorOS, RealmeUI, and OxygenOS | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeOppoRealme.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeOppoRealme.srs) |
| **`HageziNativeVivo`** | `domain` | Tracking services across OriginOS and FuntouchOS | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeVivo.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeVivo.srs) |
| **`HageziNativeLGWebOS`** | `domain` | Smart TV telemetry, ACR tracking, and diagnostics on webOS | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeLGWebOS.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeLGWebOS.srs) |
| **`HageziNativeRoku`** | `domain` | Usage analytics and telemetry reporting on Roku OS devices | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeRoku.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeRoku.srs) |
| **`HageziNativeAmazon`** | `domain` | Diagnostics on FireTV, Echo devices, and shopping analytics | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeAmazon.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeAmazon.srs) |
| **`HageziNativeTikTok`** | `domain` | Tracking servers tied to the core TikTok mobile client | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeTikTok.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeTikTok.srs) |
| **`HageziNativeTikTokExtended`**| `domain`| Aggressive fingerprinting rules targeting TikTok metrics | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeTikTokExtended.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeTikTokExtended.srs) |

---

### 7. IP Threat & Infrastructure Rulesets (IP-CIDR)

| List Name | Behavior | Target Description | Action | Supported Formats |
| :--- | :---: | :--- | :---: | :---: |
| **`HageziTIF_IP`** | `ipcidr` | Known malicious IPv4 addresses hosting C2 nodes and botnets | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziTIF_IP.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziTIF_IP.srs) |
| **`HageziDoH_IP`** | `ipcidr` | Public IPv4 addresses of encrypted DNS (DoH/DoT) resolvers | `REJECT` | [mrs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziDoH_IP.mrs) \| [srs](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziDoH_IP.srs) |

---

## 🚀 Client & Platform Integration

### 1. Sing-box Core (`config.json`) - Native Remote Rule-Sets

```json
{
  "route": {
    "rule_set": [
      {
        "tag": "hagezi-tif",
        "type": "remote",
        "format": "binary",
        "url": "https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziTIF.srs",
        "download_detour": "proxy"
      },
      {
        "tag": "hagezi-proplus",
        "type": "remote",
        "format": "binary",
        "url": "https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziProPlus.srs",
        "download_detour": "proxy"
      },
      {
        "tag": "hagezi-tif-ip",
        "type": "remote",
        "format": "binary",
        "url": "https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziTIF_IP.srs",
        "download_detour": "proxy"
      }
    ],
    "rules": [
      {
        "rule_set": ["hagezi-tif", "hagezi-tif-ip", "hagezi-proplus"],
        "action": "reject"
      }
    ]
  }
}
```

---

### 2. Mihomo / Clash.Meta (`config.yaml`) - Binary Rule Providers

```yaml
rule-providers:
  # 1. Main Adblock Tier (Pro Plus)
  hagezi-proplus:
    type: http
    behavior: domain
    format: mrs
    url: "https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziProPlus.mrs"
    path: ./ruleset/HageziProPlus.mrs
    interval: 86400

  # 2. Cyber Threat Intelligence (TIF Feed)
  hagezi-tif:
    type: http
    behavior: domain
    format: mrs
    url: "https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziTIF.mrs"
    path: ./ruleset/HageziTIF.mrs
    interval: 43200

  # 3. IP-CIDR Threat List
  hagezi-tif-ip:
    type: http
    behavior: ipcidr
    format: mrs
    url: "https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziTIF_IP.mrs"
    path: ./ruleset/HageziTIF_IP.mrs
    interval: 43200

rules:
  # Defense rules should precede global routing
  - RULE-SET,hagezi-tif,REJECT
  - RULE-SET,hagezi-tif-ip,REJECT,no-resolve
  - RULE-SET,hagezi-proplus,REJECT

  # Standard Routing Fallthrough
  - GEOIP,private,DIRECT,no-resolve
  - MATCH,PROXY
```

---

### 3. Universal Clash Verge Merge Integration

For users using **Clash Verge Rev**, **Mihomo Party**, or **FlClash**, the included `clash-verge-merge.js` script allows 1-click declarative integration:
* **Dynamic Tier Selection:** Toggle between `light`, `normal`, `pro`, `proplus`, and `ultimate` using a single variable.
* **Modular Add-ons:** Toggle TIF feeds, OEM device telemetry, NSFW, or gambling filters with zero manual YAML editing.

👉 **[View Master Integration Script (clash-verge-merge.js)](./clash-verge-merge.js)**

---

## 📡 Telemetry Sources & Upstream Attribution

* **DNS Blocklists & NRD Feeds:** Curated and maintained with excellence by [@hagezi](https://github.com/hagezi) at [hagezi/dns-blocklists](https://github.com/hagezi/dns-blocklists) and [hagezi/nrd](https://github.com/hagezi/nrd).
* **Mihomo MRS Compiler:** Maintained by [@MetaCubeX](https://github.com/MetaCubeX) at [MetaCubeX/mihomo](https://github.com/MetaCubeX/mihomo).
* **Sing-box SRS Compiler:** Maintained by [@SagerNet](https://github.com/SagerNet) at [sagernet/sing-box](https://github.com/SagerNet/sing-box).

---

## 🌐 The Unified Two-Pillar Ecosystem

This repository serves as the universal security layer within a two-pillar network architecture:

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
```

* 🛡️ **Global Security Layer:** [HaGeZi_BlockLists_mrs_format](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format)
* 🇮🇷 **Regional Routing Layer:** [Iran_Clash_Rules_mrs_format](https://github.com/Erfan4700/Iran_Clash_Rules_mrs_format)

---

## 📄 License

This compilation pipeline is released under the **[MIT License](LICENSE)**. Upstream blocklist definitions remain the intellectual property of their original creators and contributors.
