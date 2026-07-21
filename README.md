[README.md](https://github.com/user-attachments/files/30224796/README.md)
# SmartQuote Pro — הוראות העלאה ל-Vercel

## מה יש כאן
פרויקט Vite + React מוכן לפריסה. זה בדיוק אותה אפליקציה שראית בצ'אט,
רק ארוזה כפרויקט אתר אמיתי (במקום קובץ בודד בתוך Claude).

**שינוי טכני יחיד שנעשה:** האפליקציה השתמשה ב-`window.storage`, API ששייך
רק לסביבת התצוגה המקדימה של Claude. הוספתי קובץ קטן (`src/storage-polyfill.js`)
שמדמה את אותו API אבל שומר בפועל ב-localStorage של הדפדפן. כלומר: הנתונים
עדיין נשמרים רק בדפדפן של המשתמש (בדיוק כמו קודם) — זה עדיין לא בסיס נתונים
משותף לכמה משתמשים.

---

## אפשרות 1: דרך GitHub (מומלץ — נותן עדכונים אוטומטיים בכל שינוי)

### שלב 1 — התקנת Node.js (אם עוד אין)
הורד והתקן מ־https://nodejs.org (גרסת LTS)

### שלב 2 — בדיקה מקומית שהכול עובד
בתיקיית הפרויקט, בטרמינל:
```
npm install
npm run dev
```
זה יפתח את האתר על `http://localhost:5173` — תבדוק שהכול עובד לפני שממשיכים.

### שלב 3 — העלאה ל-GitHub
1. צור חשבון ב-https://github.com אם אין לך
2. צור repository חדש (ריק, בלי README)
3. בטרמינל, מתוך תיקיית הפרויקט:
```
git init
git add .
git commit -m "SmartQuote Pro - initial version"
git branch -M main
git remote add origin https://github.com/USERNAME/REPO_NAME.git
git push -u origin main
```
(תחליף USERNAME/REPO_NAME בשם המשתמש והריפו שיצרת)

### שלב 4 — חיבור ל-Vercel
1. היכנס ל-https://vercel.com והתחבר עם חשבון ה-GitHub שלך
2. לחץ "Add New Project"
3. בחר את ה-repository שיצרת
4. Vercel יזהה אוטומטית שזה פרויקט Vite — אין צורך לשנות שום הגדרה
5. לחץ "Deploy"
6. אחרי דקה תקבל כתובת ציבורית כמו `smartquote-pro.vercel.app`

מעכשיו, כל `git push` ל-main יעדכן את האתר החי אוטומטית.

---

## אפשרות 2: דרך Vercel CLI (מהיר יותר, בלי GitHub)

```
npm install -g vercel
cd smartquote-web
vercel login
vercel
```
תענה על כמה שאלות (שם הפרויקט וכו') ותקבל קישור לתצוגה מקדימה.
כדי לפרוס לכתובת הסופית (production):
```
vercel --prod
```

---

## חשוב לדעת — לפני שמראים ללקוחות אמיתיים

1. **Vercel Hobby (החינמי) אסור לשימוש מסחרי** לפי תנאי השימוש שלו. מצוין
   לבדיקות ולהדגמות ללא תשלום, אבל ברגע שגובים כסף ממישהו — צריך Vercel Pro
   ($20/חודש).
2. **הנתונים עדיין רק בדפדפן** — כל משתמש שנכנס לאתר רואה נתונים ריקים
   משלו, ואין שיתוף בין מכשירים/דפדפנים. זה עדיין לא "SaaS אמיתי" עם
   התחברות ובסיס נתונים משותף — זה השלב הבא (Supabase וכו', כמו שדיברנו).
3. אחרי הפריסה, כדאי לבדוק שוב את כפתור ה-PDF/הדפסה ואת שליחת הוואטסאפ/מייל
   בדפדפן אמיתי (לא רק בתוך Claude), כדי לוודא שהכול עובד באתר החי.
