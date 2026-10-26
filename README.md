
<div align="center">

# 🛡️ HaGeZi Blocklists (Native Mihomo MRS Format)
### High-Performance Binary DNS Blocklists & Automated Upstream Engine

[![Build Status](https://img.shields.io/github/actions/workflow/status/Erfan4700/HaGeZi_BlockLists_mrs_format/build-mrs.yml?branch=main&label=CI%2FCD%20Build&style=flat-square&logo=github-actions&logoColor=white)](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/actions)
[![GitHub Release](https://img.shields.io/github/v/release/Erfan4700/HaGeZi_BlockLists_mrs_format?display_name=tag&label=Rolling%20Release&style=flat-square&logo=github&logoColor=white)](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/tag/latest)
[![Sync Cadence](https://img.shields.io/badge/Sync%20Cadence-20%20Minutes-blue?style=flat-square&logo=git&logoColor=white)](#-pipeline-architecture)
[![Format](https://img.shields.io/badge/Format-Binary%20MRS%20(Domain%20%26%20IP--CIDR)-blueviolet?style=flat-square&logo=webassembly&logoColor=white)](#-why-mihomo-rule-set-mrs)
[![License: MIT](https://img.shields.io/badge/License-MIT-emerald?style=flat-square)](LICENSE)

Automated, pre-compiled **Mihomo Rule-Set (`.mrs`)** binaries generated directly from [HaGeZi's DNS Blocklists](https://github.com/hagezi/dns-blocklists) and [NRD feeds](https://github.com/hagezi/nrd). Optimized for ultra-low memory footprints, zero runtime regex parsing overhead, and instant cold-starts across Mihomo (Clash.Meta) environments.

[Ruleset Catalog](#-ruleset-catalog) • [Why MRS?](#-why-mihomo-rule-set-mrs) • [Client Setup](#-client-integration) • [Ecosystem](#-the-unified-ecosystem)

</div>

---

## 📐 Pipeline Architecture

Upstream blocklists are polled every 20 minutes. When a new upstream commit SHA is detected, rule files are converted into native bytecode binaries and published immediately via GitHub Releases and the edge branch:

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                       UPSTREAM HAGEZI REPOSITORIES                          │
├─────────────────────┬──────────────────────┬────────────────────────────────┤
│    Standard Tiers   │  Threat Feeds (TIF)  │ OS Telemetry, DGA, Bypass & IP │
│ (Light -> Ultimate) │ (Malware / C2 / DNS) │ (Apple, MS, Xiaomi, DoH, TLDs) │
└──────────┬──────────┴──────────┬───────────┴───────────────┬────────────────┘
           │                     │                           │
           ▼                     ▼                           ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                     AUTOMATED GITHUB ACTIONS RUNNER                         │
├─────────────────────────────────────────────────────────────────────────────┤
│  • Differential SHA validation (avoids redundant compiles)                  │
│  • Rule normalization & deduplication (+. prefixing / CIDR /32 masking)     │
│  • Binary compilation via Mihomo Engine:                                    │
│    - Domain rules:  `./mihomo convert-ruleset domain text in.txt out.mrs`   │
│    - IP lists:      `./mihomo convert-ruleset ipcidr text in.txt out.mrs`   │
└──────────────────────────────────────┬──────────────────────────────────────┘
                                       │
                    ┌──────────────────┴──────────────────┐
                    ▼                                     ▼
┌───────────────────────────────────────┐ ┌───────────────────────────────────┐
│       OFFICIAL GITHUB RELEASES        │ │    GLOBAL EDGE DISTRIBUTION       │
├───────────────────────────────────────┤ ├───────────────────────────────────┤
│  • Rolling `latest` release tag       │ │  • Committed to `release` branch  │
│  • In-place binary assets overwrite   │ │  • Automated jsDelivr edge purge  │
│  • Direct permanent download URLs     │ │  • Fallback secondary mirrors     │
└───────────────────────────────────────┘ └───────────────────────────────────┘
```

---

## ⚡ Why Mihomo Rule-Set (`.mrs`)?

Standard plain-text or YAML domain lists require significant runtime parsing, causing high latency, CPU load, and memory spikes on routers and mobile devices.

* **Memory-Mapped I/O (`mmap`):** Mihomo loads `.mrs` binaries as pre-structured radix/hash trees directly into memory with **0 ms** initial parsing time.
* **RAM Optimization:** Reduces memory consumption by **up to 80%** compared to YAML or classical text lists.
* **Deterministic Matching:** Binary lookups ensure sub-millisecond packet routing without regex backtracking bottlenecks during gigabit-speed traffic.

---

## 📦 Ruleset Catalog

All binary downloads default to **GitHub Direct Releases** (`latest` rolling tag).

> [!TIP]
> **CDN Mirror Alternative:** If GitHub is throttled in your region, replace:  
> `https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/<FileName>.mrs`  
> with the fast jsDelivr CDN endpoint:  
> `https://fastly.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/<FileName>.mrs`

---

### 1. Multi Tiers (General Ad & Tracker Protection)
*Select exactly **one** main tier based on your device profile and tolerance for false positives.*

| List Name | Behavior | Scope & Recommended Profile | Direct GitHub Download |
| :--- | :---: | :--- | :--- |
| **HageziLight** | `domain` | Basic protection for legacy hardware and low-RAM routers. | [Download `HageziLight.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziLight.mrs) |
| **HageziNormal** | `domain` | All-round protection against consumer ads, tracking, and malware. | [Download `HageziNormal.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNormal.mrs) |
| **HageziPro** | `domain` | **Recommended:** Balanced protection, metrics, tracking, and telemetry. | [Download `HageziPro.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziPro.mrs) |
| **HageziProPlus** | `domain` | **Advanced:** Aggressive blocker for users with whitelisting capabilities. | [Download `HageziProPlus.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziProPlus.mrs) |
| **HageziUltimate** | `domain` | **Maximum:** Strict privacy lockdown; may break some app functions. | [Download `HageziUltimate.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziUltimate.mrs) |

#### Size-Optimized Mini Editions (Top 1M/10M Domains Only)
| List Name | Behavior | Scope & Target Profile | Direct GitHub Download |
| :--- | :---: | :--- | :--- |
| **HageziProMini** | `domain` | Size-optimized version of Pro for mobile and constrained devices. | [Download `HageziProMini.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziProMini.mrs) |
| **HageziProPlusMini** | `domain` | Size-optimized version of Pro++ for browser and mobile environments. | [Download `HageziProPlusMini.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziProPlusMini.mrs) |
| **HageziUltimateMini** | `domain` | Size-optimized version of Ultimate for embedded routers. | [Download `HageziUltimateMini.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziUltimateMini.mrs) |

---

### 2. Threat Intelligence & Cyber Defense (Recommended Add-ons)
*Can be combined with any Multi tier to block active cyber attacks.*

| List Name | Behavior | Scope & Description | Direct GitHub Download |
| :--- | :---: | :--- | :--- |
| **HageziTIF** | `domain` | **Full Threat Feeds:** Active malware, phishing, ransomware, botnets, and C2s. | [Download `HageziTIF.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziTIF.mrs) |
| **HageziTIFMedium** | `domain` | Medium-sized TIF feed containing core primary threat intelligence. | [Download `HageziTIFMedium.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziTIFMedium.mrs) |
| **HageziTIFMini** | `domain` | Compact TIF version for memory-constrained clients. | [Download `HageziTIFMini.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziTIFMini.mrs) |
| **HageziFake** | `domain` | Blocks scam shops, phishing clones, traps, and fraudulent sites. | [Download `HageziFake.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziFake.mrs) |
| **HageziPopUpAds** | `domain` | Suppresses intrusive, aggressive, and malicious pop-up networks. | [Download `HageziPopUpAds.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziPopUpAds.mrs) |
| **HageziDynDNS** | `domain` | Dynamic DNS endpoints frequently abused by modular trojans and RATs. | [Download `HageziDynDNS.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziDynDNS.mrs) |
| **HageziBadwareHoster**| `domain` | Hosting providers repeatedly harboring malicious user content. | [Download `HageziBadwareHoster.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziBadwareHoster.mrs) |
| **HageziSpamTLDs** | `domain` | High-abuse top-level domains (`.top`, `.shop`, `.gdn`, etc.). | [Download `HageziSpamTLDs.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziSpamTLDs.mrs) |
| **HageziSpamTLDsAllow**| `domain` | Whitelist exceptions for legitimate services hosted on spam TLDs. | [Download `HageziSpamTLDsAllow.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziSpamTLDsAllow.mrs) |

---

### 3. High-Entropy & Domain Generation Algorithms (DGA)
*Freshly registered, randomized domains utilized by evasive malware C2 channels.*

| List Name | Behavior | Scope & Retention Period | Direct GitHub Download |
| :--- | :---: | :--- | :--- |
| **HageziDGA7** | `domain` | High-entropy DGA domains observed in the last 7 days. | [Download `HageziDGA7.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziDGA7.mrs) |
| **HageziDGA14** | `domain` | High-entropy DGA domains observed in the last 14 days. | [Download `HageziDGA14.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziDGA14.mrs) |
| **HageziDGA30** | `domain` | Extended 30-day DGA threat collection. | [Download `HageziDGA30.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziDGA30.mrs) |

---

### 4. Bypass Prevention & Network Integrity
*Enforces local DNS rules by preventing clients and applications from bypassing them.*

| List Name | Behavior | Scope & Protection Focus | Direct GitHub Download |
| :--- | :---: | :--- | :--- |
| **HageziBypassAll** | `domain` | Blocks encrypted DNS resolvers (DoH/DoT/DoQ), commercial VPNs, proxies, and Tor. | [Download `HageziBypassAll.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziBypassAll.mrs) |
| **HageziBypassDoH** | `domain` | Restricts outbound queries targeting standalone public encrypted DNS (DoH) servers. | [Download `HageziBypassDoH.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziBypassDoH.mrs) |

---

### 5. Content Filtering & Parental Safeguards

| List Name | Behavior | Protection Scope | Direct GitHub Download |
| :--- | :---: | :--- | :--- |
| **HageziGambling** | `domain` | Online casinos, bookmakers, unlicensed betting, and lottery portals. | [Download `HageziGambling.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziGambling.mrs) |
| **HageziGamblingMedium**| `domain` | Medium-tier gambling filter covering major betting operations. | [Download `HageziGamblingMedium.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziGamblingMedium.mrs) |
| **HageziGamblingMini** | `domain` | Compact gambling filter for devices with limited memory. | [Download `HageziGamblingMini.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziGamblingMini.mrs) |
| **HageziNSFW** | `domain` | Adult media networks, pornography, and sexually explicit services. | [Download `HageziNSFW.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNSFW.mrs) |
| **HageziSocial** | `domain` | Social networks (Facebook, TikTok, Instagram, X/Twitter, Snapchat). | [Download `HageziSocial.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziSocial.mrs) |
| **HageziAntiPiracy** | `domain` | Warez, unauthorized streaming, torrent indexes, and copyright-infringing sites. | [Download `HageziAntiPiracy.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziAntiPiracy.mrs) |
| **HageziURLShortener** | `domain` | Link shorteners masking destination URLs and malicious redirects. | [Download `HageziURLShortener.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziURLShortener.mrs) |
| **HageziNoSafeSearch** | `domain` | Search engines that do not implement or support SafeSearch restrictions. | [Download `HageziNoSafeSearch.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNoSafeSearch.mrs) |

---

### 6. Native Hardware & OS Telemetry
*Neutralizes built-in OEM telemetry, tracking beacons, and diagnostics.*

| Target Platform | Behavior | Description | Direct GitHub Download |
| :--- | :---: | :--- | :--- |
| **HageziNativeMicrosoft**| `domain` | Windows diagnostics, telemetry beacons, Office telemetry, and MSN analytics. | [Download `HageziNativeMicrosoft.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeMicrosoft.mrs) |
| **HageziNativeApple** | `domain` | Analytics, diagnostic loggers, and metrics across iOS, iPadOS, and macOS. | [Download `HageziNativeApple.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeApple.mrs) |
| **HageziNativeSamsung**| `domain` | Tracking, diagnostic telemetry, and OEM-level reporting on Samsung devices. | [Download `HageziNativeSamsung.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeSamsung.mrs) |
| **HageziNativeXiaomi** | `domain` | Diagnostic reporting, tracking, and ad-service telemetry across MIUI / HyperOS. | [Download `HageziNativeXiaomi.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeXiaomi.mrs) |
| **HageziNativeHuawei** | `domain` | Huawei mobile and IoT hardware telemetry reporting endpoints. | [Download `HageziNativeHuawei.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeHuawei.mrs) |
| **HageziNativeOppoRealme**| `domain`| Telemetry services on ColorOS, RealmeUI, and OnePlus handsets. | [Download `HageziNativeOppoRealme.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeOppoRealme.mrs) |
| **HageziNativeVivo** | `domain` | Diagnostic services and user telemetry across OriginOS and FuntouchOS. | [Download `HageziNativeVivo.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeVivo.mrs) |
| **HageziNativeLGWebOS**| `domain` | Smart TV telemetry, automatic content recognition (ACR), and analytics. | [Download `HageziNativeLGWebOS.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeLGWebOS.mrs) |
| **HageziNativeRoku** | `domain` | Analytics and telemetry reporting on Roku OS devices. | [Download `HageziNativeRoku.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeRoku.mrs) |
| **HageziNativeAmazon** | `domain` | Tracking endpoints on FireTV, Echo devices, and shopping analytics. | [Download `HageziNativeAmazon.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeAmazon.mrs) |
| **HageziNativeTikTok** | `domain` | Fingerprinting and tracking servers tied to the TikTok infrastructure. | [Download `HageziNativeTikTok.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeTikTok.mrs) |
| **HageziNativeTikTokExtended**| `domain`| Aggressive fingerprinting rules targeting TikTok analytics infrastructure. | [Download `HageziNativeTikTokExtended.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeTikTokExtended.mrs) |

---

### 7. IP-Level Threat & Infrastructure Rulesets (IP-CIDR)
> [!IMPORTANT]
> The following rulesets contain IP addresses and subnets. In your Mihomo configuration, they must be declared with `behavior: ipcidr` rather than `domain`.

| List Name | Behavior | Target Description | Direct GitHub Download |
| :--- | :---: | :--- | :--- |
| **HageziTIF_IP** | `ipcidr` | Known IPv4 addresses running command-and-control servers, malware, and spam. | [Download `HageziTIF_IP.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziTIF_IP.mrs) |
| **HageziDoH_IP** | `ipcidr` | Known IPv4 addresses of public and evasive encrypted DNS (DoH/DoT) resolvers. | [Download `HageziDoH_IP.mrs`](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziDoH_IP.mrs) |

---

## 🚀 Client Integration

### Declarative `config.yaml` Setup

Add providers directly to your custom Mihomo configuration using direct GitHub Release URLs:

```yaml
rule-providers:
  # 1. Domain Rule Provider (Example: Pro Plus Tier)
  hagezi-proplus:
    type: http
    behavior: domain
    format: mrs
    url: "https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziProPlus.mrs"
    path: ./ruleset/HageziProPlus.mrs
    interval: 86400

  # 2. Cyber Threat Defense (TIF Feed)
  hagezi-tif:
    type: http
    behavior: domain
    format: mrs
    url: "https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziTIF.mrs"
    path: ./ruleset/HageziTIF.mrs
    interval: 43200

  # 3. Native OS Telemetry (Example: Windows)
  hagezi-windows:
    type: http
    behavior: domain
    format: mrs
    url: "https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeMicrosoft.mrs"
    path: ./ruleset/HageziNativeMicrosoft.mrs
    interval: 86400

  # 4. IP-CIDR Threat List (Note the behavior: ipcidr)
  hagezi-tif-ip:
    type: http
    behavior: ipcidr
    format: mrs
    url: "https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziTIF_IP.mrs"
    path: ./ruleset/HageziTIF_IP.mrs
    interval: 43200

rules:
  # Threat mitigation must precede general routing rules
  - RULE-SET,hagezi-tif,REJECT
  - RULE-SET,hagezi-tif-ip,REJECT,no-resolve
  - RULE-SET,hagezi-proplus,REJECT
  - RULE-SET,hagezi-windows,REJECT

  # Standard Routing Fallthrough
  - GEOIP,private,DIRECT,no-resolve
  - MATCH,PROXY
```

---

## 🌐 The Unified Ecosystem

This repository serves as the global security layer within a two-pillar Mihomo networking ecosystem:

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
```

* 🛡️ **Global Layer (This Repo):** [HaGeZi_BlockLists_mrs_format](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format)
* 🇮🇷 **Regional Layer:** [Iran_Clash_Rules_mrs_format](https://github.com/Erfan4700/iran-routing-rules)

---

## 🎖️ Upstream Attribution & Credits

* **Blocklist Upstream:** Curated by [@hagezi](https://github.com/hagezi) at [hagezi/dns-blocklists](https://github.com/hagezi/dns-blocklists) and [hagezi/nrd](https://github.com/hagezi/nrd).
* **Binary Engine:** Maintained by the [@MetaCubeX](https://github.com/MetaCubeX) team at [MetaCubeX/mihomo](https://github.com/MetaCubeX/mihomo).

---

## 📄 License

This build automation suite is released under the **[MIT License](LICENSE)**. Upstream blocklist definitions remain the intellectual property of their original authors.
