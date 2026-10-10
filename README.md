<div align="center">

# 🔧 Morphe Non-Root APK Builder

[![Daily Build](https://img.shields.io/github/actions/workflow/status/bzefas/Morphe-APKs/patch.yml?label=Daily%20Build&style=for-the-badge&color=2ea44f)](https://github.com/bzefas/Morphe-APKs/actions/workflows/patch.yml)
[![Latest Release](https://img.shields.io/github/v/release/bzefas/Morphe-APKs?style=for-the-badge&label=Latest%20Release&color=0366d6)](https://github.com/bzefas/Morphe-APKs/releases/latest)
[![Python Version](https://img.shields.io/badge/Python-3.11%2B-blue?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![License](https://img.shields.io/github/license/RookieEnough/Revanced-AutoBuilds?style=for-the-badge&color=orange)](LICENSE)

<p align="center">
This system automatically fetches the latest Morphe tools, downloads base APKs from multiple sources, applies patches, and publishes optimized APKs with architecture-specific builds.
</p>

[![View Latest Release](https://img.shields.io/badge/View%20Latest%20Release-0A0A0A?style=flat&logo=github&logoColor=white)](https://github.com/bzefas/Morphe-APKs/releases/latest)

</div>

---

## ✨ Key Features

- **Daily Updates:** Fully automated builds.
- **Multiple Sources:** Automatic fallback for reliable downloads.
- **Optimized APKs:** Builds for different Android architectures.
- **Custom Patches:** Easily enable or disable patches.
- **Ready to Install:** Automatically signed APKs.
- **Always Fresh:** Latest release replaces the previous one.

---

## 🛠️ Repository Structure

```text
revanced-nonroot/
├── .github/workflows/      # GitHub Actions automation
│   ├── patch.yml           # Daily automated builds (06:00 UTC)
│   └── manual-patch.yml    # Manual trigger workflow
├── apps/                   # APK source configurations
│   ├── apkmirror/          # APKMirror definitions
│   ├── apkpure/            # APKPure definitions
│   └── uptodown/           # UptoDown definitions
├── patches/                # Patch inclusion/exclusion rules
├── sources/                # ReVanced tool source definitions
├── src/                    # Core Python build logic
├── arch-config.json        # Architecture build matrix
├── patch-config.json       # App build configuration
└── requirements.txt        # Project dependencies

```

---

## ⚙️ Configuration Guide

This builder is highly configurable. You can adjust the following files to customize the build output.

### 1. App Selection (`patch-config.json`)

Define which applications the pipeline should attempt to build.

```json
{
  "patch_list": [
    { "app_name": "youtube", "source": "morphe" },
    { "app_name": "youtube-music", "source": "morphe" },
    { "app_name": "X", "source": "crimera" }
  ]
}

```

### 2. Architecture Matrix (`arch-config.json`)

Specify which CPU architectures to target for each application.

```json
[
  {
    "app_name": "youtube",
    "source": "morphe",
    "arches": ["arm64-v8a", "armeabi-v7a", "universal"]
  },
  {
    "app_name": "youtube-music",
    "source": "morphe",
    "arches": ["arm64-v8a", "armeabi-v7a"]
  }
]

```

### 3. Source Definitions

Located in the `apps/` directory. Example for `apps/apkmirror/youtube.json`:

```json
{
  "org": "google-inc",
  "name": "youtube",
  "type": "APK",
  "arch": "universal",
  "dpi": "nodpi",
  "package": "com.google.android.youtube",
  "version": ""
}

```

### 4. Patch Rules

Located in `patches/`. Example for `patches/youtube-morphe.txt`. Use `+` to force include and `-` to exclude.

```text
# Essential patches
+ microg-support
+ premium-heading
+ hide-infocard-suggestions

# Exclusions
- custom-branding
- amoled

```

---

## 🚀 Local Build Instructions

If you prefer to build the APKs on your own machine, follow these steps.

### Prerequisites

* Python 3.11 or higher
* Java Runtime Environment (JRE)
* `zip` utility
* `apksigner` (part of Android SDK Build-Tools)

### Installation & Execution

1. **Clone the repository:**
```bash
git clone https://github.com/RookieEnough/morphe-AutoBuilds.git
cd morphe-nonroot

```


2. **Install dependencies:**
```bash
pip install -r requirements.txt
pip install requests beautifulsoup4

```


3. **Run the build:**
You can build for a specific app and source.
```bash
export APP_NAME="youtube"
export SOURCE="morphe"
python -m src

```


4. **Target specific architecture (Optional):**
```bash
export APP_NAME="youtube"
export SOURCE="morphe"
export ARCH="arm64-v8a"  # Options: arm64-v8a, armeabi-v7a, universal
python -m src

```



---

## 🔄 GitHub Actions Workflows

### Daily Automated Build (`patch.yml`)

* **Schedule:** Runs daily at 06:00 UTC.
* **Function:** Iterates through all configured apps and architectures.
* **Output:** Updates the single "Latest" release tag.

### Manual Build (`manual-patch.yml`)

* **Trigger:** Manually via the GitHub Actions "Run workflow" button.
* **Capabilities:**
* Target specific apps.
* Target specific architectures.
* Force specific APK versions.
* Option to update the public release or just build artifacts.

---


## ⚠️ Disclaimer & Legal

> **Important:** This project is an automated build tool. The APKs provided in the releases are generated automatically using official Morphe tools and patches.

* **Affiliation:** These builds are **not** officially affiliated with the Morphe Team.
* **Usage:** Provided for educational and convenience purposes only. Use at your own risk.
* **GmsCore:** Morphe's MicroG-RE is required for these non-root apps to function correctly.
* **Updates:** Patches are automatically pulled from the latest sources; builds may occasionally contain experimental features.

**Made by RookieZ**

---

