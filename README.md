# Jarkom-Modul-5-A08-2023
Praktikum Modul 5 Jaringan Komputer 2023

## Anggota Kelompok A08

| No.  | Nama Anggota       | NRP          |
|------|--------------------|--------------|
| 1    |Mohammad Zhafran Dzaky           | 5025211142   |
| 2    | Katarina Inezita Prambudi         | 5025211148   |

## Soal Modul 5

Setelah pandai mengatur jalur-jalur khusus, kalian diminta untuk membantu North Area menjaga wilayah mereka dan kalian dengan senang hati membantunya karena ini merupakan tugas terakhir.

A. Tugas pertama, buatlah peta wilayah sesuai berikut ini:

Keterangan:	
- Richter adalah DNS Server
- Revolte adalah DHCP Server
- Sein dan Stark adalah Web Server
- Jumlah Host pada SchwerMountain adalah 64
- Jumlah Host pada LaubHills adalah 255
- Jumlah Host pada TurkRegion adalah 1022
- Jumlah Host pada GrobeForest adalah 512

B. Untuk menghitung rute-rute yang diperlukan, gunakan perhitungan dengan metode VLSM. Buat juga pohonnya, dan lingkari subnet yang dilewati. 

C. Kemudian buatlah rute sesuai dengan pembagian IP yang kalian lakukan. 

D. Tugas berikutnya adalah memberikan ip pada subnet SchwerMountain, LaubHills, TurkRegion, dan GrobeForest menggunakan bantuan DHCP.


## Jawaban Modul 5

### Perhitungan VLSM

#### Berikut adalah topologi dan pembagian subnet

<img width="591" alt="image_2023-12-19_09-18-24" src="https://github.com/katarinainezita/Jarkom-Modul-2-A08-2023/assets/109232320/42acf991-e370-44a3-a8b2-2e02dde2ddfb">


#### Berikut adalah perhitungannya

<img width="312" alt="image" src="https://github.com/katarinainezita/Jarkom-Modul-2-A08-2023/assets/109232320/b71f0df4-1619-4204-9074-7e96d29e6b0a">

<img width="250" alt="image" src="https://github.com/katarinainezita/Jarkom-Modul-2-A08-2023/assets/109232320/e1a4eddd-7f8b-401c-8edd-5461e576d997">

#### Konfigurasi Network setiap node

##### Aura

```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 10.3.0.21
	netmask 255.255.255.252

auto eth2
iface eth2 inet static
	address 10.3.0.17
	netmask 255.255.255.252

```

##### Frieren 

```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
	address 10.3.0.18
	netmask 255.255.255.252
	gateway 10.3.0.17

auto eth1
iface eth1 inet static
	address 10.3.0.13
	netmask 255.255.255.252

auto eth2
iface eth2 inet static
	address 10.3.0.9
	netmask 255.255.255.252

```

#### Himmel
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
	address 10.3.0.10
	netmask 255.255.255.252
	gateway 10.3.0.9

auto eth1
iface eth1 inet static
	address 10.3.2.1
	netmask 255.255.254.0

auto eth2
iface eth2 inet static
	address 10.3.0.129
	netmask 255.255.255.128

```

##### Fern
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
	address 10.3.0.130
	netmask 255.255.255.128
	gateway 10.3.0.129

auto eth1
iface eth1 inet static
	address 10.3.0.5
	netmask 255.255.255.252

auto eth2
iface eth2 inet static
	address 10.3.0.1
	netmask 255.255.255.252

```

##### Revolte
```
auto eth0
iface eth0 inet static
	address 10.3.0.2
	netmask 255.255.255.252
	gateway 10.3.0.1

```

##### Richter
```
auto eth0
iface eth0 inet static
	address 10.3.0.6
	netmask 255.255.255.252
	gateway 10.3.0.5
```

##### SchwerMountain & Laubhills & TurkRegion & GrobeForest
```
auto eth0
iface eth0 inet dhcp
```

##### Stark
```
auto eth0
iface eth0 inet static
	address 10.3.0.14
	netmask 255.255.255.252
	gateway 10.3.0.13
```

##### Heiter
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
	address 10.3.0.22
	netmask 255.255.255.252
	gateway 10.3.0.21

auto eth1
iface eth1 inet static
	address 10.3.8.1
	netmask 255.255.252.0

auto eth2
iface eth2 inet static
	address 10.3.4.1
	netmask 255.255.252.0

```

##### Sein
```
auto eth0
iface eth0 inet static
	address 10.3.4.2
	netmask 255.255.252.0
	gateway 10.3.4.1
```

#### Routing dan Konfigurasi DNS, Web server, DHCP Server, dan DHCP relay


##### Aura

```
#!/bin/bash

# Frieren
route add -net 10.3.0.0 netmask 255.255.255.252 gw 10.3.0.18
route add -net 10.3.0.4 netmask 255.255.255.252 gw 10.3.0.18
route add -net 10.3.0.128 netmask 255.255.255.128 gw 10.3.0.18
route add -net 10.3.2.0 netmask 255.255.254.0 gw 10.3.0.18
route add -net 10.3.0.8 netmask 255.255.255.252 gw 10.3.0.18
route add -net 10.3.0.12 netmask 255.255.255.252 gw 10.3.0.18

# Heiter
route add -net 10.3.8.0 netmask 255.255.252.0 gw 10.3.0.22
route add -net 10.3.4.0 netmask 255.255.252.0 gw 10.3.0.22

```

##### Frieren

```
#!/bin/bash
route add -net 10.3.0.0 netmask 255.255.255.252 gw 10.3.0.10
route add -net 10.3.0.4 netmask 255.255.255.252 gw 10.3.0.10
route add -net 10.3.0.128 netmask 255.255.255.128 gw 10.3.0.10
route add -net 10.3.2.0 netmask 255.255.254.0 gw 10.3.0.10

```

##### Himmel

```
#!/bin/bash
route add -net 10.3.0.0 netmask 255.255.255.252 gw 10.3.0.130
route add -net 10.3.0.4 netmask 255.255.255.252 gw 10.3.0.130
```

### No. 1
Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi Aura menggunakan iptables, tetapi tidak ingin menggunakan MASQUERADE.

#### Solusi
Untuk melakukan hal ini, kita perlu menambahkan script seperti berikut pada aura untuk dapat mengakses keluar atau mengakases internet,
```
ETH0_IP=$(ip -4 addr show eth0 | grep -oP '(?<=inet\s)\d+(\.\d+){3}')
iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source $ETH0_IP
```

- `ip -4 addr show eth0` merupakan perintah yang digunakan untuk mengakses dan menampilkan informasi tentang antarmuka jaringan. Di sini, opsi -4 menunjukkan bahwa kita hanya ingin melihat informasi terkait IPv4. addr show eth0 berarti kita ingin melihat informasi alamat dari antarmuka eth0.

- grep -oP '(?<=inet\s)\d+(\.\d+){3}': Hasil dari perintah ip -4 addr show eth0 akan diambil dan difilter menggunakan grep. Penjelasan lebih rinci dari ekspresi regular (-oP) yang digunakan di dalam grep:

- `(?<=inet\s)`: Ini adalah positive lookbehind assertion yang berarti kita mencari sesuatu yang diawali dengan "inet" (alamat IP).
\d+: Mencocokkan satu atau lebih digit (0-9).
`(\.\d+){3}`: Ini adalah grup yang mencocokkan tiga blok angka yang dipisahkan oleh tanda titik. Jadi, kita mencari tiga blok digit setelah "inet" untuk membentuk alamat IPv4.

- Hasilnya adalah alamat IP IPv4 yang berhasil diekstrak dari antarmuka eth0. Variabel ETH0_IP kemudian menyimpan nilai alamat IP tersebut untuk digunakan dalam perintah iptables berikutnya. Jadi, garis ini secara efektif mendapatkan alamat IP IPv4 dari antarmuka eth0 dan menyimpannya dalam variabel ETH0_IP.

Seletah itu, test dengan melakukan ping ke google.com

<img width="766" alt="image" src="https://github.com/katarinainezita/Jarkom-Modul-5-A08-2023/assets/105977864/14bdaedb-edd6-41d5-ba92-9ccbca652d53">


### No. 2
Kalian diminta untuk melakukan drop semua TCP dan UDP kecuali port 8080 pada TCP.

#### Solusi
Karena tidak ada aturan spesifik mengenai node mana yang harus menerapkan rules di soal, maka kami memilih GrobeForest sebagai node target dengan menambahkan script berikut ini,
```
#!/bin/bash
iptables -A INPUT -p tcp --dport 8080 -j ACCEPT

iptables -A INPUT -p tcp -j DROP
iptables -A INPUT -p udp -j DROP
```
Lakukan test dengan command berikut pada grobeforest untuk membuka port 8080
```
nc -lnvp 8080
```

pilih 1 client lain untuk mencoba melakukan koneksi tcp pada port 8080 menggunakan netcat dengan command berikut
```
nc <ip grobeforest> 8080
``` 

berikut ini adalah hasil testing untuk port yang diizinkan,

<img width="1107" alt="image" src="https://github.com/katarinainezita/Jarkom-Modul-5-A08-2023/assets/105977864/a27b18f9-814e-49f3-8990-4e350e08bdd7">
  
dan berikut ini adalah hasil testing untuk port yang tidak diizinkan

<img width="1153" alt="image" src="https://github.com/katarinainezita/Jarkom-Modul-5-A08-2023/assets/105977864/7c3ab4a2-5f09-4f37-a05d-3f3a1a61db24">

### No. 3
Kepala Suku North Area meminta kalian untuk membatasi DHCP dan DNS Server hanya dapat dilakukan ping oleh maksimal 3 device secara bersamaan, selebihnya akan di drop.

#### Solusi
Untuk menyelesaikan masalah ini, kita perlu menambahkan script berikut pada DHCP Server, revolte, dan DNS Server, richter, 
```
#!/bin/bash
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP
```

- `-m state --state ESTABLISHED,RELATED`: Menggunakan modul state untuk menentukan keadaan koneksi. Aturan ini mengizinkan paket yang terkait dengan koneksi yang sudah ada (ESTABLISHED) atau terkait dengan koneksi yang diinisiasi oleh sistem (RELATED), seperti koneksi yang terkait dengan protokol seperti FTP.

- Dengan aturan ini, sistem akan mengizinkan paket-paket yang merupakan bagian dari koneksi yang sudah terjalin atau terkait dengan koneksi yang sudah ada.

- `-m connlimit --connlimit-above 3 --connlimit-mask 0`: Menggunakan modul connlimit untuk memberlakukan batasan pada jumlah koneksi. Aturan ini akan menjatuhkan (DROP) paket ICMP jika jumlah koneksi ICMP dari suatu sumber melebihi 3.
	- --connlimit-above 3: Menentukan batas jumlah koneksi di atas 3.
	- --connlimit-mask 0: Menentukan bahwa pembatasan koneksi berlaku untuk semua alamat IP sumber.

- Dengan aturan ini, sistem akan menolak paket ICMP yang datang dari suatu sumber jika jumlah koneksi ICMP dari sumber tersebut melebihi 3

Lakukan testing dengan ping dari 4 sumber yang berbeda pada periode yang sama

<img width="1277" alt="image" src="https://github.com/katarinainezita/Jarkom-Modul-5-A08-2023/assets/105977864/8ac21068-950d-41c1-9e18-ae41592ea88d">

### No. 4
Lakukan pembatasan sehingga koneksi SSH pada Web Server hanya dapat dilakukan oleh masyarakat yang berada pada GrobeForest.

#### Solusi
Untuk menyelesaikan masalah ini, kita perlu menambahkan script berikut ini pada web server, yakni Sein dan Stark.
```
#!/bin/bash
iptables -A INPUT -p tcp --dport 22 -s 10.3.4.0/22 -j ACCEPT
iptables -A INPUT -p tcp --dport 22 -j DROP
```

- command di atas pada dasarnya melakukan drop untuk semua koneksi SSH (tcp pada port 22) dan hanya menerima koneksi 