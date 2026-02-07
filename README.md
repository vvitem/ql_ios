# ql_ios
青龙 IOS客户端
# iOS Unsigned IPA Build & Usage Guide (无证书 IPA 构建与使用指南)

[English](#english) | [中文](#chinese)

<a name="english"></a>
## 🇬🇧 English

This project supports generating **unsigned IPA files** (Unsigned IPA), which is suitable for installation via **TrollStore** or self-signing tools (like **Sideloadly**, **AltStore**).

### 🚀 Why use Unsigned IPA?

- **No Developer Account Required**: You don't need to pay $99/year for an Apple Developer Program account.
- **TrollStore Support**: If your device supports TrollStore (iOS 14.0 - 17.0, depending on version), you can install it permanently with full system permissions.
- **Self-Signing**: You can use your own free Apple ID to sign and install the app (expires every 7 days).

### 🛠 How to Build Unsigned IPA

We provide a simple way to build an IPA without a certificate using `xcodebuild`.

#### Prerequisites
- macOS with Xcode installed.

#### Build Steps

Run the following commands in Terminal at the project root:

```bash
# 1. Build Release version (Disable Code Signing)
# This command compiles the app for generic iOS devices without signing requirements
xcodebuild -project qlmb.xcodeproj \
           -scheme qlmb \
           -configuration Release \
           -destination 'generic/platform=iOS' \
           clean build \
           CODE_SIGN_IDENTITY="" \
           CODE_SIGNING_REQUIRED=NO \
           -derivedDataPath ./build_output

# 2. Create Payload directory structure
mkdir -p Payload

# 3. Copy the compiled .app to Payload
# Note: The path depends on the build output
cp -R ./build_output/Build/Products/Release-iphoneos/qlmb.app Payload/

# 4. Zip it to create .ipa
zip -r qlmb.ipa Payload

# 5. (Optional) Clean up temporary files
rm -rf Payload build_output
```

After these steps, you will get a `qlmb.ipa` file in the current directory.

### 📱 Installation Guide

#### Option 1: TrollStore (Recommended)
**Requirements**: Supported iOS version (iOS 14.0 - 17.0 typically).
1. Transfer the `qlmb.ipa` to your iPhone (via AirDrop, iCloud, etc.).
2. Open **TrollStore** on your phone.
3. Tap `+` -> `Install IPA from File`.
4. Select the `qlmb.ipa`.
5. **Done!** The app is installed permanently and has extended privileges.

#### Option 2: Sideloadly / AltStore (Self-Signing)
**Requirements**: Any iOS device, a computer, and a free Apple ID.
1. Download and install [Sideloadly](https://sideloadly.io/) or [AltStore](https://altstore.io/).
2. Connect your iPhone to the computer.
3. Drag `qlmb.ipa` into Sideloadly.
4. Enter your Apple ID email.
5. Click **Start**.
6. **Note**: Free accounts require re-signing every 7 days.

---

<a name="chinese"></a>
## 🇨🇳 中文

本项目支持生成 **无证书 IPA 文件** (Unsigned IPA)，适用于通过 **TrollStore (巨魔)** 安装或使用 **自签名工具** (如 Sideloadly, AltStore) 进行安装。

### 🚀 为什么要使用无证书 IPA?

- **无需开发者账号**: 不需要支付 $99/年的 Apple Developer Program 费用。
- **支持 TrollStore**: 如果您的设备支持 TrollStore (通常是 iOS 14.0 - 17.0)，可以永久安装应用并获得完整权限。
- **自签名支持**: 您可以使用免费的 Apple ID 进行签名安装 (有效期 7 天，之后需重签)。

###  安装指南

#### 方案 1: TrollStore (推荐)
**要求**: 支持的 iOS 版本 (通常是 iOS 14.0 - 17.0)。
1. 将 `qlmb.ipa` 传输到您的 iPhone (通过 AirDrop, iCloud 等)。
2. 在手机上打开 **TrollStore**。
3. 点击右上角的 `+` -> `Install IPA from File`。
4. 选择 `qlmb.ipa` 文件。
5. **完成！** 应用已永久安装。

#### 方案 2: Sideloadly / AltStore (自签名)
**要求**: 任意 iOS 设备，一台电脑，以及一个免费的 Apple ID。
1. 下载并安装 [Sideloadly](https://sideloadly.io/) 或 [AltStore](https://altstore.io/)。
2. 将 iPhone 连接到电脑。
3. 将 `qlmb.ipa` 拖入 Sideloadly。
4. 输入您的 Apple ID 邮箱。
5. 点击 **Start** 开始安装。
6. **注意**: 免费账号每 7 天需要重新签名。

---
*Built with ❤️ for the open-source community.*


---
*Built with ❤️ for the open-source community.*
