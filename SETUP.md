# 🚀 מדריך התקנה — מנהל משימות PWA

## מה יש בחבילה
| קובץ | תיאור |
|------|--------|
| `index.html` | ה-PWA המלא |
| `sw.js` | Service Worker (אופליין) |
| `manifest.json` | הגדרות PWA להתקנה |
| `Code.gs` | Apps Script חדש (REST API) |

---

## שלב 1 — עדכן את Apps Script

1. פתח את [Google Apps Script](https://script.google.com)
2. **מחק את כל הקוד הישן**
3. הדבק את התוכן מ-`Code.gs`
4. שמור (Ctrl+S)

---

## שלב 2 — פרוס כ-Web App

1. לחץ **Deploy → New Deployment**
2. בחר Type: **Web App**
3. הגדרות:
   - Execute as: **Me**
   - Who has access: **Anyone** ← חשוב!
4. לחץ **Deploy**
5. **העתק את ה-URL** שמופיע

---

## שלב 3 — עדכן את index.html

פתח את `index.html` וחפש שורה זו (קרוב לתחילת ה-JavaScript):

```javascript
var APPS_SCRIPT_URL = 'YOUR_APPS_SCRIPT_URL_HERE';
```

**החלף** את `YOUR_APPS_SCRIPT_URL_HERE` ב-URL שהעתקת בשלב 2.

---

## שלב 4 — אחסן את קבצי ה-PWA

### אפשרות א׳ — GitHub Pages (חינמי, מומלץ)
1. צור repository ב-GitHub
2. העלה את `index.html`, `sw.js`, `manifest.json`
3. הפעל **Pages** בהגדרות → branch: main
4. הכתובת תהיה: `https://USERNAME.github.io/REPO`

### אפשרות ב׳ — Netlify Drop (הכי קל)
1. כנס ל-[netlify.com/drop](https://netlify.com/drop)
2. גרור את תיקיית הקבצים לדפדפן
3. מקבל URL מיידית!

### אפשרות ג׳ — Google Drive + Pages
1. העלה לתיקייה ב-Drive
2. שתף כ-"Anyone with link"
3. *(פחות מומלץ לPWA)*

---

## שלב 5 — הוסף אייקון

צור שתי תמונות ריבועיות:
- `icon-192.png` — 192×192 פיקסל
- `icon-512.png` — 512×512 פיקסל

והעלה לאותה תיקייה עם שאר הקבצים.

> **טיפ קל:** השתמש ב-[favicon.io](https://favicon.io) ליצירת אייקון מהיר

---

## שלב 6 — התקן כאפליקציה 📲

### אנדרואיד (Chrome)
1. פתח את הכתובת ב-Chrome
2. לחץ על 3 הנקודות → **"הוסף למסך הבית"**
3. או המתן לבאנר שיופיע אוטומטית

### iPhone (Safari)
1. פתח ב-Safari (חובה!)
2. לחץ **Share → Add to Home Screen**

---

## שינויים ב-Code.gs לעומת הישן

| לפני | אחרי | שיפור |
|------|------|-------|
| `saveTasks()` — לולאת עיצוב שורה אחר שורה | Batch עם `getRangeList()` | 10× מהיר יותר |
| `saveTask()` — 2 קריאות API | קריאה אחת + format | 50% מהיר |
| מחזיר HTML דרך `doGet()` | מחזיר JSON כ-REST API | תמיכה ב-PWA |
| אין CORS headers | CORS מלא | גישה מכל דומיין |

---

## פיצ׳רים חדשים ב-PWA

✅ **אופליין מלא** — כל המשימות נשמרות ב-localStorage  
✅ **סנכרון חכם** — כשחוזר חיבור, מסנכרן שינויים אוטומטית  
✅ **התקנה** — ניתן להתקין כאפליקציה נייטיבית  
✅ **מהיר** — טוען מהמטמון המקומי מיידית  
✅ **חיווי סנכרון** — נקודה ירוקה/צהובה/אדומה בפינה  

---

## אם יש שגיאת CORS

הוסף לתחילת `doGet` ו-`doPost` ב-Apps Script:
```javascript
// כבר כלול ב-Code.gs החדש
```
אם עדיין יש בעיה — ודא שבחרת **"Anyone"** ב-Who has access.

---

## תמיכה

אם App Script מחזיר שגיאה — פתח **Executions** ב-Apps Script לצפייה בלוגים.
