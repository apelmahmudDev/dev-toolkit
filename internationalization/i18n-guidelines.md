# 🌍Internationalization (i18n) Guidelines in React.js

This guide covers best practices for handling translations in React using `react-i18next`, including how to structure your project, manage dynamic translations, and use a custom hook for a consistent developer experience.

---

## 📦 1. Install Dependencies

```coffeescript
npm install i18next react-i18next
```

---

## 📁 2. Project Structure

```plain
/src
  ├── i18n/
  │   ├── index.js            # i18n configuration
  │   ├── locales/
  │   │   ├── en.json
  │   │   ├── es.json
  │   │   └── bn.json
  │   └── useLangTranslation.js  # Custom translation hook
  ├── components/
  │   └── ExampleComponent.jsx
  └── App.jsx
```

---

## ⚙️ 3. i18n Configuration (`/src/i18n/index.js`)

```javascript
import i18n from "i18next";
import { initReactI18next } from "react-i18next";

import en from "./locales/en.json";
import es from "./locales/es.json";
import bn from "./locales/bn.json";

i18n.use(initReactI18next).init({
	resources: {
		en: { translation: en },
		es: { translation: es },
		bn: { translation: bn },
	},
	lng: "en",
	fallbackLng: "en",
	interpolation: {
		escapeValue: false,
	},
});

export default i18n;
```

Then import it once in `App.jsx` or your entry file:

```dart
import './i18n';
```

---

## 🧩 4. Custom Hook (`/src/i18n/useLangTranslation.js`)

This hook wraps `useTranslation()` and exposes `t` as `trans`, giving a more semantic name and consistent access throughout your app.

```javascript
import { useTranslation } from "react-i18next";

const useLangTranslation = () => {
	const { t: trans } = useTranslation();
	return { trans };
};

export default useLangTranslation;
```

---

## 🧠 5. Using Translations in Components

### ✅ Static Text

```javascript
import useLangTranslation from "../i18n/useLangTranslation";

function ExampleComponent() {
	const { trans } = useLangTranslation();

	return <p>{trans("welcome_message")}</p>;
}
```

### ✅ Dynamic Text with Interpolation

```javascript
function Receipt({ receipt }) {
	const { trans } = useLangTranslation();

	return (
		<p>{trans("receipt.customer_name", { name: receipt?.customerName })}</p>
	);
}
```

#### Example `en.json`

```json
{
	"welcome_message": "Welcome to our app!",
	"receipt": {
		"customer_name": "Name: {{name}}"
	}
}
```

---

## 🚫 6. Translation Key Naming Rules

- ✅ Use **dot-separated** or **snake_case** keys.
- ❌ Avoid characters like `:`, `+`, `-`, `@`, etc.

### ✅ Good:

```json
"form.submit_button": "Submit"
```

### ❌ Bad:

```json
"form:submit+btn": "Submit"
```

---

## 📄 7. Generating & Managing Translations

1. At the end of development, extract translation keys (manually or using tools like `i18next-scanner`).
2. Create/update your base language file (`en.json`).
3. Translate the base file into other languages: `es.json`, `bn.json`, etc.

```plain
/locales
  ├── en.json
  ├── es.json
  └── bn.json
```

---

## 🔁 8. Changing Language Dynamically

```javascript
import i18n from "i18next";

i18n.changeLanguage("es"); // switch to Spanish
```

---

## ✅ Summary Checklist

| Step             | Action                                     |     |
| ---------------- | ------------------------------------------ | --- |
| 🔧 Setup         | Install `react-i18next` and create config  |     |
| 🧠 Use Hook      | Use `useLangTranslation` for clean usage   |     |
| 💬 Interpolation | Use `{{name}}` for dynamic content         |     |
| 🌐 Keys          | Use clear and symbol-free translation keys |     |
| 🛠 Finalization   | Extract keys, generate JSON, translate     |     |
| 🔄 Switch        | Support runtime language switching         |     |
