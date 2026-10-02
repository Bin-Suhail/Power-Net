# POWER NET ⚡

> **تطبيق Flutter متقدم لإدارة شبكات MikroTik اللاسلكية ومراقبة حالة الأجهزة ورسم طوبولوجيا الشبكة على خريطة تفاعلية.**

[![Flutter](https://img.shields.io/badge/Flutter-3.13+-02569B?logo=flutter)](https://flutter.dev)
[![Dart](https://img.shields.io/badge/Dart-3.13+-0175C2?logo=dart)](https://dart.dev)
[![Firebase](https://img.shields.io/badge/Firebase-🔥-FFCA28?logo=firebase)](https://firebase.google.com)
[![License](https://img.shields.io/badge/License-MIT-green)](LICENSE)

---

## 📌 نبذة عن المشروع

**POWER NET** أداة شبكات احترافية صُممت لمدراء الشبكات ومزوّدي خدمات الإنترنت (WISP). يمكّنك التطبيق من:

- اكتشاف أجهزة الشبكة المتصلة تلقائيًا عبر بروتوكول **MNDP** (MikroTik Neighbor Discovery Protocol)
- رسم مواقع الأبراج والمعدات جغرافيًا على خريطة تفاعلية
- مراقبة حالة الروابط بين الأبراج والمعدات في الزمن الحقيقي
- اكتشاف الأعطال بسرعة عبر تنبيهات بصرية فورية

---

## 🚀 الميزات الرئيسية

| الميزة | الوصف |
|---|---|
| 🗺️ **خريطة طوبولوجيا تفاعلية** | رسم الروابط بين الأبراج والمعدات على الخريطة، يتغير لون الرابط تلقائيًا (أخضر = متصل، أحمر = مقطوع) |
| 📡 **اكتشاف تلقائي** | رصد الأجهزة الجديدة غير الموزعة عبر بروتوكول MNDP وعرضها في نافذة عائمة |
| 📍 **سحب وإفلات** | إمكانية سحب أي جهاز غير موضوع وإفلاته على نقطة محددة في الخريطة لتسجيل إحداثياته الجغرافية فورًا |
| ⚡ **مراقبة مباشرة** | فلاتر سريعة (متصل، غير متصل، صيانة) مع مؤقّت تنظيف دوري كل 10 ثواني لتقييم حالة الأجهزة |
| 📱 **واجهة Material 3** | تصميم عصري مع بطاقات تفصيلية لكل جهاز (العنوان، IP، الإحداثيات، الأجهزة المتصلة) |

---

## 🛠️ التقنيات المستخدمة

### الواجهة الأمامية وإدارة الحالة
- **Framework:** Flutter (Dart SDK ^3.13.2)
- **State Management:** Riverpod (`flutter_riverpod`)
- **Routing:** `go_router`
- **تخزين وأمان:** `shared_preferences` + `flutter_secure_storage`
- **ترجمة:** `flutter_localizations` + `intl`

### الخلفية وقاعدة البيانات
- **Firebase Core + Cloud Firestore:** تخزين بيانات الأبراج والمعدات وحالات الروابط
- **Firebase Auth:** مصادقة المستخدمين وإدارة الصلاحيات

### الخرائط والمواقع
- **محرك الخرائط:** `flutter_map` مع دعم التبديل بين OpenStreetMap وArcGIS World Imagery (القمر الصناعي)
- **معالجة الإحداثيات:** `latlong2`

### الشبكات وبروتوكولات MikroTik
- **خدمة MNDP:** خدمة مخصصة لاستقبال بروتوكول اكتشاف الجوار من MikroTik عبر `UDP port 5678`
- **MikroTik API:** اتصال مباشر بـ RouterOS عبر `MikrotikApiService` للتحكم بالأجهزة وجلب بيانات الجوار

---

## 📁 هيكل المشروع

```
Power-Net/
├── lib/
│   ├── main.dart                    # نقطة الدخول
│   ├── app.dart                     # إعدادات التطبيق والثيمات
│   ├── models/                      # نماذج البيانات (Tower, Device, Link)
│   ├── providers/                   # مزودات Riverpod (حالة الشبكة، الخريطة، المصادقة)
│   ├── screens/                     # شاشات التطبيق
│   │   ├── map_screen.dart          # شاشة الخريطة الرئيسية
│   │   ├── device_details_screen.dart # تفاصيل الجهاز
│   │   └── auth_screen.dart         # تسجيل الدخول
│   ├── services/                    # خدمات (MikroTik API، MNDP، Firebase)
│   │   ├── mikrotik_api_service.dart
│   │   ├── mndp_service.dart
│   │   └── firebase_service.dart
│   └── widgets/                     # ويدجتات قابلة لإعادة الاستخدام
├── assets/                          # الصور والأيقونات
├── pubspec.yaml                     # تبعيات Flutter
└── README.md
```

---

## ⚙️ التثبيت والإعداد

### المتطلبات الأساسية
- **Flutter SDK** 3.13+
- **Firebase Project** مهيأ
- **راوتر MikroTik** في الشبكة (يدعم RouterOS API)

### 1. استنساخ المستودع
```bash
git clone https://github.com/Bin-Suhail/Power-Net.git
cd Power-Net
```

### 2. تثبيت التبعيات
```bash
flutter clean
flutter pub get
```

### 3. إعداد Firebase

#### أ. تثبيت Firebase CLI
```bash
npm install -g firebase-tools
```

#### ب. تسجيل الدخول وربط المشروع
```bash
firebase login
dart pub global activate flutterfire_cli
flutterfire configure --project=YOUR_PROJECT_ID
```

> هذا الأمر يولّد ملف `lib/firebase_options.dart` تلقائيًا.

#### ج. تفعيل الخدمات المطلوبة في Firebase Console:
- **Authentication:** تفعيل المصادقة (بريد/هاتف)
- **Cloud Firestore:** إنشاء قاعدة بيانات

### 4. تشغيل التطبيق
```bash
flutter run
flutter run -d android
flutter build apk --release
```

---

## 🔌 الاتصال براوتر MikroTik

1. فعّل API في الراوتر: `/ip service enable api`
2. أنشئ مستخدم API: `/user add name=api_user group=full password=YourPassword`

يستمع التطبيق على **UDP port 5678** لالتقاط حزم MNDP تلقائيًا.

---

## 📄 الترخيص

MIT License

---

## 👤 المطور

**بن سهيل** — [GitHub](https://github.com/Bin-Suhail)