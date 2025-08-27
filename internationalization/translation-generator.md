# 🌍 Translation File Generator

This guide helps you generate multilingual translation files (e.g., `ar.json`, `bn.json`, etc.) from a base English file (`en.json`) using a simple script powered by Google Translate. It supports both API key-based and free usage with caching for incremental translations.

---

## ✅ Prerequisites

1. Ensure your project is set up. (link: [https://bitbucket.org/techvillage/translators/src/master/](https://bitbucket.org/techvillage/translators/src/master/) )
2. Run the following to install dependencies:

```coffeescript
npm install
```

---

## 🛠 Workflow: Step-by-Step

### 🔁 Step 1: Sync with Repository

Before generating translation files, always **fetch the latest code from "develop" branch**:

```sql
git fetch && git pull
```

### ⚠️ Step 2: Handle Merge Conflicts

If any conflicts occur, resolve them properly using your preferred merge tool.

### 🚀 Step 3: Push Changes

Once resolved, push your changes:

```sql
git add .
git commit -m "Resolved merge conflicts"
git push
```

### 🌐 Step 4: Generate Translations

#### 🗂 File Structure

1. Place your `en.json` file in the root directory.
2. Create a `translated` directory (if not already exists) in the root:

```perl
mkdir translated
```

#### ▶️ With Google API Key

If you have a Google Translate API key:

```plain
node translate-json en.json ar,be,bg,bn,ca,de,es,et,fr,ka,nl,pl,pt,ru,sv,zh YOUR_GOOGLE_API_KEY
```

#### ▶️ Without API Key (Free Mode)

For limited, cache-based batch translation:

```plain
node translate-json en.json fr,et,nl
```

> ⚠️ **Note:** Free usage may be rate-limited by Google. Cached translations allow you to continue later without reprocessing existing keys. Retry after ~2 hours if blocked.

---

## 📁 Output

Translated files will be created in the `translated` folder with the following format:

```plain
translated/ar.json
translated/bn.json
translated/fr.json
...
```

---

## ✅ Step 5: Use the Translations

Move or copy the generated JSON files to your project’s localization directory as needed.

---

## 📤 Step 6: Review & Push Final Changes

1. Review the newly generated files.
2. Check for any cached content updates.
3. Commit and push your changes:

```sql
git add translated/
git commit -m "Add translated language files"
git push
```

1. Create a **pull request from** **`develop`** **to** **`master`**.

---

## ⚠️ Important Notes

- **Do not modify any other files** outside the intended translation directories.
- **Use appropriate commit messages** for clear history and review.

---

## 🎉 You're Done!

Your translations are ready to use, share, and ship. Keep your localization seamless and your users connected in every language!

---
