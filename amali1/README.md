# Cyberchase Ma'lumotlar Bazasi Bilan Ishlash Qo'llanmasi 📚

## Loyihani Boshlash 🚀

1. "cyberchase.db" faylini yuklab oling
2. "amaliy_db2" nomli papka yarating
3. Ushbu papkani VS Code da oching
4. Quyidagi SQL fayllarini yarating: `1.sql`, `2.sql`, `3.sql` ... `13.sql`

## Ma'lumotlar Bazasini Ko'rish 👀

Ma'lumotlar bazasidagi ma'lumotlarni ko'rish va tekshirish uchun quyidagi buyruqdan foydalaning:
```sql
SELECT * FROM episodes LIMIT 10;
```

## Ma'lumotlar Bazasi Tuzilishi 📋

Cyberchase ma'lumotlar bazasida `episodes` nomli bitta jadval mavjud. Bu jadvalda quyidagi ustunlar bor:

| Ustun | Tavsif |
|-------|---------|
| `id` | Har bir qatorni (epizodni) noyob identifikatsiya qiladi |
| `season` | Epizod ko'rsatilgan mavsum raqami |
| `episode_in_season` | Mavsumda epizodning tartib raqami |
| `title` | Epizod nomi |
| `topic` | Epizodda o'rgatiladigan g'oyalar |
| `air_date` | Epizod efirga chiqqan sana (YYYY-MM-DD formatida) |
| `production_code` | PBS tomonidan ichki foydalanish uchun beriladigan noyob ID |

## SQL Vazifalar 📝

### 1-vazifa
1.sql faylida Cyberchase'ning birinchi mavsumi (1-mavsum) epizodlari nomlarini ro'yxatini chiqaruvchi SQL so'rov yozing.

### 2-vazifa
2.sql faylida har bir mavsumning birinchi epizodining mavsum raqami va nomini ko'rsating.

### 3-vazifa
3.sql faylida "Hackerized!" epizodining ishlab chiqarish kodini toping.

### 4-vazifa
4.sql faylida mavzusi ko'rsatilmagan epizodlarning nomlarini topish uchun so'rov yozing.

### 5-vazifa
5.sql faylida 2004-yil 31-dekabrda efirga uzatilgan bayram epizodining nomini toping.

### 6-vazifa
6.sql faylida 6-mavsum (2008) epizodlaridan 2007-yilda erta chiqarilgan epizodlar nomlarini ro'yxatini chiqaring.

**Maslahat:** Raqamli qiymatlarni izlashda LIKE operatoridan foydalanish mumkin:
- `LIKE '2007%'` - 2007 bilan boshlanadigan barcha qiymatlarni topish
- `%` - istalgan belgilar ketma-ketligini bildiradi
- Masalan: `air_date LIKE '2007%'` - 2007-yildagi barcha sanalarni topadi

### 7-vazifa
7.sql faylida kasrlar haqida o'rgatadigan barcha epizodlarning nomlari va mavzularini ko'rsatuvchi SQL so'rov yozing.

### 8-vazifa
8.sql faylida so'nggi 6 yilda (2018-2023 yillar oralig'ida) chiqarilgan epizodlar sonini hisoblovchi so'rov yozing.
Eslatma: Sanalar bilan BETWEEN operatorini qo'llash mumkin, masalan: `BETWEEN '2000-01-01' AND '2000-12-31'`

### 9-vazifa
9.sql faylida Cyberchase'ning dastlabki 6 yilida (2002-2007 yillar oralig'ida) chiqarilgan epizodlar sonini hisoblovchi so'rov yozing.

### 10-vazifa
10.sql faylida barcha epizodlarning ID raqamlari, nomlari va ishlab chiqarish kodlarini ko'rsatuvchi SQL so'rov yozing. Natijalarni ishlab chiqarish kodi bo'yicha (ertadan keyingisigacha) tartiblang.

### 11-vazifa
11.sql faylida 5-mavsum epizodlarining nomlarini teskari alifbo tartibida ko'rsating.

### 12-vazifa
12.sql faylida noyob epizod nomlarining sonini hisoblang.

### 13-vazifa
13.sql faylida o'zingiz tanlagan savol bo'yicha SQL so'rov yozing. Bu so'rov quyidagi talablarga javob berishi kerak:
- WHERE bilan AND yoki OR operatorlarini ishlatgan holda kamida bitta shart ishlatilishi kerak

## SQLite bilan ishlash 🛠️

### Ma'lumotlar bazasini ochish
Terminalda quyidagi buyruqni kiriting:
```bash
sqlite3 cyberchase.db
```

### Natijalarni qulay ko'rinishda olish
```sql
.mode box
```

### SQL fayllarni bajarish
```sql
.read 1.sql
```

## Muhim Ko'rsatmalar ⚠️

1. Har bir savolga javob berish uchun **bitta** SQL so'rov yozishingiz kerak

2. Epizodlarning ID raqamlariga bog'liq bo'lgan so'rovlar yozmang: 
   - So'rovlaringiz har qanday ID raqamlari bilan ham to'g'ri ishlashi kerak

3. Har bir so'rov faqat savolga javob berish uchun zarur bo'lgan ma'lumotlarni qaytarishi kerak:
   - Masalan, agar savolda faqat epizod nomlari so'ralgan bo'lsa, so'rovingiz efir sanasini qaytarmasligi kerak