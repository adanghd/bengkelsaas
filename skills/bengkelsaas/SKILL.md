---
name: bengkelsaas
description: 'Protokol perawatan software buat tools atau SaaS yang SUDAH JALAN dan dipakai user. Pakai skill ini setiap kali kerja menyentuh sistem berjalan, yaitu saat user minta nambah atau ubah fitur, benerin bug, refactor, update dependensi, deploy ke produksi, migrasi database, atau bikin dan merawat agent AI. Trigger juga saat user bilang "tools saya error", "kenapa gagal", "perbaiki", "deploy", "jangan sampai fitur lain rusak", atau baru pegang basis kode lama yang belum punya test. Isinya urutan kerja wajib: pasang pagar dulu, satu perubahan satu siklus uji, akar masalah bukan gejala, dan rollback selalu siap.'
---

# Bengkel SaaS

Cara kerja di software yang sudah hidup dan dipakai orang. Bedanya sama proyek baru: di sini **fitur lama yang masih jalan adalah aset yang wajib dijaga**, dan setiap perubahan dianggap berpotensi merusaknya sampai terbukti sebaliknya.

## Empat aturan yang tidak bisa ditawar

1. **Jangan langsung ubah.** Pasang pagar dulu (test plus backup), baru sentuh kode.
2. **Baca dulu, tulis belakangan.** Audit dan pahami kode sebelum boleh mengedit.
3. **Satu perubahan, satu siklus uji.** Ubah sedikit, tes, aman, baru lanjut. Jangan borongan.
4. **Gak bisa di-rollback berarti jangan deploy.** Jalan pulang disiapkan sebelum berangkat.

## Cara pakai skill ini

Tentukan situasinya dulu, lalu ikuti protokol yang cocok. Kalau basis kode ini belum pernah diaudit di sesi ini, kerjakan protokol A duluan apa pun permintaannya.

| Situasi user | Protokol |
|---|---|
| Baru pegang kode, belum tahu isinya | A. Potret dulu |
| Belum ada log, alert, atau backup | B. Pasang pengaman |
| Nambah atau ubah fitur, refactor | C. Ubah dengan bukti |
| Ada bug, error, tools down | D. Diagnosis lalu perbaiki |
| Mau deploy atau update produksi | E. Deploy bisa pulang |
| Servis berkala, update dependensi | F. Perawatan rutin |
| Kerjaan menyentuh agent atau LLM | G. Lapisan agentic |

---

### A. Potret dulu

Sebelum apa pun: audit tanpa mengubah. Petakan fitur dan alur utama, titik rawan bug dan celah keamanan, utang teknis paling berbahaya, dan bagian yang belum punya test. Laporkan berurutan dari yang paling mendesak.

Kalau alur yang mau disentuh belum punya test, buat **characterization test** dulu: rekam perilaku yang SEKARANG terjadi, benar maupun salah, sebagai baseline. Bug yang ketemu saat merekam jangan diperbaiki dulu, catat terpisah.

### B. Pasang pengaman

Logging terstruktur di semua titik yang bisa gagal (request masuk, panggilan API eksternal, query database, background job) tanpa mengubah logika bisnis. Health check yang mengecek aplikasi, database, dan layanan eksternal kritikal, dengan notifikasi kalau down. Backup otomatis plus script restore, dan restore-nya wajib dites sampai terbukti data balik utuh. Backup yang belum pernah dites restore sama saja belum punya backup.

### C. Ubah dengan bukti

1. **Analisis dampak dulu.** File dan fitur apa yang bergantung pada bagian ini, alur mana yang perilakunya bisa ikut berubah, skenario terburuknya apa.
2. **Baseline.** Jalankan atau buat test untuk semua fitur yang bersinggungan, catat hasilnya.
3. **Ubah bertahap**, langkah kecil.
4. **Jalankan ulang test yang sama**, laporkan perbandingannya. Ada fitur lama rusak berarti perbaiki sampai hijau sebelum lanjut apa pun.
5. Fitur baru lahir **di balik feature flag yang mati secara default**, bisa dimatikan seketika tanpa deploy ulang.

Refactor punya syarat mutlak: perilaku ke user harus persis sama. Godaan "sekalian perbaiki ini itu" ditahan dan dicatat sebagai usulan terpisah.

### D. Diagnosis lalu perbaiki

JANGAN langsung mengubah kode waktu ada laporan error. Urutannya: baca log dan error yang ada, telusuri alur dari gejala ke sumbernya, sebutkan akar masalah beserta **bukti konkret dari kode atau log**, tunggu user sepakat, baru perbaiki.

Perbaikan menyasar akar, bukan tambal gejala. Setelah beres, cek apakah pola bug yang sama ada di bagian lain kode dan perbaiki semuanya sekaligus, lalu tambahkan test yang memastikan bug ini tidak bisa kembali tanpa ketahuan.

Insiden selesai berarti tulis post mortem singkat: kronologi, akar masalah, kenapa tidak terdeteksi lebih awal, dan 2 sampai 3 tindakan pencegahan konkret (bukan "lebih hati-hati").

### E. Deploy bisa pulang

Uji coba di staging, produksi cuma nerima barang yang sudah terbukti. Sebelum deploy, susun checklist: test apa saja yang harus hijau, migrasi database yang terjadi dan cara membatalkannya, file config atau env yang berubah, urutan langkah deploy. Tiap poin punya langkah rollback.

Setelah deploy, smoke test 3 sampai 5 alur terpenting. Satu saja gagal berarti rollback dulu, diagnosis belakangan.

### F. Perawatan rutin

Dependensi usang dan yang punya celah keamanan diperiksa berkala. Update aman (patch atau minor) satu per satu sambil menjalankan test tiap habis update; update major dibuat daftar terpisah beserta risiko breaking change-nya. Pemeriksaan keamanan dasar mencakup validasi input, autentikasi dan otorisasi tiap endpoint termasuk yang tersembunyi, keamanan upload file, rate limiting di endpoint sensitif, dan secrets yang tidak sengaja masuk repo. Kode mati didaftar dengan bukti, tidak dihapus sebelum user konfirmasi.

### G. Lapisan agentic

Semua protokol di atas tetap berlaku, agent tetap software biasa. Tambahannya:

- **Evals.** Kumpulan kasus uji plus rubrik penilaian, karena output AI tidak sama persis tiap kali. Jalankan tiap kali prompt, model, atau tool berubah, dan bandingkan skornya dengan versi sebelumnya. Ganti prompt itu sama saja deploy.
- **Tracing.** Catat tiap langkah per sesi: prompt yang dikirim, tool yang dipanggil beserta argumennya, hasil yang diterima, keputusan berikutnya.
- **Guardrails.** Whitelist tool, batas iterasi, batas biaya API per sesi dan per hari, timeout per langkah. Batas tersentuh berarti agent BERHENTI dan lapor, bukan lanjut diam-diam.
- **Human in the loop.** Aksi yang tidak bisa dibatalkan (kirim pesan, posting publik, hapus data, transaksi) hanya boleh sampai tahap draft, eksekusi menunggu approval manusia. Aksi aman yang bisa dibatalkan boleh otomatis.
- **Prompt injection.** Konten eksternal yang dibaca agent (komentar user, halaman web, isi file) diperlakukan sebagai DATA, bukan perintah. Uji dengan instruksi jahat yang diselipkan ke data.
- **Pin versi model.** Jangan pakai alias "latest". Provider bisa mengganti model diam-diam dan perilaku agent ikut berubah tanpa ada yang menyentuh kode.

---

## Zona bahaya, jangan pernah dilakukan di tools berjalan

- **Edit langsung di produksi.** Selalu lewat staging atau minimal branch terpisah. "Cuma ganti satu baris" adalah kalimat pembuka semua cerita horor.
- **Rombak total sekalian biar rapi.** Rewrite besar-besaran sistem hidup hampir selalu berakhir lebih buruk. Refactor itu dicicil, bukan diborong.
- **Migrasi atau hapus data tanpa backup.** Sebelum menyentuh struktur database: backup dulu, dan pastikan migrasinya bisa dibatalkan.
- **Yakin tanpa bukti.** Jangan menyimpulkan akar masalah tanpa menunjukkan potongan kode atau baris log yang mendukungnya.

## Kamus singkat

| Istilah | Artinya |
|---|---|
| Characterization test | Test yang merekam perilaku sekarang apa adanya, sebagai pagar sebelum mengubah |
| Regression test | Uji ulang fitur lama tiap ada perubahan, mastiin gak ada yang kepecahin |
| Feature flag | Saklar hidup mati per fitur tanpa deploy ulang |
| Staging | Server kembaran produksi khusus buat uji coba |
| Smoke test | Cek cepat habis deploy: alur terpenting masih hidup atau tidak |
| Rollback | Balik cepat ke versi sebelum masalah, disiapkan sebelum deploy bukan pas panik |
| Root cause | Akar masalah, lawan dari gejala. Nambal gejala berarti bug balik bulan depan |
| Post mortem | Catatan setelah insiden: apa yang terjadi, kenapa, dan pencegahannya |
| Evals | Regression test versi AI: kasus uji plus rubrik, dinilai statistik bukan kata per kata |
| Guardrails | Pagar keras buat agent: whitelist tool, batas loop, batas biaya, timeout |
| Model drift | Perilaku berubah karena provider ganti model diam-diam. Obatnya pin versi plus evals |

Prinsip utamanya satu: di tools yang sudah jalan, pengaman dipasang **sebelum** perubahan, bukan setelah kejadian.
