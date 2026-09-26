# Skill Soal UAS UNIROW Tuban (FKIP)

[![Antigravity Skill](https://img.shields.io/badge/Antigravity-Skill-6366f1.svg)](https://github.com/mariofahmi/skillUAS)
[![Template](https://img.shields.io/badge/Template-UNIROW%20FKIP-dc2626.svg)](https://unirow.ac.id)
[![Kurikulum](https://img.shields.io/badge/Kurikulum-OBE%202026-ec4899.svg)](https://unirow.ac.id)
[![Evaluasi](https://img.shields.io/badge/Evaluasi-Pertemuan%201--16-8b5cf6.svg)](https://mariofahmi.github.io/skillUAS/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Official skill and automation agent in **Google Antigravity & Agentic AI** for drafting and publishing **Final Exam (UAS / Ujian Akhir Semester)** papers adhering to UNIROW FKIP master templates, preserving floating logos, official headers, and synthesizing Bloom-level assessment questions across meetings 1 to 16 directly from OBE RPS documents.

🚀 **Web Simulator & Preview Portal:** [https://mariofahmi.github.io/skillUAS/](https://mariofahmi.github.io/skillUAS/)

---

## 🌟 Fitur Utama

1. **Preservasi 100% Format Dokumen Word XML:**
   - Mempertahankan integritas XML dokumen asli (`Template_UAS_UNIROW.docx`), termasuk **Kop Surat resmi**, **Logo ber-anchor (floating image)**, dan penataan tabel identitas mata kuliah tanpa risiko file rusak (*corrupted*).
2. **Cakupan Pembelajaran Komprehensif (Pertemuan 1–16):**
   - Mengambil secara terpadu capaian pembelajaran dan materi seluruh semester (fondasi awal, landasan hukum/teoretis, telaah komparatif pasca-UTS, hingga sintesis pemecahan masalah dan proyek inovatif).
3. **Penyusunan Soal Berbobot Taksonomi Bloom (HOTS C4–C6):**
   - Menghasilkan butir soal esai berkualitas akademik tinggi:
     - **Butir 1 (C4 – Analisis Fondasi Konseptual [Mg 1–4])**: Membedah keterkaitan landasan filosofis/teoretis terhadap kompetensi sarjana PPKn.
     - **Butir 2 (C4/C5 – Evaluasi Dinamika Sistemik & Kesenjangan Empiris [Mg 5–7])**: Menelaah kesenjangan antara *das Sollen* dan *das Sein*.
     - **Butir 3 (C5 – Telaah Kasus & Evaluasi Kebijakan Pasca-UTS [Mg 9–11])**: Evaluasi kritis efektivitas kebijakan/kasus aktual.
     - **Butir 4 (C5/C6 – Sintesis Integratif Masalah Kontemporer [Mg 12–14])**: Resolusi terpadu ancaman degradasi moral dan integrasi kebangsaan.
     - **Butir 5 (C6 – Rekonstruksi Desain Proyek Inovatif [Sintesis Mg 1–16])**: Perancangan karya/model transformatif berorientasi Profil Pelajar Pancasila.
4. **Dual Output (Word .docx & Markdown .md):**
   - Menghasilkan berkas Word `.docx` siap cetak sekaligus Markdown `.md` untuk integrasi ke portal LMS dan repositori dokumentasi.
5. **100% Pure Python (Bebas Ketergantungan Eksternal):**
   - Menggunakan modul standar bawaan Python (`zipfile` & `tempfile`), berjalan mulus lintas platform di Windows, macOS, dan Linux.

---

## 📁 Struktur Direktori

```text
skillUAS/
├── .gitignore
├── LICENSE (MIT)
├── README.md                          # Dokumentasi resmi
├── SKILL.md                           # Konfigurasi skill Antigravity IDE
├── index.html                         # Web Portal & WYSIWYG Editor (GitHub Pages)
├── assets/
│   ├── Template_UAS_UNIROW.docx       # Template master resmi UNIROW FKIP
│   └── logo_unirow.png                # Asset logo kampus UNIROW
├── references/
│   └── placeholder_map.md             # Pemetaan token XML {{...}}
└── scripts/
    └── fill_uas.py                    # Engine pengisi template lintas platform
```

---

## 🚀 Cara Penggunaan

### 1. Di Lingkungan Antigravity IDE (Slash Command)

Ketik salah satu slash command berikut pada antarmuka chat AI:
```text
/uas @RPS_Mata_Kuliah.docx
```
atau:
```text
/uas-unirow "Hukum Tata Negara"
```

AI akan secara otomatis membaca dokumen RPS / Kontrak Kuliah, menyusun butir soal evaluasi pertemuan 1–16, dan memproduksi file `.docx` ber-KOP resmi.

### 2. Eksekusi Melalui Python CLI

Jalankan skrip generator secara langsung melalui terminal:

```bash
# Sintaks umum
py scripts/fill_uas.py "Naskah_UAS_Hasil.docx" --data "data_ujian.json"
```

---

## 📝 Format Data Input (`data.json`)

```json
{
  "prodi": "Pendidikan Pancasila dan Kewarganegaraan",
  "dosen": "Dr. Sukisno, M.Pd.",
  "mata_kuliah": "Pendidikan Anti Korupsi",
  "angkt_semester": "2023/6",
  "hari": "Senin",
  "tanggal": "15 Juli 2026",
  "sifat": "Buka Buku (Analisis)",
  "waktu": "90 menit",
  "soal": [
    {
      "tipe": "esai",
      "teks": "Lakukan analisis kritis terhadap keterkaitan mendasar antara landasan teoretis Pendidikan Anti Korupsi dengan pembentukan karakter integritas calon pendidik PPKn!"
    },
    {
      "tipe": "esai",
      "teks": "Kaji dan evaluasilah prinsip-prinsip operasional delik Tipikor serta telaah kesenjangan antara das Sollen dan das Sein di Indonesia!"
    },
    {
      "tipe": "esai",
      "teks": "Berdasarkan materi pasca-UTS, analisislah efektivitas sinergi KPK-Polri-Kejaksaan dan perlindungan saksi oleh LPSK!"
    },
    {
      "tipe": "esai",
      "teks": "Sintesiskan integrasi konsep dari awal hingga akhir perkuliahan untuk merumuskan mitigasi gratifikasi di sektor pendidikan!"
    },
    {
      "tipe": "esai",
      "teks": "Rancanglah sebuah model proyek pembelajaran berbasis studi kasus integritas di persekolahan guna memperkuat Profil Pelajar Pancasila!"
    }
  ]
}
```

---

## 🏛️ Hak Cipta & Pengembang

Dikembangkan oleh **Mario Fahmi** untuk Program Studi Pendidikan Pancasila dan Kewarganegaraan (PPKn) & Fakultas Keguruan dan Ilmu Pendidikan (FKIP), Universitas PGRI Ronggolawe (UNIROW) Tuban. Lisensi di bawah [MIT License](LICENSE).
