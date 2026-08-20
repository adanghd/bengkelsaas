# 05. Mau deploy atau update produksi

**Istilah:** `staging` `pre deploy checklist` `smoke test` `rollback`

Produksi itu tempat user, bukan tempat eksperimen. Semua uji coba terjadi di staging; produksi cuma nerima barang yang udah kebukti.

---

## Siapkan staging

```text
Bantu saya menyiapkan lingkungan staging yang meniru produksi: konfigurasi yang sama, data contoh yang mirip (tanpa data asli user), dan dependensi yang sama. Mulai sekarang semua perubahan diuji di staging dulu. Jelaskan juga cara termudah menjaga staging tetap sinkron dengan produksi.
```

## Checklist pra deploy

```text
Buat checklist pra deploy untuk perubahan ini: (1) test apa saja yang harus hijau, (2) migrasi database yang terjadi dan cara MEMBATALKANNYA, (3) file config atau env yang berubah, (4) urutan langkah deploy. Untuk tiap poin, sertakan langkah rollback-nya. Jangan deploy sebelum semua poin tercentang.
```

## Smoke test habis deploy

```text
Deploy sudah selesai. Sekarang jalankan smoke test: cek alur terpenting yaitu [3 SAMPAI 5 ALUR, MISAL: LOGIN, HALAMAN UTAMA, TRANSAKSI, WEBHOOK] dan laporkan hasil tiap alur. Kalau ada satu saja yang gagal: rollback dulu ke versi sebelumnya, diagnosisnya belakangan.
```

---

[Kembali ke daftar isi](../README.md)
