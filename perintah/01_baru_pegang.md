# 01. Baru pegang atau mau mulai rapiin

**Istilah:** `code audit` `characterization test`

Tools udah jalan tapi kamu belum yakin isinya. Langkah pertama bukan memperbaiki, tapi **memotret kondisi sekarang**, biar tiap perubahan nanti ada pembandingnya.

> Pakai perintah pertama di bawah duluan, sebelum perintah lain di seluruh repo ini.

---

## Audit menyeluruh

```text
Audit basis kode ini tanpa mengubah apa pun. Petakan: (1) semua fitur dan alur utamanya, (2) titik rawan bug atau celah keamanan, (3) utang teknis yang paling berbahaya, (4) bagian yang belum punya test sama sekali. Sajikan sebagai laporan berurutan dari yang paling mendesak. Jangan langsung memperbaiki apa pun.
```

## Peta arsitektur

```text
Buatkan peta arsitektur aplikasi ini: komponen utama, alur data antar komponen, dependensi eksternal (API pihak ketiga, database, cron atau background job), dan file konfigurasi penting. Format: diagram sederhana plus penjelasan singkat per komponen, supaya orang non teknis pun paham.
```

## Characterization test, pagar sebelum nyentuh

```text
Buat characterization test untuk alur-alur utama aplikasi ini. Rekam perilaku yang SEKARANG terjadi, benar maupun salah, sebagai baseline, supaya ketahuan kalau ada perilaku yang berubah setelah kita menyentuh kode. Kalau menemukan bug saat merekam, jangan diperbaiki dulu: catat saja di daftar terpisah.
```

Bedanya sama unit test biasa: dia merekam "apa adanya", bukan "seharusnya".

---

[Kembali ke daftar isi](../README.md)
