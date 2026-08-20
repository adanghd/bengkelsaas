# 03. Mau nambah atau ubah fitur

**Istilah:** `regression test` `impact analysis` `feature flag` `refactoring`

Momen paling rawan di tools berjalan: perubahan baru diam-diam matahin fitur lama. Semua perintah di sini intinya satu, **fitur lama harus kebukti tetap hidup**.

---

## Analisis dampak dulu

```text
Saya mau mengubah [BAGIAN ATAU FITUR]. Sebelum menyentuh kode, analisis dampaknya: file dan fitur apa saja yang bergantung pada bagian ini, alur mana yang perilakunya bisa ikut berubah, dan skenario terburuknya apa. Setelah itu baru usulkan cara paling aman melakukannya, bertahap.
```

## Regression sebelum dan sesudah

```text
Saya mau mengubah [FITUR]. Prosedurnya wajib begini: (1) jalankan atau buat dulu test untuk semua fitur yang bersinggungan, catat hasilnya sebagai baseline; (2) lakukan perubahannya; (3) jalankan ulang test yang sama dan laporkan perbandingannya. Kalau ada fitur lama yang rusak, perbaiki dulu sampai hijau sebelum lanjut apa pun.
```

## Fitur baru di balik feature flag

```text
Implementasikan fitur [NAMA FITUR] di balik feature flag yang mati secara default. Saya harus bisa menyalakannya hanya untuk diri sendiri dulu buat uji coba, dan mematikannya seketika tanpa deploy ulang kalau bermasalah. Tunjukkan di mana tombol atau config untuk menyalakan dan mematikannya.
```

## Refactor tanpa ubah perilaku

```text
Refactor [BAGIAN] supaya lebih rapi dan mudah dirawat, dengan syarat mutlak: perilaku ke user harus persis sama. Kerjakan bertahap dalam langkah-langkah kecil, dan setelah tiap langkah jalankan test untuk membuktikan tidak ada yang berubah. Kalau ada godaan "sekalian perbaiki ini itu", tahan, catat saja sebagai usulan terpisah.
```

---

[Kembali ke daftar isi](../README.md)
