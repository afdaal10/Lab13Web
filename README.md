# Praktikum 13 & 14

**Nama:** Afdhal Agislam

**NIM:** 312410445  

**Kelas:** TI 24 A5



## 1. Praktikum 13: Pagination (Pembagian Halaman)
**Tujuan:** Membatasi jumlah data yang tampil agar tidak menumpuk di satu halaman, serta membaginya menjadi beberapa halaman (Page 1, 2, dst).

### 🔧 Perubahan Kode
1.  **Class Database (`class/database.php`)**:
    * Menambahkan method `total()` untuk menghitung jumlah total baris data di tabel.
    * Menambahkan method `getLimit()` untuk mengambil data dengan batasan jumlah (`LIMIT`) dan urutan awal (`OFFSET`).

2.  **Logika Utama (`modules/barang/index.php`)**:
    * **Menentukan Limit:** Mengatur variabel `$per_page = 3` (menampilkan 3 barang per halaman).
    * **Menangkap Halaman Saat Ini:** Mengambil parameter URL `?hal=...`. Jika tidak ada, default ke halaman 1.
    * **Menghitung Offset:** Rumus: `($halaman_saat_ini - 1) * $per_page`.
        * *Contoh:* Halaman 1 offset 0, Halaman 2 offset 3.
    * **Navigasi:** Membuat tombol **Previous** dan **Next** yang dinamis.

###  Alur Kerja
User membuka halaman -> Sistem menghitung total data -> Sistem memotong data menggunakan Query `LIMIT offset, jumlah` -> Data ditampilkan sebagian sesuai halaman yang dipilih.

---

## 2. Praktikum 14: Searching (Pencarian Data)
**Tujuan:** Memudahkan pengguna mencari data barang spesifik berdasarkan nama barang.

###  Perubahan Kode
1.  **Update Class Database**:
    * Memodifikasi method `total()` dan `getLimit()` agar bisa menerima parameter tambahan berupa query `WHERE`.
    * Query SQL berubah dinamis. Jika ada pencarian, SQL menambahkan: `WHERE nama LIKE '%keyword%'`.

2.  **Form Pencarian (`modules/barang/index.php`)**:
    * Menambahkan form HTML dengan method `GET` dan input bernama `q`.
    * Menambahkan tombol "Cari" dan tombol "Reset" (jika sedang mencari).

3.  **Integrasi Search & Pagination**:
    * Menjaga agar kata kunci pencarian tidak hilang saat pindah halaman.
    * Pada link pagination, ditambahkan parameter `&q=...`.
    * *Contoh URL:* `index.php?page=barang&hal=2&q=samsung`

###  Alur Kerja
User mengetik kata kunci -> Klik Cari -> URL berubah membawa parameter `?q=kata_kunci` -> Sistem menangkap `$_GET['q']` -> Query database difilter menggunakan `LIKE` -> Data yang cocok ditampilkan (tetap dengan pagination).

---

##  Hasil Implementasi

* **Pagination:** Tombol navigasi muncul di sebelah kiri bawah tabel.
* **Searching:** Kotak pencarian ada di atas tabel. Hasil pencarian otomatis ter-filter dan ter-paging.
