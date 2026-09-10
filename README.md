# منچ بازی - Manch Bazi 🎮

بازی موبایلی فارسی شبیه **لودو** (Ludo) برای اندروید.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Android](https://img.shields.io/badge/android-8+-green.svg)
![Build](https://img.shields.io/badge/build-gradle-orange.svg)

---

## 📋 مشخصات پروژه

| مورد | جزئیات |
|------|--------|
| **نام** | منچ بازی - Manch Bazi |
| **نوع** | بازی موبایلی (Android) |
| **Min SDK** | Android 8 (API 26) |
| **Target SDK** | Android 14 (API 34) |
| **اندازه APK** | ~25 MB |
| **زبان** | Kotlin |
| **معماری** | Clean Architecture |

---

## 🏗️ ساختار پروژه

```
Manch-Bazi/
├── app/                    # اپلیکیشن اصلی
├── core/                   # هسته بازی (Ludo Engine)
├── setup/                  # سیستم تنظیمات
├── themes/                 # موتور تم‌ها
├── challenges/             # محتوای چالش‌ها
├── .github/workflows/      # GitHub Actions
├── build.gradle            # تنظیمات Gradle (Root)
├── settings.gradle         # تنظیمات Module
└── gradle.properties       # خصوصیات Gradle
```

### بخش‌های کلیدی:

#### 🔒 **Core Module** (قفل - غیرقابل تغییر)
- **game-engine/**: کنترل‌کننده بازی
- **board/**: صفحه ۱۵۲ خانه‌ای
- **dice/**: منطق تاس (۱-۶)
- **tokens/**: منطق مهره‌ها
- **rules/**: قوانین Ludo
- **randomizer/**: تولید خانه‌های ویژه
- **animations/**: انیمیشن‌های بازی

#### 🎨 **Themes Module** (قفل - غیرقابل تغییر)
موتور تم برای انتخاب‌های مختلف بازیکنان:
- Mixed 2-Player Theme
- Boys Both Theme
- Girls Both Theme
- 4-Player Hybrid Theme

#### 📝 **Challenges Module** (باز - قابل تغییر)
محتوای چالش‌ها در فرمت JSON:
- `data/mixed.json`
- `data/girls.json`
- `data/boys.json`
- `data/hybrid.json`

#### ⚙️ **Setup Module** (نیمه‌باز)
- صفحات انتخاب نوع بازی
- ثبت اطلاعات بازیکنان
- اعتبارسنجی سن (حداقل 15 سال)

---

## 🚀 را��‌اندازی سریع

### ۱. Clone پروژه

```bash
git clone https://github.com/salehsafary89-netizen/Manch-Bazi.git
cd Manch-Bazi
```

### ۲. باز کردن در Android Studio

- Android Studio را باز کنید
- **File → Open** و پوشه `Manch-Bazi` را انتخاب کنید
- بعد از نمایش project، **Gradle Sync** خودکار اجرا می‌شود

### ۳. Build و Run

```bash
# Debug Build
./gradlew assembleDebug

# Release Build
./gradlew assembleRelease

# نصب روی گوشی
./gradlew installDebug
```

---

## 🔧 نیازمندی‌ها

- **Android Studio**: Hedgehog یا بالاتر
- **JDK**: Java 11+
- **Gradle**: 8.0+
- **Android SDK**:
  - Min API 26
  - Target API 34

---

## 📦 وابستگی‌های اصلی

| کتابخانه | نسخه | هدف |
|---------|------|------|
| **AndroidX Core** | 1.10.1 | توابع اندروید |
| **Compose** | 2023.09.01 | UI |
| **Kotlin Coroutines** | 1.7.2 | Async |
| **Material3** | - | Design System |
| **GSON** | 2.10.1 | JSON |

---

## 🎮 قوانین بازی

### تعداد بازیکنان
- ۲ بازیکن
- ۴ بازیکن

### مهره‌ها
- هر بازیکن: ۴ مهره
- رنگ‌های متفاوت برای هر بازیکن

### صفحه
- ۱۵۲ خانه در مسیر Ludo
- خانه‌های ویژه (تصادفی در هر دور)

### تاس
- بین ۱ تا ۶
- بازی اضافی برای شش

### سن
- حداقل: ۱۵ سال
- تا بالا: نامحدود

---

## 🎨 تم و استایل

### رنگ‌های پایه
- 🟦 آبی نفتی
- 🔵 آبی الکتریکی
- ⬜️ خاکستری سرد
- ⬛️ سرمه‌ای تیره

### استایل
- **Tactical/Cyber Dark**
- پنل‌های مدرن
- Glow کنترل‌شده
- خطوط شبکه‌ای ظریف

---

## 🤝 مشارکت

### فقط محتوای چالش را ویرایش کنید

اگر می‌خواهید **چالش‌های جدید** اضافه کنید:

```json
{
  "id": 1,
  "title": "عنوان چالش",
  "text": "متن چالش"
}
```

❌ **تغییر ندهید**: 
- `core/` - هسته بازی
- `themes/` - موتور تم‌ها
- `app/` - اپلیکیشن

---

## 📄 مستندات

- [ARCHITECTURE.md](./ARCHITECTURE.md) - معماری کامل
- [DEVELOPMENT.md](./DEVELOPMENT.md) - راهنمای توسعه
- [CONTRIBUTING.md](./CONTRIBUTING.md) - نحوه مشارکت

---

## 📝 لایسنس

MIT License - برای جزئیات بیشتر، `LICENSE` را ببینید.

---

## 👨‍💻 سازنده

**صالح سفاری**
- GitHub: [@salehsafary89-netizen](https://github.com/salehsafary89-netizen)
- ایمیل: salehsafary89@gmail.com

---

## 📞 پشتیبانی

اگر سوالی داشتید یا مشکلی پیدا کردید:
- Issues را در GitHub باز کنید
- یا مستقیم تماس بگیرید

---

**ساخته شده با ❤️ برای پلتفرم اندروید**
