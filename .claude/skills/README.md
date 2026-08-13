# Skill lokal repo ini

Folder ini menampung skill `ckm*` supaya bisa dipakai di sesi mana pun pada
repo ini, di perangkat mana pun.

## Kenapa perlu

Skill `ckm*` tersinkron dari akun claude.ai, tapi frontmatter-nya memakai nama
bergaya namespace plugin:

```yaml
name: ckm:slides
```

Tanda titik dua membuat Claude Code membacanya sebagai `plugin:skill`. Karena
tidak ada plugin bernama `ckm` yang terpasang, hanya satu skill dari kelompok
itu yang lolos terdaftar (`ckm:banner-design`, yang pertama secara alfabet) dan
sisanya dibuang. Akibatnya `ckmbrand`, `ckmdesign`, `ckmdesign-system`,
`ckmslides`, dan `ckmui-styling` tidak bisa dipanggil lewat `/nama-skill`.

Salinan di sini identik dengan yang tersinkron, hanya baris `name:` diperbaiki
agar cocok dengan nama foldernya (misal `name: ckmslides`). Skill yang cakupannya
folder repo menang atas skill global, jadi salinan ini yang dipakai.

## Perbaikan permanen (di sisi sumber)

Salinan repo hanya berlaku di repo ini. Supaya beres di semua tempat, ubah
frontmatter `name:` skill kustom di claude.ai → Settings → Capabilities → Skills,
ganti `ckm:slides` menjadi `ckmslides`, dan seterusnya. Nama skill hanya boleh
huruf kecil, angka, dan tanda hubung.

## Catatan: berkas pendukung belum ikut

Tiap skill `ckm*` merujuk berkas pendukung (`references/`, `scripts/`,
`assets/`, `templates/`) yang tidak ikut tersinkron — yang ada hanya `SKILL.md`.

| Skill            | Berkas dirujuk | Berkas tersedia |
| ---------------- | -------------- | --------------- |
| ckmbrand         | 18             | 0               |
| ckmdesign        | 26             | 0               |
| ckmdesign-system | 14             | 0               |
| ckmslides        | 5              | 0               |
| ckmui-styling    | 9              | 0               |
| ckmbanner-design | 6              | 0               |

Skill tetap jalan sebagai panduan, tapi langkah yang menyuruh membaca atau
menjalankan berkas tersebut akan gagal. Untuk melengkapinya, salin folder skill
yang utuh dari PC ke `.claude/skills/<nama>/` lalu commit.
