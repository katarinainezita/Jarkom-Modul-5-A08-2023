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



  





