# Build a Standalone Debug APK in React Native

```plain
How to Create a Standalone APK in React Native (Without Metro Bundler)
```

To create a **standalone APK** that includes the JavaScript bundle and runs independently (without requiring Metro), you need to follow these steps:

---

### **1\. Bundle the JavaScript Code**

You must package the JavaScript code into the APK.

1. Open a terminal in your project root and run:

```plain
npx react-native bundle --platform android --dev false --entry-file index.js --bundle-output android/app/src/main/assets/index.android.bundle --assets-dest android/app/src/main/res/
```

-       *   **`--platform android`**: Specifies the platform.
  - **`--dev false`**: Ensures the code is optimized for production.
  - **`--entry-file index.js`**: Specifies the entry file for your app.
  - **`--bundle-output`**: Where the bundle file will be stored.
  - **`--assets-dest`**: Ensures your assets (like images) are included in the build.

> Ensure the `android/app/src/main/assets` directory exists. If it doesn’t, create it manually.

---

### **2\. Clean the Build**

Before generating the APK, clean your build to avoid any cached issues.

1. Run the following Gradle command:

```plain
cd android
./gradlew clean
```

---

### **3\. Generate the APK**

You can generate either a **debug** or **release** APK.

#### **For a Debug APK:**

1. Run the Gradle command:

```plain
./gradlew assembleDebug
```

1. The debug APK will be located at:

```plain
android/app/build/outputs/apk/debug/app-debug.apk
```

---

## **Additional**

> 💡 If you want reduce APK size, follow the instructions

Go 👉 android\\app\\src\\main\\AndroidManifest.xml

AndroidManifest.xml

```plain
<application
      ...
      android:extractNativeLibs="true">
```

Props/cons

| Value                               | Behavior                                     | Use case                                          |
| ----------------------------------- | -------------------------------------------- | ------------------------------------------------- |
| `android:extractNativeLibs="true"`  | Extracts `.so` libs to file system           | Safe default, good for legacy compatibility       |
| `android:extractNativeLibs="false"` | Leaves `.so` files in the APK, no extraction | Reduces install size, recommended for modern apps |

---

### 📌 General Recommendations:

#### ✅ If you're targeting **API 23+ (Android 6.0+)** **and** using **App Bundles (AAB)**:

- You should use:

```plain
android:extractNativeLibs="false"
```

- This saves space and speeds up installs. Android can load native libraries directly from the APK.

#### ⚠️ If you're using **older devices**, **third-party libraries**, or just unsure:

- Stay with:

```plain
android:extractNativeLibs="true"
```

- This is safer for compatibility with native libraries that expect to be on the filesystem.

---

### ✅ Example for modern apps:

If you're targeting API 29+ and using AAB, your manifest should ideally include:

```xml
<application
    android:extractNativeLibs="false"
    ... >
```
