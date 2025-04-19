<code>Nama            : Ibnu Habib Ridwansyah</code></br>
<code>Kelas           : D3 Teknik Informatika B</code></br>
<code>NRP             : 3124500041</code></br>
<code>Dosen Pengajar  : Dr.Ferry Astika Saputra S.T., M.Sc</code></br>  

---

### 1. Program Thread Sederhana

#### **Kode Program**
```c
#include <pthread.h>
#include <stdio.h>

pthread_cond_t cond1 = PTHREAD_COND_INITIALIZER;
pthread_cond_t cond2 = PTHREAD_COND_INITIALIZER;
pthread_cond_t cond3 = PTHREAD_COND_INITIALIZER;

pthread_mutex_t lock = PTHREAD_MUTEX_INITIALIZER;

int done = 1;

void *foo(void *n) {
  while (1) {

    pthread_mutex_lock(&lock);

    if (done != (int)*(int *)n) {

      if ((int)*(int *)n == 1) {
        pthread_cond_wait(&cond1, &lock);
      } else if ((int)*(int *)n == 2) {
        pthread_cond_wait(&cond2, &lock);
      } else {
        pthread_cond_wait(&cond3, &lock);
      }
    }
    printf("%d ", *(int *)n);

    if (done == 3) {
      done = 1;
      pthread_cond_signal(&cond1);
    } else {
      done++;
      if (done == 2)
        pthread_cond_signal(&cond2);
      else
        pthread_cond_signal(&cond3);
    }

    pthread_mutex_unlock(&lock);
  }

  return NULL;
}

int main() {
  pthread_t t1, t2, t3;
  int a = 1, b = 2, c = 3;

  pthread_create(&t1, NULL, foo, (void *)&a);
  pthread_create(&t2, NULL, foo, (void *)&b);
  pthread_create(&t3, NULL, foo, (void *)&c);

  pthread_join(t1, NULL);
  pthread_join(t2, NULL);
  pthread_join(t3, NULL);

  return 0;
}
```

# Struktur Program

## 1. Thread dan Mutex
- Program ini menggunakan **threads** (benang eksekusi) untuk menjalankan kode secara bersamaan, yang diatur dengan menggunakan pustaka **pthread** di bahasa C.
- Ada tiga **threads** yang dibuat, masing-masing bertanggung jawab untuk menampilkan angka secara bergantian.
- Program menggunakan **mutex** (`pthread_mutex_t`) untuk menghindari akses bersamaan terhadap variabel yang digunakan bersama oleh thread. Mutex ini memastikan bahwa hanya satu thread yang dapat mengakses bagian tertentu dari kode pada satu waktu.

## 2. Variabel Kondisi
- **Variabel kondisi** (dalam hal ini, **cond1**, **cond2**, dan **cond3**) digunakan untuk menyinkronkan thread agar berjalan dalam urutan tertentu.
- Variabel kondisi bekerja dengan cara mengontrol kapan sebuah thread boleh melanjutkan eksekusinya, berdasarkan kondisi yang telah ditetapkan sebelumnya.
- Dengan variabel kondisi, program mengontrol urutan thread-thread yang bekerja. Thread pertama (yang akan mencetak angka 1) menunggu sampai thread lainnya selesai dengan bagian mereka sebelum melanjutkan, dan seterusnya.


# Penjelasan Langkah demi Langkah

### 1. Inisialisasi dan Pembuatan Thread:
- Variabel kondisi (`cond1`, `cond2`, `cond3`) dan mutex (`lock`) diinisialisasi terlebih dahulu.
- Variabel **done** digunakan untuk mengatur urutan eksekusi thread. Thread akan bekerja berdasarkan nilai **done**. Nilai **done** dimulai dengan 1 dan akan meningkat setelah setiap iterasi.
- Program kemudian membuat tiga thread dengan memanggil `pthread_create`:
  - Thread pertama akan menampilkan angka 1.
  - Thread kedua akan menampilkan angka 2.
  - Thread ketiga akan menampilkan angka 3.

### 2. Eksekusi Fungsi foo:
- **Fungsi foo** adalah fungsi yang dijalankan oleh setiap thread.
- Setiap thread memulai eksekusinya dengan mengunci mutex menggunakan `pthread_mutex_lock(&lock)`. Hal ini mencegah thread lain untuk mengakses bagian kritis dari kode (yaitu variabel done dan variabel kondisi) sampai thread yang sedang berjalan selesai.
  
  #### Siklus Thread:
  - Setiap thread memeriksa apakah nilai **done** sama dengan angka yang diberikan pada thread tersebut. Jika tidak sama, thread tersebut akan menunggu pada variabel kondisi yang sesuai (`pthread_cond_wait`).
    - Jika **done == 1**, thread pertama akan menunggu pada `cond1`.
    - Jika **done == 2**, thread kedua akan menunggu pada `cond2`.
    - Jika **done == 3**, thread ketiga akan menunggu pada `cond3`.
  - Setelah nilai **done** sesuai, thread akan mencetak angka yang sesuai dengan nilainya, yaitu 1, 2, atau 3.

### 3. Mengubah Nilai done dan Membangunkan Thread Lain:
- Setelah mencetak angka, thread akan memeriksa apakah nilai **done** sudah mencapai angka 3. Jika ya, maka **done** akan direset ke 1, dan thread pertama dibangunkan menggunakan `pthread_cond_signal(&cond1)` untuk melanjutkan.
- Jika nilai **done** bukan 3, maka nilai **done** akan ditingkatkan satu langkah (misalnya, dari 1 ke 2 atau dari 2 ke 3), dan thread berikutnya dibangunkan untuk melanjutkan eksekusinya:
  - Jika **done == 2**, maka `pthread_cond_signal(&cond2)` membangunkan thread kedua.
  - Jika **done == 3**, maka `pthread_cond_signal(&cond3)` membangunkan thread ketiga.
- Proses ini berulang terus-menerus dengan siklus mencetak angka 1, 2, dan 3 secara bergantian oleh ketiga thread.

### 4. Penutupan:
- Setelah ketiga thread selesai menjalankan tugas mereka, fungsi `pthread_join` dipanggil di main untuk menunggu hingga semua thread selesai sebelum program berakhir.

---

# Pemahaman Sinkronisasi:
- **Mutex** digunakan untuk mengunci akses ke variabel bersama (yaitu done dan kondisi lainnya) sehingga hanya satu thread yang bisa mengaksesnya pada satu waktu.
- **Variabel kondisi** (`cond1`, `cond2`, `cond3`) digunakan untuk menunggu dan membangunkan thread sesuai dengan urutan yang diinginkan. Ini menjamin bahwa ketiga thread berfungsi dengan urutan yang benar.
- **done** berfungsi sebagai penanda untuk mengontrol urutan eksekusi. Program memastikan bahwa setiap thread hanya akan dijalankan pada waktunya, sesuai dengan urutan yang diinginkan (1, 2, 3).


# Kesimpulan
Program ini adalah contoh dasar bagaimana **thread-thread** dapat disinkronkan menggunakan **variabel kondisi** dan **mutex** untuk berinteraksi satu sama lain dalam urutan yang diatur. Dalam konteks aplikasi yang lebih besar, konsep ini bisa digunakan untuk mengelola sumber daya bersama dan menghindari masalah seperti kondisi balapan atau **deadlock**.

---

### 2. Program Forking

#### **Kode Program**
```c
#include <stdio.h>
#include <unistd.h>
#include <sys/types.h>

int main() {
    pid_t pid;

    // Melakukan fork untuk membuat proses anak
    pid = fork();

    if (pid < 0) {
        // Jika fork gagal
        perror("Fork failed");
        return 1;
    }

    // Jika pid == 0, ini adalah proses anak
    if (pid == 0) {
        printf("Ini adalah proses anak dengan PID %d dan Parent PID %d\n", getpid(), getppid());
    }
    // Jika pid > 0, ini adalah proses induk
    else {
        printf("Ini adalah proses induk dengan PID %d dan Child PID %d\n", getpid(), pid);
    }

    return 0;
}

```
# Penjelasan Program

## 1. **fork()**:
- Fungsi **fork()** digunakan untuk membuat proses anak baru. Setelah pemanggilan **fork()**, program akan terus berjalan pada dua proses secara bersamaan: satu di proses induk dan satu lagi di proses anak.
- **Proses Induk**: Mendapatkan nilai dari **pid** yang merupakan PID (**Process ID**) dari proses anak.
- **Proses Anak**: Mendapatkan nilai **pid == 0**, yang menunjukkan bahwa proses ini adalah hasil dari pemanggilan **fork()**.

## 2. **pid_t pid**:
Variabel **pid** digunakan untuk menyimpan hasil dari **fork()**. Nilai yang dikembalikan adalah:
- **Proses Induk**: Nilai **pid** berisi PID dari proses anak yang baru saja dibuat.
- **Proses Anak**: Nilai **pid** adalah 0 karena anak adalah hasil langsung dari pemanggilan **fork()**.

## 3. **Perbedaan Proses Induk dan Anak**:
- Di dalam blok `if (pid == 0)`, program akan mengeksekusi kode yang khusus untuk proses anak, mencetak PID dari proses anak (`getpid()`) dan PID dari proses induk (`getppid()`).
- Di dalam blok `else`, kode ini dijalankan oleh proses induk dan mencetak PID induk serta PID anak.


# Cara Kerja Forking
- Setelah **fork()** dipanggil, kedua proses—induk dan anak—akan menjalankan kode berikutnya setelah pemanggilan **fork()**. Namun, masing-masing akan menjalankan bagian kode yang sesuai dengan kondisi yang diberikan (**anak** atau **induk**).
- **Proses induk** akan terus menjalankan eksekusinya setelah **fork()**, sedangkan **proses anak** akan menjalankan eksekusinya dengan kode yang sudah terpisah.
- Program ini bisa digunakan untuk membuat aplikasi yang memerlukan eksekusi paralel, seperti server yang melayani beberapa klien secara bersamaan.


# Penanganan Kesalahan
- Jika **fork()** gagal, misalnya karena terlalu banyak proses atau batasan sumber daya, maka nilai yang dikembalikan adalah **-1**. Dalam kasus ini, program akan menampilkan pesan kesalahan menggunakan **perror()**.


# Kesimpulan
Program ini menunjukkan cara membuat proses baru menggunakan **fork()** dalam bahasa C. Proses induk dan anak akan beroperasi secara paralel dan masing-masing akan mencetak informasi yang sesuai dengan statusnya. **Forking** adalah mekanisme yang kuat untuk pengelolaan proses dalam aplikasi multi-proses.

---

### Soal Nomor 3  
# Soal Nomor 3
**Apakah keuntungan menggunakan time quantum size di level yang berbeda dari sebuah antrian sistem multilevel?**

## Jawaban

Keuntungan menggunakan **time quantum size** di level yang berbeda dalam sebuah sistem antrian multilevel adalah sebagai berikut:

### 1. Pengelolaan Proses yang Lebih Efisien
- Sistem antrian multilevel mengatur proses-proses dalam beberapa antrian berdasarkan prioritasnya. Dengan menggunakan ukuran **time quantum** yang berbeda untuk setiap level, sistem dapat memberikan waktu eksekusi yang lebih fleksibel berdasarkan prioritas proses. 
  - Proses dengan prioritas tinggi (biasanya di antrian atas) akan memiliki **time quantum** yang lebih kecil, sementara proses dengan prioritas lebih rendah (di antrian bawah) bisa memiliki **time quantum** yang lebih besar.
- Keuntungan utama dari pengaturan **time quantum** ini adalah efisiensi pengalokasian waktu CPU. Proses dengan prioritas tinggi yang membutuhkan respons cepat akan mendapat lebih banyak kesempatan untuk dieksekusi dalam waktu singkat, sedangkan proses yang lebih rendah prioritasnya akan tetap diproses, namun dengan interval eksekusi yang lebih lama.

### 2. Meningkatkan Responsif Sistem
- Dalam sistem multilevel, proses dengan prioritas lebih tinggi membutuhkan waktu CPU yang lebih sedikit dan lebih sering untuk memastikan respons sistem tetap cepat. Dengan **time quantum** yang lebih kecil, proses-proses ini dapat menyelesaikan tugasnya lebih cepat dan kembali ke antrian utama.
- Sebaliknya, proses dengan prioritas lebih rendah akan diberikan **time quantum** yang lebih besar, memungkinkan mereka untuk menyelesaikan lebih banyak pekerjaan dalam sekali eksekusi. Ini mencegah sistem terlalu sering mengalihkan fokus ke proses yang lebih rendah prioritasnya, meningkatkan efisiensi eksekusi secara keseluruhan.

### 3. Meminimalkan Overhead dan Meningkatkan Utilisasi CPU
- Penggunaan **time quantum** yang berbeda di level antrian dapat membantu mengurangi overhead dari switching konteks. Proses dengan prioritas lebih tinggi tidak perlu menunggu terlalu lama untuk mendapatkan giliran, dan proses dengan prioritas lebih rendah tidak akan terlalu sering dipanggil jika tidak diperlukan. Ini membuat sistem lebih efisien dalam memanfaatkan waktu CPU.
- Overhead switching menjadi berkurang karena setiap antrian sudah disesuaikan dengan kebutuhan eksekusi masing-masing. Proses dengan prioritas tinggi bisa segera mendapatkan kesempatan CPU dengan **time quantum** yang lebih kecil dan cepat, sementara yang lebih rendah bisa memanfaatkan waktu eksekusi lebih panjang tanpa mengganggu yang lebih penting.

### 4. Meningkatkan Fairness dalam Penjadwalan
- Dengan menggunakan **time quantum** berbeda di berbagai level antrian, sistem multilevel dapat menjaga keseimbangan antara proses dengan prioritas tinggi dan rendah, menghindari satu jenis proses mendominasi penggunaan CPU.
  - Misalnya, dengan memberikan **time quantum** lebih kecil pada antrian dengan prioritas lebih tinggi, proses-proses kritis atau waktu nyata (**real-time**) dapat mendapat kesempatan lebih banyak untuk dieksekusi, sementara proses latar belakang atau batch dapat berjalan dengan lebih efisien tanpa mengganggu proses penting lainnya.

### 5. Fleksibilitas Penyesuaian Time Quantum
- **Time quantum** yang berbeda pada level antrian memungkinkan penyesuaian yang lebih baik sesuai dengan jenis dan karakteristik proses. Misalnya, untuk proses interaktif yang sering meminta I/O, lebih baik memberikan **time quantum** kecil, agar mereka bisa cepat merespons dan tidak menghabiskan terlalu banyak waktu CPU. Sebaliknya, untuk proses batch yang cenderung membutuhkan waktu eksekusi lebih lama, **time quantum** yang lebih besar memberikan mereka kesempatan untuk berjalan lebih lama tanpa sering terputus.


## Kesimpulan:
Dengan menggunakan **time quantum size** yang berbeda pada level yang berbeda dalam antrian sistem multilevel, kita bisa meningkatkan efisiensi penggunaan CPU, mempercepat respons sistem, dan memastikan keadilan dalam penjadwalan, serta mengurangi overhead switching konteks. Hal ini memungkinkan sistem untuk menangani berbagai jenis proses dengan lebih baik, baik itu yang bersifat interaktif, real-time, atau batch.

---

# Soal Nomor 4
**Gambarkan 4 diagram Chart yang mengilustrasikan eksekusi dari proses-proses tersebut menggunakan FCFS, SJF, prioritas nonpreemptive dan round robin.**

Berikut adalah empat diagram chart yang mengilustrasikan eksekusi dari proses-proses menggunakan berbagai algoritma penjadwalan:

**Output 1**
![image](https://github.com/ibnuhabibr/SisOp-2025/blob/main/img/output1.png)

**Output 2**
![image](https://github.com/ibnuhabibr/SisOp-2025/blob/main/img/output2.png)

**Output 3**
![image](https://github.com/ibnuhabibr/SisOp-2025/blob/main/img/output3.png)

**Output 4**
![image](https://github.com/ibnuhabibr/SisOp-2025/blob/main/img/output4.png)

### 1. **FCFS (First Come First Serve)**:
Proses dieksekusi sesuai dengan urutan kedatangan mereka, tanpa mempedulikan durasi burst time.

### 2. **SJF (Shortest Job First)**:
Proses dengan burst time terkecil dieksekusi terlebih dahulu, memberikan prioritas pada proses yang lebih cepat.

### 3. **Priority Non-Preemptive**:
Proses dengan prioritas lebih tinggi (nilai lebih kecil) dieksekusi terlebih dahulu. Proses dieksekusi tanpa preemption.

### 4. **Round Robin**:
Setiap proses mendapatkan waktu eksekusi dalam rotasi yang adil, dengan **time quantum** yang tetap (dalam hal ini 2).

Di masing-masing diagram, proses yang lebih kecil burst time-nya atau lebih tinggi prioritasnya akan dieksekusi lebih cepat sesuai dengan algoritma yang digunakan.
