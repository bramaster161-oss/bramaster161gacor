# BRAMASTER161 — backend akun bersama

## Yang diperbaiki
- Pendaftaran dan login pengguna menggunakan API server, bukan daftar akun lokal browser.
- Akun disimpan di file database server `data/database.json` (persisten jika DATA_DIR berada di disk persisten).
- Admin dapat melihat daftar akun yang terdaftar di server dan mengaktifkan/menonaktifkan akun.
- Password disimpan sebagai hash scrypt + salt, bukan plaintext.

## Penting
File HTML aslinya juga menyimpan hasil, jadwal, transaksi/withdrawal, rekening deposit, dan saldo dalam `localStorage`. Paket ini belum memindahkan semua modul itu ke database bersama. Yang sudah dihubungkan adalah autentikasi/registrasi serta daftar/status akun. Jangan gunakan untuk uang atau data sensitif sebelum modul lain dipindahkan dan diuji.

## Deploy di Render
1. Upload seluruh isi folder ini ke repository GitHub baru atau folder proyek backend.
2. Di Render pilih **New + → Blueprint** lalu pilih repository dan deploy `render.yaml`.
3. Isi `ADMIN_USERNAME` (misalnya nama admin baru) dan `ADMIN_PASSWORD` dengan password acak minimal 12 karakter. Jangan pakai password contoh dan jangan commit rahasia ke GitHub.
4. Untuk frontend di GitHub Pages, setelah backend aktif edit `public/index.html` bagian awal dan set `window.BRAMASTER_API_URL = 'https://NAMA-SERVICE.onrender.com';` sebelum script aplikasi berjalan. Bila frontend di-host pada service yang sama, biarkan string kosong.
5. Set `ALLOWED_ORIGIN` di Render ke origin frontend persis, misalnya `https://bramaster161-oss.github.io` (tanpa path `/bramaster161/`).
6. Perlu diingat cookie lintas situs dapat dibatasi browser. Untuk hasil paling stabil, hosting frontend dan API di origin yang sama atau gunakan domain khusus yang sama.

## Lokal
- Instal Node.js 20 atau lebih baru.
- `npm install`
- Atur `ADMIN_USERNAME` dan `ADMIN_PASSWORD` di environment.
- `npm start`
- Buka `http://localhost:3000`.

## Data akun lama
Akun yang sebelumnya hanya tersimpan di localStorage browser tidak otomatis ikut ke database server. Pengguna perlu mendaftar ulang, atau akun lama harus diekspor dan diimpor dengan proses aman.
