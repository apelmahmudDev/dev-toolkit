# 📦 React Native Customer App – Cleanup & Resource Preparation Guide

This guide outlines essential steps to clean up your **React Native Customer App** project before sharing, archiving, or debugging. These actions remove unnecessary files and system-generated clutter to ensure a smooth setup for you or your team.

---

## 🧹 1. Delete `node_modules`

Remove all installed dependencies. They’ll be restored with `npm install` or `yarn install`.

```powershell
rm -rf node_modules
```

> ✅ Good for resolving dependency issues or reducing project size before sharing.

---

## 🗃️ 2. Delete `.git` Folder

If you're preparing a fresh version without Git history:

```powershell
rm -rf .git
```

> ⚠️ This removes all commit history and remote repo links.

---

## 🗃️ 3. Delete `.yarn` Folder

If you want to remove cached Yarn files and settings for a fresh start:

```powershell
rm -rf .yarn
```

⚠️ **Warning:** This will remove the local Yarn setup, including cache and plugins. You’ll need to reinstall dependencies (e.g., `yarn install`) to regenerate it.

---

Here’s the updated version with a different icon for deleting the `__tests__` folder:

---

# 🧪 4. **Delete** **`__tests__`** **Folder**

If you don’t want to include test files in your fresh release:

```markdown
rm -rf **tests**
```

⚠️ **Warning:** This will permanently remove all test files and test-related configurations under the `__tests__` folder. Only do this if you are sure you don’t need tests for debugging or future development.

---

## 🧪 5. Clean `.env` File

Your `.env` file may contain sensitive credentials or environment-specific data. Clean or remove it before sharing.

```plain
# Open .env and clear content manually
nano .env
# or delete it
rm .env
```

> 🔒 Keep your API keys and secrets safe.

---

## ⚙️ 6. Delete Gradle Execution History

Remove Gradle's cached build execution data:

```plain
your-app/android/.gradle/8.10.2/executionHistory
```

![](https://t9018545184.p.clickup-attachments.com/t9018545184/8333a5b4-cb5c-423f-ac8e-1f8773052f8a/delete_executionHistory.png)

> 🛠 Clears out potentially corrupted build state.

---

## 📁 7. Delete `.cxx` Folder

Remove C++ intermediate build files:

```plain
your-app/android/app/.cxx
```

![](https://t9018545184.p.clickup-attachments.com/t9018545184/41a88cce-6849-4ea4-888d-af4b56b6c266/delete_cxx_folder.png)

> ✅ These files are regenerated on build.

---

## 🏗️ 8. Delete `build` Folder (Android)

Remove the Android build output:

```plain
your-app/android/app/build
```

![](https://t9018545184.p.clickup-attachments.com/t9018545184/483c24f7-704a-4f26-89cd-886d0e93346f/delete_build_folder.png)

> 🚀 This ensures a fresh build without leftovers from previous builds.

---

## 🍏 9. iOS Cleanup

If you're working with iOS, clean up Xcode-derived data and build artifacts:

```powershell
# From root of the project
cd ios
xcodebuild clean

# Optionally delete build folder
rm -rf build

# Delete Pods if needed
rm -rf Pods
rm -rf Podfile.lock
pod install
```

> 🧼 Prevents native iOS build issues related to outdated pods or derived data.

---

## ✅ Final Steps (Optional)

After cleanup, regenerate everything:

```plain
# Install JS dependencies
npm install
# or
yarn install

# iOS pod install
cd ios && pod install
```

---

## 📘 When to Use This Guide

- Before sharing the project with others
- To prepare a clean archive or backup
- After switching machines or OS
- When troubleshooting persistent errors
- Before initializing Git in a cleaned project
