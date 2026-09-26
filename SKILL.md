---
name: uas-unirow
description: >
  Membuat dokumen SOAL UJIAN AKHIR SEMESTER (UAS) resmi Universitas PGRI
  Ronggolawe (UNIROW) Tuban, FKIP, sebagai file .docx sesuai template resmi
  kampus (logo UNIROW, kop surat, tabel Prodi/Dosen/Mata kuliah/Waktu/Angkt-
  Semester/Hari/Sifat/Tanggal, instruksi, penutup "SELAMAT MENGERJAKAN").
  Gunakan setiap kali pengguna minta "soal UAS", "ujian akhir semester",
  "buatkan UAS", "susun soal UAS" untuk UNIROW/Ronggolawe Tuban/FKIP — baik
  saat sudah punya soal sendiri tinggal diformat, maupun minta dibantu
  MENYUSUN soal esai/PG dari topik/RPS (materi minggu 9-16/pasca-UTS). Juga
  saat mengunggah contoh naskah UAS lama minta versi baru, atau merevisi
  naskah UAS yang sudah ada. WAJIB dipakai juga ketika pengguna hanya
  mengunggah Kontrak Kuliah, RPS, dan/atau draft soal lalu minta dibuatkan
  UAS — skill membaca sendiri dokumen tsb untuk mengambil Prodi/Dosen/Mata
  kuliah/materi pasca-UTS dan menyusun soal, tanpa pengguna perlu mengetik
  ulang data manual.
---

# Soal UAS Universitas PGRI Ronggolawe (UNIROW) Tuban

Skill ini adalah pasangan dari `uts-unirow` — struktur templatenya **identik
1:1**, hanya judul kop yang berbeda ("UJIAN AKHIR SEMESTER" vs "UJIAN TENGAH
SEMESTER"). Skill ini menghasilkan file `.docx` yang identik secara visual
dengan template resmi Soal UAS UNIROW FKIP, berdasarkan analisis XML
mendalam terhadap contoh asli.

**Jangan coba membangun ulang dokumen ini dari nol dengan `docx` (npm)/
docx-js.** Kop suratnya memuat logo ber-anchor (floating image) yang sulit
direplikasi dari kode dan gampang rusak. Alih-alih, gunakan
`assets/Template_UAS_UNIROW.docx` — salinan template asli dengan field yang
berubah-ubah sudah ditandai token `{{...}}` — lalu isi dengan
`scripts/fill_uas.py`. Pendekatan ini menjamin kop, logo, dan formatting
selalu identik dengan aslinya.

Peta lengkap semua token & struktur tabel: `references/placeholder_map.md`.

---

## Cara membuat soal UAS baru

### 1. WAJIB baca dulu dokumen yang diunggah pengguna, sebelum bertanya apa pun

Pengguna sering hanya mengunggah **Kontrak Kuliah**, **RPS**, dan/atau
**draft soal lama** dan berharap skill ini mengambil sendiri semua data
yang dibutuhkan — jangan langsung menembak pertanyaan ke pengguna kalau
datanya sebenarnya sudah ada di dokumen yang mereka unggah.

Untuk setiap file yang diunggah, gunakan skill `file-reading` (dan `docx`
untuk `.docx`) untuk membacanya (`extract-text <file>`), lalu ambil apa
yang relevan:

- **Kontrak Kuliah**: nama mata kuliah, kode MK, sks, Prodi, semester, nama
  Dosen Pengampu, deskripsi/CPMK/topik mingguan.
- **RPS** (kalau sama seperti template `rps-unirow`): Prodi, Mata Kuliah,
  CPL/CPMK/Sub-CPMK, rencana 16 minggu. **Untuk UAS, cek dulu di minggu
  berapa UTS diletakkan (biasanya minggu 7 atau 8)** — pakai materi &
  Sub-CPMK dari minggu **sesudah UTS sampai minggu 16** sebagai cakupan
  utama soal. Minggu ke-16 pada RPS biasanya sudah ditandai "UAS". Soal UAS
  boleh bersifat kumulatif (menyentuh ulang materi awal untuk soal
  analisis/sintesis), tapi bobot utama tetap materi pasca-UTS — konfirmasi
  ke pengguna jika ambigu.
- **Draft soal lama** (docx/teks apa pun): ekstrak daftar soal apa adanya
  (dan opsi PG jika ada) untuk diformat ulang ke template.

Isi field `prodi`, `dosen`, `mata_kuliah`, dan (jika tersedia)
`angkt_semester` langsung dari dokumen-dokumen ini tanpa bertanya lagi ke
pengguna. Sebutkan singkat ke pengguna field mana yang diambil otomatis
dari dokumen mana, supaya mereka bisa mengoreksi kalau salah ambil.

### 2. Baru tanyakan ke pengguna apa yang benar-benar belum ada

Yang biasanya **tidak** tercantum di Kontrak Kuliah/RPS (wajib ditanyakan,
jangan mengarang):

- **Hari** dan **Tanggal** pelaksanaan ujian yang sebenarnya.
- **Sifat ujian** (mis. "Tutup Buku", "Buka Buku", "Take Home").
- **Waktu** pengerjaan, jika bukan default 90 menit.
- Konfirmasi **jenis soal**: esai, pilihan ganda (PG), atau campuran, dan
  jumlah soal yang diinginkan — kecuali draft soal lama sudah menjawab ini.
- Jika Kontrak Kuliah/RPS tidak memuat Prodi/Dosen/Mata kuliah sama sekali,
  baru tanyakan field itu.

Fakultas **selalu FKIP** — tidak perlu ditanyakan. Skill ini juga **tidak
menyertakan kunci jawaban/rubrik** — hanya lembar soal murni.

### 3. Susun/ekstrak soal

Jika dibantu menyusun dari RPS, prioritaskan materi & Sub-CPMK minggu
pasca-UTS (lihat langkah 1). Jelas dan sesuai tingkat kesulitan UAS, dalam
Bahasa Indonesia formal akademik (kecuali mata kuliah berbahasa asing).
Jika pengguna mengunggah draft soal lama, gunakan soal tersebut apa adanya
(atau sesuai revisi yang diminta).

### 4. Susun data JSON

```json
{
  "prodi": "...",
  "dosen": "...",
  "mata_kuliah": "...",
  "angkt_semester": "...",
  "hari": "...",
  "tanggal": "...",
  "sifat": "...",
  "waktu": "90 menit",
  "soal": [
    {"tipe": "esai", "teks": "..."},
    {"tipe": "pg", "teks": "...", "opsi": ["...", "...", "...", "..."]}
  ]
}
```

`tipe` boleh `"esai"` (default) atau `"pg"`. Field `waktu` opsional.

### 5. Jalankan script pengisi

```bash
cd /mnt/skills/user/uas-unirow   # atau lokasi skill ini terpasang
python3 scripts/fill_uas.py /mnt/user-data/outputs/UAS_<Nama_MK>.docx --data data.json
```

(Ganti path skill sesuai lokasi instalasi aktual — cek dulu dengan `view`
jika path di atas tidak ditemukan. Path template default sudah menunjuk ke
`assets/Template_UAS_UNIROW.docx` relatif terhadap `scripts/fill_uas.py`.)

### 6. Selalu verifikasi hasil secara visual sebelum diserahkan ke pengguna

```bash
python3 /mnt/skills/public/docx/scripts/office/soffice.py --headless \
  --convert-to pdf /mnt/user-data/outputs/UAS_<Nama_MK>.docx
pdftoppm -jpeg -r 120 /mnt/user-data/outputs/UAS_<Nama_MK>.pdf /tmp/preview
```

Lalu `view` gambar `/tmp/preview-1.jpg` dan periksa:

- Kop menampilkan **"UJIAN AKHIR SEMESTER"** (bukan "TENGAH"), logo dan
  tabel identitas tidak rusak/bergeser
- Semua field identitas terisi benar (tidak ada token `{{...}}` tersisa)
- Soal bernomor urut 1, 2, 3, ... dengan benar
- Opsi PG (jika ada) berlabel a., b., c., ... dan tidak terpotong
- "SELAMAT MENGERJAKAN" tetap muncul di akhir

Jika ada yang salah, perbaiki data JSON, lalu ulangi langkah 5–6. Jika
skrip gagal karena token tidak ditemukan, kemungkinan
`assets/Template_UAS_UNIROW.docx` rusak/berubah — jangan menambal manual,
laporkan ke pengguna.

### 7. Serahkan file

Salin/pastikan file akhir ada di `/mnt/user-data/outputs/` dengan nama
jelas (misal `UAS_Reading_Comprehension.docx`), lalu panggil `present_files`.

---

## Aturan Konten Penting (jangan dilanggar)

- **Fakultas selalu "FAKULTAS KEGURUAN DAN ILMU PENDIDIKAN"**.
- **Tidak menyertakan kunci jawaban atau rubrik penilaian**.
- Jangan mengarang nama dosen, prodi, atau tanggal jika pengguna belum
  memberikannya — tanyakan dulu.
- Untuk soal dari RPS: prioritaskan materi pasca-UTS (lihat langkah 1).
- Total soal disesuaikan kebutuhan pengguna; jika tidak disebutkan,
  gunakan jumlah wajar untuk UAS (4–6 soal esai, atau campuran secukupnya).
- Bahasa dokumen: Bahasa Indonesia formal akademik, kecuali soal memang
  untuk mata kuliah bahasa asing.

## Spesifikasi Halaman & Template (referensi cepat)

| Aspek | Nilai |
|---|---|
| Ukuran kertas | A4 (11906×16838 DXA) |
| Margin | top 1133 DXA, sisi lain 1440 DXA |
| Font | Times New Roman, 12pt body |
| Logo | `word/media/image1.png` — logo UNIROW, jangan diganti |
| Fakultas | Selalu FKIP |
| Judul kop | "UJIAN AKHIR SEMESTER" (tetap, berbeda dari `uts-unirow`) |

Detail lengkap peta token & format soal ada di
`references/placeholder_map.md`.
