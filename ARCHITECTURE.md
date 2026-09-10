# معماری پروژه Manch Bazi

## 📐 نمای کلی

منچ بازی بر اساس اصول **Clean Architecture** و **Modular Design** طراحی شده است.

```
┌─────────────────────────────────────────┐
│          APP (اپلیکیشن اصلی)           │
│  MainActivity + UI Framework            │
└──────────────────┬──────────────────────┘
                   │
┌──────────────────┴──────────────────────┐
│                                          │
│         SETUP (تنظیمات بازی)             │
│  GameType Selection + Player Input      │
│                                          │
└──────────────────┬──────────────────────┘
                   │
        ┌──────────┴──────────┐
        │                     │
   ┌────▼─────┐         ┌────▼──────┐
   │  THEMES  │         │ CHALLENGES│
   │ (موتور) │         │ (محتوا)   │
   └────┬─────┘         └────┬──────┘
        │                     │
        └──────────┬──────────┘
                   │
           ┌───────▼────────┐
           │                │
           │    CORE        │
           │  (هسته بازی)   │
           │                │
           └────────────────┘
```

---

## 🧩 ماژول‌ها

### 1️⃣ **Core Module** 🔒 (غیرقابل تغییر)

**مسیر**: `core/`

هسته اصلی بازی که **نباید تغییر کند**.

#### زیرماژول‌ها:

| نام | نوع | هدف | وضعیت |
|-----|------|------|--------|
| **game-engine/** | Logic | کنترل‌کننده بازی | 🔒 |
| **board/** | Logic | صفحه ۱۵۲ خانه | 🔒 |
| **dice/** | Logic | منطق تاس | 🔒 |
| **tokens/** | Logic | منطق مهره‌ها | 🔒 |
| **turns/** | Logic | مدیریت نوبت | 🔒 |
| **rules/** | Logic | قوانین Ludo | 🔒 |
| **randomizer/** | Logic | تولید خانه‌های ویژه | 🔒 |
| **animations/** | Logic | انیمیشن‌های حرکت | 🔒 |

#### فایل‌های کلیدی:

```
core/
├── game-engine/
│   ├── GameEngine.kt          # کنترل‌کننده اصلی
│   ├── GameState.kt           # وضعیت گیم
│   ├── GameRules.kt           # قوانین کلی
│   └── GameEvents.kt          # رویدادهای گیم
│
├── board/
│   ├── Board.kt               # تعریف صفحه ۱۵۲ خانه
│   ├── Cell.kt                # تعریف خانه‌ها
│   └── BoardLayout.kt         # مختصات
│
├── dice/
│   ├── Dice.kt                # تعریف تاس
│   ├── DiceRoller.kt          # منطق پرتاب
│   └── DiceState.kt           # وضعیت تاس
│
├── tokens/
│   ├── Token.kt               # تعریف مهره
│   ├── TokenPosition.kt       # موقعیت مهره
│   └── TokenState.kt          # وضعیت مهره
│
├── rules/
│   ├── RuleEngine.kt          # موتور قوانین
│   ├── MovementRules.kt       # قوانین حرکت
│   ├── CaptureRules.kt        # قوانین زدن
│   └── WinRules.kt            # قوانین برد
│
├── randomizer/
│   ├── Randomizer.kt          # تولید تصادفی
│   ├── SafeRandom.kt          # Random امن
│   └── SpecialCellGenerator.kt# تولید خانه‌های ویژه
│
└── animations/
    ├── TokenAnimation.kt      # انیمیشن مهره
    ├── DiceAnimation.kt       # انیمیشن تاس
    └── BoardAnimation.kt      # انیمیشن صفحه
```

---

### 2️⃣ **Themes Module** 🎨 (غیرقابل تغییر)

**مسیر**: `themes/`

موتور تم‌های بازی که **نباید تغییر کند**.

#### فایل‌های کلیدی:

```
themes/
├── ThemeEngine.kt             # کنترل‌کننده تم‌ها
├── ThemeConfig.kt             # تنظیمات
│
├── base/
│   ├── BaseTheme.kt           # تم پایه
│   ├── Colors.kt              # پالت رنگ
│   ├── Typography.kt          # فونت‌ها
│   └── Shapes.kt              # اشکال
│
├── themes/
│   ├── Mixed2PlayerTheme.kt   # ۱ دختر + ۱ پسر
│   ├── BoysBothTheme.kt       # دو پسر
│   ├── GirlsBothTheme.kt      # دو دختر
│   ├── Boys4Theme.kt          # ۴ پسر
│   ├── Girls4Theme.kt         # ۴ دختر
│   └── Mixed4PlayerTheme.kt   # ۴ ترکیبی
│
├── components/
│   ├── ThemeDiceVisuals.kt    # ظاهر تاس
│   ├── ThemeTokenVisuals.kt   # ظاهر مهره
│   ├── ThemeBoardVisuals.kt   # ظاهر صفحه
│   ├── ThemeCardVisuals.kt    # ظاهر کارت رویداد
│   ├── ThemeHUD.kt            # HUD
│   └── ThemeEffects.kt        # افکت‌های صوتی/بصری
│
└── animations/
    ├── EntranceAnimation.kt   # انیمیشن ورود
    └── TransitionAnimation.kt # انیمیشن انتقال
```

---

### 3️⃣ **Setup Module** ⚙️ (نیمه‌باز)

**مسیر**: `setup/`

سیستم تنظیمات و ورود بازیکنان.

#### فایل‌های کلیدی:

```
setup/
├── screens/
│   ├── GameTypeSelectionScreen.kt     # انتخاب نوع بازی
│   ├── PlayerCountScreen.kt           # انتخاب تعداد بازیکن
│   ├── PlayerInputScreen.kt           # ورود اطلاعات
│   ├── PlayerConfirmationScreen.kt    # تأیید اطلاعات
│   └── GamePreparationScreen.kt       # آماده‌سازی
│
├── models/
│   ├── PlayerData.kt                  # مدل بازیکن
│   ├── GameType.kt                    # نوع بازی
│   └── SetupState.kt                  # وضعیت
│
├── validators/
│   ├── PlayerValidator.kt             # اعتبارسنجی کلی
│   ├── AgeValidator.kt                # اعتبارسنجی سن
│   └── NameValidator.kt               # اعتبارسنجی نام
│
└── flow/
    └── SetupFlow.kt                   # مسیر تنظیمات
```

---

### 4️⃣ **Challenges Module** 📝 (باز - قابل تغییر)

**مسیر**: `challenges/`

محتوای چالش‌ها - **فقط داده، نه کد**.

#### فایل‌های کلیدی:

```
challenges/
├── models/
│   ├── Challenge.kt                   # مدل Challenge (🔒)
│   └── ChallengeType.kt               # انواع Challenge (🔒)
│
├── data/
│   ├── mixed.json                     # چالش‌های ترکیبی (📝)
│   ├── girls.json                     # چالش‌های دختران (📝)
│   ├── boys.json                      # چالش‌های پسران (📝)
│   └── hybrid.json                    # چالش‌های ۴ نفره (📝)
│
└── loader/
    └── ChallengeLoader.kt             # بارگذاری (🔒)
```

**نمونه فرمت JSON:**
```json
[
  {
    "id": 1,
    "title": "عنوان چالش",
    "text": "متن و توضیح چالش",
    "minPlayers": 2,
    "maxPlayers": 4
  }
]
```

---

### 5️⃣ **App Module** 📱 (نیمه‌باز)

**مسیر**: `app/`

اپلیکیشن اندروید اصلی.

#### فایل‌های کلیدی:

```
app/
├── src/main/java/com/manch/bazi/
│   ├── MainActivity.kt                # نقطه ورود
│   ├── AppConfig.kt                   # تنظیمات سراسری
│   │
│   └── di/
│       └── AppModule.kt               # DI Setup
│
├── src/main/res/
│   ├── values/
│   │   ├── strings.xml                # متون
│   │   ├── colors.xml                 # رنگ‌ها
│   │   ├── themes.xml                 # تم‌ها
│   │   └── dimens.xml                 # اندازه‌ها
│   │
│   ├── drawable/
│   └── raw/                           # صوت‌ها
│
└── AndroidManifest.xml                # تنظیمات اندروید
```

---

## 🔄 جریان داده

```
SetupFlow
    ↓
GameType Selection → NORMAL / ADULT
    ↓
Player Count → 2 / 4
    ↓
PlayerData Collection (سن، نام، رنگ، جنسیت)
    ↓
Age Validation (≥15)
    ↓
ThemeEngine Selection (بر اساس ترکیب بازیکنان)
    ↓
ChallengeLoader (بارگذاری چالش‌های مناسب)
    ↓
GameEngine Initialization
    ↓
Game Start
```

---

## 🔐 اصول ایمنی (Safety Principles)

### 🔒 قفل شده (Core & Themes)
❌ برنامه‌نویس محتویی **نمی‌تواند** این‌ها را تغییر دهد:
- `core/game-engine/`
- `core/board/`
- `core/dice/`
- `core/tokens/`
- `core/rules/`
- `core/randomizer/`
- `themes/ThemeEngine.kt`
- `themes/base/`
- `themes/themes/`

### 📝 باز شده (Challenges Only)
✅ برنامه‌نویس محتویی **می‌تواند**:
- `challenges/data/*.json` - فقط متن چالش‌ها
- نام، ID، و متن چالش‌ها را اضافه/تغییر دهد

### 🟡 نیمه‌باز (Setup & App)
🟡 برنامه‌نویس محتویی **می‌تواند**:
- UI صفحات
- متون فارسی
- رنگ‌ها و فونت‌ها
- افکت‌های صوتی

اما **نه**:
- منطق Validation
- منطق Setup Flow
- کلاس‌های Model

---

## 📊 وابستگی‌های Gradle

```
app/
├── core (لازمی)
├── setup (لازمی)
├── themes (لازمی)
└── challenges (لازمی)

setup/
├── core (لازمی)
└── themes (لازمی)

themes/
└── core (لازمی)

challenges/
└── (مستقل)

core/
└── (مستقل)
```

---

## 🎯 خلاصه وظایف

| ماژول | هدف | توسعه‌دهنده | قابلیت تغییر |
|--------|------|---------|------------|
| **Core** | هسته بازی Ludo | معمار | ❌ نه |
| **Themes** | موتور تم‌ها | معمار | ❌ نه |
| **Challenges** | محتوای چالش‌ها | محتوا | ✅ بله |
| **Setup** | صفحات تنظیمات | UI Dev | 🟡 جزئی |
| **App** | اپلیکیشن اصلی | UI Dev | 🟡 جزئی |

---

**ساخته شده با توجه به اصول معماری حرفه‌ای و قابلیت نگهداری طولانی‌مدت.**
