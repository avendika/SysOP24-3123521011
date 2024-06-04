TUGAS PENDAHULUAN:
Jawablah pertanyaan-pertanyaan di bawah ini :
1. Apa yang dimaksud redirection?
2. Apa yang dimaksud pipeline?
3. Apa yang dimaksud perintah di bawah ini : echo, cat, more, sort, grep, wc, cut, uniq
Jawaban Pertanyaan :
1. Redirection:
Redirection adalah fitur di shell Linux yang memungkinkan Anda untuk mengarahkan input dan output dari suatu perintah ke file atau perangkat lain.
Jenis-jenis Redirection:
Input redirection: Mengarahkan input dari suatu perintah ke file atau perangkat lain. Contohnya:
command < file_input
Output redirection: Mengarahkan output dari suatu perintah ke file atau perangkat lain. Contohnya:
command > file_output
Append redirection: Menambahkan output dari suatu perintah ke file yang sudah ada. Contohnya:
command >> file_output

2. Pipeline:
Pipeline adalah fitur di shell Linux yang memungkinkan Anda untuk menggabungkan beberapa perintah sehingga output dari satu perintah menjadi input untuk perintah berikutnya.
Contoh:
command1 | command2 | command3

3. Penjelasan Perintah:
echo: Mencetak teks ke layar.
cat: Menampilkan isi file ke layar.
more: Menampilkan file ke layar secara per halaman.
sort: Mengurutkan baris-baris file berdasarkan kolom tertentu.
grep: Mencari baris-baris file yang mengandung pola tertentu.
wc: Menghitung jumlah baris, kata, dan karakter dalam file.
cut: Memotong kolom tertentu dari baris-baris file.
uniq: Menghilangkan baris-baris duplikat dalam file.
Contoh Penggunaan:
Menampilkan isi file data.txt dan menghitung jumlah barisnya:
cat data.txt | wc -l
Mencari baris-baris dalam file data.txt yang mengandung kata "Indonesia" dan mengurutkannya berdasarkan kolom nama:
cat data.txt | grep "Indonesia" | sort -k2
Memotong kolom pertama dan kedua dari file data.txt dan menampilkannya secara per halaman:
cat data.txt | cut -d, -f1,2 | more

Percobaan 1 : File descriptor
Output ke layar (standar output), input dari system (kernel)

$ ps
Output ke layar (standar output), input dari keyboard (standard input)

 $ cat
 hallo, apa khabar
 hallo, apa khabar
 exit dengan ^d
 exit dengan ^d
 [Ctrl-d]
Input nama direktori, output tidak ada (membuat direktori baru), bila terjadi error maka tampilan error pada layar (standard error)

$ mkdir mydir
$ mkdir mydir **(Terdapat pesan error)**
<img width="399" alt="image" src="https://github.com/avendika/SysOP24-3123521011/assets/140131896/a54581df-9e1b-46c8-a98d-31d1c12c795d">

Percobaan 2 : Pembelokan (redirection)
Pembelokan standar output
 $ cat 1> myfile.txt
 Ini adalah teks yang saya simpan ke file myfile.txt
Pembelokan standar input, yaitu input dibelokkan dari keyboard menjadi dari file
 $ cat 0< myfile.txt
 $ cat myfile.txt
Pembelokan standar error untuk disimpan di file
 $ mkdir mydir (Terdapat pesan error)
 $ mkdir mydir 2> myerror.txt
 $ cat myerror.txt
Notasi 2>&1 : pembelokan standar error (2>) adalah identik dengan file descriptor 1.
 $ ls filebaru (Terdapat pesan error)
 $ ls filebaru 2> out.txt
 $ cat out.txt
 $ ls filebaru 2> out.txt 2>&
 $ cat out.txt
<img width="395" alt="image" src="https://github.com/avendika/SysOP24-3123521011/assets/140131896/9195a6d4-adc0-4fa7-ba6d-fa6e0e999978">

Notasi 1>&2 (atau >&2) : pembelokan standar output adalah sama dengan file descriptor 2 yaitu standar error
$ echo “mencoba menulis file” 1> baru
$ cat filebaru 2> baru 1>&
$ cat baru
Notasi >> (append)
$ echo “kata pertama” > surat
$ echo “kata kedua” >> surat
$ echo “kata ketiga” >> surat
$ cat surat
$ echo “kata keempat” > surat
$ cat surat
Notasi here document (<<++ .... ++) digunakan sebagai pembatas input dari keyboard. Perhatikan bahwa tanda pembatas dapat digantikan dengan tanda apa saja, namun harus sama dan tanda penutup harus diberikan pada awal baris
$ cat <<++
Hallo, apa kabar?
Baik-baik saja?
Ok!
++
$ cat <<%%%
Hallo, apa kabar?
Baik-baik saja?
Ok!
%%%
Notasi – (input keyboard) adalah representan input dari keyboard. Artinya menampilkan file 1, kemudian menampilkan input dari keyboard dan menampilkan file 2. Perhatikan bahwa notasi “-“ berarti menyelipkan input dari keyboard
$ cat myfile.txt – surat
<img width="396" alt="image" src="https://github.com/avendika/SysOP24-3123521011/assets/140131896/d5c2f5e5-5679-40fb-b6b6-0f1dc463ea05">
<img width="400" alt="image" src="https://github.com/avendika/SysOP24-3123521011/assets/140131896/d7b5cbaf-7a38-49ab-817d-5f1362f64adc">

Percobaan 3 : Pipa (pipeline)
Operator pipa (|) digunakan untuk membuat eksekusi proses dengan melewati data langsung ke data lainnya.
$ who
$ who | sort
$ who | sort –r
$ who > tmp
$ sort tmp
$ rm tmp
$ ls –l /etc | more
$ ls –l /etc | sort | more
<img width="402" alt="image" src="https://github.com/avendika/SysOP24-3123521011/assets/140131896/fd52540b-5eed-42bf-88a7-414d911ff38e">

Untuk membelokkan standart output ke file, digunakan operator ">"
$ echo hello
$ echo hello > output
$ cat output
Untuk menambahkan output ke file digunakan operator ">>"
$ echo bye >> output
$ cat output
Untuk membelokkan standart input digunakan operator "<"
$ cat < output
Pembelokan standart input dan standart output dapat dikombinasikan tetapi tidak boleh menggunakan nama file yang sama sebagai standart input dan output.
$ cat < output > out
$ cat out
$ cat < output >> out
$ cat out
$ cat < output > output
$ cat output
$ cat < out >> out (Proses tidak berhenti)
[Ctrl-c]
$ cat out
<img width="398" alt="image" src="https://github.com/avendika/SysOP24-3123521011/assets/140131896/389d5b48-5c8b-458e-ab32-2c12fe14a2b2">

Percobaan 4 : Filter
Pipa juga digunakan untuk mengkombinasikan utilitas sistem untuk membentuk fungsi yang lebih kompleks
 $ w –h | grep <user>
 $ grep <user> /etc/passwd
 $ ls /etc | wc
 $ ls /etc | wc –l
<img width="400" alt="image" src="https://github.com/avendika/SysOP24-3123521011/assets/140131896/04fcb1fe-da59-4b80-a906-b8f4638b9a53">

 $ cat > kelas1.txt
 Badu
 Zulkifli
 Yulizir
 Yudi
 Ade
 [Ctrl-d]
 $ cat > kelas2.txt
 Budi
 Gama
 Asep
 Muchlis
 [Ctrl-d]
 $ cat kelas1.txt kelas2.txt | sort
 $ cat kelas1.txt kelas2.txt > kelas.txt
 $ cat kelas.txt | sort | uniq
<img width="400" alt="image" src="https://github.com/avendika/SysOP24-3123521011/assets/140131896/97762d80-147d-4de7-a471-729a368fd587">

LATIHAN:

1. Lihat daftar secara lengkap pada direktori aktif, belokkan tampilan standard output ke file baru.
2. Lihat daftar secara lengkap pada direktori /etc/passwd, belokkan tampilan standard output ke file baru tanpa menghapus file baru sebelumnya.
3. Urutkan file baru dengan cara membelokkan standard input.
4. Urutkan file baru dengan cara membelokkan standard input dan standard output ke file baru.urut.
5. Buatlah direktori latihan2 sebanyak 2 kali dan belokkan standard error ke file rmdirerror.txt.
6. Urutkan kalimat berikut:
Jakarta
Bandung
Surabaya
Padang

JAWABAN
1.
 
![image](https://github.com/avendika/SysOP24-3123521011/assets/140131896/f1370fd2-1d7f-43ef-8969-a4ba7f4a9cdc)

$ ls -l filebaru.txt
Perintah ini digunakan untuk menampilkan informasi detail tentang file filebaru.txt. Opsi -l (long) digunakan untuk menampilkan informasi yang lebih lengkap, termasuk izin file, pemilik file, ukuran file, dan tanggal modifikasi file.
$ cat filebaru.txt
Perintah ini digunakan untuk menampilkan isi file filebaru.txt.

2.
![image](https://github.com/avendika/SysOP24-3123521011/assets/140131896/59464e8d-1ab1-4c9a-ba82-9766f2b18cb9)

$ cat /etc/passwd >> filebaru.txt
Perintah ini digunakan untuk menyalin isi file /etc/passwd ke file baru bernama filebaru.txt.
$ cat filebaru.txt
Perintah ini digunakan untuk menampilkan isi file filebaru.txt.

3.
 
![image](https://github.com/avendika/SysOP24-3123521011/assets/140131896/3ca4dba5-c533-4bb9-bd0f-ba82513d14e7)

$ sort < filebaru.txt
Penjelasan:
sort: Perintah ini digunakan untuk mengurutkan baris teks dalam suatu file.
<: Operator ini digunakan untuk mengarahkan input dari suatu file ke perintah. Dalam hal ini, input dari file filebaru.txt diarahkan ke perintah sort.
filebaru.txt: File yang ingin diurutkan isinya.
Output:
Perintah ini akan menampilkan isi file filebaru.txt yang telah diurutkan berdasarkan urutan alfabetis.
 
4.
 
![image](https://github.com/avendika/SysOP24-3123521011/assets/140131896/25c6d8d0-0e9c-4e1f-bc03-bb5e6efcd5dd)


Perintah 1:
Perintah ini digunakan untuk mengarahkan output dari perintah cat ke file filebaru.urut.
•	cat: Perintah ini digunakan untuk menampilkan isi file. Dalam hal ini, digunakan untuk mengarahkan output dari perintah cat ke file filebaru.urut.
•	filebaru.txt: File yang ingin diurutkan isinya.
•	>: Operator ini digunakan untuk mengarahkan output dari suatu perintah ke file. Dalam hal ini, output dari perintah cat diarahkan ke file filebaru.urut.
Perintah 2:
Perintah ini digunakan untuk menampilkan isi file filebaru.urut.
•	cat: Perintah ini digunakan untuk menampilkan isi file.
•	filebaru.urut: File yang ingin ditampilkan isinya.

5.
![image](https://github.com/avendika/SysOP24-3123521011/assets/140131896/af641fdd-296d-4e6a-bcaa-c8622961ad4b)

Perintah pertama:
mkdir latihan2
Perintah ini digunakan untuk membuat direktori baru dengan nama "latihan2".
Perintah kedua:
mkdir latihan2 2> rmdirerror.txt
Perintah ini sama dengan perintah pertama, namun dengan tambahan pengalihan output   error. Pengalihan output error ini akan mengarahkan semua pesan error yang dihasilkan oleh perintah mkdir ke dalam file teks dengan nama "rmdirerror.txt".
Penjelasan output:
Pada output, terlihat bahwa perintah mkdir menghasilkan pesan error:
mkdir: cannot create directory 'latihan2': File exists
Pesan error ini menunjukkan bahwa direktori dengan nama "latihan2" sudah ada, sehingga tidak dapat dibuat kembali.

6.
 
![image](https://github.com/avendika/SysOP24-3123521011/assets/140131896/0ee67d9e-6780-41c8-bcb0-8de7026ab486)

perintah sort digunakan untuk mengurutkan daftar kota di Indonesia. Daftar kota tersebut dimasukkan ke dalam perintah menggunakan operator heredoc. Operator heredoc diawali dengan << dan diakhiri dengan @@@.
Berikut adalah penjelasan tentang bagaimana perintah sort bekerja:
1.	Perintah sort membaca baris teks dari inputnya. Dalam gambar, inputnya adalah daftar kota yang dimasukkan menggunakan operator heredoc.
2.	Perintah sort mengurutkan baris teks berdasarkan urutan abjad.
3.	Perintah sort mencetak baris teks yang telah diurutkan ke outputnya.

7.
 
![image](https://github.com/avendika/SysOP24-3123521011/assets/140131896/f66bd1af-2dfe-4828-8b8a-53791a479c14)

Perintah pertama:
$ cat filebaru.urut | wc
Perintah ini menggunakan utilitas cat untuk membaca isi file filebaru.urut dan mengirimkannya ke utilitas wc. Utilitas wc kemudian menghitung jumlah baris, kata, dan karakter dalam file.
Output:
68  262  3997  
Output menunjukkan bahwa file filebaru.urut memiliki 68 baris, 3997 karakter, dan 262 kata.
Perintah kedua:
$ cat filebaru.urut | wc -l
Perintah ini menggunakan utilitas cat untuk membaca isi file filebaru.urut dan mengirimkannya ke utilitas wc dengan opsi -l. Opsi -l memerintahkan wc untuk hanya menghitung jumlah baris dalam file.
Output:
68
Output menunjukkan bahwa file filebaru.urut memiliki 68 baris.
Perintah ketiga:
avendika@avendika-VirtualBox: $ cat filebaru.urut | wc -c
Perintah ini menggunakan utilitas cat untuk membaca isi file filebaru.urut dan mengirimkannya ke utilitas wc dengan opsi -c. Opsi -c memerintahkan wc untuk hanya menghitung jumlah karakter dalam file.
Output:
3997
Output menunjukkan bahwa file filebaru.urut memiliki 3997 karakter.
Perintah keempat:
avendika@avendika-VirtualBox: $ cat filebaru.urut | wc -w
Perintah ini menggunakan utilitas cat untuk membaca isi file filebaru.urut dan mengirimkannya ke utilitas wc dengan opsi -w. Opsi -w memerintahkan wc untuk hanya menghitung jumlah kata dalam file.
Output:
262
Output menunjukkan bahwa file filebaru.urut memiliki 262 kata.
	
8.
 
![image](https://github.com/avendika/SysOP24-3123521011/assets/140131896/45503491-3849-4309-bbc3-dd5b4e51b43e)

Baris 1:
$ cat > hello.txt
•	Baris ini menggunakan perintah cat.
•	Biasanya, cat digunakan untuk melihat isi suatu file.
•	Namun, pada kasus ini, operator pengalihan > digunakan.
•	Operator ini memberitahu cat untuk menimpa isi file yang ditentukan (dalam kasus ini, "hello.txt") dengan apa pun yang diketikkan setelahnya sampai pengguna menekan Ctrl+D (karakter akhir file).
Baris 2-4:
•	dog cat
•	cat duck
•	chicken cat
•	chicken duck
•	dog duck
Baris-baris ini merupakan teks yang dimasukkan pengguna ke dalam file "hello.txt".
Karena cat berada dalam mode menimpa karena operator pengalihan, setiap baris yang dimasukkan menggantikan isi file sebelumnya.
Baris 5:
cat hello.txt | sort | uniq
•	Baris ini menggunakan pipa (|) untuk menghubungkan tiga perintah.
•	Perintah pertama, cat hello.txt, membaca isi file "hello.txt".
•	Pipa (|) mengirimkan output dari cat hello.txt (isi file) sebagai input ke perintah berikutnya, sort.
•	Perintah sort mengurutkan baris-baris teks yang diterimanya secara alfabetis.
•	Sekali lagi, pipa (|) mengirimkan output dari sort (baris-baris yang diurutkan) sebagai input ke perintah berikutnya, uniq.
•	Perintah uniq menghapus baris-baris duplikat dari input yang diurutkan yang diterimanya.
Output:
cat duck
chicken cat
chicken duck
dog cat
dog chicken
dog duck
•	Output menunjukkan isi "hello.txt" setelah diurutkan dan duplikatnya dihapus.
Perintah cat hello.txt | grep "dog" | grep -v "cat" 
digunakan untuk mencari semua baris yang mengandung kata "dog" dan kemudian mengecualikan baris yang juga mengandung kata "cat".	

LAPORAN RESMI:
Analisa hasil percobaan 1 sampai dengan 4, untuk setiap perintah jelaskan tampilannya.
Kerjakan latihan diatas dan analisa hasilnya
Berikan kesimpulan dari praktikum ini.

Jawaban Laporan Resmi : 
Output ke layar (standar output), input dari sistem (kernel)
 
![image](https://github.com/avendika/SysOP24-3123521011/assets/140131896/ad1e76bd-44a1-406b-ae07-53b2e753852e)

Perintah ps (singkatan dari "process status") digunakan untuk menampilkan informasi tentang proses yang sedang berjalan di sistem operasi Linux. Perintah ini dapat digunakan untuk memantau kinerja sistem, mendiagnosis masalah, dan mengelola proses.
Bentuk umum:

Output ke layar (standar output), input dari keyboard (standar imput)
 
![image](https://github.com/avendika/SysOP24-3123521011/assets/140131896/7071a45d-05f4-4741-8dbf-97e12aa62d48)

Perintah cat (singkatan dari "concatenate") adalah salah satu perintah dasar di sistem operasi Linux yang digunakan untuk menampilkan isi file ke terminal atau menggabungkan beberapa file menjadi satu file baru.

Input dari keyboard dan output ke alamat internet
 
![image](https://github.com/avendika/SysOP24-3123521011/assets/140131896/c236be57-512d-4c8e-bb93-b5f9a4ad3de2)

Perintah pertama:
mail aven@it.student.pens.ac.id
Perintah ini digunakan untuk mengirim email ke alamat aven@it.student.pens.ac.id.
Perintah kedua:
Cc: avendikawahyusaputra@gmail.com
Perintah ini digunakan untuk menambahkan alamat email avendikawahyusaputra@gmail.com sebagai Cc (carbon copy) pada email.
Perintah ketiga:
Subject: Pengingat
Perintah ini digunakan untuk menentukan subjek email sebagai "Pengingat".
Perintah keempat:
Jangan lupa besuk tanggal 2 maret ayo muncak di penanggungan
Perintah ini berisi isi email yang ingin disampaikan, yaitu pengingat untuk pendakian gunung Penanggungan pada tanggal 2 Maret.

Input nama direktori, output tidak ada (membuat direktori baru), bila terjadi error maka tampilan error pada layar (standar error).
 	
![image](https://github.com/avendika/SysOP24-3123521011/assets/140131896/8a05fc34-e89b-46a5-83cf-da04b32d2f84)

Perintah pertama:
mkdir latihan2
Perintah ini digunakan untuk membuat direktori baru dengan nama "latihan2".
Perintah kedua:
mkdir latihan2 2> rmdirerror.txt
Perintah ini memiliki dua fungsi:
1.	mkdir latihan2: Membuat direktori baru dengan nama "latihan2".
2.	2> rmdirerror.txt: Mengarahkan output error dari perintah mkdir ke file "rmdirerror.txt".
Perintah ketiga:
cat rmdirerror.txt
Perintah ini digunakan untuk menampilkan isi file "rmdirerror.txt".
Isi file rmdirerror.txt:
mkdir: cannot create directory 'latihan2': File exists
Isi file menunjukkan bahwa direktori "latihan2" sudah ada, sehingga perintah mkdir gagal dijalankan.







