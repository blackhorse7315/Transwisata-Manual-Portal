# Pembaruan Manual Library dan Log of Revision

Paket ini menggabungkan fitur manual tambahan dan fitur hapus/pulihkan log khusus admin. Gunakan paket ini sebagai pengganti paket pembaruan sebelumnya. Akun dan data manual yang sudah ada tetap digunakan.

## Aktivasi Firebase

1. Ekstrak firebase-manual-library-update.zip ke folder BARU, agar tidak tertukar dengan folder paket lama.
2. Buka terminal di folder firebase-admin hasil ekstrak.
3. Jalankan:

```bat
npm --prefix functions ci
firebase deploy --only functions:manual-portal --project ecrew-absensi-183ac
```

Jika perintah firebase belum dikenali, jalankan npm install -g firebase-tools terlebih dahulu. Jika Firebase meminta login, jalankan firebase login menggunakan akun Google pemilik proyek yang sebelumnya berhasil deploy.

Hasil deploy harus memuat total 9 fungsi, termasuk portalManageRevisions, lalu Deploy complete!. Tidak perlu membuat akun admin lagi, menjalankan bootstrap, atau mengubah Firestore rules.

## Memakai aplikasi

Tekan Ctrl + Shift + R pada aplikasi yang sudah diperbarui, kemudian login.

- Klik + Buat manual baru pada Manual library.
- Isi kode/nama singkat (contoh CMM, SMS, SEP) dan nama lengkap manual.
- Pilih template Standar, Seperti OM (Surat Pengantar dan Control Page DKPPU berupa image), atau Kosong.
- Centang halaman awal yang dibutuhkan: Front Page, Surat Pengantar, Control Page DKPPU, Document Control yang dapat diedit, List of Effective Pages, Record of Revision, Table of Contents.
- Klik Buat manual. Manual muncul di daftar berdampingan dengan OM A-D.
- Klik + Add content page untuk menambah isi; penomoran, font, logo, layout, revision bar dan tanda tangan tetap tersedia untuk setiap manual.
- Pilih halaman awal dapat menambah atau menyembunyikan halaman bawaan kemudian. Konten halaman yang disembunyikan dipertahankan.

Manual memiliki isi, metadata revisi, nomor halaman, LoEP, TOC dan pengaturan sendiri. Backup dan cloud menyimpan semua manual. Log of Revision dan filter manual mengenali manual tambahan dengan kode manualnya. Data OM A-D tetap dipertahankan. Maksimal 100 manual per workspace.

Penghapusan log hanya untuk admin, termasuk Hapus log, Hapus seluruh log untuk SEMUA manual, dan Pulihkan melalui Log terhapus. Penghapusan log tidak mengubah isi manual dan dapat dipulihkan.

Pemeriksaan: 13 tes backend lolos termasuk penyimpanan manual tambahan, log bernama manual baru, penolakan format rusak, proteksi OM A-D dan operasi log admin; tes antarmuka mencakup template, halaman awal, backup roundtrip, penomoran, filter dinamis dan kompatibilitas OM lama.
