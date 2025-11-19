# סיכום SQL — כל הפקודות + דוגמאות + הסברים (Markdown)

## 1. פקודות מבנה בסיס נתונים (General Commands)

### **SHOW DATABASES**
```sql
SHOW DATABASES;
```
**הסבר:** מציג את כל מסדי הנתונים הקיימים בשרת.

### **USE**
```sql
USE mydb;
```
**הסבר:** מעבר למסד נתונים מסוים.

### **SHOW TABLES**
```sql
SHOW TABLES;
```
**הסבר:** מציג את כל הטבלאות במסד הנבחר.

### **DESCRIBE**
```sql
DESCRIBE students;
```
**הסבר:** מציג את מבנה הטבלה – שמות עמודות, טיפוסים ומאפיינים.

---

## 2. תנאים ב־SQL (WHERE)

### **= שווה**
```sql
SELECT * FROM customers WHERE country = 'USA';
```
**הסבר:** מחזיר רשומות בהן country שווה ל־USA.

### **LIKE — חיפוש טקסט**
```sql
SELECT * FROM products WHERE productName LIKE '%Ford%';
```
**הסבר:** מחפש טקסט שמכיל את המילה "Ford".

### **BETWEEN**
```sql
SELECT * FROM products WHERE buyPrice BETWEEN 30 AND 50;
```
**הסבר:** ערך בין 30 ל־50 כולל.

### **IN**
```sql
SELECT * FROM customers WHERE country IN ('USA','France','UK');
```
**הסבר:** בודק אם הערך נמצא ברשימת ערכים.

### **IS NULL**
```sql
SELECT * FROM orders WHERE shippedDate IS NULL;
```
**הסבר:** מחזיר רק רשומות עם ערך NULL.

---

## 3. פונקציות אגרגציה (COUNT / SUM / AVG / MIN / MAX)

### **COUNT**
```sql
SELECT COUNT(*) FROM products;
```
**הסבר:** סופר כמות שורות.

### **SUM**
```sql
SELECT SUM(amount) FROM payments;
```
**הסבר:** סכום כל הערכים בעמודה.

### **AVG**
```sql
SELECT AVG(buyPrice) FROM products;
```
**הסבר:** ממוצע הערכים.

### **GROUP BY**
```sql
SELECT country, COUNT(*) 
FROM customers
GROUP BY country;
```
**הסבר:** קיבוץ נתונים לפי עמודה.

### **HAVING**  
```sql
SELECT country, COUNT(*) 
FROM customers
GROUP BY country
HAVING COUNT(*) > 5;
```
**הסבר:** פילטור אחרי GROUP BY.

---

## 4. DDL — יצירת מבנים (CREATE / ALTER / DROP)

### **CREATE DATABASE**
```sql
CREATE DATABASE school;
```
**הסבר:** יצירת מסד נתונים חדש.

### **CREATE TABLE**
```sql
CREATE TABLE students (
  id INT PRIMARY KEY AUTO_INCREMENT,
  name VARCHAR(50),
  age INT
);
```
**הסבר:** יצירת טבלה עם שדות, טיפוסים ומפתח ראשי.

### **ALTER TABLE — הוספת עמודה**
```sql
ALTER TABLE students ADD COLUMN phone VARCHAR(20);
```
**הסבר:** מוסיף עמודה חדשה לטבלה.

### **ALTER TABLE — שינוי שם**
```sql
ALTER TABLE students CHANGE name full_name VARCHAR(50);
```
**הסבר:** שינוי שם עמודה.

### **DROP TABLE**
```sql
DROP TABLE students;
```
**הסבר:** מוחק את הטבלה לצמיתות.

### **TRUNCATE**
```sql
TRUNCATE TABLE students;
```
**הסבר:** מוחק את כל הנתונים ומשאיר את המבנה.

---

## 5. CRUD — יצירה / קריאה / עדכון / מחיקה

### **INSERT**
```sql
INSERT INTO students (name, age) VALUES ('Dan', 22);
```
**הסבר:** יצירת שורה חדשה.

### **SELECT**
```sql
SELECT name, age FROM students;
```
**הסבר:** שליפת נתונים.

### **UPDATE**
```sql
UPDATE students SET age = 25 WHERE id = 1;
```
**הסבר:** עדכון ערכים קיימים.

### **DELETE**
```sql
DELETE FROM students WHERE id = 1;
```
**הסבר:** מחיקת שורות ספציפיות.

---

## 6. קשרים בין טבלאות (Relationships)

### **1:Many — מפתח זר**
```sql
CREATE TABLE students (
  id INT PRIMARY KEY,
  class_id INT,
  FOREIGN KEY (class_id) REFERENCES classes(id)
);
```
**הסבר:** לכל כיתה יש הרבה תלמידים.

### **1:1 — קשר יחיד**
```sql
CREATE TABLE teacher_contracts (
  teacher_id INT UNIQUE,
  FOREIGN KEY (teacher_id) REFERENCES teachers(id)
);
```
**הסבר:** לכל מורה יש חוזה יחיד.

### **Many-to-Many — טבלת גישור**
```sql
CREATE TABLE student_assignments (
  student_id INT,
  assignment_id INT,
  PRIMARY KEY (student_id, assignment_id)
);
```
**הסבר:** תלמידים ↔ משימות (שני הצדדים רבים).

---

## 7. JOINS — שילוב טבלאות

### **INNER JOIN**
```sql
SELECT s.name, c.class_name
FROM students s
INNER JOIN classes c ON s.class_id = c.id;
```
**הסבר:** מחזיר רק רשומות שיש להן התאמה בשתי הטבלאות.

### **LEFT JOIN**
```sql
SELECT s.name, c.class_name
FROM students s
LEFT JOIN classes c ON s.class_id = c.id;
```
**הסבר:** כל התלמידים + כיתה אם קיימת (אחרת NULL).

### **RIGHT JOIN**
```sql
SELECT s.name, c.class_name
FROM students s
RIGHT JOIN classes c ON s.class_id = c.id;
```
**הסבר:** כל הכיתות + תלמידים אם יש.

### **UNION**
```sql
SELECT name FROM students
UNION
SELECT name FROM teachers;
```
**הסבר:** מאחד שתי תוצאות בלי כפילויות.

---

# ✔️ הסיכום מוכן — Markdown מלא

