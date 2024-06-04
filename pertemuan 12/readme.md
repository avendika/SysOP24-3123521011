 1. ilustrasikan perbedaan serial, konkuren, paralel, dan konkuren paralel
dan berikan keterangan nya!

## Serial:
![image](https://github.com/avendika/SysOP24-3123521011/assets/140131896/427000e3-b1de-45d4-9c6f-3aba60b8bc40)


Bayangkan kamu sedang di kasir bank. Prosesnya harus berurutan, mulai dari mengambil nomor antrian, menunggu dipanggil, setor tunai/tarik tunai, sampai menerima struk. Setiap langkah harus selesai dulu sebelum ke langkah berikutnya. Ini adalah contoh proses serial.

### Keterangan:
Tugas dikerjakan satu demi satu, berurutan.
Tidak ada tugas yang dikerjakan bersamaan.
Contoh: Memasak nasi, mencuci baju, mengerjakan PR.

## Konkuren:
![image](https://github.com/avendika/SysOP24-3123521011/assets/140131896/e8de708e-74da-4d8f-a973-a507a0f3b4d7)

Bayangkan kamu dan temanmu mengerjakan tugas kelompok. Kamu mengerjakan bagian 1, temanmu mengerjakan bagian 2. Kalian berdua bekerja di waktu yang sama, tapi tidak saling membantu. Ini adalah contoh proses konkuren.

### Keterangan:
Tugas dikerjakan secara bersamaan, tetapi tidak saling terkait.
Tidak ada interaksi antar tugas.
Contoh: Mengunduh file sambil browsing internet, mendengarkan musik sambil belajar.

## Paralel:
![image](https://github.com/avendika/SysOP24-3123521011/assets/140131896/27299647-c202-4b98-b282-31519ef01984)


Bayangkan ada 4 CPU di komputermu. Saat kamu membuka banyak program, setiap program dikerjakan oleh CPU yang berbeda. Ini adalah contoh proses paralel.

### Keterangan:
Tugas dikerjakan secara bersamaan dan saling terkait.
Ada pembagian tugas antar unit pemrosesan.
Contoh: Menjalankan program video editing dengan banyak layer, rendering 3D, bermain game online.

## Konkuren Paralel:
![image](https://github.com/avendika/SysOP24-3123521011/assets/140131896/7ea63983-c153-47cf-aeea-1afa4dc3c5dc)


Bayangkan kamu dan temanmu mengerjakan tugas kelompok, tetapi kalian saling membantu dan berkolaborasi. Kamu mengerjakan bagian 1, temanmu mengerjakan bagian 2. Kalian berdua bekerja di waktu yang sama dan saling bertukar informasi. Ini adalah contoh proses konkuren paralel.

### Keterangan:
Tugas dikerjakan secara bersamaan, saling terkait, dan dengan interaksi antar tugas.
Ada pembagian tugas dan kolaborasi antar unit pemrosesan.
Contoh: Pengerjaan proyek besar dengan tim yang terbagi di beberapa lokasi, simulasi ilmiah yang kompleks.
Kesimpulan:

Serial: Tugas dikerjakan satu demi satu, berurutan.
Konkuren: Tugas dikerjakan secara bersamaan, tetapi tidak saling terkait.
Paralel: Tugas dikerjakan secara bersamaan dan saling terkait.
Konkuren Paralel: Tugas dikerjakan secara bersamaan, saling terkait, dan dengan interaksi antar tugas.

2. buat tulisan tentang dining problem dan reader writer problem

Dining Philosophers Problem
Definisi:
Dining Philosophers Problem adalah sebuah ilustrasi klasik dalam studi pemrograman concurrent dan masalah sinkronisasi dalam sistem operasi. Problema ini pertama kali diperkenalkan oleh Edsger Dijkstra pada tahun 1965. Situasinya menggambarkan lima filsuf yang duduk di meja bundar, di mana setiap filsuf memiliki satu piring makanan di depan mereka dan sebuah garpu di antara setiap pasangan filsuf.

Masalah:
Filsuf-filsuf ini membutuhkan dua garpu untuk makan, satu dari kiri dan satu dari kanan mereka. Mereka bergantian antara makan, berpikir, dan menunggu untuk makan. Problema muncul ketika semua filsuf mencoba untuk mengambil garpu secara bersamaan, yang dapat menyebabkan deadlock (kondisi di mana semua filsuf memegang satu garpu dan menunggu garpu yang lain yang tidak akan pernah datang) atau starvation (salah satu filsuf tidak pernah mendapatkan kedua garpu dan tidak bisa makan).

Solusi:

Algoritma Dijkstra:

Salah satu solusi adalah menghindari deadlock dengan mengatur bagaimana dan kapan filsuf mengambil garpu. Misalnya, seorang filsuf harus memastikan kedua garpu tersedia sebelum mengambilnya.
Strategi Hirarki Sumber Daya:

Menetapkan hirarki atau penomoran pada garpu dan setiap filsuf harus mengambil garpu dengan nomor lebih rendah terlebih dahulu sebelum mengambil garpu dengan nomor lebih tinggi. Ini menghindari lingkaran dan dengan demikian menghindari deadlock.
Penggunaan Semafor:

Menggunakan semafor untuk memastikan hanya satu filsuf yang bisa mengakses garpu tertentu pada satu waktu, mengontrol akses ke sumber daya kritis.
Reader-Writer Problem
Definisi:
Reader-Writer Problem adalah sebuah masalah sinkronisasi yang melibatkan akses ke suatu resource bersama (misalnya, database atau file) yang dibaca dan ditulis oleh beberapa proses. Tantangan utama adalah bagaimana mengatur proses baca (readers) dan tulis (writers) agar tidak saling mengganggu dan tetap menjaga konsistensi data.

Masalah:

Readers Priority (Prioritas Pembaca): Jika hanya ada pembaca, mereka bisa membaca secara bersamaan tanpa konflik. Namun, penulis harus memiliki akses eksklusif. Ini bisa menyebabkan writer starvation, di mana penulis tidak pernah mendapatkan akses karena selalu ada pembaca yang mengakses resource.
Writers Priority (Prioritas Penulis): Penulis memiliki prioritas lebih tinggi dari pembaca. Jika ada penulis yang menunggu, pembaca baru harus menunggu. Ini bisa menyebabkan reader starvation.
No Priority (Tanpa Prioritas): Menyeimbangkan kedua prioritas untuk menghindari starvation pada kedua pihak.
Solusi:

Menggunakan Semafor:

Semafor dapat digunakan untuk mengatur akses ke resource. Misalnya, menggunakan satu semafor untuk mengontrol akses pembaca dan satu lagi untuk penulis.
Algoritma Prioritas Pembaca:

Implementasi dengan dua semafor: satu untuk menunggu penulis, dan satu lagi untuk menunggu antrian pembaca. Penulis harus menunggu hingga semua pembaca selesai.
Algoritma Prioritas Penulis:

Pembaca hanya bisa membaca jika tidak ada penulis yang sedang menunggu atau menulis. Penulis memiliki hak eksklusif segera setelah ada penulis yang siap.
Pembagian Beban:

Kombinasi strategi di atas untuk memastikan bahwa tidak ada starvation baik pada pembaca maupun penulis, menggunakan penjadwalan yang adil.
Dalam kedua masalah ini, tujuan utamanya adalah untuk memastikan bahwa sistem tetap adil dan efisien tanpa deadlock atau starvation, memungkinkan akses yang aman dan terkoordinasi ke resource bersama dalam lingkungan concurrent.
