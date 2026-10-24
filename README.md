# 🛡️ HaGeZi Blocklists — Pre-Compiled MRS Format

[![Automated Build](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/actions/workflows/build-mrs.yml/badge.svg)](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/actions)
[![Latest Release](https://img.shields.io/github/v/release/Erfan4700/HaGeZi_BlockLists_mrs_format?color=blue&label=Latest%20Release)](https://github.com/Erfan4700/HaGeZi_BlockLists_mrs_format/releases)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

High-performance, automated, and pre-compiled **Mihomo Rule-Set (`.mrs`)** binary versions of the world-renowned [HaGeZi DNS Blocklists](https://github.com/hagezi/dns-blocklists).

---

## 🚀 Key Advantages

* **⚡ Ultra-Low Memory & CPU Footprint:** Binary `.mrs` files eliminate parsing overhead, reducing RAM usage by up to 70% and accelerating profile loading to milliseconds.
* **🔄 Zero-Delay Upstream Sync:** Monitored every 20 minutes via GitHub Actions. If upstream commits change, new binaries are compiled immediately.
* **🌐 Global CDN Acceleration:** Distributed globally through jsDelivr with automated edge cache purging upon each release.
* **🏷️ Fully Automated Releases:** Each update generates a timestamped GitHub Release with standalone binary assets.

---

## 📦 Available Tiers & CDN URLs

All files are hosted on the `release` branch and served through jsDelivr CDN:

| Tier | Size | Best For | jsDelivr CDN URL |
| :--- | :--- | :--- | :--- |
| **Light** | ~500 KB | Low-resource devices | `https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziLight.mrs` |
| **Normal (Multi)** | ~1.1 MB | Standard everyday protection | `https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziNormal.mrs` |
| **Pro** | ~1.4 MB | Balanced privacy & analytics | `https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziPro.mrs` |
| **Pro++ (Pro.Plus)** | ~1.5 MB | Telemetry & aggressive trackers | `https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziProPlus.mrs` |
| **Ultimate** | ~1.6 MB | Maximum privacy & strictness | `https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziUltimate.mrs` |
| **TIF** | ~8.8 MB | Real-time cyber threats & phishing | `https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziTIF.mrs` |

---

## 🛠️ Usage in Mihomo / Clash.Meta

Add desired tiers under `rule-providers` in your `config.yaml`:

```yaml
rule-providers:
  hagezi-proplus:
    type: http
    behavior: domain
    format: mrs
    url: "https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziProPlus.mrs"
    path: ./ruleset/HageziProPlus.mrs
    interval: 86400

  hagezi-tif:
    type: http
    behavior: domain
    format: mrs
    url: "https://cdn.jsdelivr.net/gh/Erfan4700/HaGeZi_BlockLists_mrs_format@release/HageziTIF.mrs"
    path: ./ruleset/HageziTIF.mrs
    interval: 86400

rules:
  # Block Ads, Telemetry, and Trackers
  - RULE-SET,hagezi-proplus,REJECT
  # Block Phishing, Malware, and Botnets
  - RULE-SET,hagezi-tif,REJECT
```

---

## ⏱️ Update Automation Pipeline

1. **Commit Polling:** GitHub Actions polls the upstream `hagezi/dns-blocklists` repository every 20 minutes using the official GitHub API.
2. **Conditional Compilation:** If a new commit hash is detected (or upon manual dispatch), the latest Mihomo core is downloaded and converts all source wildcard domain lists into binary `.mrs` rule-sets.
3. **Artifact Deployment:** Compiled `.mrs` binaries are committed to the `release` branch and packaged into a dated GitHub Release.
4. **Cache Invalidation:** An automated purge pulse is sent to jsDelivr CDN edges to ensure instantaneous delivery of fresh rules.

---

## 🎖️ Credits & Acknowledgements

* **Upstream Blocklists:** Maintained by [@hagezi](https://github.com/hagezi) at [hagezi/dns-blocklists](https://github.com/hagezi/dns-blocklists).
* **Mihomo Core:** Developed by [@MetaCubeX](https://github.com/MetaCubeX) at [MetaCubeX/mihomo](https://github.com/MetaCubeX/mihomo).
