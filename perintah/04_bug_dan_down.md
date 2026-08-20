# 04. Ada bug, error, atau tools down

**Istilah:** `incident response` `root cause analysis` `post mortem`

Reflek paling bahaya: panik, minta AI "benerin", AI nebak, makin rusak. Urutan yang bener: **diagnosis dulu, sepakati akar masalah, baru perbaiki**.

---

## Diagnosis dulu, jangan sentuh kode

```text
Aplikasi bermasalah: [GEJALA, MISAL: USER GAK BISA LOGIN SEJAK JAM 3]. JANGAN langsung mengubah kode. Diagnosis dulu: baca log dan error yang ada, telusuri alur dari gejala ke sumbernya, lalu sebutkan akar masalahnya beserta bukti konkretnya. Setelah kita sepakat akar masalahnya, baru usulkan perbaikan.
```

## Perbaiki akar, bukan gejala

```text
Perbaiki bug ini di AKAR masalahnya, bukan ditambal di gejalanya. Setelah itu periksa: apakah pola bug yang sama ada di bagian lain kode? Kalau ada, perbaiki semuanya sekaligus. Terakhir, tambahkan test yang memastikan bug ini tidak bisa kembali tanpa ketahuan.
```

## Post mortem biar gak keulang

```text
Insiden sudah beres. Buatkan post mortem singkat: kronologi kejadian, akar masalah, kenapa tidak terdeteksi lebih awal, dan 2 sampai 3 tindakan pencegahan yang konkret (bukan "lebih hati-hati"). Simpan sebagai catatan proyek, lalu langsung kerjakan tindakan pencegahan yang paling murah.
```

---

[Kembali ke daftar isi](../README.md)
