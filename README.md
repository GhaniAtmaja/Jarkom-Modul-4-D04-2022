# Jarkom-Modul-4-D04-2022

## Kelompok D04
| Name                      | NRP        | 
| ------------------------- | ---------- |
| Muhammad Ghani T. Atmaja  | 5025201110 |
| Tengku Fredly Reinaldo    | 5025201198 |
| Shaula Aljauhara Riyadi   | 5025201265 |

IP Prefix Kelompok: `10.17`

# Soal dan Jawaban
![cisconya](https://user-images.githubusercontent.com/77779184/204505073-0762a219-6dd4-44ae-aaff-ffb07ebd78c6.png)

- Soal shift dikerjakan pada Cisco Packet Tracer dan GNS3 menggunakan metode perhitungan CLASSLESS yang berbeda. Keterangan: Bila di CPT menggunakan VLSM, maka di GNS3 menggunakan CIDR atau Sebaliknya
- Jika tidak ada pemberitahuan revisi soal dari asisten, berarti semua soal BERSIFAT BENAR dan DAPAT DIKERJAKAN. Untuk di GNS3 CLOUD merupakan NAT1 jangan sampai salah agar bisa terkoneksi internet.
- Pembagian IP menggunakan Prefix IP yang telah ditentukan pada modul pengenalan.
- Pembagian IP dan routing harus SE-EFISIEN MUNGKIN.

Dalam mengerjakan soal ini, kami menggunakan teknik VLSM dengan menggunakan CPT, dan teknik CIDR dengan menggunakan GNS 3

# VLSM - CPT
## Pembagian Subnet
Hal pertama yang kami lakukan adalah dengan menentukan subnet yang ada pada topologi. Dikarenakan metode yang dipakai adalah VLSM. Kami melingkari tiap host yang terhubung pada interface router dan menghitung IP yang dibutuhkan. Berikut adalah gambaran pembagian subnetnya

![vslm labeling](https://user-images.githubusercontent.com/77779184/204505338-1e91a790-fa84-4026-99c2-1274f25c2555.png)

## Jumlah IP
Setelah melakukan pembagian subnet kita melakukan penjumlahan pada IP, sehingga didapatkan hasil penjumlahan ip berikut :

![jumlah ipunknown](https://user-images.githubusercontent.com/77779184/204505458-2d493c44-cd12-4d16-bc82-e65253610da8.png)

## VSLM-Tree
Setelah mendapatkan penjumlahan IP kita membuat tree yang terdapat pada topologi. Pada subnet memiliki NID 10.17.0.0 dengan netmask /20 sehingga pembagian IP berdasarkan NID dan Netmask yang di dapat.

![Tree Subnet drawio](https://user-images.githubusercontent.com/77779184/204505573-63ac11ee-fa70-4a26-836d-fb974a61f587.png)

Pada VLSM ini diturunkan sesuai dengan netmask atasnya sehingga ketika /20 akan diturunkan menjadi /21, lakukan secara berulang-ulang sampai node semua terpenuhi.

## Pembagian IP
Kemudian kita bagi dengan tetap menggunakan IP prefix `10.17` . hasil pembagian seperti berikut :

![subnet cidrimage](https://user-images.githubusercontent.com/77779184/204505760-28e12b35-f0c6-4422-a0c3-6c8855125f69.png)

# Config VSLM
## Menambah Ethernet / Port
Karena default hanya memiliki 2 port ethernet, maka kita bisa menambah port pada tab physical

![moduleimage](https://user-images.githubusercontent.com/77779184/204506503-d3b331f8-7665-4377-9083-3f9e1b259cdf.png)

## Config IP pada Node
![1ministerimage](https://user-images.githubusercontent.com/77779184/204506671-c9e5886f-aa4c-45ef-b895-780143d8c9bb.png)

Contoh pada The Minister, kita menambahkan IP dan Subnet Mask sesuai dengan pembagian yang telah dilakukan, dengan IP ditambah 1 dari subnetnya. dan jangan lupa untuk di on kan pada port nya.

Pada server & Client ditambahkan juga gateway yang mengarah ke router terdekat.

![guideimage](https://user-images.githubusercontent.com/77779184/204506840-052d1b00-4254-4316-9884-6062b0ea7623.png)

Lakukan berulang-ulang pada semua node.

# Routing 
Pada routing berikut adalah config yang berada pada router. Untuk langkah nya bisa masuk kedalam router, lalu menekan menu static dan menambahkan data yang diinginkan.

## The Reference
- 10.17.0.4/30 via 10.17.0.10
- 10.17.0.64/26 via 10.17.0.10
- 10.17.8.0/22 via 10.17.0.10
- 10.17.0.0/30 via 10.17.0.10
- 10.17.2.0/24 via 10.17.0.10
- 10.17.0.24/30 via 10.17.0.26
- 10.17.6.0/23 via 10.17.0.26
- 10.17.0.16/30 via 10.17.0.18
- 10.17.0.128/30 via 10.17.0.18
- 10.17.0.20/30 via 10.17.0.18
- 10.17.1.128/25 via 10.17.0.18
- 10.17.1.0/25 via 10.17.0.18
- 10.17.0.12/30 via 10.17.0.18
- 10.17.4.0/23 via 10.17.0.18
- 10.17.3.0/24 via 10.17.0.18
- 10.17.0.28/30 via 10.17.0.18

![resonanimage](https://user-images.githubusercontent.com/77779184/204507002-45c71f7c-d5b9-4c97-9c77-6b4863188376.png)

Pada The Reference merupakan pusat Router jadi semua IP dari subnet diasiggn ke Router The Reference agar semua bisa terhubung.

## The Order
- 0.0.0.0/0 via 10.17.0.9
- 10.17.8.0/22 via 10.17.0.6
- 10.17.0.0/30 via 10.17.0.6
- 10.17.2.0/24 via 10.17.0.6

![orderimage](https://user-images.githubusercontent.com/77779184/204507055-c41b81c2-5788-4d20-8482-3d97c0bc12af.png)

## The Minister
- 0.0.0.0/0 via 10.17.0.5
- 10.17.2.0/24 via 10.17.0.2

![minister statisimage](https://user-images.githubusercontent.com/77779184/204507310-4616cfd5-aa67-4f22-ad77-7d1971e210f4.png)

## The Daundless
- 0.0.0.0/0 via 10.17.0.1

![dauntlesimage](https://user-images.githubusercontent.com/77779184/204507373-a4a61426-61ca-4ca2-bbae-3e753427a42b.png)

0.0.0.0 berarti mengambil semua pesan dan diarahkan ke next hop.

## The Magical
- 0.0.0.0/0 via 10.17.0.25

![magicalimage](https://user-images.githubusercontent.com/77779184/204507397-12323e41-f65a-49a6-aa2f-c557268d8c25.png)

## The Instrument
- 0.0.0.0/0 via 10.17.0.17
- 10.17.0.20/30 via 10.17.0.22
- 10.17.1.128/25 via 10.17.0.22
- 10.17.1.0/25 via 10.17.0.22
- 10.17.0.12/30 via 10.17.0.14
- 10.17.3.0/24 via 10.17.0.14
- 10.17.4.0/23 via 10.17.0.14
- 10.17.0.28/30 via 10.17.0.14

![instrumentimage](https://user-images.githubusercontent.com/77779184/204507408-6cf3ba5b-7932-49c2-8c1b-3db1efb1102f.png)

## The Profound
- 0.0.0.0/0 via 10.17.0.21

![profoundimage](https://user-images.githubusercontent.com/77779184/204507827-7f1dda43-595e-4119-b979-f379af07f708.png)

## The Firefist
- 0.0.0.0/0 via 10.17.0.13
- 10.17.0.28/30 via 10.17.3.3

![firefistimage](https://user-images.githubusercontent.com/77779184/204507857-7d59794e-89b4-4471-9308-958080b9886e.png)
## The Queen
- 0.0.0.0/0 via 10.17.3.1

![quennimage](https://user-images.githubusercontent.com/77779184/204507475-6734102f-2c11-47fa-92a7-c3e837e9fbf2.png)

# Testing
Hasil dari message tiap node.

![testingunknown](https://user-images.githubusercontent.com/77779184/204508861-88a158e0-0f07-4f06-8d41-40947e648e8d.png)

# CIDR - GNS3

## Penggabungan Subnet
Kita melakukan penggabungan subnet-subnet paling bawah dalam topologi yaitu dimulai dari subnet yang paling jauh dengan cloud/nat hingga hanya memiliki 1 subnet (induk).

- Penggabungan Pertama (Subnet B)
</br>&nbsp;&nbsp;1. Subnet A2 dan A3 menghasilkan B1 dengan netmask /23 yaitu satu tingkat dari netmask terbesar yang diambil yaitu /24 dari A3.
</br>&nbsp;&nbsp;2. Subnet A13 dan A14 menghasilkan B2 dengan netmask /23 yaitu satu tingkat dari netmask terbesar yang diambil yaitu /24 dari A13.

- Penggabungan Kedua (Subnet C)
</br>&nbsp;&nbsp;1. Subnet A1 dan B1 menghasilkan C1 dengan netmask /21 yaitu satu tingkat dari netmask terbesar yang diambil yaitu /22 dari A1.
</br>&nbsp;&nbsp;2. Subnet A12 dan B2 menghasilkan C2 dengan netmask /22 yaitu satu tingkat dari netmask terbesar yang diambil yaitu /23 dari A12.
</br>&nbsp;&nbsp;3. Subnet A9 dan A10 menghasilkan C3 dengan netmask /24 yaitu satu tingkat dari netmask terbesar yang diambil yaitu /25 dari A9.

- Penggabungan Ketiga (Subnet D)
</br>&nbsp;&nbsp;1. Subnet C1 dan A4 menghasilkan D1 dengan netmask /20 yaitu satu tingkat dari netmask terbesar yang diambil yaitu /21 dari C1.
</br>&nbsp;&nbsp;2. Subnet A11 dan C2 menghasilkan D2 dengan netmask /21 yaitu satu tingkat dari netmask terbesar yang diambil yaitu /22 dari C2.
</br>&nbsp;&nbsp;3. Subnet A8 dan C3 menghasilkan D3 dengan netmask /23 yaitu satu tingkat dari netmask terbesar yang diambil yaitu /24 dari C3.

- Penggabungan Keempat (Subnet E)
</br>&nbsp;&nbsp;1. Subnet D1 dan A5 menghasilkan E1 dengan netmask /19 yaitu satu tingkat dari netmask terbesar yang diambil yaitu /20 dari D1.
</br>&nbsp;&nbsp;2. Subnet D2 dan A15 menghasilkan E2 dengan netmask /20 yaitu satu tingkat dari netmask terbesar yang diambil yaitu /21 dari D2.

- Penggabungan Kelima (Subnet F)
</br>&nbsp;&nbsp;1. Subnet D3 dan E2 menghasilkan F1 dengan netmask /19 yaitu satu tingkat dari netmask terbesar yang diambil yaitu /20 dari E2.

- Penggabungan Keenam (Subnet G)
</br>&nbsp;&nbsp;1. Subnet E1 dan A6 menghasilkan G1 dengan netmask /18 yaitu satu tingkat dari netmask terbesar yang diambil yaitu /19 dari E1.
</br>&nbsp;&nbsp;2. Subnet A7 dan F1 menghasilkan G2 dengan netmask /18 yaitu satu tingkat dari netmask terbesar yang diambil yaitu /19 dari F1.
</br>&nbsp;&nbsp;3. Subnet A17 dan A18 menghasilkan G3 dengan netmask /22 yaitu satu tingkat dari netmask terbesar yang diambil yaitu /23 dari A18.

- Penggabungan Ketujuh (Subnet H)
</br>&nbsp;&nbsp;1. Subnet A16 dan G3 menghasilkan H1 dengan netmask /21 yaitu satu tingkat dari netmask terbesar yang diambil yaitu /22 dari G3.

- Penggabungan Kedelapan (Subnet I)
</br>&nbsp;&nbsp;1. Subnet G2 dan H1 menghasilkan I1 dengan netmask /17 yaitu satu tingkat dari netmask terbesar yang diambil yaitu /18 dari G2.

- Penggabungan Kesembilan (Subnet J)
</br>&nbsp;&nbsp;1. Subnet G1 dan I1 menghasilkan J1 dengan netmask /16 yaitu satu tingkat dari netmask terbesar yang diambil yaitu /17 dari I1.

![cidrJ1 drawio](https://user-images.githubusercontent.com/77779184/204509870-80db413d-3aab-4824-9973-7d0e7917c19a.png)

## CIDR-Tree
Setelah mendapatkan penggabungan subnet, kita membuat tree yang terdapat pada topologi. Pada paling atas (parent) memiliki subnet dengan NID 10.17.0.0 dengan netmask /16.

![TREE cidr drawio](https://user-images.githubusercontent.com/77779184/204509976-f44fd210-c3e2-4d57-a1fc-2f024782eb85.png)

## Pembagian IP
Kemudian kita bagi dengan tetap menggunakan ip prefix `10.17`. Hasil pembagian seperti berikut :

![subnet vslmimage](https://user-images.githubusercontent.com/77779184/204510098-72e3af64-11d6-4fe5-9ef6-9fdf0c74f78c.png)


## Kendala
- Saat melakukan ping di cpt, ada yang harus dilakukan 2-3x tidak bisa langsung 1x karena failed, nemun setelah dicoba lagi menjadi succesful


