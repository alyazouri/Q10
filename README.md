<div align="center" dir="rtl">

# 🛡️ Q10 — SERVER ALYAZOURI JOR

**ملفات تعريف جاهزة لأجهزة Apple لإعداد DNS مشفّر عبر Cloudflare، مع خيار Global HTTP Proxy للأجهزة المُدارة.**

[![Apple Configuration Profile](https://img.shields.io/badge/Apple-Configuration%20Profile-000000?logo=apple&logoColor=white)](https://support.apple.com/guide/deployment/intro-to-device-management-depc0aadd3fe/web)
[![DNS over HTTPS](https://img.shields.io/badge/DNS-HTTPS%20%28DoH%29-168CFF)](https://developers.cloudflare.com/1.1.1.1/encryption/dns-over-https/)
[![Cloudflare 1.1.1.1](https://img.shields.io/badge/Cloudflare-1.1.1.1-F38020?logo=cloudflare&logoColor=white)](https://1.1.1.1/)
[![Unsigned profiles](https://img.shields.io/badge/Profiles-Unsigned-F59E0B)](#-الأمان-والخصوصية)

[صفحة التثبيت](#-التثبيت) · [الملفات](#-محتويات-المشروع) · [التحقق](#-التحقق-بعد-التثبيت) · [إزالة الملفات](#-إزالة-ملف-التعريف) · [الأمان](#-الأمان-والخصوصية)

</div>

<div dir="rtl">

## نبذة

يوفّر **Q10** صفحة عربية بسيطة ومتجاوبة لتنزيل ملفّات إعداد Apple (`.mobileconfig`) وتثبيتها على الأجهزة المتوافقة:

- **DNS مشفّر (DoH):** يرسل استعلامات DNS إلى Cloudflare عبر HTTPS بدلًا من DNS التقليدي غير المشفّر.
- **Global HTTP Proxy:** يضبط خادم Proxy يدويًا على مستوى الجهاز للأجهزة التي تسمح سياساتها بذلك.
- **تثبيت مباشر:** صفحة HTML واحدة، بلا مكتبات أو خادم خلفي.
- **قابل للإزالة:** كلا الملفين يسمحان للمستخدم بإزالة ملف التعريف لاحقًا.

> [!IMPORTANT]
> ملف DNS **ليس VPN** ولا يغيّر عنوان IP أو موقع الجهاز. وملف Global HTTP Proxy يمرّر معظم حركة HTTP/HTTPS عبر خادم وسيط، لكنه لا يضمن مرور كل بروتوكولات التطبيقات.

## ✨ المزايا

- تشفير استعلامات DNS باستخدام **DNS over HTTPS**.
- دعم عناوين Cloudflare بنوعي **IPv4 وIPv6**.
- عمل إعداد DNS على Wi‑Fi والبيانات الخلوية من خلال قاعدة اتصال تلقائي.
- واجهة تثبيت عربية، متجاوبة ومناسبة لـ iPhone وiPad.
- لا توجد تبعيات برمجية أو خطوات بناء؛ المشروع ملفات ثابتة فقط.
- إمكانية معاينة ملفات التعريف كنص XML قبل تثبيتها.

## 📦 محتويات المشروع

| الملف | الوظيفة |
|---|---|
| [`install-profile.html`](./install-profile.html) | صفحة التنزيل وتعليمات التثبيت والتحقق |
| [`SERVER_ALYAZOURI.mobileconfig`](./SERVER_ALYAZOURI.mobileconfig) | ملف DNS مشفّر عبر Cloudflare DoH |
| [`SERVER_ALYAZOURI_PROXY.mobileconfig`](./SERVER_ALYAZOURI_PROXY.mobileconfig) | ملف Global HTTP Proxy اليدوي |
| [`README.md`](./README.md) | توثيق المشروع |

## ⚙️ الإعدادات التقنية

### 1) ملف DNS المشفّر

| الخاصية | القيمة |
|---|---|
| Payload Type | `com.apple.dnsSettings.managed` |
| البروتوكول | `HTTPS` — DNS over HTTPS |
| نقطة الاتصال | `https://cloudflare-dns.com/dns-query` |
| IPv4 | `1.1.1.1` و`1.0.0.1` |
| IPv6 | `2606:4700:4700::1111` و`2606:4700:4700::1001` |
| قاعدة التشغيل | `Connect` عند الطلب |
| قابلية الإزالة | نعم |

### 2) ملف Global HTTP Proxy

| الخاصية | القيمة |
|---|---|
| Payload Type | `com.apple.proxy.http.global` |
| النوع | `Manual` |
| الخادم | `94.142.36.145` |
| المنفذ | `1080` |
| المصادقة | غير مفعّلة |
| تجاوز صفحة دخول الشبكات العامة | مسموح |
| قابلية الإزالة | نعم |

> [!WARNING]
> يتطلب Global HTTP Proxy جهاز iPhone أو iPad **خاضعًا للإشراف (Supervised)**، ويُستخدم عادةً ضمن إدارة الأجهزة. إذا لم تكن تعرف مشغّل خادم الـProxy أو لا تثق به، فلا تثبّت هذا الملف.

## 📲 التثبيت

### الطريقة الموصى بها — صفحة التثبيت

بعد [تفعيل GitHub Pages](#-نشر-صفحة-التثبيت)، افتح الرابط التالي باستخدام **Safari** على جهاز Apple:

<p align="center">
  <a href="https://alyazouri.github.io/Q10/install-profile.html"><strong>فتح صفحة تثبيت SERVER ALYAZOURI</strong></a>
</p>

ثم:

1. اضغط زر تنزيل الملف المطلوب ووافق على التنزيل.
2. على iPhone أو iPad، افتح **الإعدادات** ثم **تم تنزيل ملف تعريف**.
3. راجع اسم المؤسسة ومحتوى الملف بعناية.
4. اضغط **تثبيت** وأدخل رمز قفل الجهاز عند الطلب.

### التنزيل المباشر

- [تنزيل ملف DNS المشفّر](https://raw.githubusercontent.com/alyazouri/Q10/main/SERVER_ALYAZOURI.mobileconfig)
- [تنزيل ملف Global HTTP Proxy](https://raw.githubusercontent.com/alyazouri/Q10/main/SERVER_ALYAZOURI_PROXY.mobileconfig)

> إذا عُرض الملف كنص بدل بدء التثبيت، استخدم صفحة التثبيت عبر Safari بعد تفعيل GitHub Pages.

## ✅ التحقق بعد التثبيت

### التحقق من DNS

1. افتح [Cloudflare Connection Information](https://1.1.1.1/help).
2. ابحث عن السطر **Using DNS over HTTPS (DoH)**.
3. يجب أن تكون قيمته **Yes**.

### التحقق من Proxy

جرّب الوصول إلى الإنترنت بعد التثبيت. إذا انقطع الاتصال، فقد يكون الخادم غير متاح أو غير متوافق مع الشبكة الحالية؛ أزل ملف التعريف لاستعادة الإعداد السابق.

## 🗑️ إزالة ملف التعريف

على iPhone أو iPad:

1. افتح **الإعدادات**.
2. انتقل إلى **عام** ← **VPN وإدارة الجهاز**.
3. اختر ملف **SERVER ALYAZOURI** المطلوب.
4. اضغط **إزالة ملف التعريف** ثم أكّد باستخدام رمز الجهاز.

على macOS، افتح **إعدادات النظام** وابحث عن **Profiles / ملفات التعريف**، ثم حدّد الملف وأزله.

## 🌐 نشر صفحة التثبيت

المشروع مناسب للنشر مباشرةً عبر GitHub Pages:

1. افتح **Settings** في المستودع.
2. انتقل إلى **Pages**.
3. ضمن **Build and deployment** اختر **Deploy from a branch**.
4. اختر فرع `main` والمجلد `/ (root)`، ثم اضغط **Save**.
5. بعد اكتمال النشر ستكون الصفحة على:

```text
https://alyazouri.github.io/Q10/install-profile.html
```

### تشغيل الصفحة محليًا للتطوير

```bash
git clone https://github.com/alyazouri/Q10.git
cd Q10
python3 -m http.server 8080
```

ثم افتح `http://localhost:8080/install-profile.html` لمعاينة الواجهة. استخدم استضافة HTTPS فعلية عند الاختبار على جهاز آخر.

## 🧪 فحص الملفات قبل النشر

على macOS، يمكن التأكد من سلامة بنية ملفات `plist` بالأوامر التالية:

```bash
plutil -lint SERVER_ALYAZOURI.mobileconfig
plutil -lint SERVER_ALYAZOURI_PROXY.mobileconfig
```

ولحساب بصمة SHA‑256 بعد أي تعديل:

```bash
shasum -a 256 *.mobileconfig
```

## 🔐 الأمان والخصوصية

- الملفان الحاليان **غير موقّعين رقميًا**؛ لذلك قد يعرض النظام عبارة **Unsigned / غير موقّع**.
- راجع محتوى كل ملف في هذا المستودع، وتأكد من مصدره، قبل تثبيته.
- ملف DNS يرسل استعلامات أسماء النطاقات إلى **Cloudflare**؛ راجع [سياسة الخصوصية لخدمة 1.1.1.1](https://www.cloudflare.com/privacypolicy/).
- ملف Proxy يوجّه معظم حركة الويب عبر `94.142.36.145:1080`. يستطيع مشغّل الخادم رؤية بيانات الاتصال، وأي محتوى HTTP غير مشفّر؛ لا تستخدمه لنقل معلومات حساسة ما لم تكن تثق بالمشغّل.
- لا يتضمن ملف Proxy شهادة جذر، ولا يفعّل اعتراض TLS/HTTPS بحد ذاته.
- يُنصح بتوقيع ملفات التعريف بشهادة موثوقة قبل توزيعها في بيئة إنتاجية.

## 🛠️ التخصيص

عند إنشاء نسخة خاصة بك:

1. غيّر `PayloadIdentifier` إلى نطاق عكسي تملكه، مثل `com.example.q10`.
2. أنشئ قيمة `PayloadUUID` جديدة لكل Payload باستخدام الأمر `uuidgen`.
3. حدّث `PayloadDisplayName` و`PayloadOrganization` والوصف.
4. عدّل عنوان DNS أو خادم Proxy والمنفذ حسب حاجتك.
5. افحص الملف باستخدام `plutil`، ثم اختبره على جهاز غير أساسي أولًا.
6. حدّث النصوص والروابط داخل `install-profile.html` لتطابق الإعدادات الجديدة.

> [!CAUTION]
> لا تعِد استخدام معرّفات UUID نفسها لملفات تعريف مختلفة؛ فقد يؤدي ذلك إلى استبدال ملف سابق أو حدوث سلوك غير متوقع أثناء الإدارة.

## 📚 مراجع رسمية

- [Apple — DNS Settings payload](https://support.apple.com/guide/deployment/dns-settings-payload-settings-dep86469ba99/web)
- [Apple — Global HTTP Proxy payload](https://support.apple.com/guide/deployment/global-http-proxy-payload-settings-dep7ba46fcd/web)
- [Apple — About device supervision](https://support.apple.com/guide/deployment/about-device-supervision-dep1d89f0bff/web)
- [Cloudflare — DNS over HTTPS](https://developers.cloudflare.com/1.1.1.1/encryption/dns-over-https/)

## 🤝 المساهمة

الاقتراحات والتحسينات مرحّب بها عبر [فتح Issue](https://github.com/alyazouri/Q10/issues) أو إرسال Pull Request. عند تعديل ملفات التعريف، اشرح الإعدادات المتغيرة ونتيجة اختبارها بوضوح.

## 📄 الترخيص

لم يُضف ملف ترخيص إلى المستودع بعد. ما لم يُذكر خلاف ذلك، لا يعني نشر الشيفرة منح إذن تلقائيًا بإعادة استخدامها أو توزيعها. أضف ملف `LICENSE` مناسبًا إذا كنت تريد السماح بذلك صراحةً.

---

<div align="center">

صُنع لتبسيط إعداد DNS المشفّر على أجهزة Apple — **استخدم ملفات التعريف بمسؤولية.**

</div>

</div>
