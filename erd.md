# Modul 1 - EER (Enhanced Entity Relationship Diagram)

Tujuan Pembelajaran: Mahasiswa dapat memahami konsep ERM dan dapat membuat ERM sederhana.

## Materi

### ERM (Entity Relationship Modelling)

- ERM adalah pendekatan grafis untuk mendesain basis data. Dia merupakan model _high-level_ dari basis data yang akan dibuat yang mendefinisikan elemen data dan hubungannya. ERM terdiri dari 3 komponen utama, yaitu:

  * Entitas
  * Atribut
  * Relasi

![ERD](https://i.pinimg.com/originals/e9/bd/82/e9bd82cf92894a080eb23a15c246c52b.png)

- ERM dapat dibuat dengan menggunakan software ERM seperti MySQL Workbench, Oracle SQL Developer, dan lain-lain. Pada modul ini, kita akan menggunakan software MySQL Workbench yang dapat diunduh di [sini](https://dev.mysql.com/downloads/workbench/).

- ERM memiliki beberapa tingkat yaitu _Conceptual_, _Logical_, dan _Physical_. _Business Analyst_ menggunakan conceptual dan logical model untuk memodelkan data yang dibutuhkan dari perspektif bisnis. Sedangkan _Database Administrator_ menggunakan physical model untuk memodelkan data yang dibutuhkan dari perspektif teknis yang siap untuk diimplementasikan ke dalam database.

- Physical ERM merepresentasikan desain yang sebenarnya pada database relational. Dia menjelaskan bagaimana data harus dibentuk dan dihubungkan dalam database. Hal ini berarti tipe data yang akurat akan digunakan. Selain itu juga perlu ditambahkan primary key, foreign key, dan constraint. Pada praktikum ini, kita akan menggunakan physical ERM.

### Tipe Data

- Tipe data adalah kumpulan nilai yang memiliki karakteristik yang sama. Tipe data dapat digunakan untuk mendefinisikan kolom dalam tabel. Tipe data yang paling umum digunakan adalah:

  * `CHAR`
  * `VARCHAR`
  * `INT`
  * `TINYINT`
  * `SMALLINT`
  * `MEDIUMINT`
  * `BIGINT`
  * `FLOAT`
  * `DOUBLE`
  * `DATE`
  * `DATETIME`
  * `BLOB`
  * `TEXT`
  * `MEDIUMTEXT`
  * `LONGTEXT`
  * `BOOLEAN`
  * `ENUM`

- Tipe data `CHAR` digunakan untuk menyimpan data yang panjangnya tetap. Jika panjang data yang dimasukkan melebihi panjang yang ditentukan, maka data akan dipotong.
- Tipe data `VARCHAR` digunakan untuk menyimpan data yang panjangnya tidak tetap. Jika panjang data yang dimasukkan melebihi panjang yang ditentukan, maka data akan dipotong.
- Tipe data `TINYINT` digunakan untuk menyimpan data bilangan bulat dengan rentang nilai -128 sampai 127. 
- Tipe data `SMALLINT` digunakan untuk menyimpan data bilangan bulat dengan rentang nilai -32768 sampai 32767.
- Tipe data `MEDIUMINT` digunakan untuk menyimpan data bilangan bulat dengan rentang nilai -8388608 sampai 8388607.
- Tipe data `INT` digunakan untuk menyimpan data bilangan bulat dengan panjang 4 byte (32 bit) dan rentang nilai -2147483648 sampai 2147483647.
- Tipe data `BIGINT` digunakan untuk menyimpan data bilangan bulat dengan rentang nilai -9223372036854775808 sampai 9223372036854775807.
- Tipe data `FLOAT` digunakan untuk menyimpan data bilangan desimal.
- Tipe data `DOUBLE` digunakan untuk menyimpan data bilangan desimal dengan presisi yang lebih tinggi.
- Tipe data `DATE` digunakan untuk menyimpan data tanggal.
- Tipe data `DATETIME` digunakan untuk menyimpan data tanggal dan waktu.
- Tipe data `BLOB` digunakan untuk menyimpan data dalam bentuk binary large object.
- Tipe data `TEXT` digunakan untuk menyimpan data dalam bentuk teks.
- Tipe data `MEDIUMTEXT` digunakan untuk menyimpan data dalam bentuk teks dengan panjang maksimal 16 juta karakter.
- Tipe data `LONGTEXT` digunakan untuk menyimpan data dalam bentuk teks dengan panjang maksimal 4 miliar karakter.
- Tipe data `ENUM` digunakan untuk menyimpan data yang memiliki pilihan nilai yang terbatas.

### Primary Key

- Primary key adalah kolom yang unik dan tidak boleh ada yang sama. Primary key digunakan untuk mengidentifikasi setiap baris pada tabel. Primary key dapat terdiri dari satu kolom atau lebih. Jika terdiri dari lebih dari satu kolom, maka disebut _composite primary key_. Primary key dapat berupa kolom yang berisi angka, teks, atau kombinasi dari keduanya. Primary key __tidak boleh kosong__ dan __tidak boleh ada yang sama__. Jika ada data yang sama, maka data tersebut akan dianggap sebagai duplikat dan akan dihapus.

- Primary key juga tidak boleh berubah. Jika terjadi perubahan, maka primary key akan dianggap sebagai data baru dan akan ditambahkan ke dalam tabel. Primary key juga tidak boleh dihapus. Jika terjadi penghapusan, maka data tersebut akan dianggap hilang dan tidak akan ditampilkan. Primary key juga tidak boleh diubah. Jika terjadi perubahan, maka data tersebut akan dianggap hilang dan tidak akan ditampilkan. 

- Primary key dapat dibuat dengan menggunakan tipe data INT, TINYINT, SMALLINT, MEDIUMINT, BIGINT, atau VARCHAR. Primary key dapat dibuat secara otomatis dengan menggunakan AUTO_INCREMENT. AUTO_INCREMENT akan membuat nilai primary key secara otomatis dan bertambah 1 setiap kali data baru ditambahkan. AUTO_INCREMENT hanya dapat digunakan untuk kolom yang bertipe INT, TINYINT, SMALLINT, MEDIUMINT, atau BIGINT. 

### Foreign Key

- Foreign key adalah kolom yang berisi nilai dari primary key pada tabel lain. Foreign key digunakan untuk menghubungkan tabel dengan tabel lainnya.

### Constraint

- Constraint adalah aturan yang diberikan pada kolom atau tabel. Constraint dapat digunakan untuk membatasi nilai yang dapat dimasukkan ke dalam kolom atau tabel. Constraint yang paling umum digunakan adalah:

  * NOT NULL - nilai tidak boleh kosong
  * UNIQUE - nilai tidak boleh ada yang sama
  * PRIMARY KEY - nilai unik dan tidak boleh ada yang sama
  * FOREIGN KEY - nilai harus sama dengan primary key pada tabel lain
  * CHECK - nilai harus memenuhi kondisi tertentu
  * DEFAULT - nilai default jika tidak ada nilai yang dimasukkan
  * INDEX - membuat index untuk kolom

- Constraint dalam relasi tabel antara lain adalah:

  * One-to-One - satu baris pada tabel A hanya memiliki satu baris pada tabel B dan sebaliknya. Contoh: tabel mahasiswa dan tabel nilai.
  * One-to-Many - satu baris pada tabel A memiliki banyak baris pada tabel B dan sebaliknya. Contoh: tabel mahasiswa dan tabel mata kuliah.
  * Many-to-Many - banyak baris pada tabel A memiliki banyak baris pada tabel B dan sebaliknya. Contoh: tabel mahasiswa dan tabel dosen.

- Constraint dalam foreign key antara lain adalah:

  * ON DELETE RESTRICT - tidak menghapus data pada tabel lain jika data pada tabel yang dihapus masih memiliki data pada tabel lain. 
  * ON DELETE CASCADE - menghapus baris pada tabel yang memiliki foreign key jika baris pada tabel yang memiliki primary key dihapus.
  * ON DELETE SET NULL - mengubah nilai foreign key menjadi NULL jika baris pada tabel yang memiliki primary key dihapus.
  * ON UPDATE RESTRICT - tidak mengubah data pada tabel lain jika data pada tabel yang diubah masih memiliki data pada tabel lain.
  * ON UPDATE CASCADE - mengubah nilai foreign key menjadi nilai primary key pada tabel yang memiliki primary key jika baris pada tabel yang memiliki primary key diubah. _*Jarang digunakan karena dapat menyebabkan duplikasi data dan biasanya primary key tidak pernah diubah_.
  * ON UPDATE SET NULL - mengubah nilai foreign key menjadi NULL jika baris pada tabel yang memiliki primary key diubah.

### Entitas

- Entitas adalah objek yang ingin direpresentasikan dalam database. Contoh entitas adalah mahasiswa, dosen, matakuliah, dan lain-lain. Setiap entitas memiliki atribut yang merepresentasikan karakteristik dari entitas tersebut. Contoh atribut dari entitas mahasiswa adalah nama, nim, alamat, dan lain-lain.

- Entitas dapat direpresentasikan dalam bentuk tabel. Setiap kolom pada tabel merepresentasikan atribut dari entitas tersebut. Setiap baris pada tabel merepresentasikan satu entitas. Contoh tabel untuk entitas mahasiswa adalah tabel mahasiswa.

### Atribut

- Atribut adalah karakteristik dari entitas. Atribut dapat berupa data maupun informasi. Contoh atribut adalah nama, alamat, dan lain-lain.

- Atribut dapat direpresentasikan dalam bentuk kolom. Setiap kolom pada tabel merepresentasikan atribut dari entitas tersebut. Setiap baris pada tabel merepresentasikan satu entitas. Contoh kolom untuk atribut nama adalah kolom nama.

### Relasi

- Relasi adalah hubungan antar entitas. Contoh relasi adalah mahasiswa mengambil matakuliah, dosen mengajar matakuliah, dan lain-lain. Setiap relasi memiliki atribut yang merepresentasikan karakteristik dari relasi tersebut. Contoh atribut dari relasi mahasiswa mengambil matakuliah adalah nilai, dan lain-lain.

- Relasi dapat dinyatakan dengan notasi `n:m`. Notasi `1:1` digunakan untuk relasi one-to-one. Notasi `1:n` digunakan untuk relasi one-to-many. Notasi `n:1` digunakan untuk relasi many-to-one.

## Praktikum

- Buka aplikasi MySQL Workbench, lalu pilih menu __File__ > __New Model__. Kemudian kita akan mengubah nama _Schema_ / _Database_ menjadi `praktikum`. Klik tombol __Apply__ untuk mengubah nama _Schema_ / _Database_.

![image](https://github.com/NazirArifin/modulsbd/blob/main/images/1-1.png)

- Selanjutnya _double click_ icon __Add Diagram__ untuk membuat diagram baru.

![image](https://github.com/NazirArifin/modulsbd/blob/main/images/1-2.png)

- Pilih icon __Table__ untuk membuat tabel baru. Kemudian ubah nama tabel menjadi `prodi` dengan melakukan _double click_ pada tabel tersebut. 

![image](https://github.com/NazirArifin/modulsbd/blob/main/images/1-3.png)

- Kemudian di `Column Name` tambahkan kolom `id_prodi` dan `nama_prodi` dengan tipe data `INT` dan `VARCHAR(50)`. Pastikan kolom `id_prodi` memiliki constraint `PRIMARY KEY` __(PK)__, `NOT NULL` __(NN)__ dan `AUTO_INCREMENT` __(AI)__. Jika sudah, tekan tombol X untuk menyimpan perubahan.

![image](https://github.com/NazirArifin/modulsbd/blob/main/images/1-4.png)

- Buat tabel dengan nama `mahasiswa` dengan struktur kolom sebagai berikut:
  * `nim` - `CHAR(10)` - PRIMARY KEY
  * `nama` - `VARCHAR(50)` - NOT NULL
  * `alamat` - `VARCHAR(100)` - NOT NULL
  * `tgl_lahir` - `DATE` - NOT NULL
  * `jk` - `ENUM('L', 'P')` - NOT NULL

- Buat tabel dengan nama `matakuliah` dengan struktur kolom sebagai berikut:
  * `kode_mk` - `VARCHAR(10)` - PRIMARY KEY
  * `nama_mk` - `VARCHAR(50)` - NOT NULL
  * `sks_mk` - `TINYINT(1)` - NOT NULL
  * `semester_mk` - `TINYINT(1)` - NOT NULL

- Buat tabel dengan nama `nilai` dengan struktur kolom sebagai berikut:
  * `id_nilai` - `INT` - PRIMARY KEY - AUTO_INCREMENT
  * `nilai` - `TINYINT(3)` - NOT NULL

- Buat tabel dengan nama `dosen` dengan struktur kolom sebagai berikut:
  * `nis` - `VARCHAR(10)` - PRIMARY KEY
  * `nidn` - `VARCHAR(10)` - NULL
  * `nama` - `VARCHAR(50)` - NOT NULL
  * `alamat` - `VARCHAR(100)` - NOT NULL
  * `tgl_lahir` - `DATE` - NOT NULL
  * `jk` - `ENUM('L', 'P')` - NOT NULL

- Buat tabel dengan nama `mengajar` dengan struktur kolom sebagai berikut:
  * `id_mengajar` - `INT` - PRIMARY KEY - AUTO_INCREMENT

- Berikutnya kita buat relasi antar tabel. Kita akan membuat relasi `1:n` antara tabel `prodi` dan `mahasiswa`. Klik icon __Relationship__ `1:n` untuk membuat relasi baru. Karena relasi `1:n` maka kita harus pilih terlebih dahulu tabel yang memiliki relasi `1` yaitu tabel `mahasiswa`. Kemudian klik tabel yang memiliki relasi `n` yaitu tabel `prodi`. Maka akan muncul garis relasi antara tabel `mahasiswa` dan `prodi` dan akan muncul kolom `prodi_id_prodi` pada tabel `mahasiswa`.

![image](https://github.com/NazirArifin/modulsbd/blob/main/images/1-5.png)

- Jika Anda mengubah nama _foreign key_ atau tindakan _cascade_ pada relasi, maka Anda harus mengubahnya pada tabel yang memiliki relasi tersebut. Double click tabel `mahasiswa` dan pindah ke tab _Foreign Keys_. Ubah nama _foreign key_ menjadi `prodi_id_prodi` dan ubah tindakan _cascade_ menjadi `RESTRICT`.

![image](https://github.com/NazirArifin/modulsbd/blob/main/images/1-6.png)

- Kemudian kita akan buat relasi `1:n` untuk tabel:
  - `prodi` dan `matakuliah`
  - `prodi` dan `dosen`
  - `mahasiswa` dan `nilai`
  - `matakuliah` dan `nilai`

- Buat relasi `n:m` antara tabel `dosen` dan `matakuliah`. Relasi `n:m` digunakan karena satu dosen dapat mengajar lebih dari satu matakuliah dan satu matakuliah dapat diajar oleh lebih dari satu dosen.

- Setelah semua relasi dibuat, maka diagram akan dapat diekspor ke dalam bentuk _SQL Script_ ataupun gambar. Tekan menu __File__ dan pilih __Export__ untuk mengekspor diagram ke dalam bentuk _SQL Script_ atau gambar.

![image](https://github.com/NazirArifin/modulsbd/blob/main/images/1-7.png)

## Tugas

- Terdapat entitas `anggota` dengan atribut nomor keanggotaan, nama lengkap, jenis kelamin, tanggal lahir, alamat, dan nomor telepon. Buatlah tabel `anggota` dengan atribut yang telah ditentukan.

- Terdapat entitas `kategori` untuk kategori buku dengan atribut kode kategori, nama kategori, dan keterangan. Buatlah tabel `kategori` dengan atribut yang telah ditentukan.

- Terdapat entitas `buku` dengan atribut kode buku, judul buku, pengarang, penerbit, tahun terbit, dan jumlah buku. Buatlah tabel `buku` dengan atribut yang telah ditentukan.

- Terdapat entitas `petugas` dengan atribut nomor petugas, nama lengkap, jenis kelamin, tanggal lahir, alamat, dan nomor telepon. Buatlah tabel `petugas` dengan atribut yang telah ditentukan.

- Terdapat entitas `peminjaman` dengan atribut nomor peminjaman, nomor keanggotaan, kode buku, tanggal peminjaman, tanggal pengembalian, nomor_petugas, dan status. Buatlah tabel `peminjaman` dengan atribut yang telah ditentukan.

- Terdapat entitas `pengembalian` dengan atribut nomor pengembalian, nomor peminjaman, tanggal pengembalian, dan denda. Buatlah tabel `pengembalian` dengan atribut yang telah ditentukan.