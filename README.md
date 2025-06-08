## FP Komputasi Numerik Kelompok A15
|	NRP 	|  	Nama  	|
| :--------: | :------------: |
| 5025241030 | Agnella Agrata |
| 5025241031 | Qurrata A’yun Kamil |
| 5025241045 | Muhammad Fathan Haiban Rafif |
| 5025241094 | Fayza Lathifah Humam |
| 5025241118 | Muhammad Adi Anugerah Arrahman |

Program ini berfungsi untuk menghitung akar dari suatu persamaan non-linear f(x)=0 menggunakan metode Regula Falsi (posisi salah). Metode Regula Falsi merupakan teknik numerik berbasis pendekatan linear yang memanfaatkan dua titik batas awal dan memperbarui titik pendekatan akar secara iteratif hingga mencapai tingkat akurasi tertentu.

### 1. Import Library
```python
import sympy as sp
import numpy as np
```
Melakukan import terhadap library `sympy` untuk manipulasi simbolik dan `numpy` untuk perhitungan numerik.

### 2. Input Fungsi dan Batasan dari User
```python
x = sp.Symbol('x')

print("Masukkan fungsi f(x) dalam bentuk ekspresi matematika:")
print("Contoh: x**3 + 6*x**2 - 19*x - 84")
fungsi_str = input("f(x) = ")

try:
    fungsi = sp.sympify(fungsi_str)
    print(f"Fungsi yang dimasukkan: f(x) = {fungsi}")
except:
    print("Error: Format fungsi tidak valid!")

batas_bawah = float(input("Masukkan batas bawah (Xl): "))
batas_atas = float(input("Masukkan batas atas (Xu): "))
nilai_sebenarnya = float(input("Masukkan nilai x sebenarnya: "))

print(f"\nInterval: [{batas_bawah}, {batas_atas}]")
print(f"Nilai x sebenarnya: {nilai_sebenarnya}")
```
Mendefinisikan variabel simbolik X dan meminta masukan dari user berupa fungsi matematika, batas bawah dan atas interval pencarian akar, serta nilai akar sebenarnya.

### 3. Setup Iterasi Regula Falsi
```python
f = sp.lambdify(x, fungsi, 'numpy')

f_bawah = f(batas_bawah)
f_atas = f(batas_atas)

print(f"f({batas_bawah}) = {round(f_bawah, 2)}")
print(f"f({batas_atas}) = {round(f_atas, 2)}")
```
Mengubah fungsi simbolik menjadi fungsi numerik dengan `lambdify()`, kemudian menghitung nilai fungsi pada batas bawah dan atas sebagai persiapan awal iterasi.

### 4. Looping Iterasi
```python
while Et > 1:
    iterasi += 1

    f_xl = f(xl)
    f_xu = f(xu)

    xr = xu - f_xu * (xl - xu) / (f_xl - f_xu)
    f_xr = f(xr)

    if iterasi == 1:
        xr_sebelumnya = xr
    Ea = abs((xr - xr_sebelumnya) / xr) * 100
    Et = abs((xr - nilai_sebenarnya) / nilai_sebenarnya) * 100

    print(f"{iterasi:<8} {round(xl, 2):<10} {round(xu, 2):<10} {round(xr, 2):<12} {round(f_xl, 2):<12} {round(f_xu, 2):<12} {round(f_xr, 2):<12} {round(Et, 2):<12} {round(Ea, 2):<10}")

    if Et <= 1:
        break

    if f_xl * f_xr < 0:
        xu = xr
    else:
        xl = xr

    xr_sebelumnya = xr

    if iterasi >= 100:
        print("Peringatan: Mencapai batas maksimum iterasi!")
        break
```
Melakukan iterasi dengan metode Regula Falsi untuk mencari nilai pendekatan akar X. Pada setiap iterasi dihitung error aproksimasi (EA) dan error sebenarnya (ET). Iterasi berlanjut hingga 0 <= ET < 1 atau jumlah maksimum iterasi tercapai.

### 5. Print Hasil Akhir Perhitungan
```python
print("=" * 105)
print(f"\nHASIL AKHIR:")
print(f"Akar persamaan ditemukan: x = {round(xr, 2)}")
print(f"Nilai sebenarnya: x = {nilai_sebenarnya}")
print(f"Error true: {round(abs((xr - nilai_sebenarnya)/nilai_sebenarnya)*100, 2)}%")
print(f"Error aproximasi: {round(Ea, 2)}%")
```
Menampilkan hasil akhir dari perhitungan berupa akar pendekatan yang ditemukan, nilai sebenarnya, serta error aproksimasi dan error sebenarnya dalam bentuk persen.

## Implementasi
**f(x) = x^3 + 6x^2 - 19x - 84**
- Batas bawah (Xl) = -1
- Batas atas (Xu) = 8
- Nilai X sebenarnya = 4

Akan menghasilkan output sebagai berikut:
```txt
Interval: [-1.0, 8.0]
Nilai x sebenarnya: 4.0

f(-1.0) = -60.0
f(8.0) = 660.0

Mulai iterasi Posisi Salah...
=========================================================================================================
Iterasi  Xl         Xu         Xr           f(Xl)        f(Xu)        f(Xr)        ET (%)       EA (%)    
=========================================================================================================
1        -1.0       8.0        -0.25        -60.0        660.0        -78.89       106.25       0.0       
2        -0.25      8.0        0.63         -78.89       660.0        -93.35       84.23        139.63    
3        0.63       8.0        1.54         -93.35       660.0        -95.35       61.4         59.14     
4        1.54       8.0        2.36         -95.35       660.0        -82.31       41.03        34.55     
5        2.36       8.0        2.98         -82.31       660.0        -60.68       25.39        20.96     
6        2.98       8.0        3.41         -60.68       660.0        -39.56       14.83        12.4      
7        3.41       8.0        3.67         -39.56       660.0        -23.72       8.34         7.08      
8        3.67       8.0        3.82         -23.72       660.0        -13.51       4.58         3.94      
9        3.82       8.0        3.9          -13.51       660.0        -7.47        2.48         2.15      
10       3.9        8.0        3.95         -7.47        660.0        -4.06        1.34         1.16      
11       3.95       8.0        3.97         -4.06        660.0        -2.19        0.72         0.62      
=========================================================================================================

HASIL AKHIR:
Akar persamaan ditemukan: x = 3.97
Nilai sebenarnya: x = 4.0
Error true: 0.72%
Error aproximasi: 0.62%
```
