# 06. Perawatan rutin

**Istilah:** `dependency update` `security check` `dead code cleanup`

Kayak servis kendaraan: dilakukan berkala walau gak ada keluhan. Sebulan sekali cukup buat kebanyakan tools kecil.

---

## Update dependensi dengan aman

```text
Periksa dependensi proyek ini: mana yang usang dan mana yang punya celah keamanan yang diketahui. Update dulu yang aman (patch atau minor) SATU PER SATU sambil menjalankan test setiap habis update. Untuk update besar (major), jangan langsung, buatkan daftar terpisah beserta risiko breaking change-nya masing-masing.
```

## Pemeriksaan keamanan dasar

```text
Lakukan pemeriksaan keamanan dasar pada aplikasi ini: validasi input di semua form dan endpoint, autentikasi dan otorisasi tiap endpoint (termasuk yang "tersembunyi"), keamanan upload file, rate limiting di endpoint sensitif (login, daftar, API), dan secrets atau API key yang tidak sengaja masuk ke repo. Laporkan temuan diurutkan dari yang paling berbahaya, jangan perbaiki sebelum saya setujui.
```

## Bersih-bersih kode mati

```text
Cari kode mati di proyek ini: fitur yang tidak pernah dipakai, file yatim yang tidak di-import dari mana pun, dan dependensi yang terpasang tapi tidak pernah dipanggil. Buat daftarnya lengkap dengan bukti kenapa dianggap mati, untuk saya setujui. JANGAN hapus apa pun sebelum saya konfirmasi.
```

---

[Kembali ke daftar isi](../README.md)
