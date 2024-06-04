4.1 Berikan tiga contoh pemrograman di mana multithreading memberikan kinerja yang lebih baik daripada solusi single-threaded. Menjawab:

A. Server Web yang melayani setiap permintaan dalam thread terpisah.

B. Aplikasi yang diparalelkan seperti perkalian matriks di mana bagian-bagian matriks yang berbeda dapat dikerjakan secara paralel.

C. Program GUI interaktif seperti debugger dimana thread digunakan untuk memantau input pengguna, thread lain mewakili aplikasi yang sedang berjalan, dan thread ketiga memantau kinerja.

4.2 Apa perbedaan antara thread tingkat pengguna dan thread tingkat kernel? Dalam kondisi apa satu jenis lebih baik dibandingkan jenis lainnya?

Menjawab:

A. Thread tingkat pengguna tidak diketahui oleh kernel, sedangkan kernel mengetahui thread kernel.

B. Pada sistem yang menggunakan pemetaan M:1 atau M:N, thread pengguna dijadwalkan oleh pustaka thread dan kernel menjadwalkan thread kernel.

C. Thread kernel tidak perlu dikaitkan dengan suatu proses sedangkan setiap thread pengguna termasuk dalam suatu proses. Pemeliharaan thread kernel umumnya lebih mahal daripada thread pengguna karena harus direpresentasikan dengan struktur data kernel.

4.3 Jelaskan tindakan yang diambil oleh kernel untuk beralih konteks antar thread tingkat kernel.

Menjawab:

Peralihan konteks antar thread kernel biasanya memerlukan penyimpanan nilai register CPU dari thread yang dialihkan dan memulihkan register CPU dari thread baru yang dijadwalkan.

4.4 Sumber daya apa yang digunakan saat thread dibuat? Apa perbedaannya dengan yang digunakan saat proses dibuat?

Menjawab:

Karena thread lebih kecil dari proses, pembuatan thread biasanya menggunakan lebih sedikit sumber daya dibandingkan pembuatan proses. Membuat suatu proses memerlukan alokasi blok kontrol proses (PCB), sebuah struktur data yang agak besar. PCB mencakup peta memori, daftar file yang terbuka, dan variabel lingkungan. Mengalokasikan dan mengelola peta memori biasanya merupakan aktivitas yang paling memakan waktu. Membuat thread pengguna atau kernel melibatkan pengalokasian struktur data kecil untuk menampung set register, tumpukan, dan prioritas.

4.5 Asumsikan bahwa sistem operasi memetakan thread tingkat pengguna ke kernel menggunakan model banyak ke banyak dan pemetaan dilakukan melalui LWP. Selain itu, sistem ini memungkinkan pengembang membuat thread real-time untuk digunakan dalam sistem real-time. Apakah perlu untuk mengikat thread real-time ke LWP? Menjelaskan.

Menjawab:

Ya. Pengaturan waktu sangat penting untuk aplikasi real-time. Jika thread ditandai sebagai real-time namun tidak terikat ke LWP, thread mungkin harus menunggu untuk dipasang ke LWP sebelum dijalankan. Pertimbangkan apakah thread real-time sedang berjalan 
(terpasang ke LWP) dan kemudian melanjutkan ke blok (yaitu harus melakukan I/O, telah didahului oleh thread real-time dengan prioritas lebih tinggi, sedang menunggu kunci pengecualian bersama, dll.) Saat thread real-time diblokir, LWP yang dilampirkannya 
telah ditetapkan ke thread lain. Ketika thread real-time telah dijadwalkan untuk dijalankan kembali, thread tersebut harus menunggu terlebih dahulu untuk dilampirkan ke LWP. Dengan mengikat LWP ke thread real-time, Anda memastikan thread akan dapat berjalan 
dengan penundaan minimal setelah dijadwalkan.
