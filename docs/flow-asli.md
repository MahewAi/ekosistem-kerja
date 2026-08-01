# Flow Bisnis Asli → Pemetaan ke ATLAS

Sumber: 2 gambar business process dari Matthew (1 Agu 2026).
**Fokus checkpoint: sampai PRODUKSI MENERIMA DATA untuk mulai membuat barang.**

## Alur (dari gambar 1, nomor 1-15)

1. ORDER masuk (PO customer)
2. ABA memproses order
3. Checklist verifikasi: Gambar, Harga, Material, Deadline, Detail lainnya
4. ANALISA oleh SSA & PPIC
5. Cek LOKASI / INVENTORY material
6. PURCHASING ↔ SUPPLIER/Vendor (terhubung Budget Planning / FAT)
7. MATERIAL IN TRANSIT + Quality Check masuk
8. Checklist final sebelum produksi (gambar, material, deadline, detail)
9. PRODUCTION PROCESS  ← **checkpoint fokus berhenti di sini (produksi dapat data)**
10. Quality Check (produksi / FG / material)
11. Waste & Barang Setengah Jadi (in transit internal, Inventory Controller)
12. Finish Good → Quality Check → DELIVERY (Surat Jalan / DO)
13. Finalisasi Dokumen — BAST
14. INVOICE → FAT
15. Inventory Controller / FAT rekonsiliasi

## Peran (dari gambar 2)

| Kode | Tim | Tugas kunci |
|---|---|---|
| C–A | **All ABA** (Admin Business Analyst) | Cek PO=Penawaran; Harga–TOP; Historis pelanggan; Standard/Custom; Kebutuhan Survey/Gambar; Ketersediaan barang; Deadline kirim; Request SSA proses lanjutan; **Monitoring sampai terkirim & terbayar lunas** |
| A–B | **Annisa & Team** (Sales Support Administration / SSA) | Klarifikasi ulang semua data sebelum SO; koordinasi balik ke Sales jika kendala; Tindak lanjut PO → Finance (invoice), PPIC (jadwal produksi), Gudang (pengiriman), N1/N2 (approval gambar), ABA/Sales (perubahan), Project (progress) |
| B–C | **Bu Liana & Team** (Production Planning Inventory Controller & SCM / PPIC) | Klarifikasi ulang semua data sebelum WO; koordinasi balik ke Sales jika kendala; Tindak lanjut SO/WO → Jadwal produksi, Jadwal material (kurang), Koreksi pekerjaan, Kendali produksi, Koordinasi jadwal ke SSA/ABA/Sales/Project, Koordinasi Gudang (Material & FG) |

## Pemetaan ke stasiun peta ATLAS (9 stasiun)

Koreksi Matthew (1 Agu): **cek material adalah pekerjaan Purchasing** — digabung
jadi satu stasiun; Inventory Controller gudang berada di bawah Purchasing.

| # | Stasiun | PIC | Berkas/cek wajib (gerbang keluar) | Ket |
|---|---|---|---|---|
| 1 | Order Masuk | Sales | PO customer, data kontak & alamat | |
| 2 | ABA — Verifikasi | ABA | 7 cek ABA (lihat C–A) | Setujui / minta revisi di sini |
| 3 | SSA — Proses SO | **Annisa** | Klarifikasi data, SO terbit, Approval gambar N1/N2, Info invoice ke Finance | |
| 4 | PPIC — Proses WO | **Bu Liana** | Klarifikasi WO, Jadwal produksi, Jadwal material | |
| 5 | **Purchasing — Cek Material** | (placeholder: Dimas) | Hasil cek stok, Alokasi / PO ke supplier, Konfirmasi vendor & jadwal | **CABANG**: cukup → #7; kurang → #6 |
| 6 | Material In Transit | Ekspedisi/IC | Surat jalan supplier, QC material diterima | vendor dari luar peta |
| 7 | **Produksi Terima Data** | Bu Liana → Produksi | Gambar final, Material siap, Deadline terkonfirmasi, Detail lengkap | ✅ **CHECKPOINT SELESAI** |
| 8 | Produksi & QC | Kep. Produksi | SPK produksi, Checklist QC | di luar fokus |
| 9 | Gudang FG & Kirim | (placeholder: Raka) | QC FG, Surat Jalan/DO, BAST, Invoice→FAT | di luar fokus |

Nama selain Annisa & Bu Liana masih placeholder — menunggu struktur organisasi lengkap.
