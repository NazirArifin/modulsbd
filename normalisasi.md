# Modul 2 - Normalisasi Basis Data

Tujuan Pembelajaran: Mahasiswa dapat memahami dan menerapkan konsep normalisasi basis data.

## Materi

![image](https://149348513.v2.pressablecdn.com/wp-content/uploads/2011/01/brain.png)

### Normalisasi

Normalisasi adalah proses untuk mengubah suatu tabel yang tidak ternormalisasi menjadi tabel yang ternormalisasi. Normalisasi merupakan teknik desain database yang mengurangi duplikasi data dan mempertahankan konsistensi data. Selain itu juga untuk mengurangi anomali khususnya anomali update, insert, dan delete. Normalisasi membagi tabel yang besar menjadi tabel yang lebih kecil dan lebih sederhana (atomic). Tabel yang lebih kecil dan lebih sederhana ini disebut dengan tabel normal yang dihubungkan dengan relasi. Penemu normalisasi adalah Edgar F. Codd.

### UNF (Unnormalized Form)

Berikut adalah contoh tabel `buku` dari aplikasi perpustakaan yang belum dalam 1NF (Unnormalized Form):

![image](/images/2-1.png)

### 1NF (First Normal Form)

1NF adalah normalisasi pertama yang dilakukan pada tabel. Tabel yang sudah dalam 1NF disebut tabel yang sudah ternormalisasi. Tabel yang sudah dalam 1NF memiliki kriteria, yaitu:

  __```Setiap kolom hanya menyimpan satu nilai (tidak ada kolom yang memiliki banyak nilai)```__

  __```Setiap baris harus memiliki nilai yang unik```__

Untuk menyesuaikan tabel dengan 1NF, maka tabel perlu menambahkan primary key dan memisahkan kolom TOPIK menjadi tabel baru. Berikut adalah tabel `buku` yang sudah dalam 1NF:

![image](/images/2-2.png)

| ID | ID BUKU | TOPIK
| --- | --- | --- |
| 1 | 1 | Pemrograman |
| 2 | 1 | Java |
| 3 | 1 | Desktop |
| 4 | 2 | Pemrograman |
| 5 | 2 | Java |
| 6 | 2 | Web |

Tabel di atas sudah dalam 1NF karena setiap kolom hanya menyimpan satu nilai dan setiap baris memiliki nilai yang unik.

### 2NF (Second Normal Form)

2NF adalah normalisasi kedua yang dilakukan pada tabel. Tabel yang sudah dalam 2NF memiliki kriteria, yaitu:

  __```Tabel dalam 2NF harus sudah dalam 1NF```__

  __```Tidak ada composite primary key (tidak ada primary key yang terdiri dari lebih dari satu kolom)```__

2NF menyatakan tidak boleh terdapat _composite_key_. Pada kasus ini, keunikan data ditentukan oleh kolom `JUDUL` dan `PENERBIT`. Maka, kolom dipisah menjadi tabel baru. Berikut adalah tabel `buku` yang sudah dalam 2NF:

![image](/images/2-3.png)

| ID | NAMA
| --- | --- |
| 1 | Andi Offset |
| 2 | Media Offset |

### 3NF (Third Normal Form)

3NF adalah normalisasi ketiga yang dilakukan pada tabel. Tabel yang sudah dalam 3NF memiliki kriteria, yaitu:

  __```Tabel dalam 3NF harus sudah dalam 2NF```__

  __```Tidak ada atribut yang memiliki transitive functional dependency```__

Functional dependency adalah hubungan antara kolom yang satu dengan kolom yang lain. Jika ada kolom yang memiliki functional dependency, maka kolom tersebut harus dipisahkan menjadi tabel baru. Pada kasus ini, kolom `FORMAT` memiliki functional dependency dengan kolom `HARGA`. Jika kolom `FORMAT` berubah, maka kolom `HARGA` juga berubah. Maka, kolom `FORMAT` dan `HARGA` dipisah menjadi tabel baru. Berikut adalah tabel `buku` yang sudah dalam 3NF:

ID | JUDUL | PENGARANG | PENERBIT | TAHUN | FORMAT
--- | --- | --- | --- | --- | ---
1 | Pemrograman Java | Andi Offset | 1 | 2010 | 1
2 | Pemrograman Java (Web) | Andi Offset | 2 | 2010 | 2

| ID | FORMAT | HARGA
| --- | --- | --- |
| 1 | Buku Digital | 75000 |
| 2 | Buku | 100000 |



## Praktikum

- Buatlah tabel `buku` yang sudah dalam 1NF, 2NF, dan 3NF menggunakan MySQL Workbench.

## Tugas

1. Terdapat data `mahasiswa` yang memiliki atribut `NIM`, `NAMA`, `EMAIL`, `PRODI`, `FAKULTAS`, `MATKUL`. 
  - Kolom `MATKUL` memiliki banyak nilai.

  - Buatlah tabel `mahasiswa` yang sudah dalam 1NF, 2NF, dan 3NF menggunakan MySQL Workbench.

2. Terdapat data `produk` yang memiliki atribut `ID`, `NAMA`, `HARGA`, `STOK`, `SATUAN`, `SUPPLIER`, `KATEGORI`, `SUB KATEGORI`, `DESKRIPSI`. 
  - Kolom `KATEGORI` dan `SUB KATEGORI` memiliki banyak nilai.

  - Buatlah tabel `produk` yang sudah dalam 1NF, 2NF, dan 3NF menggunakan MySQL Workbench.

3. Terdapat data `pegawai` yang memiliki atribut `ID`, `NAMA`, `ALAMAT`, `JABATAN`, `GAJI`, `TUNJANGAN`, `POTONGAN`, `TANGGAL MASUK`, `TANGGAL KELUAR`. 
  - Kolom `GAJI`, `TUNJANGAN`, dan `POTONGAN` memiliki functional dependency.

  - Buatlah tabel `pegawai` yang sudah dalam 1NF, 2NF, dan 3NF menggunakan MySQL Workbench.

# Referensi

[https://www.guru99.com/database-normalization.html](https://www.guru99.com/database-normalization.html)

[https://en.wikipedia.org/wiki/Database_normalization](https://en.wikipedia.org/wiki/Database_normalization)











