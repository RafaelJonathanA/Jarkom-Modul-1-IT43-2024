# Laporan Resmi Praktikum Modul 1 Jaringan Komputer

### Wireshark

### Kelompok IT43 -

| Name                              |     NRP    |
| ----------------------------------|------------|
| Rafael Jonathan Arnoldus          | 5027231006 | 
| Gandhi Ert Julio                  | 5027231081 |


---
---
---

## _Soal Advance Sanity Check_

#### Pertanyaan
- Username Pengirim
- Nama File Yang Dikirim
- String Rahasia

---

![Pertama](https://github.com/user-attachments/assets/b800cc4c-43a8-48a7-a322-41e9cfabbab9)
```
tcp 
```
Disini saya sudah pengfilteran `tcp`1 dan dari hasil capture ini saya mencari manual dimana isi paket/file yang berbeda dari yang lain.

![Kedua](https://github.com/user-attachments/assets/2f174e17-9dd5-460f-8ef5-066764f50ce6)
![ketiga](https://github.com/user-attachments/assets/ab5592e2-5cf0-483e-a8fd-0e14df88381a)
![keempat](https://github.com/user-attachments/assets/c29b6828-651d-4a87-b6f0-a542c27c9e97)

Lalu Terdapat beberapa hint dari hasil stream yang lainnya yang menunjukkan identitas username, Nama file yang dikirim dan petunjuk mendapatksan string password.

Lalu dengan mengikuti dan mengarah ke peraturan praktikunm yang tersedia didapatkan hasil string password yang ada

![kelima](https://github.com/user-attachments/assets/a52be43b-c4ae-420e-8bd3-33f77d0a5c92)
> Dengan encoding `base64` didapatkan hasilnya : `penword`

![keenam](https://github.com/user-attachments/assets/66151fcc-1783-4746-a5f3-c9cad2174593)
> Pendapatan hasil Flag

nc 10.15.42.60 Port 44000


## _Soal FTP Login_

#### Pertanyaan
- Username sukses saat FTP Login
- Password sukses saat FTP Login

---

Dengan filtering `ftp` dan mencarinya secara manual
```
ftp
```
![21](https://github.com/user-attachments/assets/86a625ee-10a0-4b71-9424-589938cd9f3a)
> Didapatkan hasil saat tcp stream salah satu paket

![801](https://github.com/user-attachments/assets/11923668-cedf-4018-9348-9e2f565d1d03)

Terlihat dari sini dimana username `sn34ky` dan password `sup3rsn1ff3r` lolos autentikasi user.

Lalu dengan mengakses Port 49000 terdapat pertanyaan tadi dalam meraih flag
![4a](https://github.com/user-attachments/assets/abc908b3-60ef-49ec-aa01-2c969b3bf76c)


## _Soal Surprise_

#### Pertanyaan

- Service dipakai di FTP server
- Nama file yang dikirim attacker
- Pesan rahasia ditinggalkan attacker

---

Dengan filtering paket dengan query `ftp.response.code == 220` yang merupakan respon dari server FTP saat koneksi pertama kali.
```
ftp.response.code == 220
```
![d5dd91f7-feea-489a-afdc-328dc3798cf8](https://github.com/user-attachments/assets/e50c6762-c0ba-49dd-aab3-b8d9eff4fcde)
> Dari tampilan capture sudah memberikan banner yang menampilkan service ver 

Mencari paket yang diupload menggunakan query `ftp.request.command == "STOR"`
```
ftp.request.command == "STOR"
```
![d33fad29-5ca2-425a-a35f-6d911c372564](https://github.com/user-attachments/assets/04da3c6f-87f9-4d46-9fd2-4493a653e512)
> g0tcha.cpp

Lalu dengan Export code FTP data dan mengcompile file tersebut mendapatkan pesan rahasia

![b1232445-88d4-4b32-bedd-94aa15a4249d](https://github.com/user-attachments/assets/1c7bc882-9944-4862-8cda-240fea3e52e6)
> Pertanyaan dan peraihan flag


## _Soal Illegal Breakthrough_

#### Pertanyaan

- IP Adress korban
- Port yang dipakai sebagai webserver
- Endpoint pada login
- Tools yang digunakan attacker
- Kredensial untuk login attacker

---

![4e4a8053-5964-4ccf-83df-9c90bc584e40](https://github.com/user-attachments/assets/618611ed-2020-47db-a14e-eb1c2f7fa0b2)

Pada capture tersebut terdapat komunikasi TCP 172.21.80.1 melakukan POST ke 172.21.88.207.

![965086b8-84ff-458b-b524-7b699b6ffe43](https://github.com/user-attachments/assets/237bace2-7fb2-4f16-a846-f260db408809)
> Terlihat bahwa Source dan Destination, 1917 dipakai komunikasi HTTP ini. 
Dan dari capture tersebut sudah memberikan POST request ke ww1.php dengan data user dan pass. Menunjukkan jika itu adalah endpoint login.

![9c9cef7c-51eb-46c6-9964-9ed9c96789de](https://github.com/user-attachments/assets/749c99ef-c55b-4c36-b353-c192af4eb97f)

Dan pada bari User-Agent di heaeder http ini ada jejak dari toolsnya, `ffuf-v2.1.0-dev`

![911d7fe1-3d6b-4c61-b5a0-7a9d80bd85b5](https://github.com/user-attachments/assets/7f2b6e6d-13f7-4417-b666-44e4a24c426d)
> Mencari kredensial login attacker dengan filtering dan mendapatkan hasil

![149e947b-d9e7-419d-ad28-c3b7654b8db7](https://github.com/user-attachments/assets/13c32583-895f-4857-8a2c-e7c2118b7c0d)
> Pertanyaan dan peraihan flag

## _Soal Rizzset_

#### Pertanyaan

- Nama Domain dari dns query di log
- IP Domain
- Jarm fingerprint dihasilkan dari domain itu

---

![7f04d8cd-14e6-435e-9e08-b2ac990055b4](https://github.com/user-attachments/assets/7525c132-0a12-498d-9f2a-4c0f78af00a1)

Terlihat dari hasil capture diatas ada query dns ke `www.its.ac.id`. dan IP nya yaitu `103.94.189.5`

Lalu menyiapkan JARM Fingerprint dan mencoba menjalankan JARM ke domain yang ingin di fingerprint
![d2084b76-a37b-4848-a21c-fa463bc9dcbd](https://github.com/user-attachments/assets/fc5b26de-7f55-4a1e-afcd-16468e060506)
> Hasil JARM Fingerprint

Lalu eksekusi ke PORT
![bc5ccdc7-163e-4d45-b93e-ee50f49b4a24](https://github.com/user-attachments/assets/80d4af01-647d-44f7-bec2-94379e11bb3b)
> Pertanyaan dan peraihan flag


## _Soal Pegawai Negeri Sebelah_

#### Pertanyaan

- Siapa yang memiliki password nNnM%coQuF?
- Apa jabatan dari Taufan Kuswandari?
- Siapa yang paling awal di list?
- Apa password paling akhir dari list?


---

Pertama saya mendownload filenya lalu saya membuka dan menggunakan statistic dan conversation untuk melihat filenya lalu saya akan mencari password tersebut dengan searchnya lalu nama Taufan Kuswandari lalu melihat nama paling awal di list dan password paling akhir di list sehingga mendapatkan flagnya 

Flag : JarkomIT{Tum8eN_p45SnYa_Ku4t_B1aS4Nya_Hiow4mM5G172RSwBA8w8YJhWLL30AqhvwbyvDZrMNYRSAVwddw9vM4h}

[Pegawai Sebelah](https://github.com/user-attachments/assets/8bb7cb94-de77-4da2-a7ff-508f7b28285c)

## _Soal Corporate Breach _

#### Pertanyaan

- Siapa nama attacker?
- Apa email yang digunakan untuk login?
- Apa password yang digunakan untuk login?

---

Pertama saya mendownload file yang ada
Kedua saya langsung memfilter dengan statistic lalu menu conversation lalu saya cari mulai dari depan sampai ke paling akhir di file awal terdapat perkenalan dirinya sehingga saya mendapatkan nama attacker secara sekilas dan menemukan ada satu file yang berbeda pola formatnya dan langsung ketemu email serta password yang digunakan 

Flag : JarkomIT{supp0rt_k0k_l3m4h_bg_cv09tgcni7sDpEEaO4oyDxmfAG6XNddtZ7zBRYNW4NxDWSsDm3YwG6}

![breach](https://github.com/user-attachments/assets/25294662-9d4f-4b10-9814-01ead716dc76)

## _Soal Ez _

#### Pertanyaan

- Temukan jawaban dari log tersebut
- Port berapa yang digunakan service tersebut

---

Pertama Saya mendownload file yang ada lalu saya langsung menggunakan statistic dengan pilihan conversation lalu saya mengecek di file-file dan saya langsung menemukan jawabannya dan disaat yang sama portnya juga secara langsung terlihat 

Flag : JarkomIT{BiAr_aman_Pake_sSh_XhI4JDwoO9pxCSLUx9Rh3hrE43zSBorh9mFRyADDwCE0X0pq5yxXEZ}

![ez](https://github.com/user-attachments/assets/0dc5348a-e7fc-4523-b91f-ef0fa72d06a9)


## _Soal Malicious Code_

#### Pertanyaan

- Berapa total attempt attacker melakukan dir listing?
- Apa endpoint yang berhasil attacker dapatkan untuk login page?
- Pada attempt ke berapa attacker menemukan email dan password yang benar?
- Apa jawaban dari pertanyaan sang attacker?

---

Pertama saya buka file yang sama seperti saat mengerjakan soal corporate breach lalu saya menggunakan menu statistic dan conversation namun saya hanya menemukan pertanyaan yang berupa kode ascii yang perlu di ubah terlebih dahulu agar menjadi string yang dapat dibaca sehingga saya menggunakan filter http.request.method == "GET" untuk mendapatkan semua yang berupa request get yang kemudian dibuka melalui statistic untuk melihat jumlahnya, untuk endpoint saya menemukannya dengan filter http.request.method == "POST" untuk mendapatkan semua yang berupa request post yang kemudian saya dapatkan endpointnya, untuk yang terakhir setelah saya ubah saya dapatkan sebuah pertanyaan warna kesukaan pembuat soal dengan hint sweater, sehingga saya menjawab warna merah 

Flag : Benar! Ini flag-mu: JarkomIT{s3cr3t_m3ss4ge_fr0m_4uth0r_ZytXVTnBwhoyFIvyfW3Lk8naIC0T7J2hnXY5I9FDCm5yOQLiK73UL0R}

![malcious](https://github.com/user-attachments/assets/3f875dde-3cfe-4340-9e03-40ebf23e1782)

## _Soal Gajah terbang_

#### Pertanyaan

- Apa DBMS yang digunakan pada server tersebut?
- Di port berapa DBMS server tersebut berjalan?
- OS apa yang digunakan untuk server tersebut?
- Apa credentials username DBMS valid yang digunakan?
- Apa nama database yang digunakan?
- Ada berapa banyak users dalam database tersebut?
- Apa email yang digunakan oleh admin?
- Apa password yang digunakan oleh admin? 
---
Pertama saya membuka file gajah terbang lalu saya menggunakan statistic dan conversation untuk melihat isi dari file-filenya lalu saya mendapatkan namanya psql dan setelah itu saya mencari portnya dengan melihat dari tampilan dengan ada port berapa saja dan saya coba satu-satu sehigga mendapatkan port 6969 yang benar lalu di dalam file bila di perhatikan juga ada Debian sebagai OSnya lalu untuk nama username DBMS itu juga terlihat dari file yang ada langsung berapa pada bagian paling atas lalu untuk nama database juga sama langsung terlihat di bagian atas, jumlah user saya dapatkan dari menghitung manual pada isi file ada berapa banyak, dan unutuk password saya dapatkan dari file yang kemmudian harus di didecripsikan terlebihh dahulu

Flag : JarkomIT{Gy4tT_M5g_4U_GdGpusLONVeRns0bsCPDYOLvw5k1rq9fHseecDt9LCorWGnovNZgmBiD1}

![Gajah Terbang](https://github.com/user-attachments/assets/7ea8c5ea-c257-4704-9d21-42e108c212f2)

## Revisi
> Tidak ada
