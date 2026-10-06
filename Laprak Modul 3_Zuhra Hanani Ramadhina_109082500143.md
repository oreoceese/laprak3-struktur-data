# <h1 align="center">Laporan Praktikum Modul 3 - ABSTRACT DATA TYPE (ADT)</h1>
<p align="center">Zuhra Hanani Ramadhina - 109082500143</p>

## Dasar Teori
Abstract Data Type (ADT) adalah suatu model data yang mendefinisikan kumpulan nilai beserta operasi-operasi yang dapat dilakukan terhadap data tersebut, tanpa menjelaskan secara detail bagaimana data dan operasi tersebut diimplementasikan[1]. Dalam C++, ADT umumnya direalisasikan menggunakan struct atau class, yang memungkinkan data dan fungsi-fungsi terkait dikelompokkan menjadi satu kesatuan. Selain ADT, pemrograman C++ juga sering memanfaatkan array multidimensi dan pointer untuk mengelola data yang lebih kompleks, seperti menyimpan data dalam bentuk tabel atau melakukan manipulasi nilai secara langsung melalui alamat memori[2].

### A. Struct dan Pemrograman Multi-File<br/>
Struct digunakan untuk mengelompokkan beberapa variabel dengan tipe data berbeda ke dalam satu kesatuan data. Dalam program yang lebih besar, kode sering dipisah menjadi beberapa file (header dan implementasi) agar lebih terorganisir dan mudah dipelihara.

#### 1. Struct — mengelompokkan data dengan tipe berbeda dalam satu unit
#### 2. File header (`.h`) — berisi deklarasi struct dan prototipe fungsi
#### 3. File implementasi (`.cpp`) — berisi definisi lengkap dari fungsi yang dideklarasikan di header

### B. Array 2D dan Pointer<br/>
Array dua dimensi digunakan untuk menyimpan data dalam bentuk baris dan kolom, sedangkan pointer memungkinkan program mengakses dan memanipulasi nilai suatu variabel secara langsung melalui alamat memorinya.

#### 1. Array 2D — menyimpan dan mengakses data menggunakan indeks baris dan kolom
#### 2. Pointer — menyimpan alamat memori suatu variabel
#### 3. Pertukaran nilai menggunakan pointer — memodifikasi nilai asli melalui dereference (`*`)

## Guided 

### 1. mahasiswa.h

```C++
#ifndef MAHASISWA_H_INCLUDED
#define MAHASISWA_H_INCLUDED
struct mahasiswa{
    char nim[13];
    int nilai1, nilai2;
};

void inputMhs (mahasiswa &m) ;
float rata2 (mahasiswa m) ;
#endif // MAHASISWA_H_INCLUDED
```
File header ini mendefinisikan struct mahasiswa yang menyimpan data NIM (char nim[13]) dan dua nilai (nilai1, nilai2). File ini juga mendeklarasikan prototipe dua fungsi (inputMhs dan rata2) yang nanti diimplementasikan di mahasiswa.cpp, sehingga file lain yang meng-include header ini bisa memakai struct dan fungsi tersebut tanpa perlu tahu detail implementasinya. Directive #ifndef/#define/#endif (include guard) mencegah header ini dimasukkan berkali-kali ke file yang sama, yang bisa menyebabkan error duplikasi deklarasi.

### 2. mahasiswa.cpp

```C++
#include <iostream>
#include "mahasiswa.h"

using namespace std;

void inputMhs(mahasiswa &m) {
    cout << "input nim = ";
    cin >> (m).nim;
    cout << "input nilai = ";
    cin >> (m).nilai1;
    cout << "input nilai2 = ";
    cin >> (m).nilai2;
}

float rata2(mahasiswa m) {
    return float(m.nilai1+m.nilai2)/2;
}
```
File ini mengimplementasikan dua fungsi yang dideklarasikan di header. Fungsi inputMhs() menerima parameter struct mahasiswa secara reference (&m), sehingga nilai yang diinput langsung mengubah data struct aslinya di luar fungsi, bukan hanya salinannya. Fungsi rata2() menerima parameter secara value biasa (bukan reference) karena fungsi ini hanya perlu membaca data untuk menghitung rata-rata, tidak perlu mengubah struct aslinya.

### 3. main.cpp

```C++
#include <iostream>
#include "mahasiswa.h"

using namespace std;

int main()
{
    mahasiswa mhs;
    inputMhs (mhs) ;
    cout << "rata-rata = " << rata2 (mhs) ;
    return 0;
}
```
File ini menjadi program utama yang membuat satu variabel struct mahasiswa bernama mhs, lalu memanggil inputMhs(mhs) untuk mengisi datanya dan rata2(mhs) untuk menghitung serta menampilkan rata-rata dari dua nilai yang sudah diinput. File ini meng-include mahasiswa.h agar bisa mengenali struct dan fungsi yang didefinisikan di file lain.

## Unguided 

### 1. Buat program yang dapat menyimpan data mahasiswa (max. 10) ke dalam sebuah array dengan field nama, nim, uts, uas, tugas, dan nilai akhir. Nilai akhir diperoleh dari FUNGSI dengan rumus 0.3*uts+0.4*uas+0.3*tugas. 

```C++
#include <iostream>
#include <string>
using namespace std;

struct Mahasiswa {
    string nama;
    string nim;
    float uts, uas, tugas;
    float nilaiAkhir;
};

float hitungNilaiAkhir(float uts, float uas, float tugas) {
    return 0.3 * uts + 0.4 * uas + 0.3 * tugas;
}

int main() {
    Mahasiswa data[10];
    int jumlah;

    cout << "Masukkan jumlah mahasiswa (max 10): ";
    cin >> jumlah;

    for (int i = 0; i < jumlah; i++) {
        cout << "\nData mahasiswa ke-" << i + 1 << endl;
        cout << "Nama  : ";
        cin >> data[i].nama;
        cout << "NIM   : ";
        cin >> data[i].nim;
        cout << "UTS   : ";
        cin >> data[i].uts;
        cout << "UAS   : ";
        cin >> data[i].uas;
        cout << "Tugas : ";
        cin >> data[i].tugas;

        data[i].nilaiAkhir = hitungNilaiAkhir(data[i].uts, data[i].uas, data[i].tugas);
    }

    cout << "\n--- Rekap Nilai Akhir ---" << endl;
    for (int i = 0; i < jumlah; i++) {
        cout << data[i].nama << " (" << data[i].nim << ") : " << data[i].nilaiAkhir << endl;
    }

    return 0;
}
```
### Output Unguided 1 :

##### Output 1
![Screenshot Output Unguided 1_1](https://github.com/oreoceese/laprak3-struktur-data/blob/3-soal1.png)

##### Output 2
![Screenshot Output Unguided 1_2](https://github.com/oreoceese/laprak3-struktur-data/blob/3-soal1_2.png)

Program menyimpan data hingga 10 mahasiswa menggunakan array of struct, di mana setiap elemen array berisi nama, NIM, dan nilai UTS, UAS, serta tugas. Fungsi hitungNilaiAkhir() menghitung nilai akhir tiap mahasiswa menggunakan rumus bobot (30% UTS, 40% UAS, 30% tugas), lalu hasilnya disimpan ke dalam struct dan ditampilkan dalam bentuk rekap di akhir program.


### 2. Program Implementasi ADT Pelajaran Menggunakan Struct dan Multi-File (pelajaran.h, pelajaran.cpp, main.cpp)

#### Source Code pelajaran.h
```C++
#ifndef PELAJARAN_H_INCLUDED
#define PELAJARAN_H_INCLUDED
#include <string>
using namespace std;

struct pelajaran {
    string namaMapel;
    string kodeMapel;
};

pelajaran create_pelajaran(string namapel, string kodepel);
void tampil_pelajaran(pelajaran pel);

#endif
```

#### Source Code pelajaran.cpp
```C++
#include <iostream>
#include "pelajaran.h"
using namespace std;

pelajaran create_pelajaran(string namapel, string kodepel) {
    pelajaran p;
    p.namaMapel = namapel;
    p.kodeMapel = kodepel;
    return p;
}

void tampil_pelajaran(pelajaran pel) {
    cout << "nama pelajaran : " << pel.namaMapel << endl;
    cout << "nilai : " << pel.kodeMapel << endl;
}
```

#### Source Code main.cpp
```C++
#include <iostream>
#include "pelajaran.h"
using namespace std;

int main() {
    string namapel = "Struktur Data";
    string kodepel = "STD";
    pelajaran pel = create_pelajaran(namapel, kodepel);
    tampil_pelajaran(pel);

    return 0;
}
```
### Output Unguided 3 :

#### Output
![Screenshot Output Unguided 2_1](https://github.com/oreoceese/laprak3-struktur-data/blob/3-soal2.png)

Program ini memisahkan struct pelajaran dan deklarasi fungsinya ke dalam file header (pelajaran.h), sementara implementasi fungsi create_pelajaran() dan tampil_pelajaran() ditulis di file terpisah (pelajaran.cpp). File main.cpp hanya memanggil fungsi-fungsi tersebut tanpa perlu tahu detail implementasinya, menunjukkan penerapan konsep ADT di mana struktur data dan operasinya digunakan secara terpisah dari detail teknis di baliknya.

### 3. Program Array 2D dan Pointer untuk Menukar Nilai pada Posisi Tertentu

```C++
#include <iostream>
using namespace std;

void tampilkanArray2D(int arr[3][3]) {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cout << arr[i][j] << " ";
        }
        cout << endl;
    }
}

void tukarArray2D(int arr1[3][3], int arr2[3][3], int baris, int kolom) {
    int temp = arr1[baris][kolom];
    arr1[baris][kolom] = arr2[baris][kolom];
    arr2[baris][kolom] = temp;
}

void tukarPointer(int *p1, int *p2) {
    int temp = *p1;
    *p1 = *p2;
    *p2 = temp;
}

int main() {
    int arrA[3][3] = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };
    int arrB[3][3] = {
        {9, 8, 7},
        {6, 5, 4},
        {3, 2, 1}
    };

    cout << "Array A sebelum ditukar:" << endl;
    tampilkanArray2D(arrA);
    cout << "\nArray B sebelum ditukar:" << endl;
    tampilkanArray2D(arrB);

    int baris, kolom;
    cout << "\nMasukkan posisi baris yang ditukar (0-2): ";
    cin >> baris;
    cout << "Masukkan posisi kolom yang ditukar (0-2): ";
    cin >> kolom;

    tukarArray2D(arrA, arrB, baris, kolom);

    cout << "\nArray A setelah ditukar:" << endl;
    tampilkanArray2D(arrA);
    cout << "\nArray B setelah ditukar:" << endl;
    tampilkanArray2D(arrB);

    int x = 10, y = 20;
    int *px = &x;
    int *py = &y;

    cout << "\nSebelum ditukar (pointer): x=" << x << " y=" << y << endl;
    tukarPointer(px, py);
    cout << "Setelah ditukar (pointer): x=" << x << " y=" << y << endl;

    return 0;
}
```
### Output Unguided 3 :

##### Output 
![Screenshot Output Unguided 3_1](https://github.com/oreoceese/laprak3-struktur-data/blob/3-soal3.png)

Program ini mendemonstrasikan dua konsep sekaligus: pertama, dua buah array 2D berukuran 3x3 yang nilainya dapat ditukar pada posisi (baris, kolom) tertentu menggunakan fungsi tukarArray2D(); kedua, dua buah variabel integer yang ditukar nilainya melalui pointer menggunakan fungsi tukarPointer(), yang memodifikasi nilai asli secara langsung lewat proses dereference (*p1, *p2).

## Kesimpulan
Berdasarkan praktikum yang telah dilakukan, dapat disimpulkan bahwa ADT merupakan konsep penting dalam pemrograman yang memungkinkan data dan operasinya dikelola secara terstruktur melalui struct, serta diimplementasikan dalam program multi-file agar kode lebih terorganisir. Selain itu, penguasaan array dua dimensi dan pointer sangat diperlukan untuk mengelola data yang lebih kompleks, seperti menyimpan data mahasiswa dalam array, serta melakukan pertukaran nilai antar elemen array maupun antar variabel menggunakan pointer. Melalui latihan guided dan unguided, mahasiswa dilatih menerapkan konsep-konsep tersebut dalam penyelesaian permasalahan pemrograman yang lebih kompleks dibandingkan modul sebelumnya.

## Referensi
[1] Triase. (2020). Diktat Edisi Revisi : STRUKTUR DATA. Medan: UNIVERSTAS ISLAM NEGERI SUMATERA UTARA MEDAN.
<br>[2] Indahyanti, Uce., Rahmawati, Yunianita. (2020). *Buku Ajar Algoritma dan Pemrograman dalam Bahasa C++*. Sidoarjo: UMSIDA Press. Diakses melalui https://doi.org/10.21070/2020/978-623-6833-67-4.
