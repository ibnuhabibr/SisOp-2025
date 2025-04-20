<code>Nama            : Ibnu Habib Ridwansyah</code></br>
<code>Kelas           : D3 Teknik Informatika B</code></br>
<code>NRP             : 3124500041</code></br>
<code>Dosen Pengajar  : Dr. Ferry Astika Saputra S.T., M.Sc</code></br>  

<h1>Week 8</h1>

### 1. Jelaskan dalam 2 pargraph disertai dengan gambar tentang konsep single thread dan multithread!
### Konsep Single Thread dan Multithread

**Single thread** adalah konsep dalam pemrograman di mana suatu program hanya menjalankan satu tugas atau proses pada satu waktu. Dalam sistem single-threaded, instruksi dieksekusi secara berurutan, satu per satu, tanpa adanya paralelisasi. Hal ini membuat eksekusi program menjadi lebih sederhana, namun bisa sangat terbatas dalam hal performa, terutama untuk aplikasi yang memerlukan pemrosesan besar atau menjalankan beberapa tugas secara bersamaan. Contoh aplikasi yang menggunakan single-threading adalah banyak program desktop atau aplikasi yang tidak membutuhkan interaksi banyak pengguna atau proses paralel.

Sementara itu, **multithread** adalah konsep di mana sebuah program dapat menjalankan beberapa tugas atau proses secara bersamaan dengan memanfaatkan beberapa thread. Setiap thread dapat berjalan secara paralel, mengizinkan program untuk melakukan lebih banyak pekerjaan dalam waktu yang lebih singkat. Sistem operasi modern sering kali menggunakan multithreading untuk meningkatkan efisiensi, terutama dalam aplikasi yang memerlukan pemrosesan yang intensif, seperti pemrograman server atau aplikasi yang berhubungan dengan multimedia. Multithreading juga memungkinkan aplikasi untuk merespon beberapa input pengguna secara bersamaan, seperti dalam aplikasi web atau perangkat mobile yang melibatkan interaksi intensif.

<ul>
<li><b>Single Thread</b></li><br>
  
![image](https://github.com/ibnuhabibr/SisOp-2025/blob/main/img/Single%20Thread.png)

<li><b>Multi Thread</b></li>

![image](https://github.com/ibnuhabibr/SisOp-2025/blob/main/img/Multi%20Thread.png)


</ul>

### Tabel Perbandingan Single Thread dan Multithread

| Aspek                   | Single Thread                                      | Multithread                                        |
|-------------------------|----------------------------------------------------|----------------------------------------------------|
| **Eksekusi**             | Eksekusi instruksi secara berurutan               | Eksekusi instruksi secara paralel                  |
| **Kinerja**              | Terbatas, hanya dapat menjalankan satu tugas      | Meningkatkan kinerja, dapat menjalankan banyak tugas sekaligus |
| **Kompleksitas**         | Lebih sederhana, mudah dikelola                   | Lebih kompleks, membutuhkan pengelolaan thread     |
| **Penggunaan Sumber Daya**| Lebih efisien dalam hal penggunaan sumber daya    | Memerlukan lebih banyak sumber daya (memori dan CPU) |
| **Contoh Aplikasi**      | Aplikasi desktop sederhana, program kalkulator    | Aplikasi server, game, aplikasi multimedia         |

Tabel ini menunjukkan perbedaan utama antara kedua konsep, di mana multithreading menawarkan keunggulan dalam kinerja dan responsivitas, tetapi dengan peningkatan kompleksitas dan penggunaan sumber daya yang lebih tinggi.

### 2. Programming Exercise

#### **A. SumTask.java (Windows)**
```java

/**
 * Fork/join parallelism in Java
 *
 * Figure 4.18
 *
 * @author Gagne, Galvin, Silberschatz
 * Operating System Concepts  - Tenth Edition
 * Copyright John Wiley & Sons - 2018
 */

import java.util.concurrent.*;

public class SumTask extends RecursiveTask<Integer> {
  static final int SIZE = 10000;
  static final int THRESHOLD = 1000;

  private int begin;
  private int end;
  private int[] array;

  public SumTask(int begin, int end, int[] array) {
    this.begin = begin;
    this.end = end;
    this.array = array;
  }

  protected Integer compute() {
    if (end - begin < THRESHOLD) {
      int sum = 0;
      for (int i = begin; i <= end; i++)
        sum += array[i];

      return sum;
    } else {
      int mid = begin + (end - begin) / 2;

      SumTask leftTask = new SumTask(begin, mid, array);
      SumTask rightTask = new SumTask(mid + 1, end, array);

      leftTask.fork();
      rightTask.fork();

      return rightTask.join() + leftTask.join();
    }
  }

  public static void main(String[] args) {
    ForkJoinPool pool = new ForkJoinPool();
    int[] array = new int[SIZE];

    java.util.Random rand = new java.util.Random();

    for (int i = 0; i < SIZE; i++) {
      array[i] = rand.nextInt(10);
    }

    SumTask task = new SumTask(0, SIZE - 1, array);

    int sum = pool.invoke(task);

    System.out.println("The sum is " + sum);
  }
}
```

### **Penjelasan Program Fork/Join Parallelism dan Pthread**

### Fork/Join Parallelism dalam Java

Program yang diberikan menggunakan **fork/join parallelism** dalam Java untuk menghitung jumlah elemen dalam array dengan menggunakan teknik rekursif. Berikut adalah penjelasan lebih rinci mengenai apa yang terjadi di dalam kode:

### 1. Kelas `SumTask`:
- Kelas ini adalah subclass dari `RecursiveTask<Integer>`, yang memungkinkan kita untuk memanfaatkan **ForkJoinPool** untuk melakukan komputasi paralel.
- Kelas `SumTask` digunakan untuk menghitung jumlah elemen dalam array dengan membagi pekerjaan menjadi sub-tugas yang lebih kecil.
- Kelas ini memiliki tiga variabel:
  - `begin`: indeks awal dari bagian array yang ingin dihitung.
  - `end`: indeks akhir dari bagian array yang ingin dihitung.
  - `array`: array yang berisi elemen-elemen yang akan dijumlahkan.

### 2. Metode `compute()`:
- Jika jumlah elemen dalam rentang yang ditentukan (`end - begin`) lebih kecil dari ambang batas `THRESHOLD` (yaitu 1000), maka proses penjumlahan dilakukan secara serial menggunakan perulangan biasa.
- Jika jumlah elemen lebih besar dari ambang batas, tugas dibagi dua:
  - `leftTask`: Sub-tugas untuk menghitung jumlah bagian kiri dari array.
  - `rightTask`: Sub-tugas untuk menghitung jumlah bagian kanan dari array.
- Kedua sub-tugas kemudian dijalankan secara paralel menggunakan metode `fork()`.
- Setelah itu, kode menunggu kedua sub-tugas selesai dengan menggunakan metode `join()`, dan hasil penjumlahan dari kedua sub-tugas digabungkan dan dikembalikan.

### 3. Bagian `main`:
- Sebuah **ForkJoinPool** dibuat untuk menjalankan tugas secara paralel.
- Sebuah array `array` dengan ukuran 10000 diisi dengan angka acak antara 0 dan 9.
- Sebuah objek `SumTask` dibuat untuk menghitung jumlah seluruh elemen dalam array dari indeks 0 hingga 9999.
- `pool.invoke(task)` digunakan untuk memulai dan menunggu hasil dari tugas paralel yang dijalankan.
- Setelah selesai, hasil penjumlahan ditampilkan.

### 4. Output:
- Output dari program ini adalah jumlah dari semua elemen dalam array, yang dihitung secara paralel.
- Contoh output: The sum is 49927
- Nilai yang ditampilkan akan berbeda setiap kali karena array diisi dengan angka acak yang berbeda.

### Ringkasan:
- Program ini mengimplementasikan **fork/join parallelism** untuk menghitung jumlah elemen dalam array secara efisien. Program membagi pekerjaan menjadi sub-tugas yang lebih kecil dan menjalankannya secara paralel, meningkatkan kinerja dibandingkan dengan pendekatan serial pada array besar.

---

#### **B. thrd-posix.c (Linux)**
```c

/**
 * A pthread program illustrating how to
 * create a simple thread and some of the pthread API
 * This program implements the summation function where
 * the summation operation is run as a separate thread.
 *
 * Most Unix/Linux/OS X users
 * gcc thrd.c -lpthread
 *
 * Figure 4.11
 *
 * @author Gagne, Galvin, Silberschatz
 * Operating System Concepts  - Tenth Edition
 * Copyright John Wiley & Sons - 2018
 */

#include <pthread.h>
#include <stdio.h>
#include <stdlib.h>

int sum;

void *runner(void *param);

int main(int argc, char *argv[])
{
pthread_t tid;
pthread_attr_t attr;

if (argc != 2) {
	fprintf(stderr,"usage: a.out <integer value>\n");
	return -1;
}

if (atoi(argv[1]) < 0) {
	fprintf(stderr,"Argument %d must be non-negative\n",atoi(argv[1]));
	return -1;
}

pthread_attr_init(&attr);

pthread_create(&tid,&attr,runner,argv[1]);

pthread_join(tid,NULL);

printf("sum = %d\n",sum);
}

void *runner(void *param) 
{
int i, upper = atoi(param);
sum = 0;

	if (upper > 0) {
		for (i = 1; i <= upper; i++)
			sum += i;
	}

	pthread_exit(0);
}
```

### Pthread Program untuk Penjumlahan
Program berikut menggunakan **pthread** (POSIX threads) untuk membuat thread terpisah yang akan melakukan penjumlahan angka dari 1 hingga angka yang diberikan sebagai argumen. Berikut adalah penjelasan lebih rinci mengenai apa yang terjadi dalam kode ini:

### 1. Variabel Global:
- `sum`: Variabel global yang akan menyimpan hasil penjumlahan.

### 2. Fungsi `runner`:
- Fungsi `runner` adalah fungsi yang dijalankan dalam thread terpisah. Fungsi ini menerima argumen `param`, yang merupakan nilai batas atas untuk penjumlahan.
- Fungsi menginisialisasi `sum` menjadi 0 dan melakukan perulangan dari 1 hingga nilai yang diberikan melalui `param` untuk menghitung jumlah total angka tersebut.
- Setelah selesai, fungsi memanggil `pthread_exit(0)` untuk mengakhiri thread.

### 3. Fungsi `main`:
- **Pengecekan Argumen**: Program memeriksa apakah ada satu argumen yang diberikan melalui baris perintah (`argc != 2`) dan memeriksa apakah nilai tersebut non-negatif.
- Jika argumen tidak diberikan atau nilai argumen negatif, program menampilkan pesan kesalahan dan keluar.
- **Inisialisasi Attribute**: Fungsi `pthread_attr_init(&attr)` digunakan untuk menginisialisasi atribut untuk thread.
- **Membuat Thread**: Fungsi `pthread_create` digunakan untuk membuat thread baru. Thread ini akan menjalankan fungsi `runner` dengan argumen yang diberikan dari baris perintah.
- `pthread_create(&tid, &attr, runner, argv[1])` membuat thread dan memulai eksekusi fungsi `runner`.
- **Menunggu Thread Selesai**: Setelah thread dibuat, fungsi `pthread_join(tid, NULL)` dipanggil untuk menunggu hingga thread selesai menjalankan fungsinya.
- Setelah thread selesai, hasil penjumlahan yang disimpan di variabel global `sum` dicetak.

### 4. Output:
- Program ini akan mencetak jumlah dari angka 1 sampai dengan angka yang diberikan sebagai argumen.
- Misalnya, jika program dijalankan dengan argumen `5`, maka outputnya akan seperti ini: sum = 15 (Ini karena penjumlahan angka 1 + 2 + 3 + 4 + 5 = 15).

### Penjelasan Detil:
- **Pembuatan Thread**: Program membuat sebuah thread yang terpisah untuk menghitung jumlah dari 1 hingga angka yang diberikan. Thread tersebut berjalan secara paralel dengan thread utama.
- **Penggunaan `pthread_create` dan `pthread_join`**: 
- `pthread_create` digunakan untuk membuat dan memulai thread, dan thread tersebut akan mengeksekusi fungsi `runner`.
- `pthread_join` digunakan di thread utama untuk menunggu hingga thread terpisah selesai melakukan pekerjaannya (penjumlahan), sehingga program utama tidak melanjutkan sampai thread tersebut selesai.

### 5. Error Handling:
- Program melakukan pengecekan terhadap argumen yang diberikan. Jika tidak sesuai (misalnya tidak ada argumen atau argumen negatif), program akan menampilkan pesan kesalahan dan keluar.

### Ringkasan:
Program ini memperlihatkan penggunaan dasar thread dengan **pthread** di C untuk melakukan operasi penjumlahan secara terpisah menggunakan thread. Thread terpisah melakukan perhitungan, dan thread utama menunggu hingga thread tersebut selesai dan mencetak hasilnya.

---


#### **C. thrd-win32.c (Windows)**
```c
/**
 * This program creates a separate thread using the CreateThread() system call.
 *
 * Figure 4.13
 *
 * @author Gagne, Galvin, Silberschatz
 * Operating System Concepts  - Tenth Edition
 * Copyright John Wiley & Sons - 2018
 */

#include <stdio.h>
#include <windows.h>

DWORD Sum;

DWORD WINAPI Summation(PVOID Param) {
  DWORD Upper = *(DWORD *)Param;

  for (DWORD i = 0; i <= Upper; i++)
    Sum += i;

  return 0;
}

int main(int argc, char *argv[]) {
  DWORD ThreadId;
  HANDLE ThreadHandle;
  int Param;

  if (argc != 2) {
    fprintf(stderr, "An integer parameter is required\n");
    return -1;
  }

  Param = atoi(argv[1]);

  if (Param < 0) {
    fprintf(stderr, "an integer >= 0 is required \n");
    return -1;
  }

  ThreadHandle = CreateThread(NULL, 0, Summation, &Param, 0, &ThreadId);

  if (ThreadHandle != NULL) {
    WaitForSingleObject(ThreadHandle, INFINITE);
    CloseHandle(ThreadHandle);
    printf("sum = %d\n", Sum);
  }
}

```


### Penjelasan Program Menggunakan `CreateThread()` di Windows

Program ini menggunakan fungsi `CreateThread()` untuk membuat thread terpisah yang akan menghitung jumlah angka dari 0 hingga angka yang diberikan sebagai argumen. Berikut adalah penjelasan lebih rinci mengenai apa yang terjadi dalam kode ini:

### 1. Fungsi `Summation`:
- Fungsi `Summation` adalah fungsi yang dijalankan oleh thread yang dibuat menggunakan `CreateThread()`.
- Fungsi ini menerima satu parameter yang merupakan angka batas atas untuk penjumlahan.
- Dalam fungsi ini, `Sum` akan diinisialisasi sebagai 0 dan akan dijumlahkan dari angka 0 hingga angka yang diberikan melalui parameter `Param`.
- Fungsi akan melakukan iterasi dari 0 hingga angka yang diberikan dan menambahkan nilai-nilai tersebut ke dalam variabel global `Sum`.

### 2. Fungsi `main`:
- **Pengecekan Argumen**: Program memeriksa apakah ada satu argumen yang diberikan melalui baris perintah (`argc != 2`).
  - Jika argumen tidak diberikan, program menampilkan pesan kesalahan dan keluar.
  - Program juga memeriksa apakah nilai argumen lebih besar atau sama dengan 0. Jika tidak, program akan menampilkan pesan kesalahan dan keluar.
- **Pembuatan Thread**: Fungsi `CreateThread` digunakan untuk membuat thread baru yang menjalankan fungsi `Summation` dengan argumen yang diberikan melalui baris perintah.
  - `CreateThread(NULL, 0, Summation, &Param, 0, &ThreadId)` membuat thread dan memulai eksekusi fungsi `Summation`.
- **Menunggu Thread Selesai**: Setelah thread dibuat, fungsi `WaitForSingleObject` digunakan untuk menunggu hingga thread selesai menjalankan fungsinya.
  - `WaitForSingleObject(ThreadHandle, INFINITE)` akan menunggu hingga thread selesai sebelum melanjutkan eksekusi program.
- Setelah thread selesai, `CloseHandle` digunakan untuk menutup handle dari thread yang telah selesai, dan program mencetak hasil penjumlahan yang disimpan di variabel global `Sum`.

### 3. Output:
- Program ini akan mencetak jumlah dari angka 0 hingga angka yang diberikan sebagai argumen.
- Misalnya, jika program dijalankan dengan argumen `5`, maka outputnya akan seperti ini: sum = 15 (Karena penjumlahan angka 0 + 1 + 2 + 3 + 4 + 5 = 15.)

### Penjelasan Detil:
- **Pembuatan Thread**: Program membuat sebuah thread yang terpisah untuk menghitung jumlah dari 0 hingga angka yang diberikan. Thread tersebut berjalan secara paralel dengan thread utama.
- **Penggunaan `CreateThread` dan `WaitForSingleObject`**: 
- `CreateThread` digunakan untuk membuat dan memulai thread yang akan mengeksekusi fungsi `Summation`.
- `WaitForSingleObject` digunakan di thread utama untuk menunggu hingga thread terpisah selesai melakukan pekerjaannya (penjumlahan), sehingga program utama tidak melanjutkan sampai thread tersebut selesai.

### 4. Error Handling:
- Program melakukan pengecekan terhadap argumen yang diberikan. Jika tidak sesuai (misalnya tidak ada argumen atau argumen negatif), program akan menampilkan pesan kesalahan dan keluar.

### Ringkasan:
Program ini menunjukkan cara menggunakan fungsi `CreateThread()` di Windows untuk membuat thread yang melakukan operasi penjumlahan. Thread terpisah melakukan perhitungan, dan thread utama menunggu hingga thread tersebut selesai dan mencetak hasilnya.

---

### 3. PPT evolusi teknologi processor Intel

[Evolusi Intel Processor.pptx](https://github.com/ibnuhabibr/SisOp-2025/blob/main/PPT/Evolusi%20Intel%20Processor.pptx)

---

## 4. Multithreading: Penerapan, Kecepatan, Jenis Paralelisme, Perbedaan Thread, dan Context Switching Kernel

Soal ini mengulas beberapa topik penting terkait dengan multithreading, termasuk:

1. **Contoh kode pemrograman** yang menunjukkan peningkatan performa melalui multithreading dibandingkan solusi single-threaded.
2. **Perhitungan peningkatan kecepatan (speedup)** menggunakan Hukum Amdahl untuk aplikasi dengan 60% bagian yang dapat diparalelkan, pada dua core dan empat core.
3. **Pembahasan mengenai jenis paralelisme** yang diterapkan pada web server multithreaded.
4. **Perbedaan utama antara user-level thread dan kernel-level thread**, serta situasi yang cocok untuk masing-masing.
5. **Penjelasan mengenai langkah-langkah** yang dilakukan kernel saat berpindah dari satu thread ke thread lainnya (context switching).

---

### 1. Penerapan Multithreading untuk Peningkatan Performa

Multithreading memungkinkan eksekusi tugas secara bersamaan, yang mempercepat kinerja aplikasi. Berikut adalah beberapa contoh penerapan multithreading:

#### Contoh 1: Web Server Multithreaded
```python
import threading
import socket

def handle_client(client_socket):
    request = client_socket.recv(1024)
    client_socket.send(b"Server response")
    client_socket.close()

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.bind(('0.0.0.0', 9999))
server.listen(5)

while True:
    client, addr = server.accept()
    client_thread = threading.Thread(target=handle_client, args=(client,))
    client_thread.start()
```

Web server yang mengimplementasikan multithreading dapat melayani banyak permintaan klien secara bersamaan. Setiap permintaan diproses dalam thread terpisah, sehingga tidak ada yang perlu menunggu proses lainnya selesai.

Tanpa thread, server hanya bisa memproses satu klien dalam satu waktu, yang menyebabkan penurunan kinerja dan respons yang lebih lambat.


#### Contoh 2: Pemrosesan Video Real-Time

Pada aplikasi seperti live streaming atau deteksi wajah, memisahkan proses pengambilan gambar, pemrosesan, dan tampilan ke dalam thread yang berbeda membantu menjaga performa tetap lancar.
```python
import cv2
import threading

frame = None

def capture_video():
    global frame
    cap = cv2.VideoCapture(0)
    while True:
        ret, frame = cap.read()

def process_video():
    global frame
    while True:
        if frame is not None:
            pass

threading.Thread(target=capture_video).start()
threading.Thread(target=process_video).start()
```

Jika semua tugas dilakukan dalam satu thread, akan ada penundaan atau frame drop akibat beban pemrosesan yang tinggi.


#### Contoh 3: Kompresi Banyak File Secara Paralel

Untuk mengompres banyak file, multithreading memungkinkan setiap file dikompresi secara paralel, yang mempercepat proses, terutama pada CPU dengan banyak core.
```python
import threading
import zipfile

def compress_file(filename):
    with zipfile.ZipFile(filename + '.zip', 'w') as zipf:
        zipf.write(filename)

files = ['file1.txt', 'file2.txt', 'file3.txt']
threads = []

for file in files:
    t = threading.Thread(target=compress_file, args=(file,))
    threads.append(t)
    t.start()

for t in threads:
    t.join()
```
Proses kompresi file satu per satu akan menghambat penggunaan maksimal dari CPU. Dengan multithreading, proses menjadi lebih efisien.

---

### 2. Perhitungan Speedup dengan Hukum Amdahl

Hukum Amdahl digunakan untuk memperkirakan peningkatan kecepatan (speedup) yang bisa dicapai dengan memparalelkan sebagian program. Rumus Hukum Amdahl adalah:

$$
\text{Speedup}(N) = \frac{1}{(1 - P) + \frac{P}{N}}
$$

di mana:

- \( P \) adalah bagian program yang dapat diparalelkan (dalam desimal),
- \( N \) adalah jumlah inti prosesor (core).

Jika \( P = 0.60 \) (60%), maka:

#### Dua Inti Prosesor (N = 2)

$$
\text{Speedup}(2) = \frac{1}{(1 - 0.60) + \frac{0.60}{2}} = \frac{1}{0.40 + 0.30} = \frac{1}{0.70} \approx 1.43
$$

Artinya, kecepatan meningkat sekitar **1.43 kali** lipat dibandingkan dengan menggunakan satu core.

#### Empat Inti Prosesor (N = 4)

$$
\text{Speedup}(4) = \frac{1}{(1 - 0.60) + \frac{0.60}{4}} = \frac{1}{0.40 + 0.15} = \frac{1}{0.55} \approx 1.82
$$

Dengan empat core, kecepatan meningkat sekitar **1.82 kali** lipat.

---

### 3. Jenis Paralelisme pada Web Server Multithreaded

Web server multithreaded, seperti yang telah dijelaskan, mengimplementasikan **task parallelism**, bukan **data parallelism**.

#### 1. Paralelisme Tugas (Task Parallelism)

Dalam task parallelism, setiap thread menangani tugas yang berbeda, yang dapat berjalan secara independen. Misalnya, dalam web server:

- Setiap thread menangani permintaan klien yang berbeda.
- Setiap permintaan dapat melibatkan tugas yang berbeda, seperti mengirim halaman web, memproses form, atau menangani unggahan file.

#### 2. Paralelisme Data (Data Parallelism)

Data parallelism terjadi ketika beberapa thread bekerja bersama-sama
