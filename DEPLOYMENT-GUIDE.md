# 🚀 دليل النشر — يعمل على Render بدون أي إعداد

## ✅ المشروع جاهز للنشر مباشرةً على Render!

المشروع يستخدم **PostgreSQL** كقاعدة البيانات و**Node.js 22** للتشغيل. عند الرفع على Render عبر Blueprint، سيتم إنشاء كل شيء تلقائياً.

---

## 🎯 النشر على Render (الأسهل — موصى به)

### الخطوات:

1. **ارفع المشروع إلى GitHub:**
   ```bash
   unzip syrian-board-direct-deploy.zip
   cd syrian-board-direct-deploy
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/USERNAME/syrian-board.git
   git push -u origin main
   ```

2. **على Render:**
   - افتح https://render.com
   - سجّل بحساب GitHub
   - اذهب إلى **Dashboard** → **New +** → **Blueprint**
   - اختر مستودع `syrian-board`
   - سيقرأ Render ملف `render.yaml` تلقائياً وينشئ:
     - ✅ قاعدة بيانات PostgreSQL مجانية
     - ✅ تطبيق الويب (Node.js 22)
     - ✅ كل متغيرات البيئة
   - اضغط **Apply**

3. **انتظر 3-5 دقائق** — ستحصل على رابط: `https://syrian-board-direct.onrender.com`

### ⚠️ مهم: استخدم Blueprint وليس Web Service يدوي
- ❌ لا تختر **New → Web Service** (سيستخدم Docker ويفشل)
- ✅ اختر **New → Blueprint** (سيستخدم render.yaml و Node.js الأصلي)

### ✅ ما سيحدث تلقائياً:
- إنشاء PostgreSQL مجاني
- ربط `DATABASE_URL` تلقائياً
- تثبيت Node.js 22
- تشغيل `prisma db push` لإنشاء الجداول
- تشغيل التطبيق

---

## 🌐 النشر على Railway

1. اذهب إلى https://railway.app
2. **New Project** → **Deploy from GitHub repo**
3. اختر المستودع
4. أضف PostgreSQL: **New → Database → PostgreSQL**
5. في متغيرات البيئة، اضبط:
   - `DATABASE_URL` = رابط PostgreSQL من Railway
   - `ADMIN_PASSWORD_B64` = `JDJiJDEwJEtBaHpUNEN0N1Z0TkJNOUU5OXZFbE94ODVNck9saFFZL1VpN1h3eG5FYjRQYnV0YkR2bFVT`
   - `JWT_SECRET` = `SyrianBoard_Direct_2026_SecretKey_DoNotShare_8f3k2m1x7p5q4w6e8r0t2y4u6i8o0a1b3c5d7e9f`

---

## ▲ النشر على Vercel

1. اذهب إلى https://vercel.com
2. **New Project** → اختر المستودع
3. أضف قاعدة بيانات PostgreSQL من [Neon](https://neon.com) (مجاني):
   - أنشئ حساباً على Neon
   - انسخ `Connection string`
4. في Vercel، أضف متغيرات البيئة:
   - `DATABASE_URL` = رابط Neon
   - `ADMIN_PASSWORD_B64` = `JDJiJDEwJEtBaHpUNEN0N1Z0TkJNOUU5OXZFbE94ODVNck9saFFZL1VpN1h3eG5FYjRQYnV0YkR2bFVT`
   - `JWT_SECRET` = `SyrianBoard_Direct_2026_SecretKey_DoNotShare_8f3k2m1x7p5q4w6e8r0t2y4u6i8o0a1b3c5d7e9f`
5. **Deploy**

---

## 🌐 النشر على Netlify

1. اذهب إلى https://app.netlify.com/drop
2. اسحب مجلد المشروع
3. أضف قاعدة بيانات PostgreSQL من [Neon](https://neon.com)
4. في **Site Settings → Environment Variables**، أضف نفس المتغيرات الثلاثة
5. **Trigger Deploy**

---

## 🏃‍♂️ التشغيل المحلي (للتطوير)

تحتاج PostgreSQL محلي. الطريقة الأسهل:

```bash
# تثبيت PostgreSQL محلي أو استخدام Docker:
docker run -d --name pg -e POSTGRES_DB=board -e POSTGRES_USER=boarduser -e POSTGRES_PASSWORD=boardpass_change_me -p 5432:5432 postgres:16-alpine

# تثبيت الحزم
npm install --legacy-peer-deps

# تعيين DATABASE_URL في ملف .env
# DATABASE_URL="postgresql://boarduser:boardpass_change_me@localhost:5432/board?schema=public"

# تهيئة قاعدة البيانات
npx prisma db push --accept-data-loss

# تشغيل التطوير
npm run dev
```

افتح http://localhost:3000

---

## 🔑 المسارات

| المسار | الوصف |
|---|---|
| `/` | الاستمارة (للمتقدمين) |
| `/syrian-commission-for-medical-specialties` | لوحة الإدارة |
| `/api/applications` | API الطلبات |
| `/api/admin/*` | APIs الإدارة |

---

## 🛡️ المزايا

- 🔒 **إخفاء أعداد الشواغر** — تُرسل فقط كحالة "متاح/غير متاح"
- 🚫 **منع تكرار الرقم الوطني** — تحقق فوري ومضاعف على الخادم
- 📋 **الوثائق المطلوبة كتعداد** — لا checkboxes، فقط قائمة وزر متابعة
- 👨‍⚕️ **منطق طبيب البورد السوري** — رغبة واحدة للأطفال الخدج + معدل البورد
- 🖨️ **طباعة A4** مع علامات ✓ بجانب كل وثيقة
- 📊 **لوحة إدارة** محمية + تصدير CSV
- 🌐 **قابل للنشر على أي استضافة** (Render, Railway, Vercel, Netlify)

---

## 🔐 الأمان

**كلمة مرور لوحة الإدارة الافتراضية**: `board-admin-2026`

للتغيير:
```bash
node scripts/generate-hash.js "your-new-password"
# ضع الناتج في ADMIN_PASSWORD_B64
```

---

## 🆘 استكشاف الأخطاء

### "Docker build failed" على Render
- ❌ لا تستخدم **New → Web Service** (سيحاول استخدام Docker)
- ✅ استخدم **New → Blueprint** (سيستخدم render.yaml مع Node.js الأصلي)
- تأكد أن ملف `render.yaml` موجود في جذر المستودع

### "Database connection failed" على Render
- تأكد أن `render.yaml` موجود في المستودع
- تحقق من سجلات Render — يجب أن يظهر `prisma db push` نجح

### على Vercel/Netlify
- تأكد أن `DATABASE_URL` يبدأ بـ `postgresql://`
- أضف `?sslmode=require` لنهاية رابط Neon

### "صفحة فارغة"
- راجع Build Logs
- تأكد أن كل متغيرات البيئة موجودة

---

## 💡 ملاحظات

1. **Render PostgreSQL المجاني** يوقف قاعدة البيانات بعد 90 يوماً — للإنتاج، استخدم خطة مدفوعة
2. **Neon PostgreSQL مجاني للأبد** — موصى به لـ Vercel/Netlify
3. **غيّر كلمة المرور الافتراضية** قبل النشر الرسمي
4. **اعمل نسخة احتياطية** من قاعدة البيانات دورياً

بالتوفيق! 🎉
