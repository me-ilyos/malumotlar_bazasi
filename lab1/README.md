# Kichik Kutubxona Database - Laboratoriya ishi (SQLite3)

## Kirish
Ushbu laboratoriya ishida biz kichik kutubxona uchun SQLite3 ma'lumotlar bazasini yaratamiz va uni boshqarishni o'rganamiz. 

## 0-Qadam: SQLite3 bilan ishlash
VS Code ozizga papka ochib. Terminal/CMD da SQLite3 ni ishga tushiramiz va database yaratamiz:
```bash
sqlite3 library.db
```

Izoh: SQLite3 da database - bu oddiy fayl. Yuqoridagi buyruq library.db nomli fayl yaratadi.

## 1-Qadam: Mualliflar jadvali
Mualliflar jadvalini yaratamiz:

```sql
CREATE TABLE muallif (
    id INTEGER,
    first_name TEXT NOT NULL,
    last_name TEXT NOT NULL,
    birth_year INTEGER,
    country TEXT,
    PRIMARY KEY ("id")
);
```

Izoh: 
- SQLite3 da VARCHAR o'rniga TEXT ishlatamiz
- AUTOINCREMENT o'rniga INTEGER PRIMARY KEY yetarli (avtomatik oshib boradi)
- SQLite3 da ma'lumotlar turlari: TEXT, INTEGER, REAL, BLOB, NUMERIC

## 2-Qadam: Kitoblar jadvali

```sql
CREATE TABLE kitoblar (
    id INTEGER,
    title TEXT NOT NULL,
    author_id INTEGER,
    published_year INTEGER,
    isbn TEXT UNIQUE,
    quantity INTEGER DEFAULT 1 CHECK(quantity > 0),
    PRIMARY KEY ("id"),
    FOREIGN KEY (author_id) REFERENCES authors(id)
);
```

## 3-Qadam: Azolar jadvali

```sql
CREATE TABLE azolar (
    id INTEGER,
    first_name TEXT NOT NULL,
    last_name TEXT NOT NULL,
    email TEXT UNIQUE,
    join_date TEXT DEFAULT CURRENT_DATE,
    status TEXT DEFAULT 'active',
    PRIMARY KEY ("id")
);
```

Izoh:
- SQLite3 da sana uchun maxsus tur yo'q, TEXT ishlatamiz
- CURRENT_DATE SQLite3 da ham ishlaydi

## 4-Qadam: Kitob olish jadvali

```sql
CREATE TABLE kitob_olish (
    id INTEGER,
    book_id INTEGER,
    member_id INTEGER,
    borrow_date TEXT DEFAULT CURRENT_DATE,
    return_date TEXT,
    status TEXT DEFAULT 'olindi' CHECK(status in ('olindi', 'qaytarildi')),
    PRIMARY KEY ("id"),
    FOREIGN KEY (book_id) REFERENCES books(id),
    FOREIGN KEY (member_id) REFERENCES members(id)
);
```

## 5-Qadam: Ma'lumotlarni kiritish

```sql
-- Mualliflar
INSERT INTO muallif (first_name, last_name, birth_year, country) VALUES
('O''tkir', 'Hoshimov', 1941, 'Uzbekistan'),
('Tohir', 'Malik', 1946, 'Uzbekistan'),
('Ernest', 'Hemingway', 1899, 'USA');

-- Kitoblar
INSERT INTO kitoblar (title, author_id, published_year, isbn, quantity) VALUES
('Dunyoning ishlari', 1, 1982, '9789943282711', 3),
('Shaytanat', 2, 1992, '9789943115613', 2),
('The Old Man and the Sea', 3, 1952, '9780684801223', 1);

-- A'zolar
INSERT INTO azolar (first_name, last_name, email) VALUES
('Aziz', 'Karimov', 'aziz@example.com'),
('Nilufar', 'Sobirova', 'nilufar@example.com');
```

## 6-Qadam: SQLite3 foydali buyruqlari
```sql
.tables          -- Barcha jadvallarni ko'rish
.schema muallif  -- Authors jadvalining strukturasini ko'rish
.mode column     -- Natijalarni ustunlar ko'rinishida chiqarish
.headers on      -- Ustun nomlarini ko'rsatish
```

## 7-Qadam: Ma'lumotlarni so'rash
```sql
-- Barcha kitoblarni mualliflari bilan ko'rish
SELECT b.title, a.first_name, a.last_name
FROM kitoblar b
JOIN muallif a ON b.author_id = a.id;

-- Kutubxonada mavjud kitoblar soni
SELECT COUNT(*) as total_books
FROM kitoblar;

-- Har bir a'zoning olgan kitoblari
SELECT m.first_name, m.last_name, b.title, br.borrow_date
FROM kitob_olish br
JOIN members m ON br.member_id = m.id
JOIN kitoblar b ON br.book_id = b.id
WHERE br.status = 'borrowed';
```

## Vazifa
1. Yuqoridagi barcha buyruqlarni ketma-ketlikda bajaring
2. Quyidagi so'rovlarni yozing:
   - O'zbekistonlik mualliflarning kitoblarini ko'rsating
   - 1990-yildan keyin nashr qilingan kitoblarni ko'rsating
   - Kutubxonada 2 va undan ortiq nusxada mavjud kitoblarni ko'rsating
   - Eng ko'p kitob olgan a'zoni aniqlang

## Muhim eslatmalar
1. SQLite3 da database yaratish uchun CREATE DATABASE kerak emas
2. Data turlari soddalashtirilgan (TEXT, INTEGER, REAL, BLOB, NUMERIC)
3. SQLite3 da `.` bilan boshlanadigan maxsus buyruqlar mavjud
4. SQLite3 database oddiy fayl sifatida saqlanadi
5. Terminal/CMD dan chiqish uchun `.quit` buyrug'ini ishlating

FILE lar JOYLASHUVI va QOSHIMCHA

# Kichik Kutubxona Database - Laboratoriya ishi (SQLite3)

## Loyiha strukturasi tepadan koribham qilsayz boladi.
```
library_lab/
├── schema/
│   ├── 1_mualliflar.sql
│   ├── 2_kitoblar.sql
│   ├── 3_azolar.sql
│   └── 4_kitob_olish.sql
├── data/
│   ├── 1_mualliflar_data.sql
│   ├── 2_kitoblar_data.sql
│   └── 3_azolar_data.sql
├── queries/
│   ├── 1_oddiy_sorovlar.sql
│   └── 2_murrakkab_sorovlar.sql
└── README.md
```

## Fayllar bilan ishlash
1. Avval katalogni yarating:
```bash
mkdir library_lab
cd library_lab
mkdir schema data queries
```

2. Database yaratish:
```bash
sqlite3 library.db
```

3. SQL fayllarni ishga tushirish:
```sql
.read schema/1_muallif.sql
.read schema/2_kitoblar.sql
-- va hokazo
```

## schema/1_authors.sql
```sql
-- Agar jadval mavjud bo'lsa o'chiramiz
DROP TABLE IF EXISTS muallif;

-- Mualliflar jadvali
CREATE TABLE muallif (
    id INTEGER,
    first_name TEXT NOT NULL,
    last_name TEXT NOT NULL,
    birth_year INTEGER,
    country TEXT,
    PRIMARY KEY (id)
);
```

## schema/2_books.sql
```sql
DROP TABLE IF EXISTS kitoblar;

CREATE TABLE kitoblar (
    id INTEGER,
    title TEXT NOT NULL,
    author_id INTEGER,
    published_year INTEGER,
    isbn TEXT UNIQUE,
    quantity INTEGER DEFAULT 1 CHECK(quantity > 0),
    PRIMARY KEY ("id"),
    FOREIGN KEY (author_id) REFERENCES authors(id)
);
```

## data/1_authors_data.sql
```sql
INSERT INTO muallif (first_name, last_name, birth_year, country) VALUES
('O''tkir', 'Hoshimov', 1941, 'Uzbekistan'),
('Tohir', 'Malik', 1946, 'Uzbekistan'),
('Ernest', 'Hemingway', 1899, 'USA');
```

## queries/1_basic_queries.sql
```sql
-- SQLite sozlamalari
.mode column
.headers on

-- Barcha mualliflarni ko'rish
SELECT * FROM muallif;

-- Barcha kitoblarni ko'rish
SELECT * FROM kitoblar;
```

## Laboratoriya topshiriqlari

1. Yuqoridagi struktura bo'yicha katalog va fayllarni yarating
2. Har bir `.sql` faylni to'ldiring:
   - schema/* fayllariga jadvallar yaratish kodlarini yozing
   - data/* fayllariga test ma'lumotlarni yozing
   - queries/* fayllariga so'rovlarni yozing

3. SQLite3 da fayllarni ketma-ketlikda ishga tushiring:
```sql
.read schema/1_authors.sql
.read schema/2_books.sql
.read schema/3_members.sql
.read schema/4_borrowings.sql

.read data/1_authors_data.sql
.read data/2_books_data.sql
.read data/3_members_data.sql

.read queries/1_basic_queries.sql
```

## Qo'shimcha vazifalar
1. Barcha jadvallarni o'chirish uchun `drop_tables.sql` yarating
2. Test ma'lumotlarni ko'proq qo'shing
3. Yangi so'rovlar yozing:
   - Muallif bo'yicha kitoblarni qidirish
   - Kitob olgan/olmagan a'zolarni aniqlash
   - Qaytarish muddati o'tgan kitoblarni aniqlash

## Foydali buyruqlar
- `.tables` - barcha jadvallarni ko'rish
- `.schema table_name` - jadval strukturasini ko'rish
- `.read filename.sql` - SQL faylni ishga tushirish
- `.quit` - SQLite3 dan chiqish

## Eslatmalar
- Har bir fayl faqat bitta vazifani bajarishi kerak
- Fayllar nomida raqamlar ketma-ketlikni bildiradi
- SQL fayllarni matn muharriri (Notepad++, VSCode, ...) da tahrirlash mumkin
- Har bir SQL buyruq nuqta-vergul (;) bilan tugashi kerak

Omad! 🚀
