# React Native App Versioning Guide - Android & iOS

## Overview

App versioning in React Native involves managing two key components:

- **Version Name/String**: Human-readable version (e.g., "1.2.3")
- **Version Code/Build Number**: Internal incrementing number for app stores

## Understanding Version Components

### Semantic Versioning (Recommended)

Use the format: `MAJOR.MINOR.PATCH`

- **MAJOR**: Breaking changes
- **MINOR**: New features (backward compatible)
- **PATCH**: Bug fixes (backward compatible)
  Example: `1.2.3` → `1.2.4` (patch) → `1.3.0` (minor) → `2.0.0` (major)

---

## 📱 Android Versioning - Manual Versioning

#### Step 1: Locate Android Gradle File

Navigate to: `android/app/build.gradle`

#### Step 2: Update Version Information

```cpp
android {
    compileSdkVersion rootProject.ext.compileSdkVersion

    defaultConfig {
        applicationId "com.yourapp.name"
        minSdkVersion rootProject.ext.minSdkVersion
        targetSdkVersion rootProject.ext.targetSdkVersion

        // Version Code - Must increment for each release
        versionCode 1

        // Version Name - Human readable version
        versionName "1.0.0"
    }
}
```

#### Step 3: Version Update Rules

- **versionCode**: Must increment by at least 1 for each Play Store release
- **versionName**: Should follow semantic versioning

#### Example Version Progression:

```sql
// Initial Release
versionCode 1
versionName "1.0.0"

// Bug Fix Release
versionCode 2
versionName "1.0.1"

// Feature Release
versionCode 3
versionName "1.1.0"

// Major Release
versionCode 4
versionName "2.0.0"
```

---

## 🍎 iOS Versioning - Manual Versioning

#### Edit Info.plist Directly

Navigate to: `ios/YourAppName/Info.plist`

```xml
<dict>
    <!-- Version String (shown to users) -->
    <key>CFBundleShortVersionString</key>
    <string>1.0.0</string>

    <!-- Build Number (must increment) -->
    <key>CFBundleVersion</key>
    <string>1</string>
</dict>
```

#### ♻ Alternative

if `Info.plist` is using **Xcode build settings variables** instead of hardcoded values:

- **`$(MARKETING_VERSION)`** → maps to `Version` (human-readable) in Xcode.
- **`$(CURRENT_PROJECT_VERSION)`** → maps to `Build` (incrementing number) in Xcode.

That means you **don’t edit the numbers in Info.plist directly** — you change them in Xcode or `project.pbxproj` build settings.

#### Step 1: Open Xcode Project

Navigate to: `ios/YourAppName.xcworkspace` (or `.xcodeproj`)

#### Step 2: Select Project Target

1. Click on your project name in the navigator
2. Select your app target under "TARGETS"
3. Go to the "General" tab

#### Step 3: Update Version Information

- **Version**: Human-readable version (CFBundleShortVersionString)
- **Build**: Internal build number (CFBundleVersion)

![](https://t9018545184.p.clickup-attachments.com/t9018545184/a2085ffb-b938-486b-be6e-ad2972ffa7eb/image.png)

#### Step 4: Version Update Rules

- **CFBundleShortVersionString**: Marketing version (1.0.0, 1.1.0, etc.)
- **CFBundleVersion**: Must increment for each App Store submission

---

## Best Practices

### 1\. Version Synchronization

Keep Android `versionName` and iOS `CFBundleShortVersionString` identical:

```swift
Android: versionName "1.2.3"
iOS: CFBundleShortVersionString "1.2.3"
```

### 2\. Build Number Management

- Android `versionCode` and iOS `CFBundleVersion` can be different
- Both must increment for each store submission
- Consider using timestamps or CI build numbers

### 3\. Pre-release Versioning

For beta/alpha releases:

```sql
1.0.0-alpha.1
1.0.0-beta.1
1.0.0-rc.1
1.0.0 (final release)
```

### 4\. Git Tagging

Tag releases in Git:

```perl
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin v1.0.0
```

---

## Troubleshooting

### Common Android Issues

#### Issue: "You need to use a different version code"

**Solution**: Increment `versionCode` in `android/app/build.gradle`

#### Issue: Version not updating in app

**Solution**:

1. Clean build: `cd android && ./gradlew clean`
2. Rebuild: `npx react-native run-android`

### Common iOS Issues

#### Issue: "CFBundleVersion must be incremented"

**Solution**: Increment `CFBundleVersion` in Info.plist

#### Issue: Version not visible in TestFlight

**Solution**: Ensure both `CFBundleShortVersionString` and `CFBundleVersion` are updated

---

## Checking Current Version

### In JavaScript Code

```javascript
import DeviceInfo from "react-native-device-info";

// Get version name/string
const version = DeviceInfo.getVersion();
console.log("Version:", version); // "1.0.0"

// Get build number
const buildNumber = DeviceInfo.getBuildNumber();
console.log("Build:", buildNumber); // "1"
```

### Install react-native-device-info

```bash
npm install react-native-device-info
cd ios && pod install # iOS only
```

---

## Release Checklist

### Before Each Release:

- \[ \] Update version numbers (Android & iOS)
- \[ \] Test the build thoroughly
- \[ \] Update changelog/release notes
- \[ \] Create Git tag
- \[ \] Build release versions
- \[ \] Test release builds
- \[ \] Upload to respective stores

### Version History Tracking:

Maintain a [`CHANGELOG.md`](http://CHANGELOG.md) file:

```markdown
# Changelog

## [1.0.1] - 2024-01-15

### Fixed

- Fixed login issue on Android

## [1.0.0] - 2024-01-01

### Added

- Initial release
- User authentication
- Basic dashboard
```

This comprehensive approach ensures consistent versioning across both platforms and smooth app store submissions.
