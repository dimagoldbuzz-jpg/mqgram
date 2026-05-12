# MQGram — Telegram iOS with Enhanced Privacy

<p align="center">
  <b>MQGram</b> — a privacy-focused Telegram client for iOS with advanced anti-delete, ghost mode, and device spoofing features.
</p>

---

## ✨ Key Features

| Feature | Description |
|---------|-------------|
| 🗑 **Anti-Delete** | Intercept and save deleted messages so you never miss anything |
| 👻 **Ghost Mode** | Hide read receipts, typing indicators, and online status |
| 📱 **Device Spoofing** | Mask your real device info for extra privacy |
| 🎙 **Voice Morpher** | Transform your voice messages with built-in presets |
| ⏱ **Send Delay** | Add a configurable delay before messages are sent — undo before it's too late |
| ✏️ **Edit History** | Track and view the full edit history of any message |
| 🔒 **Forward Protection Bypass** | Copy and forward messages from restricted chats |

## 🛠 Requirements

- **macOS** (latest recommended)
- **Xcode** — see `versions.json` for the exact required version
- **Python 3.x**
- **Bazel** (managed by the build system)

## 🚀 Quick Start

### 1. Get Telegram API Credentials

Go to [my.telegram.org](https://my.telegram.org), log in, and create an application to get your `api_id` and `api_hash`.

### 2. Clone the Repository

```bash
git clone --recursive -j8 https://github.com/dimagoldbuzz-jpg/mqgram.git
cd mqgram
```

### 3. Configure the Build

1. Generate a random identifier:
   ```bash
   openssl rand -hex 8
   ```
2. Create a dummy Xcode project named `Telegram` with organization identifier `org.<YOUR_HEX_ID>`.
3. Find your **Team ID** in Keychain Access → Certificates → Apple Development certificate → Details → Organizational Unit.
4. Edit `build-system/template_minimal_development_configuration.json` with your credentials.

### 4. Generate Xcode Project

```bash
python3 build-system/Make/Make.py \
    --cacheDir="$HOME/telegram-bazel-cache" \
    generateProject \
    --configurationPath=build-system/template_minimal_development_configuration.json \
    --xcodeManagedCodesigning
```

### 5. Build & Run

Open the generated Xcode project and run on your device or simulator.

---

## 🏗 Advanced Build Options

### Building an IPA (Release)

```bash
python3 build-system/Make/Make.py \
    --cacheDir="$HOME/telegram-bazel-cache" \
    build \
    --configurationPath=your_config.json \
    --codesigningInformationPath=your_profiles_dir \
    --buildNumber=100001 \
    --configuration=release_arm64
```

### Simulator Build (No Codesigning)

Add `--disableProvisioningProfiles` to skip codesigning for simulator builds.

---

## 📲 Install via Sideloading (AltStore / Sideloadly)

The easiest way to install MQGram on your iPhone — no jailbreak required.

### Option 1: Download from GitHub Releases (Recommended)

1. Go to [**Releases**](../../releases) and download the latest `.ipa` file
2. Install using one of the tools below:

### Option 2: Build via GitHub Actions

1. Go to the [**Actions**](../../actions) tab → **Build MQGram IPA**
2. Click **Run workflow** → **Run**
3. Wait for the build to complete (~30-60 min)
4. Download the IPA from **Artifacts**

### Installation Tools

| Tool | Platform | Link |
|------|----------|------|
| **AltStore** | Windows / macOS | [altstore.io](https://altstore.io) |
| **Sideloadly** | Windows / macOS | [sideloadly.io](https://sideloadly.io) |
| **SideStore** | iOS (no PC needed) | [sidestore.io](https://sidestore.io) |
| **Scarlet** | iOS | [usescarlet.com](https://usescarlet.com) |
| **TrollStore** | iOS (permanent) | [GitHub](https://github.com/opa334/TrollStore) |

### Step-by-Step: AltStore

1. Install **AltStore** on your PC/Mac from [altstore.io](https://altstore.io)
2. Connect your iPhone via USB
3. Open AltStore on PC → **Install AltStore** to your device
4. Download the MQGram `.ipa` file to your PC
5. Open AltStore on PC → **Install app** → select `MQGram.ipa`
6. Enter your Apple ID when prompted
7. MQGram will appear on your home screen

### Step-by-Step: Sideloadly

1. Download **Sideloadly** from [sideloadly.io](https://sideloadly.io)
2. Connect your iPhone via USB
3. Drag & drop the MQGram `.ipa` into Sideloadly
4. Enter your Apple ID and click **Start**
5. MQGram will be installed on your device

> **Note:** Free Apple IDs require re-signing every 7 days. Use AltStore's background refresh or a paid Apple Developer account ($99/year) for permanent installation.

---

## 🔧 GitHub Actions Setup (for automated builds)

To enable automated IPA builds, add these secrets in your repo **Settings → Secrets → Actions**:

| Secret | Required | Description |
|--------|----------|-------------|
| `TELEGRAM_API_ID` | **Yes** | Your Telegram API ID from [my.telegram.org](https://my.telegram.org) |
| `TELEGRAM_API_HASH` | **Yes** | Your Telegram API Hash |
| `BUNDLE_ID` | No | Custom bundle ID (default: `org.mqgram.MQGram`) |
| `TEAM_ID` | No | Apple Developer Team ID |

### Creating a Release

Push a tag to trigger an automatic build + release:

```bash
git tag v1.0.0
git push origin v1.0.0
```

The workflow will build the IPA and create a GitHub Release with the download link.

---

## ❓ FAQ

### "build-request.json not updated yet"
Cancel the build in Xcode and restart it.

### "no such package @rules_xcodeproj_generated"
Re-run the `generateProject` command after a system restart.

### Overriding Xcode Version
```bash
python3 build-system/Make/Make.py --overrideXcodeVersion generateProject ...
```

---

## 📂 Project Structure

```
MQGram/
├── Telegram/          # Core app and extensions
├── submodules/        # Feature libraries
│   ├── SettingsUI/    # MQGram settings controller
│   ├── TelegramCore/  # Anti-delete & edit history logic
│   └── TelegramUI/    # Chat UI with privacy overlays
├── build-system/      # Bazel build configuration
├── third-party/       # External dependencies
└── Swiftgram/         # Swiftgram integration layer
```

## 📄 License

This project is based on [Telegram iOS](https://github.com/nicegram/nicegram-ios) source code.
See [LICENSE](LICENSE) for details.

---

> **Note**: MQGram is an unofficial Telegram client. Use at your own discretion.
> For issues and suggestions, open a GitHub issue.
