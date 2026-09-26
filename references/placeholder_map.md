# Peta Placeholder — Template_UAS_UNIROW.docx

Template ini adalah salinan persis dari contoh resmi UAS FKIP UNIROW
(`1790395620386_UAS_Angkt_2022_seminar.docx`), dengan seluruh sel isian yang
tadinya kosong / berisi contoh, diganti token `{{...}}` agar bisa dicari &
diganti secara aman lewat `scripts/fill_uas.py`.

Struktur ini **identik 1:1** dengan `uts-unirow` (paraId, tabel, dan posisi
token XML-nya sama persis) — satu-satunya perbedaan tetap adalah judul kop:
**"UJIAN AKHIR SEMESTER"** (bukan "UJIAN TENGAH SEMESTER"). Jika perlu detail
lebih dalam, bandingkan dengan `references/placeholder_map.md` milik skill
`uts-unirow`.

## Struktur dokumen

1. **Kop surat** (tetap, jangan diubah): logo UNIROW (grouped image, anchored),
   "UJIAN AKHIR SEMESTER", "TAHUN AKADEMIK 2025/2026", nama kampus, alamat,
   telp/fax, website, email.
2. **Baris fakultas** (tetap): "FAKULTAS KEGURUAN DAN ILMU PENDIDIKAN" —
   skill ini **selalu** memakai FKIP, tidak ada opsi fakultas lain.
3. **Tabel info** (2 kolom kiri-kanan × 4 baris):

   | Token | Label kolom kiri | Token | Label kolom kanan |
   |---|---|---|---|
   | `{{PRODI}}` | Prodi | `{{DOSEN}}` | Dosen |
   | `{{MATA_KULIAH}}` | Mata kuliah | `{{WAKTU}}` | Waktu |
   | `{{ANGKT_SEMESTER}}` | Angkt/Semester | `{{HARI}}` | Hari |
   | `{{SIFAT}}` | Sifat | `{{TANGGAL}}` | Tanggal |

   `{{WAKTU}}` defaultnya diisi `"90 menit"` jika field `waktu` tidak
   diberikan di data JSON.
4. **Instruksi** (tetap): *"Jawablah pertanyaan dibawah ini dengan benar"*.
5. **`{{DAFTAR_SOAL}}`** — paragraf marker tunggal, digantikan
   `scripts/fill_uas.py` dengan seluruh paragraf soal (esai bernomor, atau
   PG bernomor + opsi berlabel a./b./c./...).
6. **Penutup** (tetap): "SELAMAT MENGERJAKAN".

## Label baku yang TIDAK boleh diubah

`FAKULTAS KEGURUAN DAN ILMU PENDIDIKAN`, label kolom (`Prodi`, `Dosen`,
`Mata kuliah`, `Waktu`, `Angkt/Semester`, `Hari`, `Sifat`, `Tanggal`),
kalimat instruksi, dan "SELAMAT MENGERJAKAN".

## Detail teknis

| Parameter | Nilai |
|---|---|
| Ukuran kertas | A4 — 11906×16838 DXA |
| Margin | top 1133, sisi lain 1440 DXA |
| Font | Times New Roman, 12pt (sz=24) isi, 16pt (sz=32) judul & nama kampus |
| Logo | `word/media/image1.png` — logo UNIROW, jangan diganti/dipindah |
| Soal esai | Numbered `1. `, `2. `, dst., hanging indent 720/360 DXA |
| Opsi PG | Berlabel `a.`, `b.`, `c.`, ... otomatis, indent 1080/360 DXA |

## Konteks khusus UAS (vs UTS)

- Jika soal disusun dari RPS, cakupan materi UAS biasanya **minggu 9–16**
  (setelah UTS), bukan minggu 1–7/8. Cek dulu di RPS pengguna apakah UTS-nya
  ada di minggu 7 atau 8, lalu ambil materi & Sub-CPMK dari minggu sesudahnya
  sampai minggu 16 sebagai acuan.
- Soal UAS pada praktiknya sering mencakup materi kumulatif (bisa menyentuh
  ulang materi sebelum UTS untuk soal analisis/sintesis), tapi bobot utama
  tetap di materi pasca-UTS — tanyakan preferensi pengguna jika ambigu.

## Keterbatasan

- Tidak menyertakan kunci jawaban/rubrik penilaian.
- Fakultas selalu FKIP.
- Jika template resmi kampus berubah, ulangi proses penandaan token pada
  file contoh baru (unzip → cari paraId sel kosong → sisipkan `<w:r>`
  berisi token → rezip), lalu perbarui `assets/Template_UAS_UNIROW.docx`.
