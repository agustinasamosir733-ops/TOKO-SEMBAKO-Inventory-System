# Sistem Informasi Toko Sembako – Laravel (Tugas Web 5)

Paket ini berisi file aplikasi untuk ditempelkan ke project Laravel baru. Aplikasi menerapkan MVC, CRUD produk dan kategori, relasi Eloquent, validasi, pencarian, filter kategori, sorting, pagination, migration, factory, dan seeder.

## 1. Persiapan
- PHP 8.2 atau lebih baru
- Composer
- MySQL / MariaDB
- Laravel 11 atau 12

## 2. Membuat project Laravel
Jalankan di Terminal/CMD:

```bash
composer create-project laravel/laravel toko-sembako-laravel
cd toko-sembako-laravel
```

Ekstrak paket tugas ini. Salin isi folder `app`, `database`, `resources`, dan `routes` ke folder project `toko-sembako-laravel` dengan mempertahankan struktur folder. Izinkan penggabungan folder dan penggantian file jika diminta. File `README-INSTALASI.md` tidak perlu disalin.

## 3. Membuat database
Buat database MySQL bernama `toko_sembako_db` melalui phpMyAdmin atau MySQL.

Atur file `.env` pada project Laravel:

```env
APP_NAME="Toko Sembako"
APP_ENV=local
APP_KEY=
APP_DEBUG=true
APP_URL=http://127.0.0.1:8000

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=toko_sembako_db
DB_USERNAME=root
DB_PASSWORD=
```

Sesuaikan username dan password MySQL jika berbeda.

## 4. Menjalankan aplikasi
```bash
php artisan key:generate
php artisan migrate:fresh --seed
php artisan serve
```
Buka `http://127.0.0.1:8000`.

> `migrate:fresh` menghapus tabel lama dalam database yang dipilih lalu membuat ulang. Gunakan hanya pada database tugas, bukan database penting.

## 5. Fitur aplikasi
- Dashboard ringkasan jumlah kategori, produk, stok, dan produk stok minimum.
- CRUD kategori.
- CRUD produk.
- Pencarian nama/SKU, filter kategori, sorting, dan pagination.
- Validasi SKU unik, nama wajib, harga numerik minimal 0, stok bilangan bulat minimal 0.
- Relasi Category `hasMany` Product dan Product `belongsTo` Category.
- Penyesuaian stok masuk/keluar dengan pencatatan Stock Movement.
- Seeder kategori dan produk contoh.

## 6. Screenshot yang harus dikumpulkan
Ambil screenshot asli dari browser setelah aplikasi berjalan:
1. Halaman dashboard.
2. Halaman daftar produk (terlihat pencarian/filter/pagination).
3. Form tambah produk.
4. Hasil validasi ketika form dikirim dengan data tidak valid.
5. Data produk setelah berhasil disimpan.
6. Halaman kategori.
7. Halaman penyesuaian stok / riwayat pergerakan stok.
8. Terminal yang menunjukkan `php artisan route:list` dan `php artisan migrate:fresh --seed`.

## 7. Penjelasan singkat MVC
- **Model:** `Category`, `Product`, dan `StockMovement` mewakili data serta relasi database.
- **View:** file Blade di `resources/views` menampilkan dashboard, tabel, dan formulir.
- **Controller:** `ProductController`, `CategoryController`, dan `StockMovementController` menerima request, menjalankan validasi, memanggil model, lalu mengembalikan response.
- **Alur:** Request → Route → Controller → Model → Database → Response.

## 8. Demo yang disarankan
Buka menu Produk → Tambah Produk → isi SKU, nama, kategori, harga, dan stok → Simpan → aplikasi memvalidasi input → data tersimpan → diarahkan kembali ke daftar produk dengan pesan sukses.

## Catatan penyesuaian P4
PPT menyatakan business rule P4 harus dipertahankan. Karena source code P4 tidak disertakan, paket ini menggunakan aturan stok dasar: stok tidak boleh negatif; stok masuk menambah stok; stok keluar tidak boleh melebihi stok tersedia; setiap perubahan dicatat. Jika project P4 memiliki aturan atau kolom tambahan, sesuaikan migration, model, dan controller dengan aturan asli P4.
