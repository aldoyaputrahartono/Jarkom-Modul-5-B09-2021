# Jarkom-Modul-5-B09-2021

Repositori Praktikum Jarkom Modul 5

|NRP           |Nama                   |
|:------------:|:---------------------:|
|05111940000084|Aldo Yaputra Hartono   |
|05111940000092|Maximilian H M Lingga  |
|05111840000023|Izzulhaq Fawwaz Syauqiy|

## Topologi
![topologi](https://user-images.githubusercontent.com/31863229/144903369-1fe4329a-3fcf-4a49-b655-fff029c30dd6.PNG)

## Subnetting (VLSM)
**Pembagian Subnet**
![subnetting_01](https://user-images.githubusercontent.com/31863229/145238777-082de610-fe27-4ad5-aa59-a0c9e2414747.png)

**Perhitungan Subnet**
|Subnet|Jumlah IP|Netmask|
|------|---------|-------|
|A1|2|/30|
|A2|2|/30|
|A3|201|/24|
|A4|301|/23|
|A5|101|/25|
|A6|701|/22|
|A7|4|/29|
|A8|4|/29|
|**Total**|**1316**|**/21**|

**VLSM Tree**
![subnetting_02](https://user-images.githubusercontent.com/31863229/145238792-6e1aba9d-b343-4871-9475-44d379183eb0.png)

**Pembagian IP**
|Subnet|Network ID|Netmask|
|------|----------|-------|
|A1|192.181.0.0|255.255.255.252|
|A2|192.181.0.4|255.255.255.252|
|A3|192.181.1.0|255.255.255.0|
|A4|192.181.2.0|255.255.254.0|
|A5|192.181.0.128|255.255.255.128|
|A6|192.181.4.0|255.255.252.0|
|A7|192.181.0.16|255.255.255.248|
|A8|192.181.0.24|255.255.255.248|

## Setting GNS3
**FOOSHA (sebagai Router / DHCP Relay)**
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
        address 192.181.0.1
        netmask 255.255.255.252

auto eth2
iface eth2 inet static
         address 192.181.0.5
         netmask 255.255.255.252
```

**WATER7 (sebagai Router / DHCP Relay)**
```
auto eth0
iface eth0 inet static
        address 192.181.0.2
        netmask 255.255.255.252
        gateway 192.181.0.1

auto eth1
iface eth1 inet static
        address 192.181.0.17
        netmask 255.255.255.248

auto eth2
iface eth2 inet static
         address 192.181.0.129
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
          address 192.181.0.6
          netmask 255.255.255.252
          gateway 192.181.0.5

auto eth1
iface eth1 inet static
          address 192.181.0.25
          netmask 255.255.255.248

auto eth2
iface eth2 inet static
          address 192.181.2.1
          netmask 255.255.254.0

auto eth3
iface eth3 inet static
          address 192.181.1.1
          netmask 255.255.255.0
```

**DORIKI (sebagai DNS Server)**
```
auto eth0
iface eth0 inet static
       address 192.181.0.18
       netmask 255.255.255.248
       gateway 192.181.0.17
```

**JIPANGU (sebagai DHCP Server)**
```
auto eth0
iface eth0 inet static
       address 192.181.0.19
       netmask 255.255.255.248
       gateway 192.181.0.17
```

**JORGE (sebagai Web Server)**
```
auto eth0
iface eth0 inet static
       address 192.181.0.26
       netmask 255.255.255.248
       gateway 192.181.0.25
```

**MAINGATE (sebagai Web Server)**
```
auto eth0
iface eth0 inet static
       address 192.181.0.27
       netmask 255.255.255.248
       gateway 192.181.0.25
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
route add -net 192.181.0.16 netmask 255.255.255.248 gw 192.181.0.2
route add -net 192.181.0.128 netmask 255.255.255.128 gw 192.181.0.2
route add -net 192.181.4.0 netmask 255.255.252.0 gw 192.181.0.2
route add -net 192.181.0.24 netmask 255.255.255.248 gw 192.181.0.6
route add -net 192.181.2.0 netmask 255.255.254.0 gw 192.181.0.6
route add -net 192.181.1.0 netmask 255.255.255.0 gw 192.181.0.6
```

## Setting DHCP Relay
**Pada FOOSHA**
- Install aplikasi isc-dhcp-relay.

  ```
  apt-get install isc-dhcp-relay -y
  ```
- Edit file `/etc/default/isc-dhcp-relay` seperti pada gambar berikut:

  ![relay_01](https://user-images.githubusercontent.com/31863229/145240564-7f993ffc-4c51-4a90-a4df-67f5b434aa40.PNG)
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

  ![relay_02](https://user-images.githubusercontent.com/31863229/145240573-2ad8269a-9304-49eb-b03e-6bd2c9306d84.PNG)
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

  ![relay_03](https://user-images.githubusercontent.com/31863229/145240576-10f85a74-8621-4177-8565-d7fa9c0ebbb8.PNG)
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
- Edit file `/etc/dhcp/dhcpd.conf` untuk menambahkan subnet sebagai berikut:

  ```
  subnet 192.181.0.16 netmask 255.255.255.248 {
  }
  subnet 192.181.0.128 netmask 255.255.255.128 {
      range 192.181.0.130 192.181.0.254;
      option routers 192.181.0.129;
      option broadcast-address 192.181.0.255;
      option domain-name-servers 192.181.0.18;
      default-lease-time 600;
      max-lease-time 7200;
  }
  subnet 192.181.4.0 netmask 255.255.252.0 {
      range 192.181.4.2 192.181.4.254;
      option routers 192.181.4.1;
      option broadcast-address 192.181.4.255;
      option domain-name-servers 192.181.0.18;
      default-lease-time 600;
      max-lease-time 7200;
  }
  subnet 192.181.2.0 netmask 255.255.254.0 {
      range 192.181.2.2 192.181.2.254;
      option routers 192.181.2.1;
      option broadcast-address 192.181.2.255;
      option domain-name-servers 192.181.0.18;
      default-lease-time 600;
      max-lease-time 7200;
  }
  subnet 192.181.1.0 netmask 255.255.255.0 {
      range 192.181.1.2 192.181.1.254;
      option routers 192.181.1.1;
      option broadcast-address 192.181.1.255;
      option domain-name-servers 192.181.0.18;
      default-lease-time 600;
      max-lease-time 7200;
  }
  ```
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
iptables -t nat -A POSTROUTING -s 192.181.0.0/16 -o eth0 -j SNAT --to-source (ip eth0)
```

Catatan: ip eth0 didapatkan dengan menjalankan command `ip a` pada FOOSHA.

**BLUENO**

![01_01](https://user-images.githubusercontent.com/31863229/145242523-d871015c-1baf-4540-bc80-c768d276b2de.PNG)

## Soal 2
Kalian diminta untuk mendrop semua akses HTTP dari luar Topologi kalian pada server yang merupakan DHCP Server dan DNS Server demi menjaga keamanan.

### Jawaban
**FOOSHA**
```
iptables -A FORWARD -p tcp --dport 80 -d 192.181.0.16/29 -i eth0 -j DROP
```

**JIPANGU dan DORIKI**

Install aplikasi netcat: `apt-get install netcat`.

**Testing**
- Pada JIPANGU dan DORIKI ketikkan: `nc -l -p 80`.

  ![02_01](https://user-images.githubusercontent.com/31863229/145243939-918b8b33-4717-4ba3-a976-995584b359a2.PNG)
  ![02_02](https://user-images.githubusercontent.com/31863229/145243948-9146729b-07aa-4b0f-aa41-4ab830b8e31e.PNG)
- Pada FOOSHA ketikkan: `nmap -p 80 192.186.0.18` atau `nmap -p 80 192.186.0.19`.

  ![02_03](https://user-images.githubusercontent.com/31863229/145243954-3ea5d1ba-5771-441d-8788-9bfd1c876d86.PNG)

## Soal 3
Karena kelompok kalian maksimal terdiri dari 3 orang. Luffy meminta kalian untuk membatasi DHCP dan DNS Server hanya boleh menerima maksimal 3 koneksi ICMP secara bersamaan menggunakan iptables, selebihnya didrop.

### Jawaban
**JIPANGU dan DORIKI**
```
iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP
```

**Testing**

Lakukan ping ke JIPANGU atau DORIKI dari 4 client secara bersamaan.

![03_01](https://user-images.githubusercontent.com/31863229/145245126-fb53572c-e9f3-4e4d-982a-821711c2c903.PNG)
![03_02](https://user-images.githubusercontent.com/31863229/145245135-0740d79e-25f5-437a-8e1c-0ee42b396ea1.PNG)
![03_03](https://user-images.githubusercontent.com/31863229/145245136-d897f736-d8a8-4f14-b362-b4404fe69f88.PNG)
![03_04](https://user-images.githubusercontent.com/31863229/145245140-fbd83dcc-2bbf-4fdd-9835-1946cd276f88.PNG)

## Soal 4
Akses dari subnet Blueno dan Cipher hanya diperbolehkan pada pukul 07.00 - 15.00 pada hari Senin sampai Kamis.

### Jawaban
**DORIKI**
```
iptables -A INPUT -s 192.181.0.128/25 -m time --timestart 07:00 --timestop 15:00 --weekdays Mon,Tue,Wed,Thu -j ACCEPT
iptables -A INPUT -s 192.181.0.128/25 -j REJECT
iptables -A INPUT -s 192.181.4.0/22 -m time --timestart 07:00 --timestop 15:00 --weekdays Mon,Tue,Wed,Thu -j ACCEPT
iptables -A INPUT -s 192.181.4.0/22 -j REJECT
```

**Testing**
- Pada BLUENO ubah waktu: `date -s "3 DEC 2021 13:00:00"` dan ping DORIKI.

  ![04_01](https://user-images.githubusercontent.com/31863229/145246447-9e9617c9-28f7-41b7-84f5-8f172c600e7c.PNG)
- Pada CIPHER ubah waktu: `date -s "8 DEC 2021 13:00:00"` dan ping DORIKI.

  ![04_02](https://user-images.githubusercontent.com/31863229/145246453-3c4f25c2-84b8-491a-b869-a5ebf6c8a520.PNG)

## Soal 5
Akses dari subnet Elena dan Fukurou hanya diperbolehkan pada pukul 15.01 hingga pukul 06.59 setiap harinya.

### Jawaban
**DORIKI**
```
iptables -A INPUT -s 192.181.2.0/23 -m time --timestart 07:00 --timestop 15:00 -j REJECT
iptables -A INPUT -s 192.181.1.0/24 -m time --timestart 07:00 --timestop 15:00 -j REJECT
```

**Testing**
- Pada ELENA ubah waktu: `date -s "8 DEC 2021 13:00:00"` dan ping DORIKI.

  ![05_01](https://user-images.githubusercontent.com/31863229/145247020-8efcc71d-faf9-49fb-943b-f94d02458e2d.PNG)
- Pada FUKUROU ubah waktu: `date -s "8 DEC 2021 18:00:00"` dan ping DORIKI.

  ![05_02](https://user-images.githubusercontent.com/31863229/145247028-60a6827c-89a0-48ce-9486-5306b2408077.PNG)

## Soal 6
Karena kita memiliki 2 Web Server, Luffy ingin Guanhao disetting sehingga setiap request dari client yang mengakses DNS Server akan didistribusikan secara bergantian pada Jorge dan Maingate.

### Jawaban
**GUANHAO**
```
iptables -t nat -A PREROUTING -p tcp -d 192.181.0.18 --dport 80 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination 192.181.0.26:80
iptables -t nat -A PREROUTING -p tcp -d 192.181.0.18 --dport 80 -j DNAT --to-destination 192.181.0.27:80
iptables -t nat -A POSTROUTING -p tcp -d 192.181.0.26 --dport 80 -j SNAT --to-source 192.181.0.18:80
iptables -t nat -A POSTROUTING -p tcp -d 192.181.0.27 --dport 80 -j SNAT --to-source 192.181.0.18:80
```

**Testing**
- Pada JORGE, MAINGATE, ELENA, dan FUKUROU install aplikasi netcat: `apt-get install netcat`.
- Pada JORGE dan MAINGATE ketikkan: `nc -l -p 80`.
- Pada ELENA dan FUKUROU ketikkan: `nc 192.181.0.18 80`
- Ketikkan sembarang kata pada ELENA atau FUKUROU, nanti akan muncul pada JORGE atau MAINGATE.

![06_01](https://user-images.githubusercontent.com/31863229/145251030-7798c56b-8c1b-4ea2-bd53-1f3c4c3e66cc.PNG)
![06_03](https://user-images.githubusercontent.com/31863229/145251041-512f9e11-9748-4ce5-8821-8981c6b0cb5c.PNG)
![06_02](https://user-images.githubusercontent.com/31863229/145251038-dce5fc7b-2b45-432a-a622-28b0c7278083.PNG)
![06_04](https://user-images.githubusercontent.com/31863229/145251045-59df53af-0711-4d4c-8614-d5616ee836dd.PNG)

## Kendala
1. Bingung iptables.

## Pembagian Tugas
|Nama                   |Soal       |
|:---------------------:|:---------:|
|Aldo Yaputra Hartono   ||
