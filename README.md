# Toko Sembako - Inventory Management System (Laravel)

Project ini merupakan implementasi materi **Pertemuan 5 - Laravel Fundamental**. Tema toko diubah menjadi Toko Sembako, sedangkan ruang lingkup tugas tetap mengikuti PPT: environment, MVC, routing, resource controller, Blade, migration, model, factory, seeder, Eloquent CRUD, relationship, dan fitur inventory.

## Kebutuhan
- PHP 8.2 atau lebih baru
- Composer
- MySQL / MariaDB (XAMPP dapat digunakan)
- Ekstensi PHP yang dibutuhkan Laravel, termasuk OpenSSL, PDO, Mbstring, Tokenizer, XML, Ctype, JSON, dan BCMath

## Instalasi
1. Ekstrak folder project.
2. Buka terminal pada folder `toko-sembako-laravel`.
3. Instal dependency:
   ```bash
   composer install
   ```
4. Salin `.env.example` menjadi `.env`:
   - Windows CMD: `copy .env.example .env`
   - PowerShell: `Copy-Item .env.example .env`
5. Buat database MySQL bernama `toko_sembako` melalui phpMyAdmin.
6. Pastikan pengaturan database pada `.env`:
   ```env
   DB_CONNECTION=mysql
   DB_HOST=127.0.0.1
   DB_PORT=3306
   DB_DATABASE=toko_sembako
   DB_USERNAME=root
   DB_PASSWORD=
   ```
7. Buat application key:
   ```bash
   php artisan key:generate
   ```
8. Jalankan migration dan seeder:
   ```bash
   php artisan migrate:fresh --seed
   ```
   Perintah `migrate:fresh` menghapus tabel lama pada database yang dipilih. Gunakan hanya pada database tugas ini.
9. Jalankan aplikasi:
   ```bash
   php artisan serve
   ```
10. Buka `http://127.0.0.1:8000`.

## Fitur
- Dashboard ringkasan produk, kategori, jumlah stok, dan peringatan stok minimum.
- CRUD produk dengan validasi.
- CRUD kategori dan pemasok.
- Pencarian produk berdasarkan nama atau SKU.
- Filter berdasarkan kategori dan status stok.
- Sorting nama produk dan pagination.
- Transaksi stok masuk dan keluar dengan pembaruan stok otomatis.
- Validasi agar stok tidak menjadi negatif.
- Riwayat pergerakan stok pada detail produk.

## Struktur penting
```text
app/
  Http/Controllers/
    CategoryController.php
    ProductController.php
    StockMovementController.php
    SupplierController.php
  Models/
    Category.php
    Product.php
    StockMovement.php
    Supplier.php
database/
  factories/
  migrations/
  seeders/DatabaseSeeder.php
resources/views/
  layouts/app.blade.php
  products/
  categories/
  suppliers/
  stock-movements/
routes/web.php
.env.example
```

## Alur MVC
Request browser → Route (`routes/web.php`) → Controller → Model Eloquent → Database → Controller memilih View/Redirect → Response ke browser.

## Contoh demonstrasi
1. Buka menu Produk dan klik Tambah Produk.
2. Isi form produk dan klik Simpan.
3. Jika input tidak valid, Laravel menampilkan pesan validasi.
4. Jika valid, data disimpan melalui Eloquent dan pengguna diarahkan kembali ke daftar produk.
5. Buka Transaksi Stok untuk mencatat barang masuk atau keluar.
6. Periksa stok pada daftar produk dan riwayat transaksi.

## Screenshot untuk laporan
Ambil screenshot sendiri setelah aplikasi dijalankan:
- Dashboard.
- `php artisan route:list` di terminal.
- Daftar produk dan form tambah/edit.
- Pesan validasi (uji dengan input yang tidak sesuai).
- Daftar kategori dan pemasok.
- Transaksi stok masuk/keluar.
- Detail produk dan riwayat stok.

## Catatan kesesuaian PPT
PPT menyebutkan migrasi dari project P4 dan business rule stok P4 harus dipertahankan. File P4 tidak disertakan bersama PPT ini, sehingga aturan khusus dari project P4 yang tidak dijelaskan di PPT belum dapat diverifikasi. Implementasi ini menerapkan aturan stok minimum dan mencegah stok keluar melebihi stok tersedia sebagai aturan inventory dasar. Sesuaikan aturan tersebut dengan project P4 asli jika terdapat aturan tambahan.
