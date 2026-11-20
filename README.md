# برنامج عروض الأسعار – المصرية لتكنولوجيا أنظمة المراقبة

الملفات كلها جاهزة. الخطوات بالترتيب:

## 1) إعداد Firebase (من المتصفح)
1. ادخل https://console.firebase.google.com واعمل **Add project** (اسم أي حاجة، وممكن تقفل Google Analytics).
2. من القايمة: **Build > Authentication > Get started > Sign-in method > Google > Enable**، واختار إيميلك وادوس Save.
3. **Build > Firestore Database > Create database**: اختار أقرب موقع (مثلًا europe-west) و **Production mode**.
4. افتح تبويب **Rules** والصق ده مكان الموجود، وغيّر الإيميل لإيميل Gmail بتاعك **بحروف صغيرة**، وبعدين **Publish**:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{uid}/{document=**} {
      allow read, write: if request.auth != null
        && request.auth.uid == uid
        && request.auth.token.email == 'PUT_YOUR_GMAIL_HERE@gmail.com'
        && request.auth.token.email_verified == true;
    }
  }
}
```
5. من ترس **Project settings > General > Your apps** دوس على أيقونة الويب `</>` وسجّل التطبيق، وانسخ قيم `firebaseConfig`.
6. افتح ملف `firebase-config.js` والصق القيم مكان كلمة PASTE.

## 2) رفع الكود على GitHub
1. في الـrepository بتاعك (esst) دوس **Add file > Upload files**.
2. اسحب كل الملفات (ما عدا build.py لو موجود) وادوس **Commit changes**.

## 3) النشر على GitHub Pages
1. من **Settings > Pages**: Source = **Deploy from a branch**، Branch = **main** و Folder = **/(root)**، وادوس Save.
2. بعد دقيقة أو اتنين هيظهر الرابط: `https://ahmed197809.github.io/esst/`
3. ارجع لـ Firebase: **Authentication > Settings > Authorized domains > Add domain** وضيف: `ahmed197809.github.io`

## 4) التثبيت على الموبايل والكمبيوتر
- أندرويد (Chrome): قايمة النقط التلاتة > **Install app** أو **Add to Home screen**.
- آيفون (Safari): زرار المشاركة > **Add to Home Screen**.
- كمبيوتر (Chrome/Edge): أيقونة التثبيت في شريط العنوان، أو زرار "تثبيت التطبيق" جوه البرنامج.

## 5) النسخة الاحتياطية
من تبويب **الإعدادات** > تحميل نسخة احتياطية / استرجاع من نسخة. اعملها بشكل دوري.

## ملاحظات
- الـrepository عام (Public)، ده عادي لأن الكود مفيهوش بيانات، وبياناتك كلها في Firestore ومحمية بالقواعد اللي فوق.
- لازم إنترنت علشان البرنامج يفتح.
