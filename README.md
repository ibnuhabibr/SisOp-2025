# Tugas Sistem Operasi - 1

**Nama**: Ibnu Habib Ridwansyah  
**Kelas**: D3 IT B  
**NRP**: 3124500041  

---

## 1. Pengertian Bilangan

| **Jenis Bilangan**       | **Penjelasan**                                                                                                                                      |
|--------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| **Bilangan Biner**       | Bilangan yang berbasis 2 (dua), hanya menggunakan dua digit yaitu 0 dan 1.                                                                        |
| **Bilangan Heksadesimal**| Bilangan yang berbasis 16 (enam belas), menggunakan 16 simbol yaitu 0-9 untuk nilai 0 hingga 9, dan A-F untuk nilai 10 hingga 15.               |

---

## 2. Konversi Bilangan Desimal ke Biner

| **Bilangan Desimal** | **Langkah Konversi**                                                                                                                                                                    | **Hasil Biner**  |
|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|
| 1234                 | 1234 ÷ 2 = 617, sisa 0<br>617 ÷ 2 = 308, sisa 1<br>308 ÷ 2 = 154, sisa 0<br>...<br>1 ÷ 2 = 0, sisa 1                                                                                  | 10011010010      |
| 5670                 | 5670 ÷ 2 = 2835, sisa 0<br>2835 ÷ 2 = 1417, sisa 1<br>...                                                                                                                                 | 1011000100110    |
| 2321                 | 2321 ÷ 2 = 1160, sisa 1<br>1160 ÷ 2 = 580, sisa 0<br>...                                                                                                                                  | 100100010001     |

---

## 3. Konversi Bilangan Biner ke Desimal

| **Bilangan Biner** | **Perhitungan**                                                                                                                                                 | **Hasil Desimal** |
|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------|
| 10101010           | (1×2⁷) + (0×2⁶) + (1×2⁵) + (0×2⁴) + (1×2³) + (0×2²) + (1×2¹) + (0×2⁰)                                                                                      | 170               |
| 01010101           | (0×2⁷) + (1×2⁶) + (0×2⁵) + (1×2⁴) + (0×2³) + (1×2²) + (0×2¹) + (1×2⁰)                                                                                      | 85                |
| 11001100           | (1×2⁷) + (1×2⁶) + (0×2⁵) + (0×2⁴) + (1×2³) + (1×2²) + (0×2¹) + (0×2⁰)                                                                                      | 204               |

---

## 4. Konversi Bilangan Biner ke Oktal

| **Bilangan Biner**        | **Konversi**                                                                                                                                                  | **Hasil Oktal** |
|---------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|
| 101 011 111 001           | 101 = 5, 011 = 3, 111 = 7, 001 = 1                                                                                                                             | 5371            |
| 110 010 110 111           | 110 = 6, 010 = 2, 110 = 6, 111 = 7                                                                                                                             | 6267            |

---

## 5. Konversi Bilangan Oktal ke Biner

| **Bilangan Oktal** | **Konversi**                                                                                                                                          | **Hasil Biner**   |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------|
| 2170               | 2 = 010, 1 = 001, 7 = 111, 0 = 000                                                                                                                     | 010 001 111 000  |
| 3571               | 3 = 011, 5 = 101, 7 = 111, 1 = 001                                                                                                                     | 011 101 111 001  |

---

## 6. Konversi Bilangan Desimal ke Heksadesimal

| **Bilangan Desimal** | **Langkah Konversi**                                                                                                                                                                                                                     | **Hasil Heksadesimal** |
|----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------|
| 1780                 | 1780 ÷ 16 = 111, sisa 4<br>111 ÷ 16 = 6, sisa 15 (F)<br>6 ÷ 16 = 0, sisa 6<br>0 ÷ 16 = 0, sisa 0                                                                                                                                        | 06F4                   |
| 3666                 | 3666 ÷ 16 = 229, sisa 2<br>229 ÷ 16 = 14, sisa 5<br>14 ÷ 16 = 0, sisa 14 (E)<br>0 ÷ 16 = 0, sisa 0                                                                                                                                           | 0E52                   |
| 5230                 | 5230 ÷ 16 = 326, sisa 14 (E)<br>326 ÷ 16 = 20, sisa 6<br>20 ÷ 16 = 1, sisa 4<br>1 ÷ 16 = 0, sisa 1                                                                                                                                         | 146E                   |

---

## 7. Konversi Bilangan Heksadesimal ke Desimal

| **Bilangan Heksadesimal** | **Langkah Konversi**                                                                                                                                                                                                                         | **Hasil Desimal** |
|---------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------|
| ABCD                      | A = 10 × 16³ = 40960<br>B = 11 × 16² = 2816<br>C = 12 × 16¹ = 192<br>D = 13 × 16⁰ = 13                                                                                                          | 43981             |
| 2170                      | 2 = 2 × 16³ = 8192<br>1 = 1 × 16² = 256<br>7 = 7 × 16¹ = 112<br>0 = 0 × 16⁰ = 0                                                                                                             | 8560              |

---

## 8. Konversi Bilangan Pecahan Desimal ke Biner

| **Bilangan Desimal** | **Langkah Konversi**                                                                                                                                                               | **Hasil Biner** |
|----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|
| 0,3125               | 0,3125 × 2 = 0,625 (digit pertama = 0)<br>0,625 × 2 = 1,25 (digit kedua = 1)<br>0,25 × 2 = 0,5 (digit ketiga = 0)<br>0,5 × 2 = 1,0 (digit keempat = 1)                              | 0.0101          |
| 0,65625              | 0,65625 × 2 = 1,3125 (digit pertama = 1)<br>0,3125 × 2 = 0,625 (digit kedua = 0)<br>...                                                                                              | 0.10101         |
| 0,34375              | 0,34375 × 2 = 0,6875 (digit pertama = 0)<br>0,6875 × 2 = 1,375 (digit kedua = 1)<br>...                                                                                              | 0.01011         |

---

## 9. Konversi Bilangan Desimal ke Biner

| **Bilangan Desimal** | **Langkah Konversi**                                                                                                                                                         | **Hasil Biner**   |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------|
| rfvsv                | 11 ÷ 2 = 5 sisa 1<br>5 ÷ 2 = 2 sisa 1<br>2 ÷ 2 = 1 sisa 0<br>1 ÷ 2 = 0 sisa 1<br>Pecahan: 0,625 × 2 = 1,25 (digit pertama = 1)<br>...                                               | 1011.101₂         |
| xsxsxsx              | 0,6875 × 2 = 1,375 (digit pertama = 1)<br>0,375 × 2 = 0,75 (digit kedua = 0)<br>...                                                                                             | 0.1011₂           |
| sscsc                | 0,75 × 2 = 1,5 (digit pertama = 1)<br>0,5 × 2 = 1,0 (digit kedua = 1)                                                                                                           | 0.11₂             |

---

## 10. Konversi Bilangan Desimal ke Heksadesimal

| **Bilangan Desimal** | **Langkah Konversi**                                                                                                                                                                                                                             | **Hasil Heksadesimal** |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------|
| 348,654              | Bagian Bilangan Bulat: 348 ÷ 16 = 21 sisa 12 (C), 21 ÷ 16 = 1 sisa 5, 1 ÷ 16 = 0 sisa 1<br>Bagian Pecahan: 0,654 × 16 = 10,464 (digit pertama = A), 0,464 × 16 = 7,424 (digit kedua = 7)                                                     | 15C.A76                |
| 1784,240             | Bagian Bilangan Bulat: 1784 ÷ 16 = 111 sisa 8, 111 ÷ 16 = 6 sisa 15 (F), 6 ÷ 16 = 0 sisa 6<br>Bagian Pecahan: 0,240 × 16 = 3,84 (digit pertama = 3), 0,84 × 16 = 13,44 (digit kedua = D)                                                  | 6F8.3D7                |

---

## 11. Konversi Bilangan Biner ke Desimal

| **Bilangan Biner** | **Perhitungan**                                                                                                                                                     | **Hasil Desimal**   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------|
| 01010011,00111101  | Bagian Bilangan Bulat: 0×2⁷ + 1×2⁶ + 0×2⁵ + 1×2⁴ + 0×2³ + 0×2² + 1×2¹ + 1×2⁰ = 83<br>Bagian Pecahan: 0×2⁻¹ + 0×2⁻² + 1×2⁻³ + 1×2⁻⁴ + 1×2⁻⁵ + 1×2⁻⁶ + 0×2⁻⁷ + 1×2⁻⁸ = 0.23828125 | 83,23828125         |

---

## 12. Konversi Biner ke BCD

| **Bilangan Biner**    | **Konversi**        | **Hasil BCD** |
|-----------------------|----------------------|---------------|
| 101001110000111       | 0010 = 2, 1001 = 9, 1000 = 8, 0111 = 7 | 2987          |
| 1010101100011         | 0001 = 1, 0101 = 5, 0110 = 6, 0011 = 3 | 1563          |

---

## 13. Konversi BCD ke Biner

| **Bilangan BCD** | **Konversi**                                      | **Hasil Biner**   |
|------------------|----------------------------------------------------|-------------------|
| 1987             | 1 = 0001, 9 = 1001, 8 = 1000, 7 = 0111              | 0001 1001 1000 0111 |
| 2346             | 2 = 0010, 3 = 0011, 4 = 0100, 6 = 0110              | 0010 0011 0100 0110 |

---

## 14. Konversi Biner ke BCO

| **Bilangan Biner**     | **Konversi**        | **Hasil BCO** |
|------------------------|----------------------|---------------|
| 11111101001~2~         | 011 = 3, 111 = 7, 101 = 5, 001 = 1 | 3751          |
| 101110 010100~2~       | 101 = 5, 110 = 6, 010 = 2, 100 = 4 | 5624          |

---

## 15. Konversi Biner ke BCH

| **Bilangan Biner**     | **Konversi**        | **Hasil BCH** |
|------------------------|----------------------|---------------|
| 1101111100101110~2~    | 1101 = (D), 1111 = (F), 0010 = 2, 1110 = (E) | DF2E          |
| 110100110000001~2~     | 0110 = 6, 1001 = 9, 1000 = 8, 0001 = 1 | 6981          |

---

## 16. Konversi BCH ke Heksadesimal

| **Bilangan BCH** | **Konversi**                                         | **Hasil Heksadesimal** |
|-------------------|-------------------------------------------------------|------------------------|
| F0DE              | F = 1111, 0 = 0000, D = 1101, E = 1110                  | 1111 0000 1101 1110     |
| 1CAB              | 1 = 0001, C = 1100, A = 1010, B = 1011                  | 0001 1100 1010 1011     |

---

## 17. Nyatakan Positif atau Negatif Bilangan Biner

| **Bilangan Biner**   | **Hasil Desimal** | **Positif/Negatif** |
|----------------------|-------------------|---------------------|
| 01111111             | 127               | Positif 127         |
| 10000000             | 128               | Negatif 128         |
| 01111011             | 123               | Positif 123         |

---

## 18. Nyatakan Bilangan Biner Negatif ke Desimal

| **Bilangan Biner**   | **Hasil Desimal** |
|----------------------|-------------------|
| 10001000             | -120              |
| 11110111             | -9                |
| 10000101             | -123              |
| 10011100             | -100              |

---

## 19. Nyatakan ASCII Code dalam Bentuk Karakter

| **Kode ASCII Heksadesimal** | **Desimal** | **Karakter** |
|-----------------------------|-------------|--------------|
| 41~16~                      | 65          | 'A'          |
| 5A~16~                      | 90          | 'Z'          |
| 24~16~                      | 36          | '$'          |
| 77~16~                      | 119         | 'w'          |

---

## 20. Nyatakan Karakter dalam ASCII Code

| **Karakter** | **ASCII Code Heksadesimal** |
|--------------|-----------------------------|
| a            | 61~16~                      |
| x            | 78~16~                      |
| m            | 6D~16~                      |
| H            | 68~16~                      |

---

## 21. Keyboard ASCII Standard

| **Karakter** | **Kode ASCII Heksadesimal** | **Kode Biner** |
|--------------|-----------------------------|----------------|
| P            | 50~16~                      | 0101 0000      |
| R            | 52~16~                      | 0101 0010      |
| I            | 49~16~                      | 0100 1001      |
| N            | 4E~16~                      | 0100 1110      |
| T            | 54~16~                      | 0101 0100      |
| Space        | 20~16~                      | 0010 0000      |
| X            | 58~16~                      | 0101 1000      |

---
