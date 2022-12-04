# Modul 2 - Normalisasi Basis Data

Tujuan Pembelajaran: Mahasiswa dapat memahami dan menerapkan konsep normalisasi basis data.

## Materi

![image](https://149348513.v2.pressablecdn.com/wp-content/uploads/2011/01/brain.png)

### Normalisasi

Normalisasi adalah proses untuk mengubah suatu tabel yang tidak ternormalisasi menjadi tabel yang ternormalisasi. Normalisasi merupakan teknik desain database yang mengurangi duplikasi data dan mempertahankan konsistensi data. Selain itu juga untuk mengurangi anomali khususnya anomali update, insert, dan delete. Normalisasi membagi tabel yang besar menjadi tabel yang lebih kecil dan lebih sederhana (atomic). Tabel yang lebih kecil dan lebih sederhana ini disebut dengan tabel normal yang dihubungkan dengan relasi. Penemu normalisasi adalah Edgar F. Codd.

### UNF (Unnormalized Form)

Berikut adalah contoh tabel `buku` dari aplikasi perpustakaan yang belum dalam 1NF (Unnormalized Form):

| JUDUL | PENGARANG | TOPIK | PENERBIT | TAHUN TERBIT | FORMAT | HARGA
| --- | --- | --- | --- | --- |
| Pemrograman Java | Eko Kurniawan | Pemrograman, Java, Desktop | Andi Offset | 2010 | Buku | 100000
| Pemrograman Java | Eko Kurniawan | Pemrograman, PHP, Web | Media Offset | 2011 | Buku Digital | 750000


### 1NF (First Normal Form)

Tabel di atas memiliki beberapa masalah, yaitu:

- Kolom TOPIK memiliki banyak nilai

1NF adalah normalisasi pertama yang dilakukan pada tabel. Tabel yang sudah dalam 1NF disebut tabel yang sudah ternormalisasi. Tabel yang sudah dalam 1NF memiliki kriteria, yaitu:

  __```Setiap kolom hanya menyimpan satu nilai (tidak ada kolom yang memiliki banyak nilai)```__

  __```Setiap baris harus memiliki nilai yang unik```__

Untuk menyesuaikan tabel dengan 1NF, maka tabel perlu menambahkan primary key dan memisahkan kolom TOPIK menjadi tabel baru. Berikut adalah tabel `buku` yang sudah dalam 1NF:

| ID | JUDUL | PENGARANG | PENERBIT | TAHUN TERBIT | FORMAT | HARGA
| --- | --- | --- | --- | --- |
| 1 | Pemrograman Java | Eko Kurniawan | Andi Offset | 2010 | Buku | 100000
| 2 | Pemrograman Java | Eko Kurniawan | Media Offset | 2011 | Buku Digital | 750000

| ID | ID BUKU | TOPIK
| --- | --- | --- |
| 1 | 1 | Pemrograman |
| 2 | 1 | Java |
| 3 | 1 | Desktop |

Tabel di atas sudah dalam 1NF karena setiap kolom hanya menyimpan satu nilai dan setiap baris memiliki nilai yang unik.

### 2NF (Second Normal Form)

2NF adalah normalisasi kedua yang dilakukan pada tabel. Tabel yang sudah dalam 2NF memiliki kriteria, yaitu:

  __```Tabel dalam 2NF harus sudah dalam 1NF```__

  __```Tidak ada composite primary key (tidak ada primary key yang terdiri dari lebih dari satu kolom)```__

  __```Tidak ada atribut yang tidak bergantung pada primary key```__

2NF menyatakan tidak boleh terdapat _composite_key_. Pada kasus ini, keunikan data ditentukan oleh kolom `JUDUL` dan `PENERBIT`. Maka, kolom dipisah menjadi tabel baru. Berikut adalah tabel `buku` yang sudah dalam 2NF:

| ID | JUDUL | PENGARANG | TAHUN TERBIT | FORMAT | HARGA
| --- | --- | --- | --- | --- |
| 1 | Pemrograman Java | Eko Kurniawan | 2010 | Buku | 100000
| 2 | Pemrograman Java | Eko Kurniawan | 2011 | Buku Digital | 750000

| ID | ID BUKU | TOPIK
| --- | --- | --- |
| 1 | 1 | Pemrograman |
| 2 | 1 | Java |
| 3 | 1 | Desktop |

| ID | NAMA
| --- | --- |
| 1 | Andi Offset |
| 2 | Media Offset |

2NF juga menyatakan bahwa setiap kolom harus terkait dengan primary key. Jika ada kolom yang tidak terkait dengan primary key, maka kolom tersebut harus dipisahkan menjadi tabel baru. Pada kasus ini, kolom `HARGA` tidak terkait dengan primary key. Maka, kolom dipisah menjadi tabel baru. Berikut adalah tabel `buku` yang sudah dalam 2NF:

| ID | JUDUL | PENGARANG | TAHUN TERBIT | FORMAT
| --- | --- | --- | --- | --- |
| 1 | Pemrograman Java | Eko Kurniawan | 2010 | Buku
| 2 | Pemrograman Java | Eko Kurniawan | 2011 | Buku Digital


| ID | ID BUKU | HARGA
| --- | --- | --- |
| 1 | 1 | 100000 |
| 2 | 2 | 750000 |

### 3NF (Third Normal Form)













