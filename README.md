# ATLAS — Ekosistem Kerja Perusahaan (Prototipe)

Prototipe sistem operasi perusahaan: atasan mengirim tugas tanpa WhatsApp,
tiap karyawan punya dashboard sesuai perannya, kinerja terpantau, tidak ada
berkas yang kelewat, dan seluruh alur bisnis terlihat hidup di satu peta
gaya game (eagle eye).

> Status: **prototipe desain** dengan data dummy. Satu file HTML mandiri,
> tanpa backend. Codename "ATLAS" masih placeholder.

## Live demo

**<https://mahewai.github.io/ekosistem-kerja/>**

Terbit otomatis dari `main` lewat GitHub Actions
([`.github/workflows/deploy.yml`](.github/workflows/deploy.yml)) — tidak ada
build step, isi repo langsung disajikan. Setiap push ke `main` menerbitkan ulang
dalam ~1 menit. Run pertama menyalakan GitHub Pages sendiri; kalau gagal karena
izin, nyalakan manual di **Settings → Pages → Source: GitHub Actions**.

## Cara membuka

Online: buka tautan di atas. Offline: dobel-klik `index.html` (butuh internet
sekali untuk font Google, selebihnya jalan offline). Pindah layar: tab di atas,
tombol `1 / 2 / 3`, atau `Ctrl+K`.

Jalan di desktop, tablet, dan ponsel. Di layar kecil tab pindah ke bawah, tabel
berubah jadi kartu, dan peta punya navigator stasiun + cubit-untuk-zoom.

## Isi

| Layar | Fungsi |
|---|---|
| **Menara Kendali** | KPI live, antrean "Perlu Perhatian" diranking, tabel pipeline order (stepper 7 tahap, SLA, dokumen, PIC), beban per tahap, kinerja tim, feed aktivitas |
| **Peta Bisnis Live** | Peta isometrik 7 stasiun; order = token yang bergerak dan mengantre; zoom + pan; klik gedung → halaman sektor; filter jenis order & "Bermasalah"; kontrol simulasi Jeda/1x/4x |
| **Halaman Sektor** | Bagan hirarki tim per sektor (PIC → bawahan, 3 tingkat), kinerja sektor (throughput, lead time, beban per orang), order di sektor; klik orang → profil + Jejak Kerja (kapan mulai, kapan selesai) |
| **KPI Seluruh SDM** | Tabel 22 orang lintas 7 sektor + pencarian; klik baris → profil orangnya |
| **Ruang Kerja** | "Hari Ini" + saran (pola My Day), slot dokumen bernama dengan gerbang tahap (tombol lanjut terkunci sampai berkas lengkap), tombol Mulai pencatat jam, skor pribadi vs median tim, multi-persona (lihat dashboard karyawan mana pun) |
| **Beri Tugas** | Owner/manager menugaskan dari Menara atau profil orang: judul, tenggat, prioritas, order terkait, dokumen wajib; tugas mendarat di Ruang Kerja orangnya dengan notifikasi |

## Tangkapan layar

![Peta Bisnis Live](v4-peta.png)
![KPI Seluruh SDM](v4-sdm.png)
![Profil + Jejak Kerja](v4-person-jejak.png)
![Form Beri Tugas](v5-modal.png)
![Ruang Kerja karyawan](v5-maya.png)

## Prinsip desain

- Disiplin Linear/Vercel: Geist + Geist Mono, kanvas gelap, elevasi lewat
  langkah terang + hairline, tanpa gradien dekoratif/glassmorphism/glow,
  satu warna aksen.
- Peta mengikuti High-Performance HMI: kalem sampai ada masalah; warna jenuh
  hanya untuk status dan token order. Palet tervalidasi aman buta warna.
- KPI anti-pengawasan: karyawan melihat angkanya sendiri vs median tim
  (bukan ranking rekan); metrik kecepatan selalu berpasangan metrik kualitas.
- Gerak hanya untuk umpan balik dan momen signature (token berjalan, asap
  pabrik saat produksi aktif).

Riwayat keputusan lengkap: [CATATAN.md](CATATAN.md).

## Yang belum nyata (penting sebelum demo ke stakeholder)

Alur penugasan dan gerbang dokumen benar-benar jalan, tapi ini masih peraga:

- **Tombol "Unggah" tidak mengunggah file.** Menandai slot dokumen jadi terisi;
  tidak ada file picker maupun penyimpanan.
- **Belum ada aksi setujui/tolak.** "Review & Approval" ada sebagai tahap dan
  Matthew tercatat sebagai PIC-nya, tapi order maju karena timer simulasi —
  bukan karena ada yang menyetujui.
- **Tidak ada yang tersimpan.** Refresh = semua tugas, dokumen, dan penyelesaian
  kembali ke awal.
- **Tidak ada login.** Pemilih 22 persona adalah dropdown demo, bukan otentikasi.

## Menunggu input

1. Flow business process asli (7 stasiun sekarang dummy).
2. Struktur organisasi asli (21 nama di bagan tim fiktif).
3. Nama sistem & perusahaan pemakainya.
