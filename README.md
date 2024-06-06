# Data-Analis-PutriAulia
## LAPORAN DATA ANALITIK PT. INVESTASI MAJU JAYA (IMJ) MENGGUNAKAN BAHASA PEMROGRAMAN PYTHON DAN SOFTWARE VISUAL STUDIO CODE

Oleh: Putri Aulia

NIM: 12030122130121

Matkul: Pengkodean Kelas E

## LANGKAH-LANGKAH DALAM PROSES DATA ANALITIK PT. INVESTASI MAJU JAYA (IMJ)

# 1: Pengumpulan Data

import pandas as pd

import matplotlib .pyplot as plt

import seaborn as sns

>>Membaca data dari file CSV

data = pd.read_csv('data_transaksi_imj.csv')

print(data.head())

# 2: Data Cleaning

>>Memeriksa apakah ada nilai yang tidak valid

print(data['Tanggal'].head()) 

print(data['Tanggal'].unique())

>>Membersihkan data dengan menghapus spasi di awal/akhir

data['Tanggal'] = data['Tanggal'].str.strip()

>>Memeriksa format tanggal yang tidak valid

valid_date_format = pd.to_datetime(data['Tanggal'], errors='coerce')

invalid_dates = data[valid_date_format.isna()]

print("Invalid dates:\n", invalid_dates)

>>Menghapus baris dengan tanggal tidak valid

data = data.drop(invalid_dates.index)

# 3: Konversi Kolom “Tanggal” Menjadi Tipe Datetime

>>Konversi kolom 'Tanggal' menjadi tipe datetime

data['Tanggal'] = pd.to_datetime(data['Tanggal'])

print(data.info())

# 4: Menambahkan Kolom Tahun dan Bulan

>>Mengekstrak tahun dan bulan dari kolom 'Tanggal'

data['Tahun'] = data['Tanggal'].dt.year

data['Bulan'] = data['Tanggal'].dt.month

print(data.head())

# 5: Exploratory Data Analysis (EDA)

>>Visualisasi distribusi kategori transaksi

sns.countplot(x='Kategori', data=data)

plt.title('Distribusi Kategori Transaksi')

plt.show()

>>Visualisasi jumlah transaksi per bulan

data.groupby('Bulan')['Jumlah (Rp)'].sum().plot(kind='bar')

plt.title('Jumlah Transaksi Per Bulan')

plt.show()

# 6: Identifikasi Kesalahan Audit

>>Mengidentifikasi transaksi penjualan saham mencurigakan

penjualan_saham = data[data['Kategori'] == 'Penjualan Saham']

print(penjualan_saham.describe())

>>Mengidentifikasi transaksi pengeluaran mencurigakan

pengeluaran = data[data['Kategori'] == 'Pengeluaran']

print(pengeluaran.describe())

# 7: Visualisasi Kesalahan

>>Visualisasi penjualan saham mencurigakan

plt.figure(figsize=(10, 6))

sns.boxplot(x='Bulan', y='Jumlah (Rp)', data=penjualan_saham)

plt.title('Penjualan Saham Per Bulan')

plt.show()

>>Visualisasi pengeluaran mencurigakan

plt.figure(figsize=(10, 6))

sns.boxplot(x='Bulan', y='Jumlah (Rp)', data=pengeluaran)

plt.title('Pengeluaran Per Bulan')

plt.show()

# 8: Perbaikan data Yang Salah

>>Identifikasi dan perbaiki transaksi yang salah. Misalnya, kita mendeteksi bahwa penjualan saham pada bulan Desember terlalu tinggi

data.loc[data['Transaksi_ID'] == 'TXN1012', 'Jumlah (Rp)'] = 5_000_000 

>>Verifikasi perbaikan

print(data.loc[data['Transaksi_ID'] == 'TXN1012'])

# 9: Visualisasi Setelah Perbaikan

>>Visualisasi penjualan saham setelah perbaikan

plt.figure(figsize=(10, 6))

sns.boxplot(x='Bulan', y='Jumlah (Rp)', data=penjualan_saham)

plt.title('Penjualan Saham Per Bulan (Setelah Perbaikan)')

plt.show()

>>Visualisasi jumlah transaksi per bulan setelah perbaikan

plt.figure(figsize=(10, 6))

data.groupby('Bulan')['Jumlah (Rp)'].sum().plot(kind='bar')

plt.title('Jumlah Transaksi Per Bulan (Setelah Perbaikan)')

plt.show()











