# 🛡️ HaGeZi Multi-Format Ruleset Suite

### High-Performance Binary DNS Blocklists & Automated Upstream Engine
**Native Mihomo (`.mrs`) & sing-box (`.srs`) Formats**

[![Build Status](https://img.shields.io/badge/Build-Automated%20Rolling-brightgreen?style=flat-square&logo=githubactions)](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases)
[![GitHub Release](https://img.shields.io/github/v/release/Erfan4700/HaGeZi_BlockLists_mrs_format?style=flat-square&logo=github)](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/latest)
[![Formats](https://img.shields.io/badge/Formats-MRS%20%7C%20SRS%20%7C%20GeoIP-blue?style=flat-square)](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)

Automated, pre-compiled binary rule-sets generated directly from **HaGeZi's DNS Blocklists** and **NRD feeds**. Compiled for both **Mihomo (Clash.Meta)** and **sing-box** architectures, offering zero runtime regex parsing overhead, ultra-low memory footprint, and instant cold-starts across routers, servers, and mobile platforms.

[Ruleset Catalog](#-ruleset-catalog) • [Why Binary Rulesets?](#-why-binary-rule-sets-mrs--srs) • [Client Configuration](#-client-integration) • [Ecosystem](#-the-unified-ecosystem)

---

## 📐 Pipeline Architecture

Upstream blocklists are polled continuously. When upstream updates are detected, sources are normalized, validated, and concurrently compiled into high-speed binary artifacts:

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
│  • Differential SHA & Hash Validation                                       │
│  • Rule normalization & deduplication (+. prefixing / CIDR /32 masking)     │
│  • Concurrent Binary Compilation:                                           │
│    ├─ Mihomo Engine:   `mihomo convert-ruleset [domain/ipcidr] text ...`    │
│    └─ sing-box Engine: `sing-box rule-set compile ...`                      │
│  • Bundling: `all-rulesets.tar.gz` & `hagezi-geoip.dat`                     │
└──────────────────────────────────────┬──────────────────────────────────────┘
                                       │
                    ┌──────────────────┴──────────────────┐
                    ▼                                     ▼
┌───────────────────────────────────────┐ ┌───────────────────────────────────┐
│       OFFICIAL GITHUB RELEASES        │ │    GLOBAL EDGE DISTRIBUTION       │
├───────────────────────────────────────┤ ├───────────────────────────────────┤
│  • Rolling `latest` release tag       │ │  • Fast delivery via jsDelivr CDN │
│  • Over 90 compiled binary assets     │ │  • Automated edge cache purge     │
│  • Direct permanent download URLs     │ │  • Fallback secondary mirrors     │
└───────────────────────────────────────┘ └───────────────────────────────────┘
```

---

## ⚡ Why Binary Rule-Sets (`.mrs` & `.srs`)?

Standard plain-text or YAML lists require heavy string parsing on startup, causing high CPU consumption, memory bloating, and slow execution on low-RAM routers and mobile phones.

- **Memory-Mapped I/O (mmap):** Both Mihomo (`.mrs`) and sing-box (`.srs`) map pre-indexed binary trees directly into memory with near-zero cold-start latency.
- **RAM Optimization:** Saves up to **80% RAM** compared to classical plain-text domain files or raw YAML rule-providers.
- **Deterministic Tree Lookups:** Radix/Hash trie lookups allow gigabit line-rate processing without regular expression backtracking bottlenecks.

---

## 📦 Ruleset Catalog

All assets can be downloaded directly from GitHub Releases (`latest` tag) or via jsDelivr CDN.

> [!TIP]
> **CDN Endpoint Format:** If GitHub Releases are throttled or blocked in your network, replace:  
> `https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/<FileName>`  
> with:  
> `https://fastly.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/<FileName>`

### 📦 Bundles & GeoIP

| File Name | Description | Direct Download |
| :--- | :--- | :---: |
| **all-rulesets.tar.gz** | Complete compressed archive containing all `.mrs` and `.srs` files | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/all-rulesets.tar.gz) |
| **hagezi-geoip.dat** | Custom GeoIP database based on HaGeZi intelligence feeds | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/hagezi-geoip.dat) |

---

### 1. Multi Tiers (General Ad & Tracker Protection)
*Select **one** primary tier matching your device resources and tolerance for false positives.*

| List Name | Behavior | Scope & Recommended Profile | Mihomo (`.mrs`) | sing-box (`.srs`) |
| :--- | :---: | :--- | :---: | :---: |
| **HageziLight** | `domain` | Entry-level blocking for legacy/low-spec devices. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziLight.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziLight.srs) |
| **HageziNormal** | `domain` | Standard consumer ads, basic tracking, and malware. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNormal.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNormal.srs) |
| **HageziPro** | `domain` | **Recommended:** Balanced ad, telemetry & tracker blocking. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziPro.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziPro.srs) |
| **HageziProPlus** | `domain` | **Advanced:** Aggressive blocker for power users. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziProPlus.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziProPlus.srs) |
| **HageziUltimate** | `domain` | **Maximum:** Strict privacy lockdown (may break websites). | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziUltimate.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziUltimate.srs) |

#### Size-Optimized Mini Editions (Top 1M/10M Domains)

| List Name | Behavior | Scope & Recommended Profile | Mihomo (`.mrs`) | sing-box (`.srs`) |
| :--- | :---: | :--- | :---: | :---: |
| **HageziProMini** | `domain` | Compact Pro edition for mobile networks. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziProMini.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziProMini.srs) |
| **HageziProPlusMini** | `domain` | Compact Pro++ edition for mobile & browser clients. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziProPlusMini.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziProPlusMini.srs) |
| **HageziUltimateMini** | `domain` | Compact Ultimate edition for memory-limited routers. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziUltimateMini.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziUltimateMini.srs) |

---

### 2. Threat Intelligence Feeds (TIF & Cyber Defense)

| List Name | Behavior | Scope & Target Description | Mihomo (`.mrs`) | sing-box (`.srs`) |
| :--- | :---: | :--- | :---: | :---: |
| **HageziTIF** | `domain` | **Full Threat Feed:** Active malware, botnets, and C2s. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziTIF.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziTIF.srs) |
| **HageziTIFMedium** | `domain` | Core high-impact cyber threat domains. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziTIFMedium.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziTIFMedium.srs) |
| **HageziTIFMini** | `domain` | Compact TIF version for low-RAM appliances. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziTIFMini.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziTIFMini.srs) |
| **HageziFake** | `domain` | Phishing clones, scam storefronts, and deceitful portals. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziFake.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziFake.srs) |
| **HageziPopUpAds** | `domain` | Intrusive, malicious redirects and aggressive pop-up networks. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziPopUpAds.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziPopUpAds.srs) |
| **HageziDynDNS** | `domain` | Dynamic DNS hosts commonly abused by trojans & RATs. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziDynDNS.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziDynDNS.srs) |
| **HageziBadwareHoster** | `domain` | Malicious hosters and bulletproof infrastructure. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziBadwareHoster.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziBadwareHoster.srs) |
| **HageziSpamTLDs** | `domain` | Abused top-level domains (`.top`, `.shop`, `.cfd`, etc.). | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziSpamTLDs.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziSpamTLDs.srs) |
| **HageziSpamTLDsAllow** | `domain` | Whitelist for valid domains hosted on spam TLDs. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziSpamTLDsAllow.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziSpamTLDsAllow.srs) |

---

### 3. High-Entropy & Domain Generation Algorithms (DGA)

| List Name | Behavior | Scope & Retention Period | Mihomo (`.mrs`) | sing-box (`.srs`) |
| :--- | :---: | :--- | :---: | :---: |
| **HageziDGA7** | `domain` | Algorithmic DGA domains active in the last 7 days. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziDGA7.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziDGA7.srs) |
| **HageziDGA14** | `domain` | Algorithmic DGA domains active in the last 14 days. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziDGA14.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziDGA14.srs) |

---

### 4. Bypass Prevention & Network Integrity

| List Name | Behavior | Scope & Protection Target | Mihomo (`.mrs`) | sing-box (`.srs`) |
| :--- | :---: | :--- | :---: | :---: |
| **HageziBypassAll** | `domain` | Commercial VPNs, Tor nodes, proxies, and encrypted DNS. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziBypassAll.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziBypassAll.srs) |
| **HageziBypassDoH** | `domain` | Public DoH/DoT endpoints used to evade local filtering. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziBypassDoH.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziBypassDoH.srs) |

---

### 5. Content Filtering & Parental Safeguards

| List Name | Behavior | Category / Purpose | Mihomo (`.mrs`) | sing-box (`.srs`) |
| :--- | :---: | :--- | :---: | :---: |
| **HageziGambling** | `domain` | Online betting, casinos, and gambling services. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziGambling.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziGambling.srs) |
| **HageziGamblingMedium** | `domain` | Medium-tier gambling filter covering major portals. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziGamblingMedium.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziGamblingMedium.srs) |
| **HageziGamblingMini** | `domain` | Compact gambling filter for limited devices. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziGamblingMini.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziGamblingMini.srs) |
| **HageziNSFW** | `domain` | Adult content, pornography, and sexually explicit services. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNSFW.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNSFW.srs) |
| **HageziSocial** | `domain` | Social networks (Facebook, TikTok, Instagram, X, etc.). | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziSocial.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziSocial.srs) |
| **HageziAntiPiracy** | `domain` | Warez, illicit streaming, trackers, and copyright infringement. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziAntiPiracy.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziAntiPiracy.srs) |
| **HageziURLShortener** | `domain` | URL shorteners masking original endpoints and redirects. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziURLShortener.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziURLShortener.srs) |
| **HageziNoSafeSearch** | `domain` | Search engines lacking enforced SafeSearch filtering. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNoSafeSearch.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNoSafeSearch.srs) |

---

### 6. Native Hardware & OS Telemetry

| List Name | Behavior | Operating System / OEM Target | Mihomo (`.mrs`) | sing-box (`.srs`) |
| :--- | :---: | :--- | :---: | :---: |
| **HageziNativeMicrosoft** | `domain` | Windows diagnostics, telemetry beacons, and Office analytics. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeMicrosoft.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeMicrosoft.srs) |
| **HageziNativeApple** | `domain` | Diagnostic loggers and telemetry across iOS, iPadOS, macOS. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeApple.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeApple.srs) |
| **HageziNativeSamsung** | `domain` | Telemetry, analytics, and OEM tracking on Samsung devices. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeSamsung.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeSamsung.srs) |
| **HageziNativeXiaomi** | `domain` | Diagnostics, logging, and ad metrics across MIUI & HyperOS. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeXiaomi.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeXiaomi.srs) |
| **HageziNativeHuawei** | `domain` | Hardware telemetry on Huawei EMUI, HarmonyOS, and IoT. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeHuawei.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeHuawei.srs) |
| **HageziNativeOppoRealme**| `domain` | Telemetry on ColorOS, RealmeUI, and OxygenOS handsets. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeOppoRealme.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeOppoRealme.srs) |
| **HageziNativeVivo** | `domain` | Tracking services across OriginOS and FuntouchOS. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeVivo.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeVivo.srs) |
| **HageziNativeLGWebOS** | `domain` | Smart TV analytics, ACR, and ad beacons on webOS. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeLGWebOS.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeLGWebOS.srs) |
| **HageziNativeRoku** | `domain` | User telemetry and usage analytics on Roku OS devices. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeRoku.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeRoku.srs) |
| **HageziNativeAmazon** | `domain` | Telemetry on FireTV, Echo, Alexa, and Amazon hardware. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeAmazon.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeAmazon.srs) |
| **HageziNativeTikTok** | `domain` | Tracking beacons and telemetry servers in TikTok apps. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeTikTok.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeTikTok.srs) |
| **HageziNativeTikTokExtended**| `domain` | Strict telemetry & auxiliary data pipelines for TikTok. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeTikTokExtended.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziNativeTikTokExtended.srs) |

---

### 7. IP Threat & Infrastructure Rulesets (IP-CIDR)

> [!IMPORTANT]
> The following rulesets contain IP addresses and subnets.
> - **Mihomo:** Must be declared with `behavior: ipcidr`.
> - **sing-box:** Handled automatically as `ip_cidr` rules within `.srs`.

| List Name | Behavior | Target Description | Mihomo (`.mrs`) | sing-box (`.srs`) |
| :--- | :---: | :--- | :---: | :---: |
| **HageziTIF_IP** | `ipcidr` | Malicious IPv4 addresses running C2 servers and botnets. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziTIF_IP.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziTIF_IP.srs) |
| **HageziDoH_IP** | `ipcidr` | IPv4 addresses of public & evasive DoH/DoT resolvers. | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziDoH_IP.mrs) | [Download](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziDoH_IP.srs) |

---

## 🚀 Client Integration

### Method 1: sing-box (Remote Binary Rule-Sets)

Add to the `route.rule_set` array in your `config.json`:

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

### Method 2: Mihomo / Clash.Meta (`config.yaml`)

Add binary rule-providers to your `config.yaml`:

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

  # 2. Cyber Threat Defense (TIF)
  hagezi-tif:
    type: http
    behavior: domain
    format: mrs
    url: "https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziTIF.mrs"
    path: ./ruleset/HageziTIF.mrs
    interval: 43200

  # 3. IP Threat Intelligence
  hagezi-tif-ip:
    type: http
    behavior: ipcidr
    format: mrs
    url: "https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases/download/latest/HageziTIF_IP.mrs"
    path: ./ruleset/HageziTIF_IP.mrs
    interval: 43200

rules:
  # Threat mitigation and adblocking
  - RULE-SET,hagezi-tif,REJECT
  - RULE-SET,hagezi-tif-ip,REJECT,no-resolve
  - RULE-SET,hagezi-proplus,REJECT

  # Routing Fallthrough
  - GEOIP,private,DIRECT,no-resolve
  - MATCH,PROXY
```

---

### Method 3: Clash GUI Integration (Verge Rev / Mihomo Party)

You can use the integration script `clash-verge-merge.js` inside Clash Verge Rev, Mihomo Party, or FlClash for 1-click dynamic configuration switching.

- **Dynamic Toggles:** Easily enable/disable TIF, OS Telemetry, DynDNS, NSFW, or Gambling rules.
- **Single-Variable Switching:** Switch between `light`, `normal`, `pro`, `proplus`, and `ultimate` instantly.

👉 **[View Master Integration Script (clash-verge-merge.js)](./clash-verge-merge.js)**

---

## 🌐 The Unified Ecosystem

This repository forms the global security core of a two-pillar proxy architecture:

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

- 🛡️ **Global Security Layer:** [HaGeZi_BlockLists_mrs_format](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format)
- 🇮🇷 **Regional Routing Layer:** [Iran_Clash_Rules_mrs_format](https://github.com/Erfan4700/Iran_Clash_Rules_mrs_format)

---

## 🎖️ Upstream Attribution & Credits

- **Rule Sources:** Curated and maintained with excellence by [@hagezi](https://github.com/hagezi) at [hagezi/dns-blocklists](https://github.com/hagezi/dns-blocklists) and [hagezi/nrd](https://github.com/hagezi/nrd).
- **Mihomo Compiler:** Maintained by [@MetaCubeX](https://github.com/MetaCubeX) at [MetaCubeX/mihomo](https://github.com/MetaCubeX/mihomo).
- **sing-box Compiler:** Maintained by [@SagerNet](https://github.com/SagerNet) at [sagernet/sing-box](https://github.com/SagerNet/sing-box).

---

## 📄 License

This compilation and build automation suite is licensed under the [MIT License](LICENSE). Upstream blocklist definitions remain the intellectual property of their original creators.
