# PRD MediFlow

**Nama Aplikasi:** MediFlow  
**Jenis Aplikasi:** Aplikasi Antrian Klinik Berbasis Flutter  
**Backend:** Supabase  
**Platform:** Mobile Android  
**Tujuan Dokumen:** Product Requirement Document untuk pembagian tugas, alur fitur, struktur database, dan panduan pengembangan project UAS.  
**Versi:** 1.1  

---

## 1. Ringkasan Produk

MediFlow adalah aplikasi antrian klinik digital yang membantu pasien mengambil nomor antrian secara online dan membantu petugas klinik mengelola antrian secara lebih rapi. Aplikasi ini dibuat menggunakan Flutter sebagai frontend dan Supabase sebagai backend untuk autentikasi, database, serta pengelolaan data pengguna dan antrian.

MediFlow dirancang agar proses antrian klinik menjadi lebih mudah, cepat, dan terstruktur. Pasien dapat login, memilih poli, mengisi data antrian, mendapatkan nomor antrian digital, melihat status antrian, serta melihat riwayat antrian. Admin atau petugas klinik dapat login, melihat daftar antrian hari ini, memanggil pasien, mengubah status pelayanan, dan melihat riwayat pelayanan.

---

## 2. Latar Belakang

Pada sistem antrian klinik konvensional, pasien biasanya harus datang langsung ke lokasi klinik untuk mengambil nomor antrian. Hal ini dapat menyebabkan penumpukan pasien di ruang tunggu, waktu tunggu yang tidak jelas, dan pengelolaan data yang kurang efisien. Selain itu, petugas klinik perlu mencatat dan memanggil pasien secara manual, sehingga rawan terjadi kesalahan urutan atau kehilangan data.

MediFlow hadir sebagai solusi digital untuk membantu pasien mengambil nomor antrian dan memantau status antrian melalui aplikasi. Dengan dukungan Supabase, data antrian dapat disimpan secara online sehingga lebih mudah diakses, dikelola, dan diperbarui oleh petugas klinik.

---

## 3. Tujuan Produk

Tujuan pengembangan MediFlow adalah:

1. Membuat aplikasi antrian klinik berbasis Flutter yang memiliki alur penggunaan seperti aplikasi klinik nyata.
2. Menyediakan fitur login dan register menggunakan Supabase Authentication.
3. Menyimpan data pengguna, layanan poli, dan antrian menggunakan Supabase Database.
4. Menghilangkan pemilihan role manual pada halaman login agar role pengguna dibaca langsung dari database.
5. Memudahkan pasien mengambil nomor antrian dan memantau status antrian.
6. Memudahkan admin mengelola, memanggil, dan menyelesaikan antrian pasien.
7. Mendukung kerja kelompok melalui pembagian modul, branch Git, dan pull request.

---

## 4. Ruang Lingkup Produk

### 4.1 Fitur yang Termasuk

Fitur utama yang termasuk dalam project MediFlow:

1. Splash screen dan welcome screen.
2. Login menggunakan email dan password.
3. Register akun pasien.
4. Pengambilan role pengguna dari tabel `profiles` di Supabase.
5. Dashboard pasien.
6. Pilihan poli atau layanan klinik.
7. Form pendaftaran antrian pasien.
8. Tiket antrian digital.
9. Halaman antrian saya.
10. Riwayat antrian pasien.
11. Dashboard admin.
12. Daftar antrian hari ini.
13. Pemanggilan antrian oleh admin.
14. Perubahan status antrian.
15. Riwayat pelayanan admin.
16. Integrasi Supabase untuk Auth dan Database.

### 4.2 Fitur yang Tidak Termasuk

Fitur berikut tidak menjadi prioritas untuk versi UAS:

1. Pembayaran online.
2. Rekam medis lengkap pasien.
3. Chat dokter dan pasien.
4. Notifikasi push real-time.
5. Video konsultasi.
6. Multi-cabang klinik.
7. Integrasi BPJS atau asuransi.

---

## 5. Target Pengguna

### 5.1 Pasien

Pasien adalah pengguna aplikasi yang ingin mengambil nomor antrian klinik secara digital. Pasien dapat memilih layanan, mengisi data, mendapatkan nomor antrian, melihat status antrian, dan melihat riwayat kunjungan.

### 5.2 Admin atau Petugas Klinik

Admin adalah pengguna yang bertugas mengelola antrian. Admin dapat melihat daftar pasien, memanggil nomor antrian, mengubah status pasien menjadi dipanggil, dilayani, selesai, dilewati, atau dibatalkan.

---

## 6. Konsep Role Pengguna

Aplikasi tidak menggunakan pilihan role pada halaman login. Pengguna cukup memasukkan email dan password. Setelah login berhasil, aplikasi akan mengambil data role dari tabel `profiles` di Supabase.

Alur role:

```text
User memasukkan email dan password
↓
Supabase Auth memvalidasi akun
↓
Aplikasi mengambil data user dari tabel profiles
↓
Jika role = pasien, user diarahkan ke dashboard pasien
Jika role = admin, user diarahkan ke dashboard admin
```

Role yang digunakan:

| Role | Keterangan |
|---|---|
| pasien | Pengguna biasa yang mengambil nomor antrian |
| admin | Petugas klinik yang mengelola antrian |

Catatan penting:

1. Pasien dapat register melalui aplikasi.
2. Role pasien dibuat otomatis saat register.
3. Akun admin sebaiknya dibuat manual melalui Supabase agar pengguna biasa tidak bisa mendaftar sebagai admin.

---

## 7. Alur Utama Aplikasi

### 7.1 Alur Pasien

```text
Splash Screen
↓
Welcome Screen
↓
Login atau Register
↓
Dashboard Pasien
↓
Pilih Poli
↓
Isi Form Antrian
↓
Dapat Tiket Antrian Digital
↓
Lihat Antrian Saya
↓
Pantau Status Antrian
↓
Lihat Riwayat Antrian
```

### 7.2 Alur Admin

```text
Splash Screen
↓
Welcome Screen
↓
Login
↓
Dashboard Admin
↓
Lihat Daftar Antrian Hari Ini
↓
Panggil Pasien Berikutnya
↓
Ubah Status Antrian
↓
Selesai atau Lewati Pasien
↓
Lihat Riwayat Pelayanan
```

---

## 8. Kebutuhan Fitur Detail

## 8.1 Modul Auth dan Supabase

### Deskripsi

Modul ini bertanggung jawab terhadap sistem login, register, logout, koneksi Supabase, dan pengecekan role pengguna.

### Fitur

1. Login dengan email dan password.
2. Register akun pasien.
3. Logout.
4. Membaca data role dari tabel `profiles`.
5. Mengarahkan pengguna berdasarkan role.
6. Menampilkan pesan error jika login gagal.
7. Menghapus alur pilih role manual.

### Acceptance Criteria

1. Pengguna dapat login menggunakan email dan password.
2. Pasien baru dapat membuat akun melalui halaman register.
3. Setelah login, aplikasi otomatis membaca role dari Supabase.
4. Pengguna role pasien masuk ke dashboard pasien.
5. Pengguna role admin masuk ke dashboard admin.
6. Tidak ada tombol pilih role pada halaman login.
7. Logout berhasil mengembalikan pengguna ke halaman login.

---

## 8.2 Modul Pasien

### Deskripsi

Modul pasien adalah bagian aplikasi yang digunakan oleh pasien untuk mengambil dan memantau nomor antrian klinik.

### Fitur

1. Dashboard pasien.
2. Menampilkan sapaan pengguna.
3. Menampilkan ringkasan antrian aktif pasien.
4. Menampilkan pilihan poli.
5. Form pendaftaran antrian.
6. Pembuatan nomor antrian.
7. Tiket antrian digital.
8. Halaman antrian saya.
9. Riwayat antrian pasien.
10. Tombol batal antrian jika status masih `menunggu`.

### Data yang Dibutuhkan

1. Nama pasien.
2. Umur.
3. Jenis kelamin.
4. Nomor HP.
5. Poli yang dipilih.
6. Keluhan singkat.
7. Nomor antrian.
8. Status antrian.
9. Tanggal antrian.

### Acceptance Criteria

1. Pasien dapat melihat dashboard setelah login.
2. Pasien dapat memilih poli yang tersedia.
3. Pasien dapat mengisi form antrian dengan validasi sederhana.
4. Pasien mendapat nomor antrian otomatis setelah form dikirim.
5. Nomor antrian tersimpan ke Supabase.
6. Pasien dapat melihat status antrian miliknya.
7. Pasien dapat melihat riwayat antrian.
8. Pasien hanya dapat melihat data antriannya sendiri.

---

## 8.3 Modul Admin dan Manajemen Antrian

### Deskripsi

Modul admin digunakan oleh petugas klinik untuk memantau dan mengelola antrian pasien.

### Fitur

1. Dashboard admin.
2. Menampilkan jumlah antrian hari ini.
3. Menampilkan jumlah pasien menunggu.
4. Menampilkan nomor yang sedang dipanggil.
5. Menampilkan daftar antrian hari ini.
6. Fitur panggil pasien.
7. Fitur ubah status menjadi `dipanggil`.
8. Fitur ubah status menjadi `dilayani`.
9. Fitur ubah status menjadi `selesai`.
10. Fitur ubah status menjadi `dilewati`.
11. Filter antrian berdasarkan poli.
12. Riwayat pelayanan.

### Acceptance Criteria

1. Admin dapat melihat semua antrian hari ini.
2. Admin dapat memanggil pasien berikutnya.
3. Status antrian berubah sesuai aksi admin.
4. Admin dapat menandai pasien selesai dilayani.
5. Admin dapat melewati pasien yang tidak hadir.
6. Admin dapat melihat riwayat pelayanan.
7. Pasien tidak dapat mengakses halaman admin.

---

## 9. Status Antrian

Status yang digunakan dalam aplikasi:

| Status | Keterangan |
|---|---|
| menunggu | Pasien sudah mengambil nomor antrian dan belum dipanggil |
| dipanggil | Pasien sedang dipanggil oleh admin |
| dilayani | Pasien sedang mendapatkan pelayanan |
| selesai | Pelayanan pasien sudah selesai |
| dilewati | Pasien tidak hadir saat dipanggil |
| dibatalkan | Pasien membatalkan antrian |

Alur normal:

```text
menunggu → dipanggil → dilayani → selesai
```

Alur jika pasien tidak hadir:

```text
menunggu → dipanggil → dilewati
```

Alur jika pasien membatalkan:

```text
menunggu → dibatalkan
```

---

## 10. Struktur Database Supabase

## 10.1 Tabel `profiles`

Tabel ini menyimpan data tambahan pengguna setelah akun dibuat di Supabase Auth.

| Kolom | Tipe Data | Keterangan |
|---|---|---|
| id | uuid | Primary key, sama dengan id user dari Supabase Auth |
| full_name | text | Nama lengkap pengguna |
| phone | text | Nomor HP pengguna |
| role | text | Role pengguna, yaitu pasien atau admin |
| created_at | timestamp | Waktu data dibuat |

Contoh data:

```text
full_name: Rafa
phone: 08123456789
role: pasien
```

---

## 10.2 Tabel `services`

Tabel ini menyimpan daftar poli atau layanan klinik.

| Kolom | Tipe Data | Keterangan |
|---|---|---|
| id | bigint | Primary key |
| service_name | text | Nama poli atau layanan |
| code | text | Kode antrian |
| description | text | Deskripsi layanan |
| estimated_minutes | int | Estimasi waktu pelayanan per pasien |
| is_active | boolean | Status aktif layanan |
| created_at | timestamp | Waktu data dibuat |

Contoh data:

| service_name | code | estimated_minutes |
|---|---|---|
| Poli Umum | UM | 5 |
| Poli Gigi | GG | 7 |
| Poli Anak | AN | 6 |
| Laboratorium | LB | 10 |
| Farmasi | FR | 3 |

---

## 10.3 Tabel `queues`

Tabel ini menyimpan data antrian pasien.

| Kolom | Tipe Data | Keterangan |
|---|---|---|
| id | bigint | Primary key |
| user_id | uuid | ID pasien dari Supabase Auth |
| service_id | bigint | ID layanan atau poli |
| queue_number | text | Nomor antrian, contoh UM-001 |
| patient_name | text | Nama pasien |
| age | int | Umur pasien |
| gender | text | Jenis kelamin |
| complaint | text | Keluhan singkat |
| status | text | Status antrian |
| queue_date | date | Tanggal antrian |
| created_at | timestamp | Waktu antrian dibuat |

---

## 11. SQL Awal Supabase

SQL berikut dapat digunakan sebagai struktur awal database.

```sql
create table public.profiles (
  id uuid primary key references auth.users(id) on delete cascade,
  full_name text not null,
  phone text,
  role text not null default 'pasien'
    check (role in ('pasien', 'admin')),
  created_at timestamp with time zone default now()
);

create table public.services (
  id bigint primary key generated always as identity,
  service_name text not null,
  code text not null unique,
  description text,
  estimated_minutes int not null default 5,
  is_active boolean not null default true,
  created_at timestamp with time zone default now()
);

create table public.queues (
  id bigint primary key generated always as identity,
  user_id uuid not null references auth.users(id) on delete cascade,
  service_id bigint not null references public.services(id),
  queue_number text not null,
  patient_name text not null,
  age int,
  gender text,
  complaint text,
  status text not null default 'menunggu'
    check (status in ('menunggu', 'dipanggil', 'dilayani', 'selesai', 'dilewati', 'dibatalkan')),
  queue_date date not null default current_date,
  created_at timestamp with time zone default now()
);

insert into public.services (service_name, code, description, estimated_minutes)
values
('Poli Umum', 'UM', 'Layanan pemeriksaan umum pasien', 5),
('Poli Gigi', 'GG', 'Layanan pemeriksaan kesehatan gigi', 7),
('Poli Anak', 'AN', 'Layanan pemeriksaan anak', 6),
('Laboratorium', 'LB', 'Layanan pemeriksaan laboratorium', 10),
('Farmasi', 'FR', 'Layanan pengambilan obat', 3);
```

---

## 12. Row Level Security Supabase

Row Level Security atau RLS digunakan agar data lebih aman.

Aturan utama:

1. Pasien hanya dapat melihat dan membuat data antrian miliknya sendiri.
2. Admin dapat melihat dan mengubah semua data antrian.
3. Semua pengguna login dapat melihat daftar layanan yang aktif.

SQL awal:

```sql
alter table public.profiles enable row level security;
alter table public.services enable row level security;
alter table public.queues enable row level security;

create or replace function public.is_admin()
returns boolean
language sql
security definer
set search_path = public
as $$
  select exists (
    select 1
    from public.profiles
    where id = auth.uid()
    and role = 'admin'
  );
$$;

create policy "users can view own profile"
on public.profiles
for select
to authenticated
using (id = auth.uid());

create policy "users can update own profile"
on public.profiles
for update
to authenticated
using (id = auth.uid())
with check (id = auth.uid());

create policy "authenticated users can view services"
on public.services
for select
to authenticated
using (is_active = true);

create policy "users can view own queues or admins can view all"
on public.queues
for select
to authenticated
using (user_id = auth.uid() or public.is_admin());

create policy "users can create own queues"
on public.queues
for insert
to authenticated
with check (user_id = auth.uid());

create policy "admins can update all queues"
on public.queues
for update
to authenticated
using (public.is_admin())
with check (public.is_admin());
```

---

## 13. Struktur Project Flutter yang Direkomendasikan

Struktur project saat ini sudah dipisah berdasarkan fitur. Struktur yang direkomendasikan:

```text
lib/
├── data/
│   └── dummy_data.dart
├── features/
│   ├── auth/
│   │   ├── login_page.dart
│   │   ├── register_page.dart
│   │   └── welcome_screen.dart
│   ├── user/
│   │   ├── user_dashboard_page.dart
│   │   ├── registration_form_page.dart
│   │   ├── my_queue_page.dart
│   │   ├── patient_history_page.dart
│   │   └── queue_ticket_page.dart
│   └── admin/
│       ├── admin_dashboard_page.dart
│       ├── admin_queue_list_page.dart
│       ├── call_queue_page.dart
│       ├── called_queue_page.dart
│       └── admin_history_page.dart
├── services/
│   ├── auth_service.dart
│   ├── polyclinic_service.dart
│   ├── queue_service.dart
│   └── tts_service.dart
├── shared/
│   └── widgets/
│       └── mediflow_widgets.dart
└── main.dart
```

Catatan revisi:

1. `role_selection_page.dart` tidak perlu digunakan lagi dalam alur login.
2. File `dummy_data.dart` dapat dipakai sementara, tetapi target akhir data berasal dari Supabase.
3. File `main.dart` sebaiknya hanya sering diubah oleh anggota yang bertanggung jawab pada routing dan integrasi utama.

---

## 14. Pembagian Tugas Kelompok

Pembagian tugas disusun menjadi 3 modul utama agar pekerjaan lebih jelas dan tidak saling bertabrakan. Setiap anggota bertanggung jawab pada modul, branch, dan file kerja masing-masing.

| Modul | Penanggung Jawab | Branch | Fokus Utama |
|---|---|---|---|
| Auth dan Supabase/Login | Sekar Paramitha Galuh | `feature/auth-supabase` | Login, register, logout, koneksi Supabase, dan pengecekan role pengguna |
| Halaman Pasien | Natasha Salsha Bila | `feature/patient-pages` | Dashboard pasien, pilih poli, form antrian, tiket digital, status, dan riwayat pasien |
| Admin dan Manajemen Antrian | Pradina Aulia Resti | `feature/admin-queue` | Dashboard admin, daftar antrian, panggil pasien, ubah status, dan riwayat pelayanan |

### 14.1 Modul 1: Auth dan Supabase/Login

**Penanggung Jawab:** Sekar Paramitha Galuh  
**Branch:** `feature/auth-supabase`

**Tanggung jawab:**

1. Menghubungkan Flutter dengan Supabase.
2. Menambahkan dependency `supabase_flutter`.
3. Mengatur inisialisasi Supabase di `main.dart`.
4. Membuat login email dan password.
5. Membuat register pasien.
6. Membuat logout.
7. Membaca role dari tabel `profiles`.
8. Mengarahkan pengguna berdasarkan role.
9. Menghapus alur pilih role manual.
10. Membuat script database dan RLS di Supabase.

**File utama:**

```text
lib/main.dart
lib/features/auth/login_page.dart
lib/features/auth/welcome_screen.dart
lib/features/auth/register_page.dart
lib/services/auth_service.dart
```

---

### 14.2 Modul 2: Halaman Pasien

**Penanggung Jawab:** Natasha Salsha Bila  
**Branch:** `feature/patient-pages`

**Tanggung jawab:**

1. Membuat dan menyempurnakan dashboard pasien.
2. Menampilkan daftar poli.
3. Membuat form ambil antrian.
4. Membuat tiket antrian digital.
5. Menampilkan halaman antrian saya.
6. Menampilkan status antrian pasien.
7. Menampilkan riwayat antrian pasien.
8. Membuat tampilan kosong jika belum ada antrian.
9. Membuat validasi input form.
10. Menyesuaikan UI dengan tema MediFlow.

**File utama:**

```text
lib/features/user/user_dashboard_page.dart
lib/features/user/registration_form_page.dart
lib/features/user/my_queue_page.dart
lib/features/user/patient_history_page.dart
lib/features/user/queue_ticket_page.dart
```

---

### 14.3 Modul 3: Admin dan Manajemen Antrian

**Penanggung Jawab:** Pradina Aulia Resti  
**Branch:** `feature/admin-queue`

**Tanggung jawab:**

1. Membuat dashboard admin.
2. Menampilkan statistik antrian harian.
3. Menampilkan daftar antrian hari ini.
4. Membuat fitur panggil pasien.
5. Membuat fitur pasien sedang dilayani.
6. Membuat fitur selesai pelayanan.
7. Membuat fitur lewati pasien.
8. Membuat filter berdasarkan poli.
9. Membuat riwayat pelayanan admin.
10. Menyesuaikan UI admin dengan tema MediFlow.

**File utama:**

```text
lib/features/admin/admin_dashboard_page.dart
lib/features/admin/admin_queue_list_page.dart
lib/features/admin/call_queue_page.dart
lib/features/admin/called_queue_page.dart
lib/features/admin/admin_history_page.dart
lib/services/queue_service.dart
```

---

## 15. Aturan Kolaborasi Git dan VS Code

Aturan kerja kelompok:

1. Branch `main` hanya digunakan untuk kode yang sudah stabil.
2. Setiap anggota wajib mengerjakan fitur di branch masing-masing.
3. Jangan push langsung ke branch `main`.
4. Sebelum mulai mengerjakan fitur, lakukan `pull` dari branch `main`.
5. Setiap fitur yang selesai harus dibuat commit.
6. Setelah selesai, push branch ke GitHub.
7. Gabungkan perubahan ke `main` melalui Pull Request.
8. Hindari mengedit file yang sama secara bersamaan tanpa diskusi.
9. File `main.dart` sebaiknya dikelola oleh anggota yang memegang modul Auth dan Supabase.
10. Jika terjadi conflict, diskusikan bagian kode mana yang harus dipakai.

Contoh command Git:

```bash
git checkout main
git pull origin main
git checkout -b feature/patient-pages
git add .
git commit -m "feat: add patient queue pages"
git push origin feature/patient-pages
```

---

## 16. Standar Penamaan Commit

Gunakan format commit yang jelas:

| Prefix | Fungsi | Contoh |
|---|---|---|
| feat | Menambahkan fitur baru | `feat: add patient dashboard` |
| fix | Memperbaiki bug | `fix: repair login validation` |
| style | Mengubah tampilan tanpa mengubah logika | `style: update queue card layout` |
| refactor | Merapikan struktur kode | `refactor: split patient pages` |
| docs | Mengubah dokumentasi | `docs: update PRD` |

---

## 17. Kebutuhan Non-Fungsional

### 17.1 Tampilan

1. Tampilan harus rapi, bersih, dan sesuai tema klinik.
2. Warna utama mengikuti logo MediFlow, yaitu hijau tosca, biru tua, dan putih.
3. Tombol utama harus mudah terlihat.
4. Status antrian harus dibedakan dengan warna.
5. Tampilan harus nyaman digunakan pada layar Android.

### 17.2 Keamanan

1. Password tidak disimpan manual di database aplikasi.
2. Login menggunakan Supabase Authentication.
3. Role pengguna disimpan di tabel `profiles`.
4. Pasien tidak boleh mengakses halaman admin.
5. Pasien hanya dapat melihat antriannya sendiri.

### 17.3 Performa

1. Aplikasi harus dapat menampilkan data antrian tanpa loading terlalu lama.
2. Query data harus dibatasi sesuai kebutuhan.
3. Data antrian hari ini harus dapat difilter berdasarkan tanggal.

### 17.4 Kemudahan Penggunaan

1. Pasien dapat mengambil antrian dengan langkah yang sederhana.
2. Admin dapat mengubah status antrian melalui tombol yang jelas.
3. Pesan error dan sukses harus mudah dipahami.

---

## 18. Dependensi Flutter

Dependensi utama yang dibutuhkan:

```yaml
dependencies:
  flutter:
    sdk: flutter
  supabase_flutter: ^2.0.0
  intl: ^0.19.0
  flutter_tts: ^4.0.0
  audioplayers: ^6.0.0
```

Catatan:

1. Versi dependency dapat disesuaikan dengan versi Flutter yang digunakan kelompok.
2. `supabase_flutter` digunakan untuk Auth dan Database.
3. `intl` digunakan untuk format tanggal dan waktu.
4. `flutter_tts` dan `audioplayers` dapat digunakan untuk fitur pemanggilan antrian jika tetap dipakai.

---

## 19. Validasi Form

Validasi minimal untuk form antrian pasien:

| Field | Validasi |
|---|---|
| Nama pasien | Wajib diisi |
| Umur | Wajib diisi dan berupa angka |
| Jenis kelamin | Wajib dipilih |
| Poli | Wajib dipilih |
| Keluhan | Wajib diisi singkat |

Pesan error harus sederhana, misalnya:

```text
Nama pasien wajib diisi.
Umur harus berupa angka.
Silakan pilih poli terlebih dahulu.
Keluhan wajib diisi.
```

---

## 20. Nomor Antrian

Format nomor antrian menggunakan kode poli dan nomor urut harian.

Contoh:

| Poli | Kode | Contoh Nomor |
|---|---|---|
| Poli Umum | UM | UM-001 |
| Poli Gigi | GG | GG-001 |
| Poli Anak | AN | AN-001 |
| Laboratorium | LB | LB-001 |
| Farmasi | FR | FR-001 |

Logika sederhana:

```text
Nomor berikutnya = jumlah antrian pada poli tersebut di tanggal hari ini + 1
```

Contoh:

```text
Hari ini sudah ada UM-001, UM-002, UM-003
Pasien berikutnya mendapat UM-004
```

---

## 21. Estimasi Waktu Tunggu

Estimasi waktu tunggu dihitung dari jumlah pasien yang masih menunggu sebelum pasien tersebut.

Rumus:

```text
Estimasi = jumlah pasien sebelum pasien × estimasi menit per poli
```

Contoh:

```text
Pasien mendapat nomor UM-006
Nomor yang sedang dilayani UM-003
Sisa antrian sebelum pasien = 3
Estimasi per pasien = 5 menit
Estimasi tunggu = 3 × 5 = 15 menit
```

---

## 22. Skenario Demo UAS

Skenario demo yang direkomendasikan:

1. Buka aplikasi MediFlow.
2. Tampilkan splash screen dan welcome screen.
3. Login sebagai pasien.
4. Pasien membuka dashboard.
5. Pasien memilih poli.
6. Pasien mengisi form antrian.
7. Sistem membuat nomor antrian digital.
8. Pasien melihat halaman antrian saya.
9. Logout pasien.
10. Login sebagai admin.
11. Admin melihat daftar antrian hari ini.
12. Admin menekan tombol panggil.
13. Status pasien berubah menjadi `dipanggil`.
14. Admin mengubah status menjadi `dilayani`.
15. Admin mengubah status menjadi `selesai`.
16. Data masuk ke riwayat pelayanan.

---

## 23. Timeline Pengembangan

| Tahap | Kegiatan | Output |
|---|---|---|
| Tahap 1 | Analisis project lama dan penyusunan PRD | PRD selesai |
| Tahap 2 | Setup Supabase dan database | Tabel dan RLS tersedia |
| Tahap 3 | Implementasi Auth | Login, register, logout |
| Tahap 4 | Implementasi halaman pasien | Dashboard, form, tiket, riwayat |
| Tahap 5 | Implementasi halaman admin | Dashboard admin dan kelola antrian |
| Tahap 6 | Integrasi final | Semua modul tersambung |
| Tahap 7 | Testing dan perbaikan UI | Aplikasi siap demo |

---

## 24. Risiko dan Solusi

| Risiko | Dampak | Solusi |
|---|---|---|
| Conflict Git karena file yang sama diedit banyak orang | Kode sulit digabung | Bagi file kerja berdasarkan modul |
| Supabase gagal connect | Login dan database tidak berjalan | Cek URL, publishable key, dan dependency |
| RLS terlalu ketat | Data tidak muncul di aplikasi | Periksa policy Supabase |
| Role tidak terbaca | User tidak diarahkan ke halaman yang benar | Pastikan data `profiles` dibuat setelah register |
| Nomor antrian bentrok | Data antrian tidak rapi | Untuk versi UAS gunakan testing satu perangkat, untuk versi lanjut gunakan fungsi database |
| UI tidak konsisten | Aplikasi terlihat kurang profesional | Gunakan shared widget dan tema warna yang sama |

---

## 25. Indikator Keberhasilan

Project MediFlow dianggap berhasil jika:

1. Aplikasi dapat berjalan di perangkat atau emulator Android.
2. Pengguna dapat register sebagai pasien.
3. Pengguna dapat login menggunakan Supabase.
4. Role pengguna terbaca dari Supabase.
5. Pasien dapat mengambil nomor antrian.
6. Data antrian tersimpan di Supabase.
7. Pasien dapat melihat antrian miliknya.
8. Admin dapat melihat daftar antrian pasien.
9. Admin dapat mengubah status antrian.
10. Alur demo UAS dapat dijalankan dari awal sampai akhir.

---

## 26. Kesimpulan

MediFlow adalah aplikasi antrian klinik digital berbasis Flutter dan Supabase yang dirancang untuk memudahkan pasien dalam mengambil nomor antrian serta membantu admin mengelola antrian secara lebih terstruktur. Aplikasi ini menggunakan sistem login email dan password, role pengguna dari database, serta penyimpanan data antrian melalui Supabase.

Dengan pembagian kerja menjadi tiga modul utama, yaitu Auth dan Supabase, Halaman Pasien, serta Admin dan Manajemen Antrian, pengembangan project dapat dilakukan secara lebih rapi dan aman. Penggunaan branch Git membantu setiap anggota kelompok mengerjakan tugas masing-masing tanpa mengganggu kode utama.
