# Peta Data Dashboard · PT Selaras Lawang Sewu

Sumber: tabel parameter dashboard dari Matthew (4 Agustus 2026).
Dokumen ini menerjemahkan tabel itu menjadi spesifikasi data yang bisa langsung
dipakai programmer untuk merancang tabel, hak akses, dan jejak audit.

**14 parameter · 7 sektor pemilik data.**

---

## 1. Tabel parameter

| # | Parameter | Sumber data awal | Sifat | Pemicu perubahan | Boleh mengubah | Tampilan di dashboard |
|---|---|---|---|---|---|---|
| 1 | Nomor Penawaran | ABA | berubah | Kode bisa beda saat ada penyesuaian | ABA | Kunci query, status di bawahnya menyusul |
| 2 | Nomor PO / SPK | ABA | berubah | Kode bisa beda saat ada penyesuaian | ABA | Kunci query, status di bawahnya menyusul |
| 3 | Nama Pemesan (PT / Perorangan) | ABA | tetap | — | — | Nilai tunggal |
| 4 | Nama Proyek | ABA | tetap | — | — | Nilai tunggal |
| 5 | Total Nilai Pesanan (DPP) | ABA | berubah | Koreksi, biasanya proyek dengan addendum tambah kurang | ABA, SSA | Nilai tunggal |
| 6 | Status PDD | ABA | berubah | Percepatan atau perlambatan | SSA | Nilai tunggal |
| 7 | Nomor SO | SSA | tetap | — | — | Nilai tunggal |
| 8 | Registrasi N1 | SSA | bertambah | Kode gambar bertambah saat ada pekerjaan tambah kurang | SSA, PPIC, N1 | Daftar kode gambar |
| 9 | Registrasi N2 | PPIC | bertambah | Kode gambar bertambah saat ada pekerjaan tambah kurang | PPIC, N1/N2 | Daftar kode gambar |
| 10 | Nomor WO | PPIC | tetap | — | — | Nilai tunggal |
| 11 | Status Produksi | Produksi | berubah | Entry mengikuti pergerakan produksi | PPIC, Produksi | Nilai tunggal |
| 12 | Status Invoice | Keuangan | berubah | Status tagihan bergerak: DP, BMOS, Progress, AI, dan seterusnya | SSA, Keuangan | **Tabel** langkah invoice |
| 13 | Pemasangan | Project | berubah | Prioritas pekerjaan berubah, jadwal mengikuti dashboard implementasi proyek | SSA, Project | **Tabel** status pekerjaan |
| 14 | Pengiriman | Gudang | berubah | Penyesuaian jadwal | PPIC, Gudang | **Tabel** status pengiriman |

Catatan asli pada kolom status dashboard: nilai keluar sesuai data yang dientry
oleh ABA, SSA, PPIC, Engineering, atau Produksi.

---

## 2. Kepemilikan data per sektor

| Sektor | Jumlah parameter | Parameter yang dibuat |
|---|---|---|
| ABA | 6 | Nomor Penawaran, Nomor PO/SPK, Nama Pemesan, Nama Proyek, Total Nilai Pesanan, Status PDD |
| SSA | 2 | Nomor SO, Registrasi N1 |
| PPIC | 2 | Registrasi N2, Nomor WO |
| Produksi | 1 | Status Produksi |
| Keuangan | 1 | Status Invoice |
| Project | 1 | Pemasangan |
| Gudang | 1 | Pengiriman |

Urutan pembuatan data mengikuti alur kerja: ABA membuka order sampai Status PDD,
lalu diserahkan ke SSA. SSA menerbitkan Nomor SO dan Registrasi N1, lalu menyebar
data ke PPIC, Purchasing, Keuangan, ASS, Project, dan N1/N2 secara paralel.

---

## 3. Matriks izin

`B` = membuat data pertama kali · `U` = boleh mengubah setelahnya

| Parameter | ABA | SSA | PPIC | N1 | N2 | Produksi | Keuangan | Project | Gudang |
|---|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
| Nomor Penawaran | B U | | | | | | | | |
| Nomor PO / SPK | B U | | | | | | | | |
| Nama Pemesan | B | | | | | | | | |
| Nama Proyek | B | | | | | | | | |
| Total Nilai Pesanan | B U | U | | | | | | | |
| Status PDD | B | U | | | | | | | |
| Nomor SO | | B | | | | | | | |
| Registrasi N1 | | B U | U | U | | | | | |
| Registrasi N2 | | | B U | U | U | | | | |
| Nomor WO | | | B | | | | | | |
| Status Produksi | | | U | | | B U | | | |
| Status Invoice | | U | | | | | B U | | |
| Pemasangan | | U | | | | | | B U | |
| Pengiriman | | | U | | | | | | B U |

Pola yang terlihat: **SSA dan PPIC adalah dua pengubah lintas sektor.** SSA boleh
mengubah data milik ABA, Keuangan, dan Project. PPIC boleh mengubah data milik
SSA, Produksi, dan Gudang. Keduanya perlu hak akses khusus di atas hak sektornya
sendiri.

---

## 4. Catatan teknis untuk programmer

### 4.1 Jangan pakai nomor bisnis sebagai kunci utama

Dashboard melakukan query berdasarkan Nomor Penawaran dan Nomor PO/SPK, tetapi
tabel yang sama menyatakan kedua nomor itu **bisa berubah** saat ada penyesuaian.
Kalau nomor bisnis dipakai sebagai primary key, riwayat order akan putus begitu
nomornya diganti.

Yang benar: satu ID internal yang tidak pernah berubah sebagai kunci, sedangkan
Nomor Penawaran dan Nomor PO/SPK menjadi atribut biasa yang punya riwayat versi.
Pencarian tetap bisa memakai nomor bisnis, termasuk nomor lama.

### 4.2 Tiga parameter bukan nilai tunggal, melainkan tabel anak

Status Invoice, Pemasangan, dan Pengiriman ditampilkan sebagai tabel langkah,
bukan satu kolom status. Ketiganya perlu tabel tersendiri berisi baris per
langkah, lengkap dengan tanggal, pelaku, dan keterangan. Kolom di order induk
cukup menyimpan ringkasan langkah terakhir.

### 4.3 Registrasi N1 dan N2 bersifat jamak

Keterangan aslinya menyebut kode gambar bisa bertambah saat ada pekerjaan tambah
kurang. Artinya satu order bisa punya banyak kode gambar. Ini relasi satu ke
banyak, bukan satu kolom teks.

### 4.4 Sepuluh dari empat belas parameter bisa berubah

Hanya empat yang benar-benar tetap: Nama Pemesan, Nama Proyek, Nomor SO, dan
Nomor WO. Sisanya bisa berubah, dan tujuh di antaranya bisa diubah lebih dari
satu sektor. Setiap perubahan wajib tercatat: siapa, kapan, nilai lama, nilai
baru, dan alasannya. Tanpa itu, prinsip Tercatat Termonitor Terevaluasi tidak
terpenuhi.

### 4.5 Perubahan yang berasal dari addendum perlu diperlakukan khusus

Total Nilai Pesanan berubah karena addendum tambah kurang, dan pada saat yang
sama Registrasi N1 dan N2 bertambah karena gambar kerja baru. Ketiganya berasal
dari satu peristiwa yang sama. Sebaiknya ada entitas addendum yang mengikat
perubahan nilai dan penambahan gambar dalam satu catatan, bukan tiga perubahan
lepas yang kebetulan berdekatan waktunya.

### 4.6 Status PDD dipegang ABA tetapi diubah SSA

Ini satu-satunya parameter yang pembuatnya tidak boleh mengubahnya sendiri.
Perlu dipastikan apakah memang disengaja, karena aturan hak aksesnya berbeda
dari parameter lain.

---

## 5. Pertanyaan terbuka

Perlu jawaban dari manajemen sebelum tabel dikunci:

1. Kepanjangan resmi **PDD** dan daftar nilai statusnya.
2. Arti **BMOS** dan **AI** pada status invoice, serta urutan lengkap langkah
   tagihan dari DP sampai lunas.
3. Beda peran **N1** dan **N2**: mengapa Registrasi N1 dibuat SSA sedangkan
   Registrasi N2 dibuat PPIC.
4. Kolom status dashboard menyebut **Engineering** sebagai salah satu pengentry,
   tetapi Engineering tidak muncul di kolom sumber data mana pun. Apakah
   Engineering sama dengan N1/N2.
5. **ASS** menerima data paralel dari SSA, tetapi tidak memiliki satu pun
   parameter di tabel ini. Data apa yang mereka pegang dan tampilkan.
6. **Purchasing** juga menerima data paralel dari SSA, tetapi tidak punya
   parameter. Apakah status material akan ditambahkan.
7. Apakah daftar 14 parameter ini sudah final, atau masih akan bertambah
   mengikuti penjelasan alur berikutnya.
