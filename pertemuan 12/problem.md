Masalah Bounded-Buffer:

![image](https://github.com/avendika/SysOP24-3123521011/assets/140131896/5a1c4683-6835-4f06-aded-feff43e43eeb)

Masalah Bounded-Buffer, juga dikenal sebagai masalah produsen-konsumen, adalah contoh klasik dari masalah sinkronisasi dalam pemrograman komputer. Ini menggambarkan situasi di mana dua proses berbagi buffer terbatas ukuran, yaitu:

1. **Produsen** menghasilkan data dan menempatkannya ke dalam buffer.
2. **Konsumen** mengambil data dari buffer.

Masalah ini menjadi lebih kompleks ketika beberapa produsen dan beberapa konsumen bekerja secara bersamaan, karena perlu ada cara untuk memastikan bahwa produsen tidak menempatkan data ke dalam buffer ketika sudah penuh dan konsumen tidak mengambil data ketika buffer kosong.

### Detail Masalah

- **Buffer:** Area memori yang digunakan untuk menyimpan data sementara antara produsen dan konsumen.
- **Ukuran Buffer:** Batasan maksimum dari jumlah item yang bisa disimpan dalam buffer.
- **Produsen:** Proses yang menghasilkan item dan memasukkannya ke dalam buffer.
- **Konsumen:** Proses yang mengambil item dari buffer dan memprosesnya.

### Masalah yang Muncul

1. **Buffer Overflow:** Terjadi ketika produsen mencoba menambahkan item ke buffer yang sudah penuh.
2. **Buffer Underflow:** Terjadi ketika konsumen mencoba mengambil item dari buffer yang kosong.
3. **Deadlock:** Terjadi ketika dua atau lebih proses saling menunggu selamanya, misalnya, produsen menunggu konsumen untuk mengosongkan buffer dan konsumen menunggu produsen untuk mengisi buffer.
4. **Race Condition:** Terjadi ketika dua atau lebih proses mengakses data bersama-sama secara bersamaan dan hasil akhirnya bergantung pada urutan eksekusi proses.

### Penyelesaian Masalah

Untuk menyelesaikan masalah bounded-buffer, kita bisa menggunakan berbagai teknik sinkronisasi seperti semaphore, mutex, dan monitor. Di sini, kita akan menggunakan semaphore untuk mengelola akses ke buffer bersama.

#### Langkah Penyelesaian dengan Semaphore:

1. **Semaphore untuk menghitung item dalam buffer:** 
   - `empty`: Menghitung jumlah slot kosong dalam buffer (diinisialisasi dengan ukuran buffer).
   - `full`: Menghitung jumlah item dalam buffer (diinisialisasi dengan 0).

2. **Semaphore untuk eksklusifitas akses:** 
   - `mutex`: Mengamankan akses eksklusif ke buffer (diinisialisasi dengan 1).

Berikut adalah contoh kode menggunakan pseudocode untuk menunjukkan cara kerja semaphore dalam masalah bounded-buffer:

```python
# Inisialisasi
empty = Semaphore(N)   # N adalah ukuran buffer
full = Semaphore(0)
mutex = Semaphore(1)
buffer = []

# Fungsi produsen
def producer():
    while True:
        item = produce_item()
        empty.wait()        # Tunggu jika buffer penuh
        mutex.wait()        # Tunggu akses eksklusif ke buffer
        buffer.append(item) # Tambah item ke buffer
        mutex.signal()      # Lepaskan akses eksklusif ke buffer
        full.signal()       # Sinyal bahwa ada satu item baru dalam buffer

# Fungsi konsumen
def consumer():
    while True:
        full.wait()         # Tunggu jika buffer kosong
        mutex.wait()        # Tunggu akses eksklusif ke buffer
        item = buffer.pop(0)# Ambil item dari buffer
        mutex.signal()      # Lepaskan akses eksklusif ke buffer
        empty.signal()      # Sinyal bahwa ada satu slot kosong baru dalam buffer
        consume_item(item)
```

#### Penjelasan Pseudocode:
- `empty.wait()`: Produsen akan menunggu hingga ada slot kosong di buffer.
- `mutex.wait()`: Produsen atau konsumen akan menunggu hingga mendapatkan akses eksklusif ke buffer.
- `buffer.append(item)`: Produsen menambah item ke buffer.
- `buffer.pop(0)`: Konsumen mengambil item dari buffer.
- `mutex.signal()`: Produsen atau konsumen melepaskan akses eksklusif ke buffer.
- `full.signal()`: Produsen memberi sinyal bahwa ada item baru di buffer.
- `empty.signal()`: Konsumen memberi sinyal bahwa ada slot kosong baru di buffer.

Dengan cara ini, kita memastikan bahwa produsen tidak akan menempatkan data ke dalam buffer ketika sudah penuh dan konsumen tidak akan mengambil data ketika buffer kosong. Semaphore memastikan bahwa hanya satu proses yang mengakses buffer pada satu waktu, sehingga mencegah kondisi balapan dan deadlock.

**Dining Philosophers Problem.**

![image](https://github.com/avendika/SysOP24-3123521011/assets/140131896/e29f3fcb-7c60-45f9-87a4-f05a9c904478)

**Masalah Dining Philosophers:**

Masalah Dining Philosophers adalah salah satu masalah klasik dalam ilmu komputer yang menggambarkan tantangan sinkronisasi dan penghindaran deadlock. Masalah ini diusulkan oleh Edsger Dijkstra pada tahun 1965.

### Deskripsi Masalah

Ada lima filsuf yang duduk di sekitar meja melingkar. Di antara setiap dua filsuf, ada satu garpu. Setiap filsuf membutuhkan dua garpu (satu di kanan dan satu di kiri) untuk makan. Proses ini dapat dijelaskan dalam tiga fase:

1. **Berpikir (Thinking):** Filsuf berpikir tentang dunia dan hidupnya.
2. **Lapar (Hungry):** Filsuf menjadi lapar dan berusaha mengambil dua garpu untuk makan.
3. **Makan (Eating):** Setelah mendapatkan kedua garpu, filsuf mulai makan. Setelah selesai, mereka meletakkan kedua garpu kembali dan mulai berpikir lagi.

### Masalah yang Muncul

1. **Deadlock:** Terjadi ketika setiap filsuf mengambil garpu sebelah kanan (atau sebelah kiri) secara bersamaan dan menunggu garpu yang lain sehingga tidak ada yang bisa makan.
2. **Kelaparan (Starvation):** Terjadi ketika satu atau lebih filsuf tidak pernah mendapatkan kesempatan untuk makan karena garpu terus-menerus diambil oleh filsuf lain.

### Penyelesaian Masalah

Untuk menghindari deadlock dan starvation, kita bisa menggunakan beberapa teknik sinkronisasi seperti semaphore atau mutex. Di sini kita akan membahas solusi menggunakan semaphore.

#### Pendekatan Semaphore:

Kita akan menggunakan semaphore untuk mewakili garpu, dengan setiap semaphore diinisialisasi dengan nilai 1 (menandakan bahwa garpu tersedia).

##### Pseudocode:

```python
# Inisialisasi
import threading
import time
import random

class Philosopher(threading.Thread):
    def __init__(self, name, left_fork, right_fork):
        threading.Thread.__init__(self)
        self.name = name
        self.left_fork = left_fork
        self.right_fork = right_fork

    def run(self):
        while True:
            self.think()
            self.hungry()
            self.eat()

    def think(self):
        print(f"{self.name} is thinking.")
        time.sleep(random.uniform(1, 3))

    def hungry(self):
        print(f"{self.name} is hungry.")
        # Mengambil kedua garpu
        self.left_fork.acquire()
        print(f"{self.name} picked up left fork.")
        self.right_fork.acquire()
        print(f"{self.name} picked up right fork.")

    def eat(self):
        print(f"{self.name} is eating.")
        time.sleep(random.uniform(1, 3))
        # Meletakkan kedua garpu
        self.left_fork.release()
        print(f"{self.name} put down left fork.")
        self.right_fork.release()
        print(f"{self.name} put down right fork.")

# Membuat semaphore untuk setiap garpu
forks = [threading.Semaphore(1) for _ in range(5)]

# Membuat dan menjalankan lima filsuf
names = ["Philosopher 1", "Philosopher 2", "Philosopher 3", "Philosopher 4", "Philosopher 5"]
philosophers = [Philosopher(names[i], forks[i], forks[(i + 1) % 5]) for i in range(5)]

for philosopher in philosophers:
    philosopher.start()
```

#### Penjelasan Pseudocode:

1. **Class Philosopher:** Mengimplementasikan perilaku seorang filsuf dengan metode `think`, `hungry`, dan `eat`.
2. **Semaphore Forks:** Menginisialisasi lima semaphore untuk lima garpu.
3. **Proses Filsuf:**
   - `think`: Filsuf berpikir selama waktu acak.
   - `hungry`: Filsuf mencoba mengambil garpu kiri dan kanan.
   - `eat`: Filsuf makan selama waktu acak dan kemudian meletakkan kembali garpu.

#### Meminimalkan Deadlock:

Pendekatan di atas bisa menyebabkan deadlock jika semua filsuf mengambil garpu kiri secara bersamaan. Untuk menghindari deadlock, kita bisa menggunakan beberapa pendekatan, seperti:

1. **Asymmetric Approach:** Satu filsuf mengambil garpu kanan terlebih dahulu dan yang lainnya mengambil garpu kiri terlebih dahulu.
2. **Resource Hierarchy Solution:** Menomori setiap garpu dan setiap filsuf harus mengambil garpu dengan urutan tertentu (misalnya, selalu mengambil garpu dengan nomor lebih kecil dulu).

Berikut adalah contoh modifikasi untuk pendekatan Asymmetric:

```python
# Pendekatan Asymmetric untuk menghindari deadlock
class Philosopher(threading.Thread):
    def __init__(self, name, left_fork, right_fork, index):
        threading.Thread.__init__(self)
        self.name = name
        self.left_fork = left_fork
        self.right_fork = right_fork
        self.index = index

    def run(self):
        while True:
            self.think()
            self.hungry()
            self.eat()

    def think(self):
        print(f"{self.name} is thinking.")
        time.sleep(random.uniform(1, 3))

    def hungry(self):
        print(f"{self.name} is hungry.")
        if self.index % 2 == 0:
            self.left_fork.acquire()
            print(f"{self.name} picked up left fork.")
            self.right_fork.acquire()
            print(f"{self.name} picked up right fork.")
        else:
            self.right_fork.acquire()
            print(f"{self.name} picked up right fork.")
            self.left_fork.acquire()
            print(f"{self.name} picked up left fork.")

    def eat(self):
        print(f"{self.name} is eating.")
        time.sleep(random.uniform(1, 3))
        self.left_fork.release()
        print(f"{self.name} put down left fork.")
        self.right_fork.release()
        print(f"{self.name} put down right fork.")

# Membuat dan menjalankan lima filsuf dengan pendekatan Asymmetric
philosophers = [Philosopher(names[i], forks[i], forks[(i + 1) % 5], i) for i in range(5)]
```

Pendekatan Asymmetric memastikan bahwa tidak semua filsuf mengambil garpu yang sama pada waktu yang sama, mengurangi kemungkinan deadlock.

**Masalah Readers and Writers:**

![image](https://github.com/avendika/SysOP24-3123521011/assets/140131896/ef1be1ed-c663-4c24-a311-b1ce16902574)


Masalah Readers and Writers menggambarkan skenario sinkronisasi di mana beberapa proses membaca dan menulis pada sumber data yang sama. Tantangannya adalah mengelola akses ke sumber data tersebut sehingga tidak terjadi konflik antara proses pembacaan dan penulisan.

### Detail Masalah

- **Readers (Pembaca):** Proses yang hanya membaca data. Beberapa pembaca bisa membaca data secara bersamaan tanpa saling mengganggu.
- **Writers (Penulis):** Proses yang menulis atau mengubah data. Ketika penulis sedang menulis, tidak ada pembaca atau penulis lain yang boleh mengakses data tersebut.

### Masalah yang Muncul

1. **Kebuntuan (Deadlock):** Terjadi ketika pembaca atau penulis menunggu satu sama lain selamanya.
2. **Kelaparan (Starvation):** Terjadi ketika satu jenis proses (pembaca atau penulis) tidak pernah mendapatkan giliran untuk mengakses sumber daya.
3. **Kondisi Balapan (Race Condition):** Terjadi ketika dua atau lebih proses mengakses data bersama-sama secara bersamaan, menyebabkan hasil yang tidak dapat diprediksi.

### Penyelesaian Masalah

Terdapat dua varian utama dari masalah Readers and Writers:

1. **Prioritas Pembaca (Reader Priority):** Mengizinkan pembaca untuk mengakses data kapan saja, tetapi penulis harus menunggu sampai semua pembaca selesai membaca.
2. **Prioritas Penulis (Writer Priority):** Memberikan penulis prioritas sehingga penulis dapat menulis segera setelah tersedia, tanpa harus menunggu pembaca selesai.

Di sini, kita akan membahas solusi menggunakan semaphore untuk kedua varian.

#### 1. **Prioritas Pembaca:**

Pada solusi ini, pembaca dapat terus membaca jika ada pembaca lain yang sedang membaca, tetapi penulis harus menunggu sampai semua pembaca selesai.

##### Langkah Penyelesaian:

- Menggunakan semaphore untuk melacak jumlah pembaca dan penulis.
- Semaphore `mutex` untuk melindungi akses ke variabel penghitung pembaca.
- Semaphore `wrt` untuk melindungi akses ke sumber data.

##### Pseudocode:

```python
# Inisialisasi semaphore
mutex = Semaphore(1)
wrt = Semaphore(1)
read_count = 0

# Fungsi pembaca
def reader():
    global read_count
    while True:
        mutex.wait()        # Tunggu akses eksklusif ke read_count
        read_count += 1
        if read_count == 1:
            wrt.wait()      # Pembaca pertama mengunci penulis
        mutex.signal()      # Lepaskan akses ke read_count
        
        # Membaca data
        read_data()
        
        mutex.wait()        # Tunggu akses eksklusif ke read_count
        read_count -= 1
        if read_count == 0:
            wrt.signal()    # Pembaca terakhir melepaskan penulis
        mutex.signal()      # Lepaskan akses ke read_count

# Fungsi penulis
def writer():
    while True:
        wrt.wait()          # Tunggu akses eksklusif ke sumber data
        
        # Menulis data
        write_data()
        
        wrt.signal()        # Lepaskan akses eksklusif ke sumber data
```

#### 2. **Prioritas Penulis:**

Pada solusi ini, penulis diberikan prioritas sehingga segera setelah penulis ingin menulis, penulis akan mendapatkan akses eksklusif ke sumber data.

##### Langkah Penyelesaian:

- Menggunakan semaphore untuk melacak jumlah pembaca dan penulis.
- Semaphore `mutex` untuk melindungi akses ke variabel penghitung pembaca.
- Semaphore `wrt` untuk melindungi akses ke sumber data.
- Semaphore `turn` untuk memastikan bahwa jika penulis ingin menulis, pembaca baru harus menunggu.

##### Pseudocode:

```python
# Inisialisasi semaphore
mutex = Semaphore(1)
wrt = Semaphore(1)
turn = Semaphore(1)
read_count = 0

# Fungsi pembaca
def reader():
    global read_count
    while True:
        turn.wait()         # Pembaca mencoba mendapatkan giliran
        mutex.wait()        # Tunggu akses eksklusif ke read_count
        read_count += 1
        if read_count == 1:
            wrt.wait()      # Pembaca pertama mengunci penulis
        mutex.signal()      # Lepaskan akses ke read_count
        turn.signal()       # Pembaca melepas giliran
        
        # Membaca data
        read_data()
        
        mutex.wait()        # Tunggu akses eksklusif ke read_count
        read_count -= 1
        if read_count == 0:
            wrt.signal()    # Pembaca terakhir melepaskan penulis
        mutex.signal()      # Lepaskan akses ke read_count

# Fungsi penulis
def writer():
    while True:
        turn.wait()         # Penulis mencoba mendapatkan giliran
        wrt.wait()          # Tunggu akses eksklusif ke sumber data
        turn.signal()       # Penulis melepas giliran
        
        # Menulis data
        write_data()
        
        wrt.signal()        # Lepaskan akses eksklusif ke sumber data
```

Dalam kedua solusi ini, semaphore digunakan untuk mengelola akses dan memastikan sinkronisasi antara pembaca dan penulis, sehingga tidak terjadi konflik saat mengakses sumber data yang sama.
