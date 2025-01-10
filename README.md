# UAS Pemrograman Sisi Server

## API LMS Laravel dengan Docker

### Fitur yang Tersedia
- **Pendaftaran, Login, & Logout** - Fungsi Dasar
- **Analitik Kursus** - Fungsi Dasar
- **Pembatasan Jumlah Maksimum Mahasiswa** - Fungsi Dasar
- **Pengumuman** - Fungsi Tambahan
- **Umpan Balik** - Fungsi Tambahan
- **Kategori** - Fungsi Tambahan

### Teknologi yang Digunakan
- **Laravel** - Framework PHP
- **MySQL** - Sistem Manajemen Basis Data Relasional
- **Nginx** - Server Web
- **Docker** - Platform Container

### Persyaratan
Sebelum memulai, pastikan sistem Anda telah terpasang salah satu dari berikut ini:
- **Docker Desktop** atau
- Paket **docker** dan **docker-compose**

### Panduan Instalasi

#### 1. Clone Proyek
```bash
git clone https://github.com/gent0nk/uas-pss.git
```
Salin repositori ke direktori kerja Anda.

#### 2. Masuk ke Direktori Proyek
```bash
cd uas-pss
```
Akses folder hasil clone.

#### 3. Jalankan Instalasi

##### Untuk Sistem UNIX (Linux & MacOS)
```bash
./setup.sh
```
Jalankan skrip otomatis untuk menyiapkan proyek.

##### Untuk Sistem Windows
Karena skrip `setup.sh` tidak kompatibel di Windows, lakukan instalasi manual dengan langkah-langkah berikut:

###### 3.1. Inisialisasi Container
```bash
docker-compose up -d --build
```

###### 3.2. Atur Izin Direktori
```bash
docker-compose exec app chmod -R 777 /var/www/html/storage /var/www/html/bootstrap/cache
```

###### 3.3. Instal Dependency Frontend
```bash
docker exec laravel_app npm i
```

###### 3.4. Build Frontend
```bash
docker exec laravel_app npm run build
```

###### 3.5. Instal Dependency PHP
```bash
docker exec laravel_app composer install
```

###### 3.6. Salin File Konfigurasi `.env`
```bash
docker exec laravel_app cp .env.example .env
```

###### 3.7. Generate Kunci Aplikasi
```bash
docker exec laravel_app php artisan key:generate
```

###### 3.8. Konfigurasi Database
Edit file `.env` pada proyek ini:
Sebelum:
```plaintext
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=database
DB_USERNAME=root
DB_PASSWORD=
```
Sesudah:
```plaintext
DB_CONNECTION=mysql
DB_HOST=db
DB_PORT=3306
DB_DATABASE=lms_api
DB_USERNAME=root
DB_PASSWORD=root
```

###### 3.9. Migrasi Basis Data
```bash
docker exec laravel_app php artisan migrate
```

### Struktur Proyek
- **docker-compose.yml** - Definisi konfigurasi multi-container Docker
- **Dockerfile** - Instruksi pembuatan image Docker
- **uas-pss** - Kode sumber API LMS
- **nginx.conf** - File konfigurasi Nginx
- **setup.sh** - Skrip otomatis untuk instalasi