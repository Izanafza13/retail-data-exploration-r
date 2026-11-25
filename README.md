# Eksplorasi Data Ritel Mitra Toserba Xera dengan R

Analisis eksplorasi data transaksi stok dan penjualan sebuah toserba menggunakan R dan Quarto. Proyek ini menjawab pertanyaan sederhana yang biasa muncul di ritel: bagaimana tren penjualan tiap bulan, siapa pelanggan terbesar, apakah stok barang terlalu banyak, dan di rentang harga berapa barang paling laku.

Studi kasus ini berasal dari kelas DQLab. Laporan akhirnya dirender menjadi satu file HTML dengan tema gelap.

## Dataset

- **Sumber:** DQLab, file `transaksi_stok_dan_penjualan.tsv` (dipisahkan tab).
- **Dimuat langsung dari URL**, jadi tidak perlu mengunduh data secara manual:

  ```r
  data <- read.csv("https://dqlabcdn.xeratic.com/dqlab-dataset/transaksi_stok_dan_penjualan.tsv",
                   header = TRUE, sep = "\t")
  ```

- **Kolom yang dipakai dalam analisis:** `Tanggal`, `Jenis.Transaksi` (Penjualan atau Stok Masuk), `Nama.Pelanggan`, `No.Transaksi`, `Harga`, dan `Jumlah`.

## Langkah analisis

1. **Import dan eksplorasi awal.** Memuat data lalu memeriksa 5 baris teratas, 5 baris terbawah, dan struktur data dengan `head()`, `tail()`, dan `str()`.
2. **Pembersihan tipe data.** Mengubah `Tanggal` menjadi tipe tanggal (format `dd-mm-yyyy`) dan membuat kolom `Bulan_Tahun`. Mengubah `Harga` menjadi numerik, dengan nilai kosong (`NA`) diganti 0.
3. **Penjualan per bulan.** Memfilter transaksi bertipe Penjualan, menjumlahkan per bulan dengan `aggregate()`, lalu menampilkannya dalam bar plot.
4. **Pelanggan dengan pembelian terbesar.** Menjumlahkan pembelian per pelanggan, mengurutkannya dari yang terbesar, dan mengambil 10 teratas.
5. **Barang masuk dan keluar.** Menggabungkan total Stok Masuk dan Penjualan tiap bulan dengan `merge()`, lalu membandingkannya dalam bar plot berdampingan.
6. **Harga dan jumlah transaksi.** Menghitung jumlah transaksi pada tiap harga, lalu menampilkan sebaran harga dalam histogram.

## Temuan utama

- **Penjualan menurun dari April sampai Juni 2020.** Penjualan tertinggi terjadi pada April 2020 dengan 1.753 barang terjual, sedangkan Juni 2020 hanya 170 barang.
- **Stok masih berlebih.** Rata-rata sekitar 4.000 barang masuk tiap bulan, sementara penjualan hanya sekitar 1.400 sampai 1.700 barang pada April dan Mei.
- **Barang paling laku ada di rentang Rp10.000 sampai Rp15.000.** Posisi kedua ditempati barang dengan harga di bawah Rp5.000.

## Cara menjalankan

Kebutuhan: [R](https://www.r-project.org/) dan [Quarto](https://quarto.org/docs/get-started/). Analisis hanya memakai fungsi bawaan R, jadi tidak ada paket tambahan yang perlu dipasang.

```bash
quarto render nama-file.qmd
```

Ganti `nama-file.qmd` dengan nama file laporan di repo ini. Pastikan `style.css` berada di folder yang sama, karena dipanggil oleh pengaturan tampilan laporan. Hasilnya berupa satu file HTML mandiri (`embed-resources: true`) yang bisa langsung dibuka di browser.

## Catatan

- Nilai `Harga` yang kosong diganti 0 mengikuti langkah analisis. Nilai 0 ini ikut terhitung di histogram, jadi sebaiknya diperiksa lebih lanjut jika hasilnya dipakai untuk keputusan bisnis.
- Rentang waktu data hanya mencakup beberapa bulan di tahun 2020, jadi tren yang terlihat belum tentu mewakili pola jangka panjang.

## Tentang saya

**Hamizan Afza Al Isyraqi**, lulusan S1 Teknik Informatika Universitas Trunojoyo Madura.

- Portofolio: [izanafza13.github.io/portoHamizan](https://izanafza13.github.io/portoHamizan/)
- GitHub: [Izanafza13](https://github.com/Izanafza13)
- LinkedIn: [izanafza](https://linkedin.com/in/izanafza)
