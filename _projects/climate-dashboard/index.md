---
layout: post
title: Dashboard Visualisasi Data Iklim
description: Dasbor interaktif berbasis Streamlit yang menampilkan hubungan antara emisi CO2, energi terbarukan, dan bencana di wilayah Pasifik.
skills:
  - Python
  - Streamlit
  - Data Visualization
  - Plotly Express
  - GitHub
main-image: /climate.jpg
---

## Deskripsi Proyek

Proyek ini dikembangkan sebagai tugas besar untuk mata kuliah Visualisasi Data dan diikutsertakan dalam **Pacific Data Viz Challenge 2025**. Dasbor ini memvisualisasikan tantangan ganda yang dihadapi oleh negara-negara Kepulauan Pasifik: urgensi mitigasi perubahan iklim melalui energi terbarukan dan perlindungan terhadap dampak bencana alam.

Menggunakan data dari **Pacific Data Hub (Blue Pacific 2050)**, dashboard ini berfungsi sebagai alat bantu pengambilan keputusan bagi pembuat kebijakan untuk melihat apakah transisi energi yang dilakukan memiliki korelasi langsung dengan pengurangan dampak bencana.

**Tautan Aplikasi:** [**Live Demo Streamlit**](https://visdat-climate.streamlit.app/) | [**Repositori GitHub**](https://github.com/keishahz/DATAVIZ)

---

## Fitur Utama

Aplikasi ini dirancang dengan pendekatan *User-Centric* untuk memudahkan eksplorasi data yang kompleks:

1.  **Analisis Korelasi Multivariat**: Memvisualisasikan hubungan antara kapasitas energi terbarukan (Watt/kapita), emisi CO₂, dan jumlah populasi terdampak bencana.
2.  **Filter Data Dinamis**: Pengguna dapat memfilter berdasarkan Negara, Rentang Tahun, dan Indikator spesifik secara *real-time*.
3.  **Automated Insights**: Sistem secara otomatis menghasilkan narasi teks dan kesimpulan statistik berdasarkan data yang dipilih pengguna.
4.  **Visualisasi Interaktif**: Menggunakan Plotly untuk grafik yang responsif (Zoom, Pan, Hover details).

---

## Implementasi Teknis

Proyek ini dibangun menggunakan **Python** dengan library **Streamlit** untuk antarmuka web dan **Plotly Express** untuk visualisasi data tingkat lanjut.

### 1. Data Processing & Caching
Salah satu tantangan utama adalah menangani dataset besar agar dashboard tetap responsif. Saya mengimplementasikan `@st.cache_data` untuk mengoptimalkan waktu muat data.

```python
# Optimasi performa dengan Caching
@st.cache_data
def load_data():
    file_path = 'Blue Pacific 2050_ Climate Change And Disasters.csv'
    df = pd.read_csv(file_path)
    
    # Data Cleaning & Renaming
    df = df.rename(columns={
        'Pacific Island Countries and territories': 'Country',
        'TIME_PERIOD': 'Year',
        'OBS_VALUE': 'Renewable Capacity (W/capita)'
    })
    
    # Type Casting untuk konsistensi data
    df = df.dropna(subset=['Year', 'Renewable Capacity (W/capita)'])
    df['Year'] = df['Year'].astype(int)
    
    return df