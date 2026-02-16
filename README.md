Berdasarkan dokumen Tugas Modul 3 yang berisi tentang data profiling dan pembersihan data, berikut adalah rekomendasi nama repository dan README-nya:
​

Nama Repository GitHub
pizza-sales-eda-data-cleaning

Alternatif lain:

enhanced-pizza-sales-profiling

pizza-delivery-data-exploration

pizza-sales-data-profiling-analysis

README.md
text
# Pizza Sales EDA & Data Cleaning

Laporan Data Profiling dan Pembersihan Dataset Penjualan Pizza oleh Kelompok 14 Starterpack - Tugas Modul 3 Data Sains.

## 📊 Dataset

**Sumber:** Enhanced Pizza Sales Data (2024–2025)  
**Link Dataset:** [Google Drive](link_dataset)  
**File Akhir:** `Data Penjualan Pizza_Sudah bersih.xlsx`

Dataset terdiri dari **1004 entri** dengan **25 variabel** yang mencakup informasi pesanan pizza, waktu pengiriman, detail restoran, dan karakteristik produk.

## 🔍 Variabel Dataset

Dataset mencakup 25 kolom dengan berbagai tipe data:

### Variabel Utama
- **Order ID**: ID unik pesanan
- **Restaurant Name**: Nama restoran (6 restoran)
- **Location**: Lokasi pengiriman (84 lokasi)
- **Order Time & Delivery Time**: Waktu pemesanan dan pengiriman
- **Delivery Duration (min)**: Durasi pengiriman dalam menit
- **Pizza Size**: Ukuran pizza (Small/Medium/Large/XL)
- **Pizza Type**: Jenis pizza (Veg/Non-Veg, 12 tipe)
- **Toppings Count**: Jumlah topping
- **Distance (km)**: Jarak pengiriman
- **Traffic Level**: Tingkat lalu lintas (Low/Medium/High)
- **Payment Method**: Metode pembayaran (6 metode)
- **Is Peak Hour & Is Weekend**: Indikator waktu sibuk dan akhir pekan
- **Delivery Efficiency (min/km)**: Efisiensi pengiriman
- **Pizza Complexity**: Tingkat kerumitan pizza
- **Estimated Duration & Delay**: Estimasi waktu dan keterlambatan

## 📈 Statistik Deskriptif

### Ringkasan Data Numerik
- **Delivery Duration**: rata-rata 29.49 menit (15-50 menit)
- **Toppings Count**: rata-rata 3.36 topping (1-5 topping)
- **Distance**: rata-rata 4.95 km (2-10 km)
- **Delay**: rata-rata 17.62 menit (9-30 menit)

### Ringkasan Data Kategorikal
- **Restaurant Name**: Domino's (212 pesanan), Papa John's (204), Little Caesars (199)
- **Location**: Atlanta, GA paling banyak (78 pesanan)
- **Pizza Size**: Medium paling populer (429 pesanan)
- **Pizza Type**: Non-Veg lebih banyak (216 pesanan)
- **Traffic Level**: Medium dominan (398 pesanan)
- **Payment Method**: Card paling banyak (276 transaksi)

## 🛠️ Data Profiling & Identifikasi Masalah

### ✅ Kualitas Data Baik
- **Tidak ada data duplikat** (0 duplikasi)
- **Tidak ada missing values** (semua kolom lengkap)
- **Tipe data sudah sesuai** (datetime, numerik, kategorikal)

### ⚠️ Masalah yang Ditemukan

1. **Data Tidak Relevan**: Terdapat 304 pesanan dengan tanggal order setelah 14 September 2025 20:00 (termasuk tahun 2026)
2. **Inkonsistensi Nama Restoran**: "Marco's Pizza" vs "Marco's Pizza" (perbedaan karakter apostrophe)
3. **Outlier Terdeteksi** pada beberapa kolom:
   - Delivery Duration: 167 outlier
   - Toppings Count: 43 outlier
   - Distance: 38 outlier
   - Delivery Efficiency: 20 outlier
   - Order Hour: 51 outlier
   - Restaurant Avg Time: 3 outlier

## 🔧 Proses Pembersihan Data

### 1. Penghapusan Data Tidak Relevan
- **Metode**: Filter data dengan `Order Time <= 14 September 2025 20:00`
- **Hasil**: Dataset berkurang dari 1004 menjadi **700 baris**

### 2. Perbaikan Inkonsistensi Nama Restoran
- **Metode**: Replace karakter `'` dengan `'` menggunakan `str.replace()`
- **Hasil**: "Marco's Pizza" dan "Marco's Pizza" berhasil digabung menjadi "Marco's Pizza"

### 3. Penanganan Outlier
- **Metode**: Winsorization dengan batas 5th dan 95th percentile
- **Kolom yang ditangani**: 
  - Delivery Duration, Toppings Count, Distance
  - Delivery Efficiency, Topping Density
  - Estimated Duration, Delay, Pizza Complexity
  - Traffic Impact, Order Hour, Restaurant Avg Time
- **Hasil**: Sebagian besar outlier berhasil dimitigasi

### Pipeline Pembersihan Data
Data Penjualan Pizza.xlsx
↓ (Filter tanggal)
Salinan Data Penjualan Pizza_Tgl_Bersih.xlsx
↓ (Perbaikan nama restoran)
Salinan Data Nama Restoran Pizza_Bersih.xlsx
↓ (Winsorization outlier)
Salinan Data Penjualan Pizza_Winsorized.xlsx
↓ (Pembersihan Order Hour)
Data Penjualan Pizza_Sudah bersih.xlsx
