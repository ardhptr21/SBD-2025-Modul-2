# Database Normalization
Praktikum Sistem Basis Data Modul 2

## Data Diri

Nama : Ardhi Putra Pradana

NRP : 5027241022

Kelas : C

## Tahap Normalisasi

> - [+] : Tabel yang ditambahkan atau tabel baru
> - [*] : Tabel yang sudah ada dan diubah

### Bentuk awal

| ID_Pesanan | Nama_Pelanggan | Alamat_Pelanggan      | Tanggal_Pesanan | Item_Dipesan      | Harga_Item    | Nama_Karyawan | Posisi_Karyawan | Metode_Pembayaran |
| ---------- | -------------- | --------------------- | --------------- | ----------------- | ------------- | ------------- | --------------- | ----------------- |
| 1          | Agus Sustisna  | Jl. Medokan semampir  | 2023-09-21      | Burger, Aquase    | 15.000, 2.500 | Tuna          | Kasir           | Tunai             |
| 2          | Udin Pangalila | Sukolilo Park Regency | 2023-10-02      | Salad, Kopi Tarik | 15.000, 5.000 | Alice         | Pelayan         | Kartu Kredit      |
| 3          | Selamet        | Kejawan Gebang No. 15 | 2023-10-03      | Pizza, Teh Anget  | 20.000, 3.000 | Tuna          | Kasir           | Tunai             |
| 4          | Wahyu Purnama  | Keputih Tegal Timur   | 2023-10-12      | Steak, Kopi Tarik | 30.000, 5.000 | Samsul        | Koki            | QRIS              |
| 5          | Suci Aprillia  | Jl. Gebang Putih      | 2023-10-13      | Pasta, Aquase     | 17.000, 2.500 | Alice         | Pelayan         | Kartu Debit       |

### Normalisasi 1NF

Jika dilihat pada bentuk awal tabel terdepat duplikasi atribut data yaitu pada atribut `Item_Dipesan` dan `Harga_Item`.
Karena syarat pada **Normalisasi 1NF** tidak diperkenankan adanya duplikasi atribut, maka harus dilakukan perubahan.

Akan dibentuk 3 tabel dalam tahap ini:

#### [*] Tabel `Pesanan`

| ID_Pesanan | Nama_Pelanggan | Alamat_Pelanggan      | Tanggal_Pesanan | Nama_Karyawan | Posisi_Karyawan | Metode_Pembayaran |
| ---------- | -------------- | --------------------- | --------------- | ------------- | --------------- | ----------------- |
| 1          | Agus Sustisna  | Jl. Medokan semampir  | 2023-09-21      | Tuna          | Kasir           | Tunai             |
| 2          | Udin Pangalila | Sukolilo Park Regency | 2023-10-02      | Alice         | Pelayan         | Kartu Kredit      |
| 3          | Selamet        | Kejawan Gebang No. 15 | 2023-10-03      | Tuna          | Kasir           | Tunai             |
| 4          | Wahyu Purnama  | Keputih Tegal Timur   | 2023-10-12      | Samsul        | Koki            | QRIS              |
| 5          | Suci Aprillia  | Jl. Gebang Putih      | 2023-10-13      | Alice         | Pelayan         | Kartu Debit       |

#### [+] Tabel `Pesanan_Item`

| ID_Pesanan | ID_Item |
| ---------- | ------- |
| 1          | 1       |
| 1          | 2       |
| 2          | 3       |
| 2          | 4       |
| 3          | 5       |
| 3          | 6       |
| 4          | 7       |
| 4          | 4       |
| 5          | 8       |
| 5          | 2       |

#### [+] Tabel `Item`

| ID_Item | Nama       | Harga   |
| ------- | ---------- | ------- |
| 1       | Burger     | 15.000  |
| 2       | Aquase     | 2.500   |
| 3       | Salad      | 15.0000 |
| 4       | Kopi Tarik | 3.000   |
| 5       | Pizza      | 20.000  |
| 6       | Teh Anget  | 3.000   |
| 7       | Steak      | 30.000  |
| 8       | Pasta      | 17.000  |

Dengan melakukan pembagian menjadi 3 tabel untuk menghilangkan duplikasi atribut maka sekarang sudah memenuhi syarat **Normalisasi 1NF**

### Normalisasi 2NF

Untuk bisa memenuhi syarat pada **Normalisasi 2NF** maka harus menghilangkan *ketergantungan parsial*.
Jika dilihat masih ada *ketergantungan parsial* yang ada struktur tabel sebelumnya, yaitu dimana atribut `Nama_Karyawan` dan `Posisi_Karyawan` tidak memiliki korelasi apapun dengan primary key `ID_Pesanan`.

Harus dilakukan pemisahan pada dan melakukan struktur tabelnya, dan berikut adalah hal - hal yang ditambah dan atau diubah pada struktur tabel sebelumnya:

#### [*] Tabel `Pesanan`

| ID_Pesanan | ID_Karyawan | Nama_Pelanggan | Alamat_Pelanggan      | Tanggal_Pesanan | Metode_Pembayaran |
| ---------- | ----------- | -------------- | --------------------- | --------------- | ----------------- |
| 1          | 1           | Agus Sustisna  | Jl. Medokan semampir  | 2023-09-21      | Tunai             |
| 2          | 2           | Udin Pangalila | Sukolilo Park Regency | 2023-10-02      | Kartu Kredit      |
| 3          | 1           | Selamet        | Kejawan Gebang No. 15 | 2023-10-03      | Tunai             |
| 4          | 3           | Wahyu Purnama  | Keputih Tegal Timur   | 2023-10-12      | QRIS              |
| 5          | 2           | Suci Aprillia  | Jl. Gebang Putih      | 2023-10-13      | Kartu Debit       |


#### [+] Tabel `Karyawan` 

| ID_Karyawan | Nama   | Posisi  |
| ----------- | ------ | ------- |
| 1           | Tuna   | Kasir   |
| 2           | Alice  | Pelayan |
| 3           | Samsul | Koki    |

Dengan memperbarui tabel `Pesanan` dan menambahkan tabel `Karyawan` untuk mengelola data karyawan maka disini sudah memenuhi syarat **Normalisasi 2NF** yaitu menghilangkan *ketergantungan parsial*

### Normalisasi 3NF