Masalah Bounded-Buffer:

![image](https://github.com/avendika/SysOP24-3123521011/assets/140131896/5a1c4683-6835-4f06-aded-feff43e43eeb)

Masalah Bounded-Buffer, juga dikenal sebagai masalah produsen-konsumen, adalah contoh klasik dari masalah sinkronisasi dalam pemrograman komputer. Ini menggambarkan situasi di mana dua proses berbagi buffer terbatas ukuran, yaitu:

Produsen menghasilkan data dan menempatkannya ke dalam buffer.
Konsumen mengambil data dari buffer.
Masalah ini menjadi lebih kompleks ketika beberapa produsen dan beberapa konsumen bekerja secara bersamaan, karena perlu ada cara untuk memastikan bahwa produsen tidak menempatkan data ke dalam buffer ketika sudah penuh dan konsumen tidak mengambil data ketika buffer kosong.

Detail Masalah
Buffer: Area memori yang digunakan untuk menyimpan data sementara antara produsen dan konsumen.
Ukuran Buffer: Batasan maksimum dari jumlah item yang bisa disimpan dalam buffer.
Produsen: Proses yang menghasilkan item dan memasukkannya ke dalam buffer.
Konsumen: Proses yang mengambil item dari buffer dan memprosesnya.
Masalah yang Muncul
Buffer Overflow: Terjadi ketika produsen mencoba menambahkan item ke buffer yang sudah penuh.
Buffer Underflow: Terjadi ketika konsumen mencoba mengambil item dari buffer yang kosong.
Deadlock: Terjadi ketika dua atau lebih proses saling menunggu selamanya, misalnya, produsen menunggu konsumen untuk mengosongkan buffer dan konsumen menunggu produsen untuk mengisi buffer.
Race Condition: Terjadi ketika dua atau lebih proses mengakses data bersama-sama secara bersamaan dan hasil akhirnya bergantung pada urutan eksekusi proses.
Penyelesaian Masalah
Untuk menyelesaikan masalah bounded-buffer, kita bisa menggunakan berbagai teknik sinkronisasi seperti semaphore, mutex, dan monitor. Di sini, kita akan menggunakan semaphore untuk mengelola akses ke buffer bersama.

Langkah Penyelesaian dengan Semaphore:
Semaphore untuk menghitung item dalam buffer:

empty: Menghitung jumlah slot kosong dalam buffer (diinisialisasi dengan ukuran buffer).
full: Menghitung jumlah item dalam buffer (diinisialisasi dengan 0).
Semaphore untuk eksklusifitas akses:

mutex: Mengamankan akses eksklusif ke buffer (diinisialisasi dengan 1).
Berikut adalah contoh kode menggunakan pseudocode untuk menunjukkan cara kerja semaphore dalam masalah bounded-buffer:
