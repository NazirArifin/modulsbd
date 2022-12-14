# Modul 5 - Query

Tujuan Pembelajaran: Mahasiswa dapat memahami konsep query dan dapat membuat query sederhana dan kompleks.

## Materi

![](https://preview.redd.it/423ha0w8lq181.png?width=640&crop=smart&auto=webp&s=51303b9336749de18dbf5663e3f76fc31d8c9de6)

### SELECT Query

- Query adalah sebuah perintah yang digunakan untuk mengambil data dari database. Query dapat berupa perintah untuk mengambil data, mengubah data, menghapus data, dan sebagainya. SELECT query adalah perintah untuk mengambil data dari database. Perintah SELECT query terdiri dari dua bagian, yaitu:

  * SELECT Clause
  * FROM Clause

```sql
SELECT column_name(s) FROM table_name;
```

Contoh:

```sql
SELECT * FROM customers;

--- atau ---
SELECT customerName, contactName, address FROM customers;
```

### SELECT DISTINCT

- Dalam tabel, sebuah kolom dapat memiliki data yang sama. Misalnya, tabel customers memiliki kolom country. Kolom country memiliki data yang sama, yaitu USA. SELECT DISTINCT adalah perintah untuk mengambil data yang unik saja. Perintah ini digunakan untuk menghilangkan data yang duplikat.

```sql
SELECT DISTINCT country FROM customers;
```

### WHERE Clause

- WHERE Clause adalah perintah untuk memfilter data yang diambil. WHERE Clause digunakan untuk menambahkan kondisi pada SELECT Clause. Perintah WHERE Clause terdiri dari dua bagian, yaitu:

  * Operator __(>, <, =, >=, <=, !=, LIKE, IN, BETWEEN, IS NULL, IS NOT NULL, AND, OR, NOT)__
  * Operator Value (Nilai yang akan dibandingkan dengan nilai pada kolom)

```sql
SELECT * FROM customers WHERE country = 'USA';

--- atau ---

SELECT * FROM customers WHERE customeId = 1;
```

- SQL membutuhkan tanda kutip untuk membedakan antara nama kolom dan nilai. Jika nilai adalah string, maka tanda kutip harus berupa tanda kutip tunggal. Jika nilai adalah angka, tidak perlu menggunakan tanda kutip.

### AND, OR, NOT

- AND, OR, dan NOT adalah operator logika yang digunakan untuk menggabungkan dua atau lebih kondisi.

```sql
SELECT * FROM customers WHERE country = 'USA' AND city = 'New York';

--- atau ---

SELECT * FROM customers WHERE city = 'New York' OR city = 'London';
```

- NOT digunakan untuk membalikkan kondisi.

```sql
SELECT * FROM customers WHERE NOT country = 'USA';
```

### ORDER BY

- ORDER BY adalah perintah untuk mengurutkan data yang diambil. ORDER BY digunakan untuk menambahkan kondisi pada SELECT Clause. Perintah ORDER BY terdiri dari dua bagian, yaitu:

  * ORDER BY Clause
  * ASC atau DESC

```sql
SELECT * FROM customers ORDER BY country ASC;

--- atau ---
SELECT * FROM customers ORDER BY country DESC;
```

- ASC adalah perintah untuk mengurutkan data dari nilai terkecil ke terbesar. DESC adalah perintah untuk mengurutkan data dari nilai terbesar ke terkecil. Order juga bisa menggunakan lebih dari satu kolom.

```sql
SELECT * FROM customers ORDER BY country ASC, city DESC;
```

### LIMIT dan OFFSET

- LIMIT dan OFFSET adalah perintah untuk membatasi jumlah data yang diambil. LIMIT digunakan untuk menentukan jumlah data yang diambil. OFFSET digunakan untuk menentukan jumlah data yang dilewati.

```sql
SELECT * FROM customers LIMIT 5;

--- atau ---

SELECT * FROM customers LIMIT 5 OFFSET 5;

--- atau menggabungkan ---

SELECT * FROM customers LIMIT 5, 5;
```

### MIN, MAX, AVG, SUM, COUNT

- MIN, MAX, AVG, SUM, dan COUNT adalah perintah untuk mengambil nilai tertentu dari data yang diambil. Perintah ini digunakan untuk menambahkan kondisi pada SELECT Clause.

```sql
SELECT MIN(price) FROM products;

--- atau ---
SELECT MAX(price) FROM products;

--- atau ---
SELECT AVG(price) FROM products;

--- atau ---
SELECT SUM(price) FROM products;

--- atau ---
SELECT COUNT(price) FROM products;
```

- COUNT digunakan untuk menghitung jumlah data yang sesuai dengan kondisi.

### LIKE

- LIKE adalah operator untuk membandingkan nilai dengan pola tertentu. LIKE digunakan untuk menambahkan kondisi pada SELECT Clause. Perintah LIKE terdiri dari dua bagian, yaitu:

  * Operator LIKE
  * Operator Value (Nilai yang akan dibandingkan dengan nilai pada kolom)

```sql
SELECT * FROM customers WHERE country LIKE 'U%';

--- atau ---

SELECT * FROM customers WHERE country LIKE '%a';

--- atau ---

SELECT * FROM customers WHERE country LIKE '%a%';

--- atau ---

SELECT * FROM customers WHERE country LIKE '_S%';

--- atau ---

SELECT * FROM customers WHERE country LIKE '[US]%';
```

  - `%` adalah wildcard yang digunakan untuk mencocokkan satu atau lebih karakter di mana saja. 
  - `_` digunakan untuk mencocokkan satu karakter.
  - `[]` digunakan untuk mencocokkan satu karakter dari beberapa karakter yang ditentukan. Contoh: `[US]` akan mencocokkan karakter U atau S.

### IN

- IN adalah operator untuk membandingkan nilai dengan beberapa nilai yang ditentukan. IN digunakan untuk menambahkan kondisi pada SELECT Clause. Perintah IN terdiri dari dua bagian, yaitu:

  * Operator IN
  * Operator Value (Nilai yang akan dibandingkan dengan nilai pada kolom)

```sql
SELECT * FROM customers WHERE country IN ('USA', 'UK', 'Canada');

--- atau ---
SELECT * FROM customers WHERE country IN ('USA', 'UK', 'Canada') AND city IN ('New York', 'London');
```

- Value dari IN bisa menggunakan SELECT Statement.

```sql
SELECT * FROM customers WHERE country IN (SELECT country FROM customers WHERE city = 'New York');
```

### BETWEEN

- BETWEEN adalah operator untuk membandingkan nilai dengan rentang nilai tertentu. BETWEEN digunakan untuk menambahkan kondisi pada SELECT Clause. Perintah BETWEEN terdiri dari dua bagian, yaitu:

  * Operator BETWEEN
  * Operator Value (Nilai yang akan dibandingkan dengan nilai pada kolom)

```sql
SELECT * FROM customers WHERE age BETWEEN 20 AND 30;
```

- BETWEEN juga bisa digunakan untuk membandingkan tanggal.

```sql
SELECT * FROM customers WHERE date BETWEEN '2019-01-01' AND '2019-12-31';
```

### ALIAS

- ALIAS adalah perintah untuk memberi nama alias pada tabel atau kolom. ALIAS digunakan untuk menambahkan kondisi pada SELECT Clause. Perintah ALIAS terdiri dari dua bagian, yaitu:

  * AS
  * Alias Name

```sql
SELECT COUNT(*) AS total_customers FROM customers;

--- atau ---

SELECT customer_city AS city, COUNT(*) AS total_customers FROM customers;

--- atau ---

SELECT c.name, c.city FROM customers AS c;

--- atau ---

SELECT c.name AS customer_name, c.city AS customer_city FROM customers AS c;
```


### IS NULL dan IS NOT NULL

- IS NULL dan IS NOT NULL adalah operator untuk membandingkan nilai dengan NULL. IS NULL digunakan untuk menambahkan kondisi pada SELECT Clause. Perintah IS NULL terdiri dari dua bagian, yaitu:

  * Operator IS NULL
  * Operator Value (Nilai yang akan dibandingkan dengan nilai pada kolom)

```sql
SELECT * FROM customers WHERE age IS NULL;

--- atau ---

SELECT * FROM customers WHERE age IS NOT NULL;
```

### GROUP BY & HAVING

- GROUP BY adalah perintah untuk mengelompokkan data yang diambil. GROUP BY digunakan untuk menambahkan kondisi pada SELECT Clause. Data yang diambil akan diurutkan berdasarkan kolom yang ditentukan dan data yang muncul hanya satu. Perintah GROUP BY terdiri dari dua bagian, yaitu:

  * GROUP BY Clause
  * HAVING Clause

```sql
SELECT country, COUNT(*) AS total_customers FROM customers GROUP BY country;
```

- HAVING digunakan untuk menambahkan kondisi pada GROUP BY Clause.

```sql
SELECT country, COUNT(*) AS total_customers FROM customers GROUP BY country HAVING COUNT(*) > 5;
```

### UNION

- UNION adalah perintah untuk menggabungkan hasil dari dua atau lebih SELECT Statement. UNION digunakan untuk menambahkan kondisi pada SELECT Clause. Jumlah kolom pada SELECT Statement yang digabungkan harus sama. Perintah UNION terdiri dari dua bagian, yaitu:

  * UNION Clause
  * SELECT Statement

```sql
SELECT name, city FROM customers WHERE country = 'USA' UNION SELECT name, city FROM customers WHERE country = 'UK';
```

- UNION ALL digunakan untuk menggabungkan hasil dari dua atau lebih SELECT Statement tanpa menghapus data yang sama.

```sql
SELECT name, city FROM customers WHERE country = 'USA' UNION ALL SELECT name, city FROM customers WHERE country = 'UK';
```

### EXISTS

- EXISTS adalah operator untuk membandingkan nilai dengan nilai yang ada pada tabel lain. EXISTS digunakan untuk menambahkan kondisi pada SELECT Clause. Perintah EXISTS terdiri dari dua bagian, yaitu:

  * Operator EXISTS
  * SELECT Statement

```sql
SELECT * FROM customers WHERE EXISTS (SELECT * FROM orders WHERE customers.id = orders.customer_id);
```

- Perbedaan EXISTS dan IN adalah, EXISTS akan mengembalikan nilai TRUE jika SELECT Statement mengembalikan nilai, sedangkan IN akan mengembalikan nilai TRUE jika SELECT Statement mengembalikan nilai yang sama dengan nilai pada kolom.

### ANY, ALL

- ANY dan ALL adalah operator untuk membandingkan nilai dengan nilai yang ada pada tabel lain. ANY dan ALL digunakan untuk menambahkan kondisi pada SELECT Clause. Perintah ANY dan ALL terdiri dari dua bagian, yaitu:

  * Operator
  * SELECT Statement

```sql
SELECT * FROM customers WHERE age > ANY (SELECT age FROM customers WHERE country = 'USA');

--- atau ---

SELECT * FROM customers WHERE age > ALL (SELECT age FROM customers WHERE country = 'USA');
```

- Perbedaan ANY dan ALL adalah, ANY akan mengembalikan nilai TRUE jika SELECT Statement mengembalikan setidaknya satu nilai yang sama dengan nilai pada kolom, sedangkan ALL akan mengembalikan nilai TRUE jika SELECT Statement mengembalikan __semua__ nilai yang sama dengan nilai pada kolom.

### CASE

- CASE adalah perintah untuk membuat kondisi. CASE digunakan untuk menambahkan kondisi pada SELECT Clause. Perintah CASE terdiri dari dua bagian, yaitu:

  * CASE Clause
  * WHEN Clause

```sql
SELECT name, city, country, CASE WHEN country = 'USA' THEN 'American' ELSE 'Non American' END 
FROM customers;

--- atau ---

SELECT name, city, country, CASE WHEN country = 'USA' THEN 'American' WHEN country = 'UK' THEN 'British' ELSE 'Non American' END AS Nationality
FROM customers;
```

### OPERATOR

- Di SQL, terdapat beberapa operator yang dapat digunakan untuk melakukan operasi pada nilai. Operator terdiri dari operator aritmatika, operator logika, dan operator perbandingan.

#### OPERATOR ARITMATIKA

- Operator aritmatika adalah operator untuk melakukan operasi matematika pada nilai. Operator aritmatika digunakan untuk menambahkan kondisi pada SELECT Clause.

| Operator | Deskripsi |
| --- | --- |
| + | Penjumlahan |
| - | Pengurangan |
| * | Perkalian |
| / | Pembagian |
| % | Modulus |

```sql
SELECT name, age, age + 5 AS age_in_5_years FROM customers;
```

#### OPERATOR LOGIKA

- Operator logika adalah operator untuk melakukan operasi logika pada nilai. Operator logika digunakan untuk menambahkan kondisi pada SELECT Clause.

| Operator | Deskripsi |
| --- | --- |
| AND | Operator logika AND |
| OR | Operator logika OR |
| NOT | Operator logika NOT |

```sql
SELECT name, age, age + 5 AS age_in_5_years FROM customers WHERE age > 20 AND age < 30;
```

#### OPERATOR PERBANDINGAN

- Operator perbandingan adalah operator untuk membandingkan nilai. Operator perbandingan digunakan untuk menambahkan kondisi pada SELECT Clause.

| Operator | Deskripsi |
| --- | --- |
| = | Sama dengan |
| <> | Tidak sama dengan |
| != | Tidak sama dengan |
| > | Lebih besar dari |
| < | Lebih kecil dari |
| >= | Lebih besar dari atau sama dengan |
| <= | Lebih kecil dari atau sama dengan |
| BETWEEN | Nilai antara dua nilai |
| LIKE | Nilai yang mirip dengan nilai tertentu |
| IN | Nilai yang ada pada list |

```sql
SELECT name, age, age + 5 AS age_in_5_years FROM customers WHERE age BETWEEN 20 AND 30;
```

- Operator gabungan adalah operator untuk menggabungkan dua atau lebih nilai. Operator gabungan digunakan untuk menambahkan kondisi pada SELECT Clause.

| Operator | Deskripsi |
| --- | --- |
| CONCAT | Menggabungkan dua atau lebih nilai |
| || | Menggabungkan dua atau lebih nilai |

```sql
SELECT CONCAT(name, ' ', city) AS full_name FROM customers;

--- atau ---

SELECT name || ' ' || city AS full_name FROM customers;
```

### Built-in Function (Fungsi Bawaan) yang Umum

- Di SQL, terdapat beberapa fungsi bawaan yang dapat digunakan untuk melakukan operasi pada nilai. Fungsi bawaan terdiri dari fungsi matematika, fungsi string, dan fungsi tanggal.

#### Fungsi Matematika

| Fungsi | Deskripsi |
| --- | --- |
| ABS | Mengembalikan nilai absolut |
| CEIL | Mengembalikan nilai pembulatan ke atas |
| FLOOR | Mengembalikan nilai pembulatan ke bawah |
| ROUND | Mengembalikan nilai pembulatan |
| RAND | Mengembalikan nilai random |

```sql
SELECT name, age, ROUND(age / 2) AS age_in_5_years FROM customers;
```

#### Fungsi String

| Fungsi | Deskripsi |
| --- | --- |
| CONCAT | Menggabungkan dua atau lebih nilai |
| || | Menggabungkan dua atau lebih nilai |
| LENGTH | Mengembalikan panjang karakter |
| LOWER | Mengembalikan nilai huruf kecil |
| UPPER | Mengembalikan nilai huruf besar |
| SUBSTRING | Mengembalikan nilai substring |

```sql
SELECT name, SUBSTRING(name, 1, 3) AS first_3_letters FROM customers;
```

#### Fungsi Tanggal

| Fungsi | Deskripsi |
| --- | --- |
| NOW | Mengembalikan tanggal dan waktu saat ini |
| CURDATE | Mengembalikan tanggal saat ini |
| CURTIME | Mengembalikan waktu saat ini |
| YEAR | Mengembalikan tahun |
| MONTH | Mengembalikan bulan |
| DAY | Mengembalikan hari |
| HOUR | Mengembalikan jam |
| MINUTE | Mengembalikan menit |
| SECOND | Mengembalikan detik |
| DATE | Mengembalikan tanggal |
| TIME | Mengembalikan waktu |
| TIMESTAMP | Mengembalikan tanggal dan waktu |
| DATEDIFF | Mengembalikan selisih hari |
| DATE_ADD | Menambahkan tanggal |
| DATE_SUB | Mengurangi tanggal |
| DATE_FORMAT | Mengembalikan format tanggal |
| DAYNAME | Mengembalikan nama hari |
| DAYOFWEEK | Mengembalikan hari dalam bentuk angka |
| TO_CHAR | Mengembalikan format tanggal (YYYY/YYY/YY/RRRR/RR/MM/MON/MONTH/MI/DD/DY/HH/HH12/HH24/SS) |

```sql
SELECT name, CURDATE() AS today, CURTIME() AS now FROM customers;

--- atau ---

SELECT name, DATE_FORMAT(NOW(), '%d-%m-%Y') AS today, DATE_FORMAT(NOW(), '%H:%i:%s') AS now FROM customers;

--- atau ---

SELECT name, TO_CHAR(NOW(), 'DD-MM-YYYY') AS today, TO_CHAR(NOW(), 'HH24:MI:SS') AS now FROM customers;
```

## Praktikum

- Download dan import [database employee](./sql/employee.sql) yang akan digunakan pada praktikum ini ke MySQL Workbench. Jalankan query berikut untuk mengecek apakah database employee sudah terimport dengan benar.

```sql
SELECT * FROM employees;
```

- Berikutnya kerjakan soal-soal berikut:

1. Tampilkan semua salary (gaji) karyawan
  
```sql
SELECT salary FROM employees;
```

2. Tampilkan job_name (nama pekerjaan) yang unique (tidak ada yang sama)

```sql
SELECT DISTINCT job_name FROM employees;
```

3. Tampilkan dep_id (department id) yang unique dan job_name nya

```sql
SELECT DISTINCT dep_id, job_name FROM employees;
```

4. Tampilkan data karyawan yang memiliki dep_id (departemen) bukan 2001

5. Tampilkan data karyawan yang hire_date (tanggal bekerja) sebelum 2001

6. Tampilkan rata-rata gaji yang pekerjaannya adalah 'ANALYST'

7. Tampilkan karyawan yang memiliki gaji (salary) lebih terbesar nomor 2

8. Tampilkan karyawan yang commision (komisi) lebih dari gaji (salary) nya

9. Tampilkan karyawan yang salary (gaji) nya lebih dari 3000 setelah mendapatkan 25% peningkatan gaji

10. Tampilkan nama karyawan dan nama (manager_id) managernya menghasilkan string 'BLAZE bekerja untuk KAYLING' (gunakan fungsi CONCAT)

11. Tampilkan karyawan yang gaji (salary) nya kurang dari 3500

12. Tampilkan karyawan yang bergabung (hire_date) pada tahun 1991

13. Tampilkan karyawan yang tidak memiliki manager

14. Tampilkan karyawan yang menjadi manager

15. Tampilkan karyawan yang bergabung (hire_date) pada bulan APRIL

16. Tampilkan data karyawan yang bergabung (hire_date) pada bulan apapun tapi nama bulan harus memiliki huruf 'A' (gunakan fungsi TO_CHAR dan LIKE)

17. Tampilkan karyawan yang memiliki nama yang diakhiri huruf 'S' dan panjang karakternya 6

18. Tampilkan jumlah pegawai, rata-rata gaji di kelompokkan berdasarakan job_name dan dep_id

19. Tampilkan seluruh manager beserta jumlah karyawan yang bekerja di bawahnya. Hasil diurutkan berdasarkan manager_id

20. Tampilkan karyawan kecuali PRESIDENT dan MANAGER (gunakan fungsi NOT IN) urutkan berdasarkan salary (gaji) dari yang terbesar

## Tugas

Kerjakan minimal __50 soal__ yang ada di [https://www.w3resource.com/sql-exercises/employee-database-exercise/index.php](https://www.w3resource.com/sql-exercises/employee-database-exercise/index.php) dan belum dikerjakan di praktikum.



