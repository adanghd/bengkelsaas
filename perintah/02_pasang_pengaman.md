# 02. Pasang pengaman

**Istilah:** `monitoring` `logging` `backup dan restore`

Tools jalan tanpa monitoring itu kayak nyetir malem tanpa lampu. Target: kamu tahu ada masalah dalam hitungan menit, bukan denger dari user berhari-hari kemudian.

---

## Logging dan error tracking

```text
Tambahkan logging terstruktur di semua titik yang bisa gagal: request masuk, panggilan API eksternal, query database, dan background job. Sertakan error tracking yang mencatat stack trace beserta konteksnya (siapa, endpoint apa, input apa). Syarat mutlak: jangan ubah logika bisnis apa pun.
```

## Health check plus alert

```text
Buatkan endpoint health check yang mengecek: aplikasi hidup, koneksi database, dan layanan eksternal yang kritikal. Lalu siapkan pemantauan endpoint ini dengan notifikasi kalau down, boleh pakai cron sederhana atau layanan uptime gratis. Kirim alert-nya ke [TELEGRAM ATAU EMAIL KAMU].
```

## Backup yang beneran bisa balik

```text
Rancang strategi backup untuk data aplikasi ini: apa saja yang di-backup, seberapa sering, disimpan di mana (harus beda mesin dari servernya), dan berapa lama disimpan. Buat script backup otomatis plus script restore, lalu pandu saya MENGETES restore-nya di lingkungan terpisah sampai terbukti datanya balik utuh.
```

Backup yang belum pernah dites restore sama saja belum punya backup.

---

[Kembali ke daftar isi](../README.md)
