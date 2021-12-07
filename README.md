# Jarkom-Modul-5-B09-2021

Repositori Praktikum Jarkom Modul 5

|NRP           |Nama                   |
|:------------:|:---------------------:|
|05111940000084|Aldo Yaputra Hartono   |
|05111940000092|Maximilian H M Lingga  |
|05111840000023|Izzulhaq Fawwaz Syauqiy|

## Topologi
![topologi](https://user-images.githubusercontent.com/31863229/144903369-1fe4329a-3fcf-4a49-b655-fff029c30dd6.PNG)

## Subnetting (CIDR)
**Langkah 1**
![subnetting_01](https://user-images.githubusercontent.com/31863229/144903254-3af2f1e8-08b5-4fb6-b83c-bcf9e8d139ef.png)

**Langkah 2**
![subnetting_02](https://user-images.githubusercontent.com/31863229/144903297-f4268c43-8089-4d77-9f0d-735ba4c19678.png)

**Langkah 3**
![subnetting_03](https://user-images.githubusercontent.com/31863229/144903316-ceb0378e-db57-4339-b979-9ffac0af660c.png)

**Langkah 4**
![subnetting_04](https://user-images.githubusercontent.com/31863229/144903322-7ed6a7c0-a29c-4c65-80ab-ecc521718c1c.png)

**Langkah 5**
![subnetting_05](https://user-images.githubusercontent.com/31863229/144903336-5ac08b4c-b1d9-46de-b957-4ebd6e8d197f.png)

**Hasil subnetting**
![subnetting_06](https://user-images.githubusercontent.com/31863229/144903344-2e9f3397-994c-49b6-ac5a-278e943d1d6c.png)

**CIDR Tree**
![subnetting_07](https://user-images.githubusercontent.com/31863229/144903365-eb8d880b-90bd-49ee-8c64-dac5e445bf93.png)

## Setting GNS3
**FOOSHA (sebagai Router / DHCP Relay)**
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 192.181.8.1
	netmask 255.255.255.252

auto eth2
iface eth2 inet static
	address 192.181.20.1
	netmask 255.255.255.252
```

**WATER7 (sebagai Router / DHCP Relay)**
```
auto eth0
iface eth0 inet static
	address 192.181.8.2
	netmask 255.255.255.252
	gateway 192.181.8.1

auto eth1
iface eth1 inet static
	address 10.151.79.105
	netmask 255.255.255.248

auto eth2
iface eth2 inet static
	address 192.181.0.1
	netmask 255.255.255.128

auto eth3
iface eth3 inet static
	address 192.181.4.1
	netmask 255.255.252.0
```

**GUANHAO (sebagai Router / DHCP Relay)**
```
auto eth0
iface eth0 inet static
	address 192.181.20.2
	netmask 255.255.255.252
	gateway 192.181.20.1

auto eth1
iface eth1 inet static
	address 192.181.17.1
	netmask 255.255.255.248

auto eth2
iface eth2 inet static
	address 192.181.18.1
	netmask 255.255.254.0

auto eth3
iface eth3 inet static
	address 192.181.16.1
	netmask 255.255.255.0
```

**DORIKI (sebagai DNS Server)**
```
auto eth0
iface eth0 inet static
	address 10.151.79.106
	netmask 255.255.255.248
	gateway 10.151.79.105
```

**JIPANGU (sebagai DHCP Server)**
```
auto eth0
iface eth0 inet static
	address 10.151.79.107
	netmask 255.255.255.248
	gateway 10.151.79.105
```

**JORGE (sebagai Web Server)**
```
auto eth0
iface eth0 inet dhcp
```

**MAINGATE (sebagai Web Server)**
```
auto eth0
iface eth0 inet dhcp
```

**BLUENO (sebagai Client)**
```
auto eth0
iface eth0 inet dhcp
```

**CIPHER (sebagai Client)**
```
auto eth0
iface eth0 inet dhcp
```

**ELENA (sebagai Client)**
```
auto eth0
iface eth0 inet dhcp
```

**FUKUROU (sebagai Client)**
```
auto eth0
iface eth0 inet dhcp
```

## Routing
**FOOSHA**
```
route add -net 10.151.79.104 netmask 255.255.255.248 gw 192.181.8.2
route add -net 192.181.0.0 netmask 255.255.240.0 gw 192.181.8.2
route add -net 192.181.16.0 netmask 255.255.248.0 gw 192.181.20.2
```

## Setting DHCP Relay
**Pada FOOSHA**
- Install aplikasi isc-dhcp-relay.

  ```
  apt-get install isc-dhcp-relay -y
  ```
- Edit file `/etc/default/isc-dhcp-relay` seperti pada gambar berikut:

  ![relay_01](https://user-images.githubusercontent.com/31863229/145034296-8deb82f8-7698-4ef4-956a-97ec8adb930e.PNG)
- Restart isc-dhcp-relay.

  ```
  service isc-dhcp-relay restart
  ```

**Pada WATER7**
- Install aplikasi isc-dhcp-relay.

  ```
  apt-get install isc-dhcp-relay -y
  ```
- Edit file `/etc/default/isc-dhcp-relay` seperti pada gambar berikut:

  ![relay_02](https://user-images.githubusercontent.com/31863229/145034303-0dc3f133-ac63-4fa6-ab7a-b1c4b260ce00.PNG)
- Restart isc-dhcp-relay.

  ```
  service isc-dhcp-relay restart
  ```

**Pada GUANHAO**
- Install aplikasi isc-dhcp-relay.

  ```
  apt-get install isc-dhcp-relay -y
  ```
- Edit file `/etc/default/isc-dhcp-relay` seperti pada gambar berikut:

  ![relay_03](https://user-images.githubusercontent.com/31863229/145034313-b5c2d391-32aa-4597-9b2a-fe595651b133.PNG)
- Restart isc-dhcp-relay.

  ```
  service isc-dhcp-relay restart
  ```

## Setting DHCP Server
**Pada JIPANGU**
- Install aplikasi isc-dhcp-server.

  ```
  apt-get install isc-dhcp-server -y
  ```
- Edit file `/etc/default/isc-dhcp-server` seperti pada gambar berikut:

  ![dhcp_server_01](https://user-images.githubusercontent.com/31863229/145035123-6f90a17b-541a-4bac-bc93-cd7dedfe3d0a.PNG)
- Edit file `/etc/dhcp/dhcpd.conf` seperti pada gambar berikut:

  ![dhcp_server_02](https://user-images.githubusercontent.com/31863229/145035129-009a4c73-0300-4209-b76b-ac25a07ba039.PNG)
  ![dhcp_server_03](https://user-images.githubusercontent.com/31863229/145035131-28f9faae-9c49-45ae-95ce-d4e580bdc57c.PNG)
  ![dhcp_server_04](https://user-images.githubusercontent.com/31863229/145035132-f555225a-92c4-4741-b2b9-f4e062cb049f.PNG)
  ![dhcp_server_05](https://user-images.githubusercontent.com/31863229/145035134-184949a5-1ffb-4636-9975-c36935272e7f.PNG)
  ![dhcp_server_06](https://user-images.githubusercontent.com/31863229/145035139-1cb78583-8dc3-4046-9571-4f5b66eb9788.PNG)
- Restart isc-dhcp-server.

  ```
  service isc-dhcp-server restart
  ```

## Setting DNS Server
**Pada DORIKI**
- Install aplikasi bind9.

  ```
  apt-get install bind9 -y
  ```
- Edit file `/etc/bind/named.conf.options` seperti pada gambar berikut:

  ![dns_server_01](https://user-images.githubusercontent.com/31863229/145035515-a86870da-9438-4c07-9803-43b147823464.PNG)
- Restart bind9.

  ```
  service bind9 restart
  ```

## Soal 1
Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi Foosha menggunakan iptables, tetapi Luffy tidak ingin menggunakan MASQUERADE.

### Jawaban
**FOOSHA**
```
iptables -t nat -A POSTROUTING -s 192.181.0.0/16 -o eth0 -j SNAT --to-source 10.151.79.106
```

## Soal 2
Kalian diminta untuk mendrop semua akses HTTP dari luar Topologi kalian pada server yang merupakan DHCP Server dan DNS Server demi menjaga keamanan.

### Jawaban
**FOOSHA**
```
iptables -A FORWARD -p tcp --dport 80 -d 10.151.79.104/29 -i eth0 -j DROP
```

## Soal 3
Karena kelompok kalian maksimal terdiri dari 3 orang. Luffy meminta kalian untuk membatasi DHCP dan DNS Server hanya boleh menerima maksimal 3 koneksi ICMP secara bersamaan menggunakan iptables, selebihnya didrop.

### Jawaban
**JIPANGU**
```
iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP
```

**DORIKI**
```
iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP
```

## Soal 4
Akses dari subnet Blueno dan Cipher hanya diperbolehkan pada pukul 07.00 - 15.00 pada hari Senin sampai Kamis.

### Jawaban
**DORIKI**
```
iptables -A INPUT -s 192.181.0.0/25 -m time --timestart 07:00 --timestop 15:00 --weekdays Mon,Tue,Wed,Thu -j ACCEPT
iptables -A INPUT -s 192.181.4.0/22 -m time --timestart 07:00 --timestop 15:00 --weekdays Mon,Tue,Wed,Thu -j ACCEPT
iptables -A INPUT -s 192.181.0.0/25 -j REJECT
iptables -A INPUT -s 192.181.4.0/22 -j REJECT
```

## Soal 5
Akses dari subnet Elena dan Fukuro hanya diperbolehkan pada pukul 15.01 hingga pukul 06.59 setiap harinya.

### Jawaban
**DORIKI**
```
iptables -A INPUT -s 192.168.18.0/23 -m time --timestart 07:00 --timestop 15:00 -j REJECT
iptables -A INPUT -s 192.168.16.0/24 -m time --timestart 07:00 --timestop 15:00 -j REJECT
```

## Soal 6
Karena kita memiliki 2 Web Server, Luffy ingin Guanhao disetting sehingga setiap request dari client yang mengakses DNS Server akan didistribusikan secara bergantian pada Jorge dan Maingate.

### Jawaban
**FOOSHA**
```
iptables -A PREROUTING -t nat -p tcp -d 10.151.79.106 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination 192.181.17.2:80
iptables -A PREROUTING -t nat -p tcp -d 10.151.79.106 -j DNAT --to-destination 192.181.17.3:80
```

## Kendala


## Pembagian Tugas
|Nama                   |Soal       |
|:---------------------:|:---------:|
|Aldo Yaputra Hartono   ||
|||
|||
