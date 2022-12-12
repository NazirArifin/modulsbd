# Modul 4 - DML (Data Manipulation Language)

Tujuan Pembelajaran: Mahasiswa dapat memahami dan menerapkan DML (Data Manipulation Language) dalam pengolahan data.

## Materi

![](https://ih1.redbubble.net/image.1611596569.2539/ssrco,classic_tee,mens,101010:01c5ca27c6,front_alt,square_product,600x600.u4.jpg)

### DML (Data Manipulation Language)

DML adalah bahasa yang digunakan untuk memanipulasi data dalam database. DML digunakan untuk memasukkan, mengubah, dan menghapus data dari database. Beberapa perintah DML yang umum digunakan adalah:

  * INSERT
  * UPDATE
  * DELETE
  * REPLACE
  * MERGE

#### INSERT

* Perintah INSERT digunakan untuk memasukkan data ke dalam tabel. Perintah INSERT memiliki sintaks sebagai berikut:

```sql
INSERT INTO nama_tabel (kolom1, kolom2, kolom3, ...) VALUES (nilai1, nilai2, nilai3, ...);`
```

* Bisa juga menggunakan perintah INSERT tanpa menuliskan nama kolom. Perintah INSERT tanpa menuliskan nama kolom memiliki sintaks sebagai berikut:

```sql
INSERT INTO nama_tabel VALUES (nilai1, nilai2, nilai3, ...);
```

* Bagian VALUES dapat diisi dengan beberapa nilai. Contoh:

```sql
INSERT INTO mahasiswa VALUES 
('1234567890', 'Nazir', 'Jl. Jendral Sudirman'),
('1234567891', 'Arifin', 'Jl. Jendral Sudirman');
```

* Perintah INSERT juga dapat digunakan untuk memasukkan data dari tabel lain. Perintah INSERT untuk memasukkan data dari tabel lain memiliki sintaks sebagai berikut:

```sql
INSERT INTO nama_tabel (kolom1, kolom2, kolom3, ...) SELECT kolom1, kolom2, kolom3, ... FROM nama_tabel;
```

* Perintah INSERT dapat juga menggunakan SET untuk memasukkan data ke dalam tabel. Perintah INSERT dengan SET memiliki sintaks sebagai berikut:

```sql
INSERT INTO nama_tabel SET kolom1 = nilai1, kolom2 = nilai2, kolom3 = nilai3, ...;
```

* INSERT dengan ON DUPLICATE KEY UPDATE akan memasukkan data ke dalam tabel jika data tersebut belum ada. Jika data sudah ada, maka data tersebut akan diupdate. Perintah INSERT dengan ON DUPLICATE KEY UPDATE memiliki sintaks sebagai berikut:

```sql
INSERT INTO nama_tabel (kolom1, kolom2, kolom3, ...) VALUES (nilai1, nilai2, nilai3, ...) ON DUPLICATE KEY UPDATE kolom1 = nilai1, kolom2 = nilai2, kolom3 = nilai3, ...;
```

* INSERT dengan IGNORE akan memasukkan data ke dalam tabel jika data tersebut belum ada. Jika data sudah ada, maka data tersebut akan diabaikan. Perintah INSERT dengan IGNORE memiliki sintaks sebagai berikut:

```sql
INSERT IGNORE INTO nama_tabel (kolom1, kolom2, kolom3, ...) VALUES (nilai1, nilai2, nilai3, ...);
```

* Perintah INSERT ke tabel yang memiliki kolom AUTO_INCREMENT akan mengisi kolom tersebut dengan nilai yang otomatis. Hasil dari perintah INSERT ke tabel yang memiliki kolom AUTO_INCREMENT akan mengembalikan nilai AUTO_INCREMENT yang baru dapat diakses dengan menggunakan fungsi `LAST_INSERT_ID()`. Contoh:

```sql
INSERT INTO mahasiswa (nim, nama, alamat) VALUES ('1234567890', 'Nazir', 'Jl. Jendral Sudirman');
SELECT LAST_INSERT_ID();
```

#### UPDATE

* Perintah UPDATE digunakan untuk mengubah data yang sudah ada di dalam tabel. Perintah UPDATE memiliki sintaks sebagai berikut:

```sql
UPDATE nama_tabel SET kolom1 = nilai1, kolom2 = nilai2, kolom3 = nilai3, ... WHERE kondisi;
```

* Dengan kondisi tertentu, kita bisa menentukan data mana saja yang akan diubah. Contoh:

```sql
UPDATE mahasiswa SET alamat = 'Jl. Jendral Sudirman' WHERE nim = '1234567890';

--- beberapa baris data diubah
UPDATE mahasiswa SET alamat = 'Jl. Jendral Sudirman' WHERE nim = '1234567890' OR nim = '1234567891';

--- semua baris data diubah
UPDATE mahasiswa SET alamat = 'Jl. Jendral Sudirman';
```

* Kita bisa mengupdate data dari data yang sudah ada di dalam tabel. Perintah UPDATE untuk mengupdate data dari data yang sudah ada di dalam tabel memiliki sintaks sebagai berikut:

```sql
UPDATE t1 SET col1 = col1 + 1;
```

* Kita bisa mengupdate data dari data yang sudah ada di dalam tabel dengan menggunakan data dari tabel lain. Perintah UPDATE untuk mengupdate data dari data yang sudah ada di dalam tabel dengan menggunakan data dari tabel lain memiliki sintaks sebagai berikut:

```sql
UPDATE t1 SET col1 = (SELECT col1 FROM t2 WHERE t1.id = t2.id);
```

* Untuk mengupdate beberapa table sekaligus, dapat menggunakan sintaks sebagai berikut:

```sql
UPDATE items, month SET items.price=month.price WHERE items.id=month.id;
```

* Kita tidak bisa mengupdate dan select data dari tabel yang sama dalam satu perintah UPDATE. Hal ini dikarenakan tabel yang sama akan diupdate terlebih dahulu sebelum select data dari tabel yang sama.

#### DELETE

* Perintah DELETE digunakan untuk menghapus data yang sudah ada di dalam tabel. Perintah DELETE memiliki sintaks sebagai berikut:

```sql
DELETE FROM nama_tabel WHERE kondisi;
```

* Jika kita tidak menentukan kondisi, maka semua data di dalam tabel akan dihapus. Contoh:

```sql
DELETE FROM mahasiswa;
```

* Jika kita menentukan kondisi, maka data yang sesuai dengan kondisi yang ditentukan akan dihapus. Contoh:

```sql
DELETE FROM mahasiswa WHERE nim = '1234567890';
```

* Untuk mengosongkan isi table, Perintah `TRUNCATE` akan lebih cepat dari perintah `DELETE` karena perintah `TRUNCATE` tidak akan mengecek kondisi yang ditentukan.

* Kita tidak bisa menghapus dan select data dari tabel yang sama dalam satu perintah DELETE. Hal ini dikarenakan tabel yang sama akan dihapus terlebih dahulu sebelum select data dari tabel yang sama.

* Kita bisa menambahkan kondisi `LIMIT` dan `ORDER BY` untuk menentukan jumlah data yang akan dihapus. Contoh:

```sql
DELETE FROM mahasiswa ORDER BY nim LIMIT 1;
```

#### REPLACE

* Perintah REPLACE hampir sama dengan perintah INSERT. Perbedaannya adalah jika data yang akan diinsert sudah ada di dalam tabel, maka data tersebut akan diganti dengan data yang baru. Perintah REPLACE memiliki sintaks sebagai berikut:

```sql
REPLACE INTO nama_tabel (kolom1, kolom2, kolom3, ...) VALUES (nilai1, nilai2, nilai3, ...);
```

#### MERGE

* Perintah MERGE adalah perintah yang digunakan untuk mengupdate data pada tabel yang sudah ada dan menginsert data baru ke dalam tabel berdasarkan kondisi tertentu. Perintah ini berguna untuk mengupdate data yang sudah ada dan menginsert data baru ke dalam tabel dalam satu perintah. Perintah MERGE memiliki sintaks sebagai berikut:

```sql
MERGE INTO nama_tabel1 AS t1 USING nama_tabel2 AS t2 ON t1.kolom1 = t2.kolom1 WHEN MATCHED THEN UPDATE SET t1.kolom1 = t2.kolom1, t1.kolom2 = t2.kolom2 WHEN NOT MATCHED THEN INSERT (kolom1, kolom2) VALUES (nilai1, nilai2);
```

* Pertama kita tentukan tabel sumber dan tabel tujuan. Kemudian kita tentukan kondisi untuk mengupdate data yang sudah ada dan menginsert data baru ke dalam tabel. Setelah itu perintah ini menyediakan tiga kondisi yaitu: `WHEN MATCHED`, `WHEN NOT MATCHED BY SOURCE`, dan `WHEN NOT MATCHED BY TARGET`.

* Kondisi `WHEN MATCHED` digunakan untuk mengupdate data yang sudah ada di dalam tabel. Kondisi `WHEN NOT MATCHED BY SOURCE` digunakan untuk menginsert data baru ke dalam tabel. Kondisi `WHEN NOT MATCHED BY TARGET` digunakan untuk menghapus data yang sudah ada di dalam tabel.

* Contoh:

```sql
MERGE INTO mahasiswa AS t1 USING mahasiswa_baru AS t2 
ON t1.nim = t2.nim 
WHEN MATCHED THEN 
  UPDATE SET t1.nama = t2.nama, t1.alamat = t2.alamat 
WHEN NOT MATCHED BY SOURCE THEN 
  INSERT (nim, nama, alamat) VALUES (t2.nim, t2.nama, t2.alamat) 
WHEN NOT MATCHED BY TARGET THEN DELETE;
```

* Cara menggunakan perintah MERGE ini adalah dengan mengupdate data yang sudah ada di dalam tabel dan menginsert data baru ke dalam tabel. Jika data yang sudah ada di dalam tabel tidak ada di tabel sumber, maka data tersebut akan dihapus.

## Praktikum

- Buat tabel `mahasiswa` dan `matakuliah` dengan menggunakan perintah `CREATE TABLE`. 
- Insert data ke dalam tabel `mahasiswa` dan `matakuliah` dengan menggunakan perintah `INSERT`. 
- Update data yang sudah ada di dalam tabel `mahasiswa` dengan menggunakan perintah `UPDATE`. 
- Hapus data yang sudah ada di dalam tabel `mahasiswa` dengan menggunakan perintah `DELETE`. 
- Insert data ke dalam tabel `mahasiswa` dan `matakuliah` dengan menggunakan perintah `REPLACE`. 
- Update data yang sudah ada di dalam tabel `mahasiswa` dan menginsert data baru ke dalam tabel `mahasiswa` dengan menggunakan perintah `MERGE`.

## Tugas

- Buat database dengan nama `puskesmas` dengan isi tabel `pasien`, `dokter`, `pegawai`, `obat`, `transaksi` dan `periksa`.

- Buat tabel `pasien` dengan kolom `id_pasien`, `nama`, `alamat`, `no_telp`, `jenis_kelamin`, `tgl_lahir`, `gol_darah`, `pekerjaan`,  `tgl_daftar`.

- Buat tabel `dokter` dengan kolom `id_dokter`, `nama`, `alamat`, `no_telp`, `jenis_kelamin`, `tgl_lahir`, `gol_darah`, `spesialis` varchar(50), `email`.

- Buat tabel `pegawai` dengan kolom `id_pegawai`, `nama`, `alamat`, `no_telp`, `jenis_kelamin`, `tgl_lahir`, `gol_darah`, `jabatan`, `email`.

- Buat tabel `obat` dengan kolom `id_obat`, `nama_obat`, `jenis_obat`, `tgl_kadaluarsa`, `harga`.

- Buat tabel `transaksi` dengan kolom `id_transaksi`, `id_pasien`, `id_dokter`, `id_pegawai`, `tgl_transaksi`, `total`.

- Buat tabel `periksa` dengan kolom `id_periksa`, `id_transaksi`, `hasil`

- Buat tabel `detil_transaksi` dengan kolom `id_detil`, `id_transaksi`, `id_obat`, `jumlah`, `subtotal`.

- Insert data ke dalam tabel `pasien`, `dokter`, `pegawai`, `obat`, `transaksi` dan `periksa` dengan menggunakan perintah `INSERT` minimal 10 data.

- Insert data ke tabel `dokter` dan `pegawai` dengan menggunakan perintah `REPLACE` minimal 5 data.

- Insert data ke tabel `obat` minimal 5 data.

- Update data yang sudah ada di dalam tabel `pasien` dengan menggunakan perintah `UPDATE` minimal 5 data.

- Update data yang sudah ada di dalam tabel `dokter` dan `pegawai` dengan menggunakan perintah `MERGE` minimal 5 data.









