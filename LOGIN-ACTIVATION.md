# Aktivasi login dan Log of Revision

Status: kode siap diuji/deploy. Backend dan akun admin belum diaktifkan di Firebase produksi. Halaman utama lama tetap aktif sampai seluruh langkah di bawah selesai.

## Fitur

- Login username/password menggunakan Firebase Authentication Email/Password.
- Username `admin` untuk akun administrator awal. Password awal dimasukkan secara privat saat bootstrap, sesuai password yang diminta pemilik; password tidak ada dalam paket/kode publik.
- Admin menambah, mengedit nama/username, mengganti password, dan menghapus akses user. Password disamarkan dan tidak dapat dibaca kembali. Penghapusan menonaktifkan akun serta mencabut sesi; identitas tetap dipertahankan untuk riwayat.
- User dan admin mengakses manual A–D serta riwayat revisi yang sama.
- Backend menghitung teks tambahan/hapus dari snapshot sebelum dan sesudah, mencatat UID/nama/username, manual, chapter, nomor halaman, perubahan metadata/format, dan timestamp server. Tampilan tanggal/jam memakai Asia/Jakarta.
- Riwayat hanya mencakup perubahan yang disimpan setelah aktivasi. Tidak menebak editor perubahan lama.
- Snapshot lama pada `operationsManualPortal/transwisata/workspace/current` tetap kompatibel. Tidak perlu menghapus atau mengimpor ulang manual.

## Langkah pemilik Firebase

Gunakan komputer/terminal pribadi atau Google Cloud Shell yang terhubung ke proyek `ecrew-absensi-183ac`. Jangan masukkan password atau file service account ke GitHub maupun chat.

1. Cadangkan manual dari aplikasi lama dan simpan salinan aturan Firestore produksi yang sedang aktif. Pastikan aturan produksi masih sama dengan aturan lama yang menjadi dasar file ini. Jika sudah berubah, gabungkan pengecualian portal ke aturan terbaru dan pertahankan aturan aplikasi lain.
2. Dari folder `firebase-admin`, jalankan:

   ```bash
   npm --prefix functions ci
   npx firebase-tools login
   npx firebase-tools deploy --only functions:manual-portal --project ecrew-absensi-183ac
   ```

3. Buat akun admin awal dengan kredensial pemilik proyek. Gunakan Google Application Default Credentials milik pemilik proyek, lalu bootstrap meminta password dengan input tersembunyi:

   ```bash
   gcloud auth application-default login
   gcloud auth application-default set-quota-project ecrew-absensi-183ac
   node scripts/bootstrap-admin.cjs
   ```

   Script menolak mereset akun admin yang sudah ada. Untuk metode Firebase Console, buat akun Email/Password `admin@manual.transwisata.internal`, masukkan password sendiri, catat UID, lalu buat dokumen `operationsManualPortal/transwisata/members/<UID>` dengan `name: "Administrator"`, `username: "admin"`, `role: "admin"`, `active: true`. Tidak ada password dalam dokumen Firestore.

4. Uji login pada `login-admin-preview.html`. Pastikan administrator bisa membuka manual lama dan Log of Revision. Pastikan pengguna biasa tidak dapat menjalankan pengelolaan akun. Buat perubahan uji hanya pada manual yang memang boleh diubah, kemudian periksa isi log.
5. **Cutover:** setelah backend/admin terverifikasi, salin `login-admin-preview.html` sebagai `index.html` pada repository dan deploy aturan:

   ```bash
   npx firebase-tools deploy --only firestore:rules --project ecrew-absensi-183ac
   ```

   Kedua perubahan harus dilakukan dalam jendela cutover yang sama. Setelah aturan aktif, versi klien lama tidak dapat menulis langsung atau mengakses sebagai anonymous. Jangan hanya menambahkan blok aturan baru di bawah blanket allow lama: Firestore menggabungkan izin overlapping dengan OR sehingga login bisa dilewati.
6. Setelah GitHub Pages selesai deploy, refresh aplikasi dan uji lagi login admin, user, logout, upload, serta audit. Tidak perlu mematikan Anonymous untuk seluruh proyek karena aplikasi lain mungkin menggunakannya; akses anonymous ke portal sudah ditolak aturan/backend.

## Pengujian lokal

```bash
npm --prefix functions test
```

Tes akun/audit berjalan dengan datastore palsu, tidak menulis data produksi. Tes aturan menggunakan emulator melalui `firebase emulators:exec` dan tidak memakai Firestore produksi.

## Catatan operasional

- Versi cloud dan audit dipertahankan; pemakaian Firestore bertambah seiring revisi. Atur retensi/arsip tersendiri jika diperlukan, jangan menghapus snapshot yang masih menjadi sumber audit tanpa arsip.
- Autocomplete password/login dikelola Firebase/browser; password user tidak disimpan dalam backup manual atau IndexedDB aplikasi.
- Sebelum logout, simpan perubahan tertunda atau unduh backup. Salinan offline aplikasi lama tetap berada pada perangkat; gunakan perangkat perusahaan yang sesuai.
- Snapshot staging gagal tidak muncul pada log revisi. Backend hanya menampilkan versi dengan status `committed`.
- `maxInstances: 5` membatasi jumlah instance backend; tetap monitor billing proyek Blaze.
- `firestore.rules` hanya mempertahankan kebijakan lama bagi koleksi selain `operationsManualPortal`. Periksa aturan proyek terbaru sebelum deploy karena proyek juga digunakan aplikasi lain.
