# Modul 6 - SQL Join, Stored Procedure & Function

Tujuan Pembelajaran: Mahasiswa dapat memahami konsep join, view, stored procedure dan function dan dapat mengimplementasikannya dalam bahasa SQL.

## Materi

### JOIN

- Join adalah proses menggabungkan data dari dua atau lebih tabel berdasarkan kolom yang sama. Join dapat dilakukan dengan menggunakan keyword `JOIN`, `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, `FULL JOIN`, `CROSS JOIN`, `NATURAL JOIN`, `SELF JOIN`, `UNION`, `UNION ALL`, `INTERSECT`, `EXCEPT`. MySQl mendukung 5 jenis join, yaitu `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, dan `CROSS JOIN`.

#### INNER JOIN

- `JOIN` atau `INNER JOIN` menggabungkan dua tabel dengan menghasilkan baris yang memiliki nilai yang sama pada kolom yang sama di kedua tabel. `INNER JOIN` sama dengan `JOIN`. `INNER JOIN` adalah keyword yang lebih spesifik.

![inner join](https://www.w3schools.com/mysql/img_innerjoin.gif)

```sql
SELECT column_name(s)
FROM table1
INNER JOIN table2
ON table1.column_name = table2.column_name;
```

Contoh:

```sql
SELECT Orders.OrderID, Customers.CustomerName, Orders.OrderDate FROM Orders INNER JOIN Customers ON Orders.CustomerID=Customers.CustomerID;
```

-  `INNER JOIN` juga dapat dituliskan tanpa keyword `JOIN` dan `ON` yaitu dengan menuliskan hubungan antara tabel secara langsung.

```sql
SELECT Orders.OrderID, Customers.CustomerName, Orders.OrderDate FROM Orders, Customers WHERE Orders.CustomerID=Customers.CustomerID;
```

- `INNER JOIN` juga dapat digunakan untuk menggabungkan lebih dari dua tabel.

```sql
SELECT Orders.OrderID, Customers.CustomerName, Shippers.ShipperName FROM Orders INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID INNER JOIN Shippers ON Orders.ShipperID = Shippers.ShipperID;

--- atau tanpa keyword JOIN
SELECT Orders.OrderID, Customers.CustomerName, Shippers.ShipperName FROM Orders, Customers, Shippers WHERE Orders.CustomerID = Customers.CustomerID AND Orders.ShipperID = Shippers.ShipperID;
```

- Jika nama kolom yang sama ada di kedua tabel, maka kita harus menuliskan nama tabel sebelum nama kolom. Tapi jika nama kolom yang sama tidak ada di kedua tabel, maka kita tidak perlu menuliskan nama tabel sebelum nama kolom.

#### LEFT JOIN

- `LEFT JOIN` menggabungkan dua tabel dengan menghasilkan baris yang memiliki nilai yang sama pada kolom yang sama di kedua tabel dan baris yang hanya ada di tabel kiri. Jika tidak ada baris yang cocok, maka nilai dari kolom yang ada di tabel kanan akan bernilai `NULL`.

![left join](https://www.w3schools.com/mysql/img_leftjoin.gif)

```sql
SELECT column_name(s)
FROM table1
LEFT JOIN table2
ON table1.column_name = table2.column_name;
```

Contoh:

```sql
SELECT Orders.OrderID, Customers.CustomerName, Orders.OrderDate FROM Orders LEFT JOIN Customers ON Orders.CustomerID=Customers.CustomerID;
```

#### RIGHT JOIN

- `RIGHT JOIN` menggabungkan dua tabel dengan menghasilkan baris yang memiliki nilai yang sama pada kolom yang sama di kedua tabel dan baris yang hanya ada di tabel kanan.

![right join](https://www.w3schools.com/mysql/img_rightjoin.gif)

```sql
SELECT column_name(s)
FROM table1
RIGHT JOIN table2
ON table1.column_name = table2.column_name;
```

Contoh:

```sql
SELECT Orders.OrderID, Customers.CustomerName, Orders.OrderDate FROM Orders RIGHT JOIN Customers ON Orders.CustomerID=Customers.CustomerID;
```

- `RIGHT JOIN` juga dapat digunakan untuk menggabungkan lebih dari dua tabel. Jika ada baris yang tidak cocok, maka nilai dari kolom yang ada di tabel kiri akan bernilai `NULL`.

#### CROSS JOIN

- `CROSS JOIN` menggabungkan dua tabel dengan menghasilkan seluruh kemungkinan kombinasi baris dari kedua tabel.

![cross join](https://www.w3schools.com/mysql/img_crossjoin.png)

```sql
SELECT column_name(s)
FROM table1
CROSS JOIN table2;
```

Contoh:

```sql
SELECT Orders.OrderID, Customers.CustomerName, Orders.OrderDate FROM Orders CROSS JOIN Customers;
```

- `CROSS JOIN` tidak menggunakan keyword `ON` atau `WHERE` untuk menggabungkan dua tabel dan dapat menghasilkan data yang sangat banyak karena semua data di tabel kiri akan di gabungkan dengan semua data di tabel kanan meskipun tidak ada baris yang cocok.

- Jika kita menggunakan `WHERE` maka hasilnya akan sama dengan `INNER JOIN`.

```sql
SELECT Orders.OrderID, Customers.CustomerName, Orders.OrderDate FROM Orders CROSS JOIN Customers WHERE Orders.CustomerID=Customers.CustomerID;
```

#### SELF JOIN

- `SELF JOIN` menggabungkan satu tabel dengan dirinya sendiri. `SELF JOIN` digunakan untuk menggabungkan satu tabel dengan dirinya sendiri, misalnya kita ingin menggabungkan tabel `Customers` dengan dirinya sendiri untuk mencari pelanggan yang memiliki alamat yang sama.

```sql
SELECT A.CustomerName AS CustomerName1, B.CustomerName AS CustomerName2, A.City FROM Customers A, Customers B WHERE A.CustomerID <> B.CustomerID AND A.City = B.City ORDER BY A.City;
```

- `SELF JOIN` tidak menggunakan keyword `JOIN` dan `ON` untuk menggabungkan dua tabel tapi menggunakan `WHERE` untuk menggabungkan dua tabel.

## Variabel

- Kita dapat menggunakan variabel dalam query yang kita buat. Cara pembuatan variabel query `SELECT` adalah `@var_name := value` dimana variabel dapat digunakan di query selanjutnya (di `WHERE`, `INSERT`, dsb)

```sql
SELECT @id := cust_id, @name := cust_name FROM customers WHERE cust_id = 1001;
SELECT @max_limbs := MAX(num_limbs) FROM animals;
```

- Mengubah nilai variabel dapat dilakukan dengan menggunakan `SET`, `:=`, `=`, atau `INTO`

```sql
SET @id = 1001;
SET @id := 1001;
SET @id = @id + 1;
SELECT @id := cust_id, @name := cust_name FROM customers WHERE cust_id = 1001;
SELECT customer_id, name INTO @id, @name FROM customers WHERE cust_id = 1001;
```

## Stored Procedure

- `Stored Procedure` adalah sekumpulan perintah SQL yang disimpan di dalam database dan dapat dipanggil kapan saja. Pada umumnya `Stored Procedure` digunakan untuk mengerjakan tugas-tugas yang sering dilakukan dan membutuhkan waktu yang lama. `Stored Procedure` sangat berguna untuk mempercepat operasi database karena penggunaan cache. `Stored Procedure` akan menyimpan hasil dari perintah SQL yang sudah pernah dijalankan dan akan mengambil hasil dari cache ketika perintah SQL yang sama dijalankan kembali.

### Membuat Stored Procedure

- Untuk membuat `Stored Procedure` kita harus menggunakan keyword `CREATE PROCEDURE` dan menuliskan nama `Stored Procedure` yang akan kita buat.

```sql
DELIMITER $$
CREATE PROCEDURE sp_name([parameter, ...])
BEGIN
    -- perintah SQL
END$$
```
- `Stored Procedure` dapat memiliki parameter yang digunakan untuk mengirimkan data ke `Stored Procedure` ketika dipanggil. `DELIMITER` digunakan untuk mengubah delimiter dari `;` menjadi `$$` agar `Stored Procedure` dapat memiliki delimiter `;` di dalamnya. ___Jika menggunakan MySQL Workbench, maka `DELIMITER` tidak perlu ditulis karena otomatis ditambakan.___

- Di dalam `Stored Procedure`, kita juga dapat menggunakan variabel dengan keyword `DECLARE` dan menuliskan nama variabel, tipe data, dan nilai default dari variabel tersebut.

```sql
CREATE PROCEDURE sp_name()
BEGIN
    DECLARE variabel1 datatype DEFAULT value;
    DECLARE variabel2 datatype;
    
    SET @user := 123456;

    SET variabel1 = 10;
    SELECT value INTO variabel2 FROM table WHERE user_id = @user;
END
```

### Memanggil Stored Procedure

- Untuk memanggil `Stored Procedure` kita harus menggunakan keyword `CALL` dan menuliskan nama `Stored Procedure` yang akan kita panggil.

```sql
CALL sp_name();
-- atau prosedur dengan parameter
CALL sp_name(3, 'Hello');
```

### Struktur Kendali

- `Stored Procedure` dapat menggunakan struktur kendali seperti `IF`, `ELSE`, `WHILE`, `REPEAT`, `UNTIL`, `LOOP`, `CASE`, `LEAVE`, `ITERATE`, `RETURN`, `CONTINUE`, `GOTO`.

- Contoh `Stored Procedure` yang menggunakan struktur kendali `IF`, `ELSE` dan `WHILE`

```sql
CREATE PROCEDURE sp_name()
BEGIN
    DECLARE variabel1 datatype DEFAULT value;
    DECLARE variabel2 datatype;
    
    SET @user := 123456

    SET variabel1 = 10;
    SELECT value INTO variabel2 FROM table WHERE user_id = @user;

    IF variabel1 > 10 THEN
        SET variabel1 = 10;
    ELSE
        SET variabel1 = 0;
    END IF;

    WHILE variabel1 < 10 DO
        SET variabel1 = variabel1 + 1;
    END WHILE;
END
```

- Contoh `Stored Procedure` yang menggunakan struktur kendali `REPEAT`, `UNTIL`, `LOOP`, `CASE`, `LEAVE`, `ITERATE`, `RETURN`, `CONTINUE`, `GOTO`.

```sql
CREATE PROCEDURE sp_name()
BEGIN
    DECLARE variabel1 datatype DEFAULT value;
    DECLARE variabel2 datatype;
    
    SET @user := 123456

    SET variabel1 = 10;
    SELECT value INTO variabel2 FROM table WHERE user_id = @user;

    REPEAT
        SET variabel1 = variabel1 + 1;
    UNTIL variabel1 = 10
    END REPEAT;

    LOOP
        SET variabel1 = variabel1 + 1;
        IF variabel1 = 10 THEN
            LEAVE;
        END IF;
    END LOOP;

    CASE variabel1
        WHEN 10 THEN
            SET variabel1 = 10;
        WHEN 20 THEN
            SET variabel1 = 20;
        ELSE
            SET variabel1 = 0;
    END CASE;

    WHILE variabel1 < 10 DO
        SET variabel1 = variabel1 + 1;
        ITERATE;
    END WHILE;
END
```

- Kita juga bisa menggunakan function bawaan dari MySQL untuk mempermudah proses pengambilan data dari database menggunakan `IF()`, `CASE`, `WHILE()`, `REPEAT()`, `LOOP()`, `LEAVE()`, `ITERATE()`, `RETURN()`, `CONTINUE()`, `GOTO()`. Contoh `Stored Procedure` yang menggunakan function bawaan dari MySQL.

```sql
CREATE PROCEDURE sp_name()
BEGIN
    ...
    IF(variabel1 > 10, 10, 0);
    SELECT CASE variabel1  WHEN 10 THEN 10 WHEN 20 THEN 20 ELSE 0 END INTO variabel1;
    WHILE(variabel1 < 10, variabel1 = variabel1 + 1);
    REPEAT(variabel1 = variabel1 + 1) UNTIL variabel1 = 10;
    LOOP
        SET variabel1 = variabel1 + 1;
        IF variabel1 = 10 THEN
            LEAVE;
        END IF;
    END LOOP;
END
```

## Function

- `Function` adalah sekumpulan perintah SQL yang disimpan di dalam database dan dapat dipanggil kapan saja. `Function` dapat digunakan untuk mempercepat proses pengambilan data dari database. `Function` dapat mengembalikan nilai dan dapat digunakan di dalam `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `WHERE`, dsb.

### Membuat Function

- Untuk membuat `Function` kita harus menggunakan keyword `CREATE FUNCTION` dan menuliskan nama `Function` yang akan kita buat.

```sql
CREATE FUNCTION fn_name()
RETURNS datatype
BEGIN
    -- perintah SQL
    
    -- RETURN untuk mengembalikan nilai
    RETURN value;
END
```

- `Function` dapat memiliki parameter yang digunakan untuk mengirimkan data ke `Function` ketika dipanggil.

```sql
CREATE FUNCTION fn_name(parameter1 datatype, parameter2 datatype)
RETURNS datatype
BEGIN
    -- perintah SQL
END
```

- Sama dengan procudure, `Function` juga dapat menggunakan variabel dan cara pembuatannya adalah dengan menggunakan keyword `DECLARE` dan menuliskan nama variabel, tipe data, dan nilai default dari variabel tersebut. `Function` juga dapat menggunakan struktur kendali seperti `IF`, `ELSE`, `WHILE`, `REPEAT`, `UNTIL`, `LOOP`, `CASE`, `LEAVE`, `ITERATE`, `RETURN`, `CONTINUE`, `GOTO`.

### Memanggil Function

- Untuk memanggil `Function` kita harus menggunakan keyword `SELECT` dan menuliskan nama `Function` yang akan kita panggil.

```sql
SELECT fn_name();
-- atau
@variabel := fn_name();
-- atau
SELECT fn_name2(4) INTO @variabel, IF(fn_name2(4) > 10, 1, 0) AS variabel2;
```

## Praktikum

### Membuat Database

- Buatlah database dengan nama `blog` dan buatlah tabel `user` dengan struktur seperti berikut.

```sql
CREATE TABLE user (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(255) NOT NULL,
    email VARCHAR(255) NOT NULL,
    password VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

- Buatlah tabel `post` dengan struktur seperti berikut.

```sql
CREATE TABLE post (
    id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT NOT NULL,
    title VARCHAR(255) NOT NULL,
    content TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES user(id)
);
```

- Buatlah tabel `comment` dengan struktur seperti berikut.

```sql
CREATE TABLE comment (
    id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT NOT NULL,
    post_id INT NOT NULL,
    content TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES user(id),
    FOREIGN KEY (post_id) REFERENCES post(id)
);
```

### Stored Procedure

- Buatlah Stored Procedure untuk menambahkan data ke tabel `user` dengan nama `sp_add_user` dengan parameter `name`, `email`, dan `password`.     
  - Stored Procedure ini akan mengembalikan nilai id user terakhir yang ditambahkan jika berhasil dan `0` jika gagal. 
  - Stored Procedure ini juga akan mengecek apakah email sudah terdaftar atau belum. 
  - Jika email sudah terdaftar maka Stored Procedure ini akan mengembalikan nilai `2`. 
  - Stored Procedure ini juga akan mengecek apakah email dan password kosong atau tidak. 
  - Jika email dan password kosong maka Stored Procedure ini akan mengembalikan nilai `3`. 
  - Stored Procedure ini juga akan mengecek apakah email dan password lebih dari 255 karakter atau tidak. 
  - Jika email dan password lebih dari 255 karakter maka Stored Procedure ini akan mengembalikan nilai `4`. 

```sql
CREATE PROCEDURE `sp_add_user`(name VARCHAR(255), emailInput VARCHAR(255), password VARCHAR(255), OUT result INT)
BEGIN
    DECLARE result INT DEFAULT 0;
    DECLARE email_count INT DEFAULT 0;
    DECLARE email_length INT DEFAULT 0;
    DECLARE password_length INT DEFAULT 0;
    
    SELECT COUNT(*) INTO email_count FROM user WHERE email = emailInput;
    SELECT LENGTH(emailInput) INTO email_length;
    SELECT LENGTH(password) INTO password_length;
    
    IF email_count > 0 THEN
        SET result = 0;
    ELSEIF email_length = 0 OR password_length = 0 THEN
        SET result = 0;
    ELSEIF email_length > 255 OR password_length > 255 THEN
        SET result = 0;
    ELSE
        INSERT INTO user (name, email, password) VALUES (name, emailInput, password);
        SET result = LAST_INSERT_ID();
    END IF;
    
    SELECT result;
END
```

```sql
SET @a := 0;
CALL sp_add_user('noname', 'admin@localhost3', 'aaaaa', @a);
```

- Buatlah Stored Procedure untuk menghapus data `user` dengan parameter `id` dengan nama `sp_delete_user` dan mengembalikan nilai `1` jika berhasil dan `0` jika gagal. Pastikan data `user` yang akan dihapus tidak memiliki `post` atau `comment`. Jika memiliki `post` atau `comment` maka Stored Procedure akan menghapusnya terlebih dahulu.
- Buatlah Stored Procedure yang menghapus semua `post` yang `created_at` lebih dari 10 tahun yang lalu dan tidak memiliki `comment`. Jika memiliki `comment` maka Stored Procedure akan menghasilkan angka 2.
- Buatlah Stored Procedure yang menghapus semua `comment` yang `created_at` lebih dari 10 tahun yang lalu dan memiliki `post` yang `created_at` lebih dari 5 tahun yang lalu. Jika jumlah `comment` dari `post` tersebut lebih dari 10 penghapusan akan dibatalkan.
- Buatlah Stored Procedure yang menghapus semua `user` yang `created_at` lebih dari 3 tahun yang lalu dan tidak memiliki `post` atau `comment`. Pastikan bahwa nama `user` tidak mengandung kata `admin` atau `administrator`

### Function

- Buatlah Function untuk mengecek apakah email sudah terdaftar atau belum dengan nama `fn_check_email` dengan parameter `email`.

```sql
CREATE FUNCTION fn_check_email(email VARCHAR(255))
RETURNS INT
BEGIN
    DECLARE email_count INT DEFAULT 0;
    
    SELECT COUNT(*) INTO email_count FROM user WHERE email = email;
    
    RETURN email_count;
END
```

- Buatlah function yang mengembalikan jumlah `post` yang dibuat oleh user dengan nama `fn_count_post` dengan parameter `user_id`.
- Buatlah function yang mengembalikan jumlah `comment` yang dibuat oleh user dengan nama `fn_count_comment` dengan parameter `user_id`.
- Buatlah function yang mengembalikan jumlah `comment` dari `post` dengan nama `fn_count_comment_post` dengan parameter `post_id`.
- Buatlah function yang mengembalikan data `user` yang memiliki jumlah `post` terbanyak dengan nama `fn_user_most_post`.
- Buatlah function yang mengembalikan data `user` yang memiliki jumlah `comment` terbanyak dengan nama `fn_user_most_comment`.
- Buatlah function yang mengembalikan data `post` yang memiliki jumlah `comment` terbanyak dengan nama `fn_post_most_comment`.
- Buatlah function yang mengembalikan data `user` yang paling banyak memberi `comment` terhadap `post` yang dibuat oleh `user` itu sendiri dengan nama `fn_user_comment_self_post`, dengan parameter `user_id`.
- Buatlah function yang menghasilkan kata terbanyak dari kolom `title` table `post`. Kata yang dihasilkan harus berupa huruf kecil, tidak mengandung tanda baca, dan panjang kata minimal 3 karakter. Kata tidak boleh mengandung kata hubung seperti `dan`, `atau`, `yang`, `tidak`, dsb.

## Tugas

- Tidak ada tugas untuk materi ini. Sampai jumpa di Ujian Akhir Semester! :D















