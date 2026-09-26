# הגדרת המנויים בפועל — Play Console + RevenueCat

מודל התשלום: פרופיל ראשון חינם. כל פרופיל נוסף (עד 3 נוספים, סה"כ 4) הוא **מנוי חודשי נפרד** של 10 ₪, כי Google Play לא תומך ב"כמות" על מנוי בודד — צריך מוצר נפרד לכל פרופיל נוסף.

## מזהי המוצרים (חייבים להיות מדויקים — הקוד כבר מצפה להם)
| Product ID | פותח | מחיר |
|---|---|---|
| `person_slot_2` | פרופיל מס' 2 | 10 ₪ / חודש |
| `person_slot_3` | פרופיל מס' 3 | 10 ₪ / חודש |
| `person_slot_4` | פרופיל מס' 4 | 10 ₪ / חודש |

## שלב 1 — Play Console
עבור כל אחד משלושת ה-IDs למעלה:
1. **Monetize → Products → Subscriptions → Create subscription**
2. Product ID: בדיוק כמו בטבלה (רגיש לאותיות, אי אפשר לשנות אחרי יצירה)
3. Base plan: חודשי (Monthly), מחיר 10 ₪
4. הפעל (Activate) את שלושתם

## שלב 2 — RevenueCat
1. הרשמה בחינם ב-app.revenuecat.com
2. Create Project → הוסף אפליקציה, פלטפורמה Google Play, applicationId: `com.madruach.app`
3. **חיבור ל-Play Console (נדרש לאימות רכישות):** Play Console → Setup → API access → צור/קשר Google Cloud project → צור Service Account עם הרשאת "Financial data" → הורד קובץ JSON → העלה אותו בהגדרות RevenueCat של האפליקציה
4. **Products:** צור ב-RevenueCat שלושה מוצרים עם אותם Product IDs בדיוק (`person_slot_2/3/4`), מקושרים למוצרי ה-Play Console המתאימים
5. **Offering:** צור Offering אחד (למשל "default") עם שלושה Packages, אחד לכל מוצר
6. **API Key:** Project settings → API keys → העתק את ה-**Public Google/Android API key**

## שלב 3 — חיבור ל-קוד
תן לי את ה-API key מסעיף 6, ואני:
1. אכניס אותו ל-`RC_API_KEY.android` ב-`index.html`
2. אבנה מחדש AAB חתום
3. אבדוק שהרכישה בפועל עובדת (sandbox/test track לפני production)

## תזכורת חשובה
כל עוד ה-API key ריק בקוד, האפליקציה נשארת ב"מצב בדיקה" (פתיחה מקומית חינמית, מתויגת ככה בממשק) — אין סיכון שמשתמשים אמיתיים ישלמו לפני שהכל מוגדר נכון.
