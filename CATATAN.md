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

## Update 31 Jul malam (3): v5 — loop penugasan atasan -> karyawan

Inti visi yang belum ada akhirnya dibangun: "atasan kirim tugas tanpa WA".
1. Tombol "Beri Tugas" di Menara Kendali + di panel profil orang (nama
   langsung terisi). Form: pilih orang (tergrup per sektor), judul, deskripsi,
   tenggat, prioritas (Normal/Penting/Kritis), order terkait, dan DOKUMEN
   WAJIB yang otomatis jadi gerbang penguncian penyelesaian.
2. Tugas mendarat di Ruang Kerja orangnya: chip "Baru" + prioritas, deskripsi,
   slot dokumen, titik notifikasi di tab Ruang Kerja, tercatat di feed
   ("Matthew menugaskan ... ke Maya"), beban orang ikut naik.
3. Ruang Kerja jadi MULTI-PERSONA: klik nama di header -> menu 22 orang per
   sektor; dashboard menyesuaikan (sapaan sesuai jam, tugas, skor KPI pribadi,
   umur tugas, streak). Peraga "dashboard sesuai role masing-masing".
4. Nama pelaku di feed mengikuti persona aktif.

## Update 31 Jul malam (4): v6 — tema terang (siang) + peta rasa game simulasi

1. Toggle tema di topbar (ikon matahari/bulan), tersimpan di localStorage.
   Seluruh UI ditokenisasi (termasuk warna status per tema supaya kontras aman).
2. Konsep: GELAP = MALAM, TERANG = SIANG. Peta punya dua palet penuh (PAL.dark/
   PAL.light) dan seluruh scene statis dibangun ulang saat ganti tema
   (buildScene). Malam: jendela menyala, lampu jalan berpendar. Siang: gedung
   putih, bayangan matahari, kaca jendela biru, lampu mati.
3. Rasa game simulasi: pohon (hijau di siang, gelap di malam), mobil parkir,
   pelat zona diberi rona distrik tipis ala SimCity, strip sumber daya ala
   game strategi di atas peta (order aktif / pipeline / terkirim), dan pekerja
   kecil berlarian keluar gedung setiap stasiun memproses peristiwa.
4. Logo topbar dipindah ke token warna supaya tampil di kedua tema.

## Update 31 Jul larut (5): v7 — terrain lembah hijau (permintaan Matthew)

Peta jadi diorama game: seluruh kampus berdiri di PULAU LEMBAH HIJAU dengan
dinding plateau di tepinya. Isi terrain: hamparan rumput dengan petak gradasi
(blob organik low-poly, deterministik), plaza beraspal tempat gedung berdiri,
kolam air dengan tepi terang, batu-batu, 8 semak, dan total 27 pohon.
Semua ikut tema: siang = lembah hijau segar + kolam biru; malam = lembah
gelap tenang. Default tema kini TERANG (permintaan "saya maunya terang").

## Update 1 Agu: v8 — dekorasi game penuh (peta + hirarki)

Peta: papan nama ATLAS di gerbang masuk, tiang bendera aksen di plaza Review,
pagar semak zona kantor, garis parkir + zebra cross + strip dok muat (marka
jalan), pagar besi sisi utara pabrik, dermaga kayu di kolam, forklift di dok
pabrik, truk trailer staging, kontainer kargo biru (part() kini menerima warna
kustom), bayangan awan lembut di rumput (siang), burung samar di langit (siang).
Semua ikut palet siang/malam.

Hirarki (halaman sektor) ikut di-game-kan: header memakai MINI-DIORAMA gedung
sektor yang dirender dari peta (klik = terbang ke gedungnya di peta), kartu
manager berbendera "PIC" ungu, konektor bagan diberi titik simpul, kartu orang
terangkat halus saat hover. Catatan: sebelum mulai, pull dulu (sesi cloud
sempat menambah 8 commit: responsif + Pages + Alur Proses + Tur; sudah
dianalisis & diuji, 0 error).

## Update 1 Agu (3): penyimpanan lokal + unggah file sungguhan

1. State demo tersimpan per browser (localStorage, debounce 700 ms): orders +
   docState + hist, tugas semua persona (PT), TEAMS (beban/tugas), saran,
   persona aktif, hitungan terkirim. Refresh tidak me-reset. Muat ulang aman:
   simulasi lanjut dari state tersimpan (event untuk order yang sudah terkirim
   otomatis no-op). Reset: Ctrl+K -> "Reset demo".
2. Unggah file sungguhan: file picker asli, blob ke IndexedDB (atlas-files),
   nama+ukuran file tampil di slot, tombol "Lihat" membuka kembali filenya.
   Pola sama dengan lampiran kartu PETA BISNIS. Tur tetap jalur demo (klik
   programatik tidak bisa membuka dialog file).
3. Perbaikan kecil: urutan deklarasi penyimpanan (TDZ), koma param.

## Update 1 Agu (4): REMODEL KE FLOW ASLI (input Matthew masuk!)

Business process asli dari 2 gambar Matthew dipetakan penuh (docs/flow-asli.md).
Fokus checkpoint: sampai PRODUKSI MENERIMA DATA.
1. 10 stasiun baru: Order -> ABA Verifikasi (7 cek nyata jadi gerbang berkas) ->
   SSA/Annisa Proses SO -> PPIC/Bu Liana Proses WO -> Cek Material (CABANG:
   cukup langsung / kurang lewat Purchasing -> vendor -> Material In Transit +
   QC masuk) -> Produksi Terima Data (cp) -> [luar fokus] Produksi & QC ->
   Gudang FG & Kirim (BAST + invoice di feed).
2. Mesin rute jadi graf EDGES bercabang (nextOf per order, matKurang flag);
   jalan vendor masuk dari tepi peta.
3. Ribbon Alur Proses: penanda hijau "Checkpoint" + tahap luar fokus kelabu.
4. Setujui/Minta revisi pindah ke ABA (kembali ke Sales/Rio bila gagal cek).
5. TEAMS 10 sektor (~26 orang); NAMA NYATA: Annisa (SSA), Bu Liana (PPIC);
   sisanya placeholder. 4 sprite dipetakan ulang (ABA/SSA/PPIC/pabrik).
6. Tur, simulasi, feed, tugas Dimas ditulis ulang mengikuti flow; save state
   naik ke atlas-state-v2 (state lama tidak kompatibel).
Terverifikasi: siklus penuh 4x tanpa error; cabang cukup/kurang & checkpoint
feed bekerja.

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

## 2 Agu 2026 - Dokumen PDF: flowchart + hierarki per divisi

Dua dokumen cetak A4 landscape di `docs/` (sumber HTML bisa diedit, PDF hasil render):

- `flowchart-alur-bisnis.html/.pdf` - 1 halaman, alur order masuk sampai
  Produksi Terima Data (checkpoint fokus), cabang material cukup/kurang,
  zona kelabu di luar fokus.
- `hirarki-divisi.html/.pdf` - 3 halaman: (1) strip alur 9 divisi + tabel
  ringkas + daftar singkatan, (2) bagan garis komando divisi 1-5,
  (3) bagan divisi 6-9. Nomor divisi = nomor stasiun flowchart supaya dua
  PDF bisa dibaca berdampingan.

Keputusan:

1. Data personel diambil apa adanya dari TEAMS di index.html (26 orang,
   9 divisi); hanya Annisa & Bu Liana nama nyata, sisanya placeholder dan
   ditandai jelas di dokumen. Reversibel: regenerasi PDF setelah struktur
   organisasi resmi masuk.
2. Panel verifikasi 3 agen (data/bahasa/visual) dijalankan sebelum ekspor;
   22 temuan, hampir semua diterapkan: em-dash dibuang total dari KEDUA
   dokumen (pemisah jadi titik tengah), ejaan hierarki/standar/survei/riwayat,
   istilah dikunci (supplier bukan vendor, barang jadi bukan finish good,
   "fokus checkpoint" bukan "checkpoint fokus"), daftar singkatan ditambah,
   font kartu dinaikkan untuk keterbacaan cetak, garis pohon dipertegas.
3. Ditolak sadar: tugas Ujang tetap generik (dokumen struktur, bukan
   penugasan live) dan notasi "PO = Penawaran" dipertahankan karena itu
   notasi asli gambar proses Matthew.

## 2 Agu 2026 (sore) - Hierarki divisi DITULIS ULANG dari dokumen sumber asli

Koreksi Matthew: PDF hierarki harus diserap dari dokumen business process
yang pernah dia kasih (Selaras Lawang Sewu), bukan dari TEAMS prototipe.
docs/hirarki-divisi.html/.pdf dirombak total:

- Sumber: Projects/selaras-ekosistem/ringkasan-alur-hirarki.md (bagian C)
  + peta-business-process.md (transkrip 7 lembar) + flow-asli.md.
- Isi sekarang 100% nama/peran asli dokumen: Evelyn, Sarah, Nadia, Nita/
  Citra, Annisa, Sinta, Esti, Bu Liana, Riki, Bobby, Fischa, Hardy, Kidam,
  Yenni, Dilla, Agus, Titok, Athoko, Andy Pang, dst. Nol nama karangan.
- Ketidakjelasan dokumen ditandai jujur: tag "tidak dijelaskan" (nama/
  kepanjangan/garis), tag amber "PIC belum ada" (survey Modern Outlet
  masih "Siapa?"), Riki vs RIKI belum dipastikan orang yang sama.
- Panel verifikasi 3 agen menemukan 16 hal; 2 kritis terbukti benar
  (Bobby dan Fischa/RABT-MIU hilang) dan semua klaim dicek manual ke
  transkrip sebelum diterapkan. Ditolak sadar: usulan ganti "All ABA"
  dan potong "terkirim &" karena keduanya persis tulisan dokumen
  Back Office Detail.
- Struktur 3 halaman: (1) Pimpinan + ABA + SSA + Sales 4 kanal,
  (2) PPIC/Inventory/SCM + Produksi + Gudang (otoritas 5 gudang) +
  Quality, (3) Project + Finance + After Sales + Tim Expert + Segitiga
  Kontrol.

Catatan: TEAMS di index.html (peta live) masih memakai struktur lama
9 stasiun; penyelarasan prototipe ke struktur Selaras asli = pekerjaan
lanjutan bila Matthew minta.

## 3 Agu 2026 - Tanda "perlu nama" di hierarki divisi

Permintaan Matthew: tandai baris seperti Account Payable yang berupa
jabatan tanpa nama orang, disapukan ke SEMUA sektor. Chip biru "perlu
nama" / "perlu daftar nama" / "perlu nama kepala" ditambahkan di 21
posisi (3 kepala pimpinan, kepala ABA, Sales Leader, PPIC, IC, SCM,
Purchasing, Product Management, Kepala+Supervisor+Operator Produksi,
Kepala Gudang, Gerbang QC, Teknisi, Finance, Account Payable, FAT,
Accounting, Audit Internal). Legenda jadi 3 tanda; rekap total di
halaman 1. PDF ini sekarang berfungsi ganda: bagan + checklist isian
struktur organisasi.

## 3 Agu 2026 - Format kotak seragam: jabatan -> nama -> keterangan

Keluhan Matthew: kotak campur aduk (atasan pakai nama orang, bawahan pakai
nama kerjaan) bikin bingung. Rombak total: SETIAP kotak sekarang berformat
sama, baris 1 jabatan (huruf kecil kapital), baris 2 nama orang atau chip
"perlu nama", baris 3 keterangan kerjaan. Atasan = kotak biru teratas,
bawahan menggantung di garis. Divisi tanpa kepala tertulis (Project,
After Sales) diberi kotak "Kepala" bertag "posisi usulan" supaya rantai
atasan-bawahan tetap terbaca, menunggu koreksi Matthew. Total 23 posisi
perlu nama (21 dari dokumen + 2 kepala usulan). Avatar "?" kelabu untuk
kotak tanpa orang. Konten dipadatkan supaya 3 halaman tetap muat
(cardBottom max 729 vs footer 749, diukur via getBoundingClientRect).

## 14 Agu 2026 - Workflow Sales dan SSE ke SSA (dokumen baru)

Permintaan Matthew: flowchart alur bisnis untuk dasar pembangunan dashboard.
Alur yang diberikan: Sales dan SSE mengisi form, minta approval atasan, setelah
atasan setuju baru terkirim ke SSA.

`docs/workflow-sales-sse-ssa.html/.pdf`, 3 halaman A4 landscape:

- Halaman 1: alur sederhana, satu kartu besar per peran. Tiga kartu bernomor
  (Sales dan SSE, Sales Leader, SSA) dengan empat sampai lima butir kerja, palang
  status di kaki tiap kartu, jalur revisi amber putus-putus balik dari atasan ke
  pelaksana, ditutup kartu Aturan Inti.
- Halaman 2: rincian tiap peran. Tiga kolom dengan urutan yang sama seperti
  halaman 1, jadi bisa dibaca berdampingan: cara mengisi form dan slot isi form,
  daftar periksa atasan dan dua keluaran keputusan, aturan gerbang dan paket
  serah terima. Ditutup contoh perjalanan satu order dengan satu putaran revisi.
- Halaman 3: terjemahan ke dashboard. Rantai lima status, tabel pemegang bola
  dan hak ubah per langkah, komponen yang harus dibangun, dan daftar yang belum
  ditetapkan.

Struktur ini hasil koreksi Matthew atas versi pertama: versi pertama menaruh
flowchart rinci sekaligus kartu aturan di halaman 1 sehingga padat. Sekarang
halaman 1 hanya menjawab "siapa mengerjakan apa", rinciannya turun ke belakang.

Keputusan (dikonfirmasi Matthew sebelum menggambar):

1. **SSE = nama baru ABA.** Peran yang sama, istilah berubah. Dokumen lama
   (`workflow-aba-ssa`, `hirarki-divisi`, `flow-asli`, `data-dashboard`) masih
   menulis ABA dan sengaja tidak disentuh dulu. Penyeragaman istilah lintas
   dokumen dicatat sebagai keputusan terbuka di halaman 2.
2. **Atasan yang menyetujui = Sales Leader (Manager Sales)**, bukan Project
   Controller. Approval satu tingkat, tidak berjenjang.
3. **Isi form dikosongkan.** Matthew akan memberi daftar fieldnya menyusul, jadi
   kartu form memakai slot bertanda "menunggu daftar field" dengan rujukan
   sementara ke enam parameter sisi penjualan di `peta-data-dashboard`. Sisa
   dokumen tidak bergantung pada daftar itu, jadi alurnya bisa dibangun duluan.

Yang ditambahkan sendiri dan perlu dikoreksi Matthew bila salah: daftar periksa
atasan (ditandai chip "daftar periksa usulan awal"), aturan bahwa atasan tidak
memperbaiki sendiri isi form, dan kewajiban mengisi catatan pada kedua keputusan
approval.

Catatan render: Chromium di lingkungan ini tidak mempercayai CA proxy sehingga
Google Fonts gagal dimuat dan huruf jatuh ke DejaVu. PDF dirender dari salinan
sementara yang menyematkan Geist sebagai data URI; sumber HTML tetap memakai
tautan Google Fonts seperti dokumen lain.
