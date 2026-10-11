# Aktivasi hapus Log of Revision khusus admin

Pembaruan ini menambah satu Firebase callable: portalManageRevisions, dan memperbarui portalListRevisions serta portalRevisionDetail.

1. Ekstrak firebase-revision-log-update.zip ke folder baru.
2. Buka terminal di folder firebase-admin hasil ekstrak.
3. Jalankan:

```bat
npm --prefix functions ci
firebase deploy --only functions:manual-portal --project ecrew-absensi-183ac
```

Gunakan akun Firebase yang sebelumnya berhasil deploy. Jika diminta login oleh Firebase CLI, ikuti login resmi. Tidak perlu membuat admin baru, menjalankan bootstrap, atau mengganti Firestore rules.

Sesudah muncul Deploy complete!, buka aplikasi dan tekan Ctrl + Shift + R. Login admin, lalu buka Log of Revision.

- Hapus log: satu catatan, dengan konfirmasi.
- Hapus seluruh log: semua catatan OM A-D yang tersimpan saat perintah dijalankan, termasuk catatan yang belum dimuat atau di luar filter.
- Log terhapus: hanya admin; tombol Pulihkan mengembalikan satu catatan.
- Penghapusan tidak mengubah isi manual, versi cloud, akun, maupun nomor revisi. Catatan disembunyikan secara dapat dipulihkan, bukan dihapus permanen dari database.
- Revisi baru setelah penghapusan seluruh log tetap tercatat otomatis.
- User biasa tetap dapat membaca log aktif, tetapi server menolak semua operasi hapus/pulihkan dan akses log terhapus.

Pemeriksaan: 12 backend tests lolos, termasuk akses admin, hapus satu, hapus semua, pulihkan, detail log terhapus, revisi baru setelah clear, dan retensi snapshot; pemeriksaan antarmuka admin/user juga lolos.
