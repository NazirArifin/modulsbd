# Modul 3 - DDL (Data Definition Language)

Tujuan Pembelajaran: Mahasiswa dapat memahami dan menerapkan konsep DDL dan DML dalam pengembangan aplikasi berbasis database.

## Materi

![image](https://www.w3schools.in/wp-content/uploads/2014/08/SQL-Commands-1-700x470.png?ezimgfmt=ng%3Awebp%2Fngcb21%2Frs%3Adevice%2Frscb21-1)

### DDL (Data Definition Language)

DDL adalah bahasa yang digunakan untuk mendefinisikan struktur database. Dengan menggunakan DDL, kita dapat membuat database, tabel, kolom, indeks, dan lain-lain. Beberapa perintah DDL yang umum digunakan adalah:

  * CREATE
  * ALTER
  * DROP
  * TRUNCATE
  * COMMENT
  * RENAME

#### DDL DATABASE

* Untuk membuat database, kita dapat menggunakan perintah CREATE DATABASE. Kode SQL berikut akan membuat database baru dengan nama database_name dan menggunakan karakter set utf8 dan collation utf8_general_ci.

```sql
CREATE DATABASE database_name CHARACTER SET utf8 COLLATE utf8_general_ci;
```

* Untuk mengubah database, kita dapat menggunakan perintah ALTER DATABASE. Kode SQL berikut akan mengubah nama database database_name menjadi new_database_name.

```sql
ALTER DATABASE database_name RENAME TO new_database_name;

--- mengubah karakter set dan collation
ALTER DATABASE database_name CHARACTER SET utf8 COLLATE utf8_general_ci;
```

* Untuk menghapus database, kita dapat menggunakan perintah DROP DATABASE.

```sql
DROP DATABASE database_name;
```

#### DDL TABLE

* Untuk membuat tabel, kita dapat menggunakan perintah `CREATE TABLE`. Kode SQL berikut akan membuat tabel baru dengan nama `table_name` dan memiliki beberapa kolom dimana `column1` adalah primary key dan `column4` adalah foreign key.

```sql
CREATE TABLE table_name (
  column1 datatype PRIMARY KEY,
  column2 datatype NOT NULL,
  column3 datatype,
  column4 datatype REFERENCES table_name(column_name)
);
```

* `column_name` adalah nama kolom yang akan digunakan untuk kolom tersebut.
* `datatype` adalah tipe data yang akan digunakan untuk kolom tersebut seperti VARCHAR, INT, DATE, dan lain-lain.

* Untuk mengubah tabel, kita dapat menggunakan perintah ALTER TABLE. Kode SQL berikut akan menambahkan kolom baru ke tabel table_name.

```sql
ALTER TABLE table_name ADD column_name datatype NOT NULL AFTER column_name;
```

* `ALTER TABLE` juga dapat digunakan untuk mengubah nama kolom, menghapus kolom, mengubah tipe data kolom, mengubah nama tabel, menentukan kolom sebagai primary key, menerapkan foreign key, dan lain-lain.

```sql
ALTER TABLE table_name CHANGE column_name new_column_name datatype NOT NULL;

--- menambahkan primary key
ALTER TABLE table_name ADD CONSTRAINT constraint_name PRIMARY KEY (column_name);

--- menambahkan foreign key
ALTER TABLE table_name ADD CONSTRAINT constraint_name FOREIGN KEY (column_name) REFERENCES table_name(column_name);
```

* Untuk menghapus constraint, kita dapat menggunakan perintah ALTER TABLE.

```sql
ALTER TABLE table_name DROP CONSTRAINT constraint_name;
```

* Untuk menghapus tabel, kita dapat menggunakan perintah DROP TABLE.

```sql
DROP TABLE table_name;
```

* Untuk menghapus semua data dari tabel, kita dapat menggunakan perintah TRUNCATE TABLE.

```sql
TRUNCATE TABLE table_name;
```

* Untuk menambahkan komentar pada tabel, kita dapat menggunakan perintah COMMENT.

```sql
COMMENT ON TABLE table_name IS 'comment';
```

#### DDL INDEX

* Indeks adalah sebuah struktur data yang digunakan untuk mempercepat pencarian data. Indeks dapat digunakan untuk kolom yang memiliki banyak data dan sering digunakan untuk pencarian data. Mengupdate table yang memiliki indeks akan memakan waktu yang lebih lama karena indeks harus diupdate juga. Jadi, buat indeks hanya untuk kolom yang sering digunakan untuk pencarian data.

* Untuk membuat indeks, kita dapat menggunakan perintah CREATE INDEX. Kode SQL berikut akan membuat indeks baru dengan nama index_name dan menggunakan kolom column_name.

```sql
CREATE INDEX index_name ON table_name(column_name);

--- membuat unique index
CREATE UNIQUE INDEX index_name ON table_name(column_name);

--- membuat index dengan kombinasi kolom
CREATE INDEX index_name ON table_name(column_name1, column_name2);
```

* Untuk menghapus indeks, kita dapat menggunakan perintah DROP INDEX.

```sql
DROP INDEX index_name ON table_name;
```

* Untuk menambahkan komentar pada indeks, kita dapat menggunakan perintah COMMENT.

```sql
COMMENT ON INDEX index_name ON table_name IS 'comment';
```

#### DDL VIEW

* View adalah sebuah virtual table yang dibuat dari query yang sudah ada. View berisi baris dan kolom seperti table biasa. Kolom di view dapat diambil dari satu atau lebih table. View dapat digunakan untuk membatasi hak akses pengguna terhadap data. View juga dapat digunakan untuk mempermudah penggunaan query yang kompleks.

* Untuk membuat view, kita dapat menggunakan perintah CREATE VIEW. Kode SQL berikut akan membuat view baru dengan nama view_name dan menggunakan query query_name.

```sql
CREATE VIEW view_name AS query_name
SELECT column_name(s)
FROM table_name
WHERE condition;

--- memanggil view
SELECT * FROM view_name;
```

* View dapat di update dan di delete seperti table biasa. Untuk mengupdate view digunakan CREATE OR REPLACE VIEW.

```sql
CREATE OR REPLACE VIEW view_name AS query_name
SELECT column_name(s)
FROM table_name
WHERE condition;
```

* Untuk menghapus view, kita dapat menggunakan perintah DROP VIEW.

```sql
DROP VIEW view_name;
```

* Untuk menambahkan komentar pada view, kita dapat menggunakan perintah COMMENT.

```sql
COMMENT ON VIEW view_name IS 'comment';
```

#### DDL TRIGGER

* Trigger adalah sebuah prosedur yang akan dijalankan secara otomatis ketika terjadi suatu event. Trigger dapat digunakan untuk memvalidasi data sebelum diinsert, diupdate, atau didelete. Trigger juga dapat digunakan untuk mengupdate data lain ketika data di table yang lain diupdate.

* Untuk membuat trigger, kita dapat menggunakan perintah CREATE TRIGGER. Kode SQL berikut akan membuat trigger baru dengan nama trigger_name dan akan dijalankan ketika terjadi event event_name.

```sql
CREATE TRIGGER trigger_name event_name ON table_name FOR EACH ROW trigger_body;
```

* `event_name` adalah event yang akan memicu trigger. Event yang dapat digunakan adalah INSERT, UPDATE, dan DELETE.
* `trigger_body` adalah kode SQL yang akan dijalankan ketika event terjadi.

* Contohnya adalah sebagai berikut.

```sql
CREATE TRIGGER agecheck BEFORE INSERT ON person FOR EACH ROW 
BEGIN 
  IF NEW.age < 0 THEN 
    NEW.age = 0;
  END IF; 
END;

--- memanggil trigger
INSERT INTO person (name, age) VALUES ('John', -1);
```

* Trigger dapat di update dan di delete seperti table biasa. Untuk mengupdate trigger digunakan CREATE OR REPLACE TRIGGER. Mengupdate trigger akan menghapus trigger lama dan membuat trigger baru.

```sql
CREATE OR REPLACE TRIGGER trigger_name event_name ON table_name FOR EACH ROW trigger_body;
```

* Selain itu, kita juga dapat menggunakan perintah ALTER TRIGGER untuk mengupdate trigger.

```sql
ALTER TRIGGER trigger_name event_name ON table_name FOR EACH ROW trigger_body;
```

* Untuk menghapus trigger, kita dapat menggunakan perintah DROP TRIGGER.

```sql
DROP TRIGGER trigger_name;
```

* Untuk menambahkan komentar pada trigger, kita dapat menggunakan perintah COMMENT.

```sql
COMMENT ON TRIGGER trigger_name IS 'comment';
```

#### DDL STORED PROCEDURE

* Stored procedure adalah sebuah prosedur (subprogram) yang disimpan di database. Stored procedure dapat digunakan untuk mempermudah penggunaan query yang kompleks. Prosedur memungkinkan kita untuk mengelompokkan kode SQL menjadi satu unit yang dapat dipanggil kapan saja. Prosedur memiliki parameter yang dapat digunakan untuk mengirimkan data ke prosedur.

* Untuk membuat stored procedure, kita dapat menggunakan perintah CREATE PROCEDURE. Kode SQL berikut akan membuat stored procedure baru dengan nama procedure_name.

```sql
CREATE PROCEDURE procedure_name (parameter_name parameter_type)
BEGIN
  query;
END;
```

* `parameter_type` adalah tipe data dari parameter. Tipe data yang dapat digunakan adalah INT, VARCHAR, dan DATE.

* Contohnya adalah sebagai berikut.

```sql
--- set delimiter menjadi $$ untuk membuat stored procedure
DELIMITER $$
--- membuat stored procedure
CREATE PROCEDURE get_person (person_id INT)
BEGIN
  SELECT * FROM person WHERE id = person_id;
END;
$$
--- set delimiter menjadi ; untuk membuat query lain
DELIMITER ;

--- memanggil stored procedure
CALL get_person(1);
```

* Stored procedure dapat di update dan di delete seperti table biasa. Untuk mengupdate stored procedure digunakan CREATE OR REPLACE PROCEDURE.

```sql
CREATE OR REPLACE PROCEDURE procedure_name (parameter_name parameter_type)
BEGIN
  query;
END;
```

* Selain itu, kita juga dapat menggunakan perintah ALTER PROCEDURE untuk mengupdate stored procedure.

```sql
ALTER PROCEDURE procedure_name (parameter_name parameter_type)
BEGIN
  query;
END;
```

* Untuk menghapus stored procedure, kita dapat menggunakan perintah DROP PROCEDURE.

```sql
DROP PROCEDURE procedure_name;
```

* Untuk menambahkan komentar pada stored procedure, kita dapat menggunakan perintah COMMENT.

```sql
COMMENT ON PROCEDURE procedure_name IS 'comment';
```

#### DDL FUNCTION

* Stored function adalah sekumpulan kode SQL yang dapat digunakan untuk mengembalikan nilai. Sama seperti fungsi bahasa pemrograman, fungsi dapat menerima parameter dan mengembalikan nilai. Pemanggilannya dapat dilakukan dalam query.

* Untuk membuat stored function, kita dapat menggunakan perintah CREATE FUNCTION. Kode SQL berikut akan membuat stored function baru dengan nama function_name.

```sql
CREATE FUNCTION function_name (parameter_name parameter_type)
RETURNS return_type
BEGIN
  query;
END;
```

* `parameter_type` adalah tipe data dari parameter. Tipe data yang dapat digunakan adalah INT, VARCHAR, dan DATE.
* `return_type` adalah tipe data yang akan dikembalikan oleh fungsi.

* Contohnya adalah sebagai berikut.

```sql
--- set delimiter menjadi $$ untuk membuat stored function
DELIMITER $$
--- membuat stored function
CREATE FUNCTION get_person (person_id INT)
RETURNS VARCHAR(255)
BEGIN
  DECLARE person_name VARCHAR(255);
  SELECT name INTO person_name FROM person WHERE id = person_id;
  RETURN person_name;
END;
$$
--- set delimiter menjadi ; untuk membuat query lain
DELIMITER ;

--- memanggil stored function
SELECT get_person(1);
```

* Stored function dapat di update dan di delete seperti table biasa. Untuk mengupdate stored function digunakan CREATE OR REPLACE FUNCTION.

```sql
CREATE OR REPLACE FUNCTION function_name (parameter_name parameter_type)
RETURNS return_type
BEGIN
  query;
END;
```

* Selain itu, kita juga dapat menggunakan perintah ALTER FUNCTION untuk mengupdate stored function.

```sql
ALTER FUNCTION function_name (parameter_name parameter_type)
RETURNS return_type
BEGIN
  query;
END;
```

* Untuk menghapus stored function, kita dapat menggunakan perintah DROP FUNCTION.

```sql
DROP FUNCTION function_name;
```

* Untuk menambahkan komentar pada stored function, kita dapat menggunakan perintah COMMENT.

```sql
COMMENT ON FUNCTION function_name IS 'comment';
```

#### DDL EVENT

* Event adalah sebuah tugas yang akan dijalankan secara otomatis pada waktu tertentu. Event dapat digunakan untuk menjalankan query secara otomatis pada waktu tertentu. Event berisi kode SQL yang mana kode ini disimpan di database dan akan dijalankan secara otomatis pada waktu tertentu.

* Untuk membuat event, kita dapat menggunakan perintah CREATE EVENT. Kode SQL berikut akan membuat event baru dengan nama event_name.

```sql
CREATE EVENT event_name
ON SCHEDULE schedule
DO
  query;
```

* `schedule` adalah waktu event akan dijalankan. `schedule` dapat diatur dengan menggunakan beberapa parameter, yaitu:

  * `AT` digunakan untuk menjalankan event pada waktu tertentu. Contohnya adalah sebagai berikut.

    ```sql
    AT '2019-01-01 00:00:00'
    ```

  * `EVERY` digunakan untuk menjalankan event secara berulang. Contohnya adalah sebagai berikut.

    ```sql
    EVERY 1 DAY
    ```

  * `STARTS` digunakan untuk menentukan waktu mulai event. Contohnya adalah sebagai berikut.

    ```sql
    STARTS '2019-01-01 00:00:00'
    ```

  * `ENDS` digunakan untuk menentukan waktu berakhir event. Contohnya adalah sebagai berikut.

    ```sql
    ENDS '2019-01-01 00:00:00'
    ```

* Contohnya adalah sebagai berikut.

```sql
CREATE EVENT event_name ON SCHEDULE EVERY 1 DAY STARTS '2019-01-01 00:00:00' ENDS '2019-01-02 00:00:00' DO UPDATE person SET name = 'John Doe' WHERE id = 1;
```

* Event dapat di update dan di delete seperti table biasa. Untuk mengupdate event digunakan CREATE OR REPLACE EVENT.

```sql
CREATE OR REPLACE EVENT event_name ON SCHEDULE schedule DO query;
```

* Untuk menghapus event, kita dapat menggunakan perintah DROP EVENT.

```sql
DROP EVENT event_name;
```

* Untuk menambahkan komentar pada event, kita dapat menggunakan perintah COMMENT.

```sql
COMMENT ON EVENT event_name IS 'comment';
```

## Praktikum

- Dengan menggunakan MySQL Workbench, berdasarkan database yang telah dibuat pada praktikum sebelumnya (Tugas No. 1), silakan mencoba kegiatan berikut:

1. Menghapus primary key pada tabel mahasiswa.
2. Menambahkan kolom baru pada tabel mahasiswa dengan nama `JENIS_KELAMIN` dengan tipe data `ENUM` dan nilai `L` dan `P`.
3. Mengubah tipe data kolom `NIM` pada tabel mahasiswa menjadi `VARCHAR(10)`.
4. Mengubah nama kolom `EMAIL` menjadi `SUREL` pada tabel mahasiswa dan mengubah tipe data menjadi `VARCHAR(50)`.
5. Mengubah nama tabel `mahasiswa` menjadi `siswa`.
6. Menghapus tabel `siswa`.
7. Terserah kalian mau bikin apa... :D


## Tugas

- Dengan menggunakan MySQL Workbench, berdasarkan database yang telah dibuat pada praktikum sebelumnya (Tugas No. 2), silakan mencoba kegiatan berikut:

1. Hapus semua relasi pada tabel, ubah nama tabel `supplier` menjadi `penyedia`, `produk` menjadi `barang`, dan kemudian buat ulang relasi yang baru.
2. Buat stored procedure, stored function, dan event sederhana sesuai dengan keinginan kalian














