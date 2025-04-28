# Data Overview
Jadi data ini akan digunakan untuk menganalisis kepadatan pengguna TransJakarta berdasarkan waktu untuk mendapatkan wawasan yang berguna dalam perencanaan operasional dan pelayanan. 

# Data Cleansing Steps
*1. Pengecekan Missing Value*
- Mengecek missing value pada kolom TapInStopName dan TapOutStopName.
- Data yang memiliki missing value di kedua kolom tersebut dihapus untuk menjaga keakuratan informasi perjalanan.

*2. Konversi Tipe Data Datetime dan Pembuatan Durasi*
- Kolom waktu tap-in dan tap-out dikonversi menjadi format datetime.
- Membuat kolom baru Duration yang berisi selisih waktu antara TapOut dan TapIn dalam satuan menit.
- Langkah ini penting untuk mengidentifikasi anomali perjalanan, seperti perjalanan yang tidak masuk akal.

*3. Pembuangan Durasi Tidak Wajar*
- Menghapus data dengan Duration yang terlalu cepat (contoh: di bawah 2 menit) atau terlalu lama (contoh: lebih dari 120 menit).
- Batasan ini ditentukan untuk merepresentasikan perjalanan yang realistis.

*4. Filter Berdasarkan Jam Operasional*
- Menghapus data TapIn yang terjadi di luar jam operasional layanan (misal: sebelum jam 5 pagi atau setelah jam 11 malam).

*5. Validasi Kolom Corridor*
- Mengecek kolom CorridorID dan CorridorName untuk menemukan data yang kosong, tidak konsisten, atau salah format.
- Menghapus baris data yang tidak memiliki informasi koridor atau memiliki ID yang tidak valid.

*6. Pengecekan Duplikat*

- Mengecek apakah terdapat data duplikat berdasarkan kombinasi kolom CardID, TapInTime, TapOutTime, TapInStopName, dan TapOutStopName.
- Duplikat yang ditemukan dihapus untuk menjaga keunikan setiap perjalanan.

*7. Validasi Kolom PayAmount*
- Memeriksa nilai PayAmount untuk mendeteksi potensi error seperti pembayaran nol (gratis/error sistem).
- Data dengan PayAmount yang tidak sesuai kebijakan tarif normal dianalisis lebih lanjut atau dibuang.

*8. Pembersihan Outlier di Durasi*
- Menggunakan metode statistik (seperti IQR atau Z-Score) untuk mengidentifikasi dan membuang durasi perjalanan yang outlier.

*9. Pembuatan Dataset Baru*
- Setelah semua proses cleansing selesai, dibuat file baru dalam format CSV yang berisi data bersih untuk analisis dan visualisasi lebih lanjut.

# Output
`transjakarta_clean.csv`
Berisi data perjalanan yang sudah melalui proses pembersihan dan siap digunakan untuk analisis lanjutan atau visualisasi.

# Hasil Visualisasi

*Kepadatan Berdasarkan Waktu*
Dari heatmap dan grafik garis yang dihasilkan, terlihat bahwa kepadatan pengguna TransJakarta mengalami puncaknya pada dua periode utama setiap harinya, yaitu pada pagi hari antara pukul 06.00 dan sore hari antara pukul 18. Lonjakan pada pagi hari umumnya berkaitan dengan jam keberangkatan kerja dan sekolah, sementara lonjakan sore hari disebabkan oleh aktivitas pulang kerja. 

*Kepadatan Berdasarkan Rute (Koridor)*
Visualisasi dalam bentuk bar chart memperlihatkan bahwa terdapat beberapa koridor TransJakarta yang jauh lebih padat dibandingkan koridor lainnya. Koridor-koridor utama seperti Rute Ciputat - CSW tercatat memiliki jumlah penumpang tertinggi sepanjang periode analisis. Sementara itu koridor-koridor yang melayani jalur pinggiran atau daerah baru cenderung memiliki jumlah perjalanan yang lebih rendah.

link tableu: [text](https://public.tableau.com/app/profile/raihan.alifianto/viz/Book2_17458506698900/Sheet2?publish=yes)
