# 📊 Studi Kasus Data Iris: Manipulasi dan Ekspor Data
### **Implementasi Komparatif 11 Operasi Inti dalam Python dan R**

![Python](https://img.shields.io/badge/Python-3.7+-blue.svg)
![R](https://img.shields.io/badge/R-4.0+-purple.svg)
![Pandas](https://img.shields.io/badge/Pandas-Manipulation-blue.svg)
![Tidyverse](https://img.shields.io/badge/Tidyverse-Data_Wrangling-purple.svg)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)
![Affiliation](https://img.shields.io/badge/Affiliation-UNTIRTA-orange.svg)

Repositori ini menyajikan modul pembelajaran yang memandu Anda melalui 11 tugas fundamental dalam **data wrangling** dan **manipulasi data**, menggunakan dataset Iris sebagai studi kasus. Proyek ini mendemonstrasikan implementasi paralel dari setiap tugas di **Python (Pandas)** dan **R (Tidyverse/dplyr)**, diakhiri dengan proses ekspor data ke format universal (CSV dan Excel).

---

## ✨ Fitur Utama

Proyek ini mencakup 11 operasi data manipulation dasar yang penting untuk preprocessing:

- **1️⃣ Transformasi Variabel**:
    - Membuat **Variabel Turunan** (`Petal.Area`) dari operasi kolom yang sudah ada.
    - Membuat **Variabel Logika** (`Is_Panjang`) berdasarkan kondisi (`Panjang_Petal > 5`).
- **2️⃣ Penataan Data (Tidying)**:
    - **Mengubah Nama Variabel** (Rename) agar konsisten.
    - **Mengonversi Tipe** variabel dari numerik menjadi string.
- **3️⃣ Kategori & String**:
    - **Recode Kategori** (misal: 'setosa' menjadi 'S') menggunakan `case_when`/`map`.
    - **Operasi String** (misal: Mengubah semua teks menjadi huruf kapital).
- **4️⃣ Inspeksi & Seleksi**:
    - **Identifikasi Duplikat** dalam baris data.
    - **Subsetting & Sorting** data berdasarkan kriteria tertentu.
- **5️⃣ Integrasi Data**:
    - **Menggabungkan Data** (Merge/Join) dengan tabel informasi eksternal (`Habitat`).
- **6️⃣ Ekspor Data**:
    - Menyimpan data final ke format **CSV** (`.csv`) dan **Excel** (`.xlsx`).

---

## 📂 Struktur Proyek

- `Data_Iris_Manipulasi_Python.ipynb`: Notebook Python dengan implementasi Pandas.
- `Data_Iris_Manipulasi_R.Rmd`: Dokumen R Markdown dengan implementasi Tidyverse/dplyr.
- `iris_data_final.csv`: File hasil ekspor akhir.
- `iris_data_final.xlsx`: File hasil ekspor akhir.

---

## 🔧 Tumpukan Teknologi (Tech Stack)

- **Bahasa**: `Python 3.7+`, `R 4.0+`
- **Pustaka Python**: `pandas`, `numpy`, `scikit-learn` (untuk memuat data).
- **Pustaka R**: `tidyverse` (`dplyr`, `readr`), `writexl`.
- **Lingkungan**: `Jupyter Notebook / Lab`, `RStudio`.

---

## 🚀 Cara Memulai

### Prasyarat

- Instalasi Python dan R.
- Pustaka yang diperlukan (akan diinstal secara otomatis oleh skrip/perintah).
- Jupyter Notebook/Lab atau RStudio.

### Instalasi & Penggunaan

1. **Unduh Repositori**: *Clone* atau unduh proyek ini ke komputer Anda.
2. **Jalankan Notebook/R Markdown**:
    - Untuk proyek **Python**, jalankan Jupyter Lab/Notebook dan buka file `Data_Iris_Manipulasi_Python.ipynb`.
    - Untuk proyek **R**, buka RStudio dan buka file `Data_Iris_Manipulasi_R.Rmd` lalu klik "Knit" atau jalankan *chunk* kode.

---

## 📊 Ringkasan Hasil Utama

| Operasi Inti | Tujuan | Output Utama | Keterangan |
|---|---|---|---|
| **Transformasi** | Membuat `Petal.Area` | Kolom numerik baru | Variabel turunan berhasil dibuat di kedua bahasa. |
| **Recode Kategori** | Menyederhanakan `Species` | Kolom `Species_Code` (S, VE, VI) | Berhasil menerapkan conditional recoding. |
| **Integrasi Data** | Menggabungkan habitat | Kolom `Habitat` baru | Menggunakan `left_join` (R) / `merge` (Python). |
| **Ekspor Data** | Menyimpan hasil akhir | `iris_data_final.csv/xlsx` | Data siap digunakan di berbagai platform bisnis dan analisis. |

---

## ⚖️ Lisensi & Ketentuan Penggunaan

- **Hak Cipta**: © 2025 Ferdian Bangkit Wijaya - Seluruh Hak Dilindungi.
- **Penggunaan Akademik**: Diizinkan secara bebas untuk keperluan penelitian dan pendidikan non-komersial dengan atribusi.
- **Penggunaan Komersial**: Memerlukan izin tertulis dari pengembang.

---

## 👨‍💻 Author

- **Ferdian Bangkit Wijaya**
- Universitas Sultan Ageng Tirtayasa (UNTIRTA)
- Banten, Indonesia 🇮🇩

---

> Proyek ini berfungsi sebagai panduan *hands-on* yang efektif, menunjukkan kesamaan fundamental dan perbedaan sintaksis dalam melakukan manipulasi data antara R dan Python.
