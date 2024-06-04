**1. Buatlah presentasi langkah demi langkah tentang siklus CPU (fetch,decode,execute) utk mengeksekusi sebuah program. Jelaskan juga peran dari Bahasa pemrograman dan compiler, begitu juga dengan peran dari Sistem Operaso. Gunakan referensi : [Video referensi 1](https://www.youtube.com/watch?v=Z5JC9Ve1sfI) dan [Video referensi 2](https://www.youtube.com/watch?v=jFDMZpkUWCw)**

CPU memiliki tiga register , ini adalah bit penyimpanan cepat tempat CPU menyimpan nilai-nilai yang sedang dikerjakan saat ini
Ini adalah register yang melacak siklus instruksi kita:

<img width="295" alt="image" src="https://github.com/avendika/SysOP24-3123521011/assets/140131896/57b3b6d6-5ac8-4e29-808a-9e2440fbcb1d">

Ini yang memuat instruksi kita dari memori:

<img width="132" alt="image" src="https://github.com/avendika/SysOP24-3123521011/assets/140131896/fd584a81-0a7f-4cc6-ba9a-3d74678e4493">

Dan akumulasi :

<img width="125" alt="image" src="https://github.com/avendika/SysOP24-3123521011/assets/140131896/5dd648ea-9880-4b57-9320-62d97151b390">

Hal terkahir yang kita perluhkan dalam komputer sederhana adalah tempat untuk menyimpan intruksi dan nilai apapun yang akhirnya kita hitung itu adalah RAM

<img width="79" alt="image" src="https://github.com/avendika/SysOP24-3123521011/assets/140131896/a2d49463-74c5-4e1e-bd20-06036115841c">


Siklus fetch-execute adalah proses fundamental yang dilakukan oleh CPU (Central Processing Unit) untuk menjalankan instruksi dan menyelesaikan tugas dalam komputer. Siklus ini berulang terus-menerus selama komputer dihidupkan dan sedang menjalankan program.

penjelasan tentang tiga tahap utama dalam siklus fetch-execute:

<img width="133" alt="image" src="https://github.com/avendika/SysOP24-3123521011/assets/140131896/a286a066-0530-4b60-b298-6dbddbf6356f">

1. Fetch (Pengambilan):

Pada tahap ini, CPU mengambil instruksi dari memori utama. Memori utama adalah tempat penyimpanan data dan instruksi program yang diakses oleh CPU.
CPU menggunakan Program Counter (PC) untuk melacak alamat instruksi selanjutnya yang harus diambil. PC adalah sebuah register yang menyimpan alamat memori dari instruksi yang akan dieksekusi.
CPU kemudian mengambil instruksi dari alamat memori yang ditunjukkan oleh PC. Instruksi ini kemudian disimpan dalam Instruction Register (IR). IR adalah sebuah register yang menyimpan instruksi yang sedang diproses oleh CPU.

<img width="135" alt="image" src="https://github.com/avendika/SysOP24-3123521011/assets/140131896/324b40a8-04b6-4413-9e35-55901dd4ce74">

2. Decode (Pendekodean):

Pada tahap ini, CPU menerjemahkan instruksi yang disimpan dalam IR. Instruksi terdiri dari opcode dan operand.
Opcode adalah kode yang memberitahu CPU operasi apa yang harus dilakukan.
Operand adalah data yang digunakan dalam operasi.
CPU menggunakan Control Unit (CU) untuk menerjemahkan opcode dan operand. CU adalah bagian dari CPU yang bertanggung jawab untuk mengontrol dan mengarahkan operasi CPU.
CU kemudian meneruskan informasi yang diterjemahkan ke Arithmetic Logic Unit (ALU). ALU adalah bagian dari CPU yang bertanggung jawab untuk melakukan operasi aritmatika dan logika.

<img width="132" alt="image" src="https://github.com/avendika/SysOP24-3123521011/assets/140131896/97df8301-2841-40c7-bb32-43a448fd58d0">


3. Execute (Pelaksanaan):

Pada tahap ini, CPU melakukan operasi yang ditentukan oleh instruksi.
Jika instruksi adalah operasi aritmatika atau logika, ALU akan melakukan operasi tersebut.
Jika instruksi adalah operasi kontrol, CU akan mengarahkan aliran program ke alamat memori yang berbeda.
Setelah operasi selesai, CPU akan memperbarui PC untuk menunjuk ke instruksi selanjutnya yang harus diambil.
Siklus fetch-execute kemudian berulang dengan CPU mengambil instruksi selanjutnya dari memori, menerjemahkannya, dan menjalankannya. Siklus ini terus berulang selama komputer dihidupkan dan sedang menjalankan program.

Berikut adalah beberapa istilah penting yang terkait dengan siklus fetch-execute:

CPU: Central Processing Unit, unit pemrosesan pusat
Memori Utama: Tempat penyimpanan data dan instruksi program
Program Counter (PC): Register yang menyimpan alamat instruksi selanjutnya yang harus diambil
Instruction Register (IR): Register yang menyimpan instruksi yang sedang diproses
Control Unit (CU): Bagian dari CPU yang bertanggung jawab untuk mengontrol dan mengarahkan operasi CPU
Arithmetic Logic Unit (ALU): Bagian dari CPU yang bertanggung jawab untuk melakukan operasi aritmatika dan logika
Opcode: Kode yang memberitahu CPU operasi apa yang harus dilakukan
Operand: Data yang digunakan dalam operasi

  $ make
  $ make clean
  $ sudo make install
  $ sudo make uninstall
<img width="397" alt="image" src="https://github.com/avendika/SysOP24-3123521011/assets/140131896/e8e65ad2-8b63-4f18-add2-5212e4ec85ef">

$ iops64 $(nproc)
<img width="394" alt="image" src="https://github.com/avendika/SysOP24-3123521011/assets/140131896/2b133874-0f81-4a4d-9245-71e31f963776">

$ flops64 $(nproc)
<img width="396" alt="image" src="https://github.com/avendika/SysOP24-3123521011/assets/140131896/a3d83e5d-1da8-4c59-b704-964037ec19c4">

Kesimpulan tentang IOPS dan FLOPS
FLOPS (Floating-point Operations Per Second) dan IOPS (Input/Output Operations Per Second) adalah metrik penting untuk mengukur kemampuan komputer, namun keduanya mengukur aspek yang berbeda:

FLOPS mengukur performa CPU dalam melakukan operasi floating-point. Semakin tinggi nilai FLOPS, semakin cepat CPU dalam menangani perhitungan matematis kompleks yang sering dibutuhkan dalam aplikasi seperti engineering simulation, machine learning, dan scientific computing.
IOPS mengukur performa storage (hard disk drive, solid state drive) dalam melakukan operasi transfer data. Semakin tinggi nilai IOPS, semakin cepat storage dalam membaca dan menulis data, yang berdampak pada kecepatan keseluruhan sistem saat mengakses file dan aplikasi.
Hubungan antara IOPS dan FLOPS:

Hasil pengujian menunjukkan adanya korelasi positif antara IOPS dan FLOPS. Komputer dengan CPU yang lebih kuat (biasanya memiliki FLOPS lebih tinggi) juga cenderung memiliki storage yang lebih baik (menghasilkan IOPS lebih tinggi).  Namun perlu dicatat bahwa:

Keterkaitan ini tidak selalu pasti. Faktor lain seperti jenis storage dan konfigurasi sistem juga mempengaruhi performa.
Peningkatan RAM tidak selalu berdampak signifikan terhadap FLOPS dan IOPS. RAM lebih berperan dalam menjalankan program secara keseluruhan, bukan perhitungan individual atau transfer data.
Kesimpulan:

FLOPS dan IOPS memberikan gambaran mengenai kemampuan komputasi dan transfer data pada sebuah komputer.
Untuk memilih komputer yang sesuai, perlu dipertimbangkan jenis pekerjaan yang akan dilakukan. Aplikasi komputasi berat membutuhkan FLOPS tinggi, sedangkan aplikasi yang sering mengakses file besar membutuhkan IOPS tinggi.
Idealnya, komputer memiliki keseimbangan yang baik antara FLOPS dan IOPS untuk performa optimal.

Apabila Debian VM mu masih belum terdapat packeage gcc, make dan git, lakukan instalasi dan catat setiap langkahnya!

$ su -l
$ apt install make
$ apt install git
$ apt install gcc
$ git clone https://github.com/ferryastika/flops-iops
$ cd flops-iops



