# Ekosistem Kerja Perusahaan - Papan Progres

Prototipe desain untuk sistem kerja perusahaan: atasan kirim tugas, karyawan kerja
lewat dashboard sesuai role, kinerja terpantau, berkas tidak ada yang kelewat,
plus peta business process live gaya game (eagle eye).

Status: PROTOTIPE DESAIN SELESAI & TERVERIFIKASI (31 Jul 2026).
Data dummy, belum ada backend. Tujuan: Matthew menilai arah desain dulu,
sambil menunggu flow business process + hirarki final.

Cara buka: dobel-klik `C:\Users\PC\Documents\Claude\Projects\ekosistem-kerja\index.html`
(butuh internet sekali untuk font Google; selain itu jalan offline).
Pindah layar: tombol tab di atas, atau tekan 1 / 2 / 3, atau Ctrl+K.

## Progres

| Fase | Status |
|---|---|
| Riset web (5 agen paralel: Linear-class UI, mission control, peta gaya game, KPI karyawan, bahasa visual 2026) | SELESAI |
| Validasi palet warna (validator dataviz, mode gelap) | LOLOS semua cek |
| Bangun prototipe 1 file HTML (3 layar + simulasi live + palet perintah) | SELESAI |
| Verifikasi Playwright: console 0 error, alur dokumen-gerbang, token pindah stasiun, popover, overlay Beban, Ctrl+K | SEMUA LOLOS |

## Update 31 Jul sore: Peta Live v2 (permintaan Matthew)

Tampilan: gedung khas per stasiun (pabrik + roof monitor + cerobong + pintu
hangar, menara review bertingkat, gudang kirim berpintu dok, gerbang pemindai
QC), jendela/pintu gelap, zona kampus (KANTOR/PENGADAAN/PABRIK/LOGISTIK),
kontainer + truk parkir, kontras muka gedung dinaikkan, chevron arah statis
(mengganti animasi ants supaya arah terbaca saat dijeda), takik slot antrian
di aspal, token jadi truk kecil saat leg antar ke customer.

Fungsi: zoom + pan (scroll, drag, tombol +/-/reset, fokus otomatis ke order),
panel detail order dengan timeline "Perjalanan Order" aktual vs normal per
tahap, filter jenis order via legend + toggle Bermasalah, kontrol simulasi
(Jeda / 1x / 4x), ticker peristiwa, panel Antrian & hambatan bisa diklik
(hambatan ditaruh paling atas), stasiun berisi order kritis menyala merah +
label "macet X hari", token warn bercincin amber (legend: Perlu perhatian),
label stasiun pakai level-of-detail (PIC muncul saat zoom dekat).

QA: 1 putaran kritik adversarial (2 kritikus desain + 1 reviewer kode) via
workflow; 20 temuan, semua yang valid diterapkan, termasuk 7 bug kode
(spawn ganda ORD-0143, animasi ganda per token, scroll panel loncat, popover
vs zoom, pulse tidak restart, slot kedatangan salah urut, tombol kecepatan
lag). Verifikasi Playwright ulang: 0 error console, semua interaksi lolos.

## Update 31 Jul malam: Peta Live v3 + Halaman Sektor (permintaan Matthew)

3D: gradasi cahaya per muka gedung (matahari kiri-atas) + ambient occlusion,
garis atap penangkap cahaya, pelat dasar tiap gedung, jalan bercekung (underlay
gelap), detail atap (AC, skylight pabrik, antena menara, cerobong), jendela
menyala, bayangan digeser searah cahaya.

Animasi: asap cerobong pabrik (hidup hanya saat ada produksi, mati saat kosong),
cincin denyut saat token tiba, gedung berkedip halus saat memproses peristiwa,
token membesar saat hover, truk berputar mengikuti arah jalan, token baru
muncul dengan pop, panel/halaman pakai transisi masuk.

Halaman Sektor: klik gedung mana pun -> halaman tim sektor itu. Isi: breadcrumb
balik ke peta (atau Esc), statistik live (order, waktu normal, selesai bulan
ini, paling lama), BAGAN HIRARKI dari PIC/manager sampai bawahan (3 tingkat,
konektor CSS murni), kartu orang (status aktif/lapangan/cuti + beban tugas),
daftar order di sektor dengan pemegangnya, klik orang -> panel detail (status,
atasan, bawahan, telepon, kinerja privat vs median, tugas aktif, order yang
dipegang). Ctrl+K juga bisa langsung "Tim Produksi" dst. Data tim = DUMMY
(21 orang fiktif), menunggu hirarki asli.

## Update 31 Jul malam (2): v4 — lapisan KPI per orang

Sesuai visi awal Matthew ("KPI setiap orang, kerjaan selesai dari kapan sampai
kapan"):
1. Jejak Kerja di panel orang: garis waktu Sen-Jum, blok mulai-selesai per hari
   (hover = jam persis). Data dummy deterministik.
2. Panel Kinerja Sektor di halaman sektor: throughput 8 minggu, lead time vs
   normal, beban per orang (klik nama -> profil).
3. Halaman KPI Seluruh SDM: 22 orang lintas 7 sektor, kolom status/beban/
   selesai/rata-rata vs median/kualitas + pencarian. Masuk dari Menara
   ("Semua SDM ->") atau Ctrl+K. Klik baris -> sektor + profil orangnya.
4. Ruang Kerja: tombol "Mulai" per tugas mencatat jam mulai; saat selesai,
   feed menulis "mulai HH:MM, selesai HH:MM" (sumber data kapan-sampai-kapan).
5. Peta: lampu jalan + kolam cahaya halus di 5 titik rute.
6. Baris Kinerja Tim di Menara kini bisa diklik -> langsung profil orang.

## Isi prototipe

1. **Menara Kendali (owner)**: 5 KPI + sparkline, antrean "Perlu Perhatian"
   diranking (bukan log), tabel pipeline (stepper 7 tahap, umur tahap ala Jira,
   SLA ala Zendesk, chip dokumen, PIC), beban per tahap, kinerja tim, feed live.
2. **Peta Bisnis Live (eagle eye)**: peta isometrik SVG, 7 stasiun, token order
   bergerak menyusuri jalur saat tahap berpindah, antrean terlihat di jalan
   (sinyal bottleneck ala Factorio), klik stasiun/token = popover detail,
   overlay Beban, panel antrian & hambatan.
3. **Ruang Kerja (karyawan, persona Dimas/Purchasing)**: Hari Ini + Saran
   (pola My Day), detail tugas dengan SLOT DOKUMEN BERNAMA + tombol lanjut
   TERKUNCI sampai semua berkas ada (jawaban "tidak ada berkas kelewat"),
   skor pribadi vs median tim, target bulanan (bullet chart), umur tugas berjalan.
4. Simulasi live tiap 6,5 dtk; satu aksi karyawan (terbitkan PO) menggerakkan
   token di peta, membereskan alert owner, dan meng-update KPI. Semua rekonsil.

## Keputusan desain (dengan alasan, semua reversibel)

1. **Satu file HTML mandiri**, dobel-klik. Nanti dipecah jadi app sungguhan
   (mis. Next + Postgres + role login) saat flow final masuk.
2. **Nama folder `ekosistem-kerja` + codename produk "ATLAS"** = placeholder,
   belum tanya konvensi. Ganti kapan saja.
3. **Konteks dummy = perusahaan pintu/pabrikan** sesuai alur yang dijelaskan
   (penawaran -> finance/purchasing -> pabrik -> kirim). Flow 7 stasiun ini
   PLACEHOLDER sampai flow asli masuk.
4. **Bahasa visual**: disiplin Linear/Vercel. Geist + Geist Mono, kanvas #050505,
   elevasi = langkah terang + hairline putih-alpha, tanpa shadow/gradien/glass,
   satu aksen #5E6AD2, warna penuh hanya untuk status. Peta ikut prinsip
   High-Performance HMI: kalem sampai ada masalah.
5. **Palet chart/token divalidasi**: proyek #4269D0, retail #2FA89A,
   custom #A463F2 (lolos cek CVD & kontras di permukaan gelap).
6. **KPI anti-pengawasan**: karyawan lihat angkanya sendiri vs MEDIAN TIM,
   bukan ranking rekan; metrik kecepatan selalu dipasangkan metrik kualitas
   (anti-akal-akalan, Goodhart); zona merah dibingkai "minta bantuan", bukan hukuman.
   Alasan: riset menunjukkan leaderboard individu menurunkan motivasi mayoritas.
7. **Motion dibatasi** sesuai aturan: gerak hanya token peta (signature moment),
   flash baris saat data berubah, dan feedback klik. Tidak ada pulse dekoratif.
8. Panduan skill high-end (bento/double-bezel/py-24) TIDAK dipakai mentah karena
   itu pola marketing page; untuk dashboard padat, riset Linear/Vercel menang.

## Pertanyaan terbuka untuk Matthew

- Flow business process asli + hirarki role (akan mengganti 7 stasiun dummy)
- Nama sistem & perusahaan pemakainya (menentukan brand, warna, logo)
- Mode terang perlu? (token sudah siap, tinggal satu blok override)
- Berapa role dashboard yang dibutuhkan di v1 (owner + berapa jenis karyawan)?

## File

- `index.html` - prototipe (1 file, semua di dalamnya)
- `shot-*.png` - bukti verifikasi visual
