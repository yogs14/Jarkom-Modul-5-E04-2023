# Jarkom-Modul-5-E04-2023

### Anggota Kelompok:
1. Yoga Firman Syahputra (5025221212)
2. Vidiawan Nabiel Arrasyid (5025221231)


# Klusterisasi Subnet pada Topologi
![A1](https://github.com/yogs14/Jarkom-Modul-5-E04-2023/assets/121499055/029c8c69-40b7-4c46-b45c-365750db9245)
Keterangan:	
- Richter adalah DNS Server
* Revolte adalah DHCP Server
+ Sein dan Stark adalah Web Server
- Jumlah Host pada SchwerMountain adalah 64
* Jumlah Host pada LaubHills adalah 255
+ Jumlah Host pada TurkRegion adalah 1022
- Jumlah Host pada GrobeForest adalah 512

# VLSM (Variable Length Subnet Masking)

| Subnet | Node-node | Jumlah IP | Length | 
|------- | --------- | --------- | ------ |
| A1 | NAT1 - Aura | 2 | /30 |
| A2 | Aura - Frieren | 2 | /30 |
| A3 | Aura - Heiter | 2 | /30 |
| A4 | Heiter - TurkRegion | 1023 | /21 |
| A5 | Heiter - Switch3 - Sein - Switch3 - GrobeForest | 514 | /22 |
| A6 | Frieren - Stark | 2 | /30 |
| A7 | Frieren - Himmel | 2 | /30 |
| A8 | Himmel - LaubHills | 256 | /23 |
| A9 | Himmel - Switch2 - SchwerMountain - Switch2 - Fern | 66 | /25 |
| A10 | Fern - Richter | 2 | /30 |
| A11 | Fern - Switch1 - Revolte | 2 | /30 |
|   Total  |                          | 1873 | /20 |

# Pohon IP
![VLSM Modul 5 drawio](https://github.com/yogs14/Jarkom-Modul-5-E04-2023/assets/121499055/dc5636ad-e704-4dd6-9863-bd8baeae053f)

# Hasil Pembagian IP per Node
| Subnet | Node | IP | Jumlah IP | Length | Subnet Mask | Assignable Range |
| ------ | ---- | --------- | ------ | -- | ----------- | ---------------- |
| A1 | NAT1 - Aura | 192.208.14.128 | 2 | /30 | 255.255.255.252 | 192.208.14.129 - 192.208.14.130 |
| A2 | Aura - Frieren | 192.208.14.140 | 2 | /30 | 255.255.255.252 | 192.208.14.141 - 192.208.14.142 |
| A3 | Aura - Heiter | 192.208.14.144 | 2 | /30 | 255.255.255.252 | 192.208.14.145 - 192.208.14.146 |
| A4 | Heiter - TurkRegion | 192.208.0.0 | 1023 | /21 | 255.255.248.0 | 192.208.0.1 - 192.208.7.254 |
| A5 | Heite - Sein - GrobeForest | 192.208.8.0 | 514 | /22 | 255.255.252.0 | 192.208.8.1 - 192.208.11.254 |
| A6 | Frieren - Stark | 192.208.14.148 | 2 | /30 | 255.255.255.252 | 192.208.14.149 - 192.208.14.150 |
| A7 | Frieren - Himmel | 192.208.14.152 | 2 | /30 | 255.255.255.252 | 192.208.14.153 - 192.208.14.154 |
| A8 | Himmel - LaubHills | 192.208.12.0 | 256 | /23 | 255.255.254.0 | 192.208.12.1 - 192.208.13.254 |
| A9 | Himmel - SchwerMountain - Fern | 192.208.14.0 | 66 | /25 | 255.255.255.128 | 192.208.14.1 - 192.208.14.126 |
| A10 | Fern - Richter | 192.208.14.132 | 2 | /30 | 255.255.255.252 | 192.208.14.133 - 192.208.14.134 |
| A11 | Fern - Revolte | 192.208.14.136 | 2 | /30 | 255.255.255.252 | 192.208.14.133 - 192.208.14.136 |

# Configuration
## Config ETH

### Aura
Karena menggunakan DHCP, pada Aura dibuat fix address dengan memasukkan hwaddress agar ip tidak berubah-ubah.
* ip eth0 192.168.122.1
```
auto eth0
iface eth0 inet dhcp
hwaddress ether 0a:ae:7e:7f:84:4c

auto eth1
iface eth1 inet static
	address 192.208.14.145
	netmask 255.255.255.252

auto eth2
iface eth2 inet static
	address 192.208.14.141
	netmask 255.255.255.252
```
### Frieren
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.208.14.142
netmask 255.255.255.252
gateway 192.208.14.141

auto eth1
iface eth1 inet static
address 192.208.14.153
netmask 255.255.255.252

auto eth2
iface eth2 inet static
address 192.208.14.149
netmask 255.255.255.252
```
### Heiter
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.208.14.146
netmask 255.255.255.252
gateway 192.208.14.145

auto eth1
iface eth1 inet static
address 192.208.0.1
netmask 255.255.255.248

auto eth2
iface eth2 inet static
address 192.208.8.1
netmask 255.255.252.0
```

### Fern
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.208.14.1
netmask 255.255.255.128

auto eth1
iface eth1 inet static
address 192.200.14.133
netmask 255.255.255.252

auto eth2
iface eth2 inet static
address 192.208.14.137
netmask 255.255.255.252
```

### Richter
```
auto eth0
iface eth0 inet static
address 192.208.14.134
netmask 255.255.255.248
gateway 192.208.14.133
```

### Revolte
```
auto eth0
iface eth0 inet static
address 192.208.14.138
netmask 255.255.255.248
gateway 192.208.14.137
```

### Stark
```
auto eth0
iface eth0 inet static
address 192.208.14.150
netmask 255.255.255.252
gateway 192.208.14.149
```

### Sein
```
auto eth0
iface eth0 inet static
address 192.208.8.3
netmask 255.255.252.0
gateway 192.208.8.1
```

## Routing (Static)

### Fern
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.208.14.2
```

### Himmel
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.208.14.153
route add -net 192.208.14.132 netmask 255.255.255.252 gw 192.208.14.1
route add -net 192.208.14.136 netmask 255.255.255.252 gw 192.208.14.1
```

### Frieren
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.208.14.141
route add -net 192.208.14.132 netmask 255.255.255.252 gw 192.208.14.154
route add -net 192.208.14.136 netmask 255.255.255.252 gw 192.208.14.154
route add -net 192.208.14.0 netmask 255.255.255.128 gw 192.208.14.154
route add -net 192.208.12.0 netmask 255.255.254.0 gw 192.208.14.154
```

### Heiter
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.208.14.145
```

### Aura
```
#bawah
route add -net 192.208.14.132 netmask 255.255.255.252 gw 192.208.14.142
route add -net 192.208.14.136 netmask 255.255.255.252 gw 192.208.14.142
route add -net 192.208.14.0 netmask 255.255.255.128 gw 192.208.14.142
route add -net 192.208.12.0 netmask 255.255.254.0 gw 192.208.14.142
route add -net 192.208.14.148 netmask 255.255.255.252 gw 192.208.14.142

#kanan
route add -net 192.208.0.0 netmask 255.255.248.0 gw 192.208.14.146
route add -net 192.208.8.0 netmask 255.255.252.0 gw 192.208.14.146
```


## Config DHCP (Dynamic Host Configuration Protocol)
### 1. Host yang menggunakan DHCP berjumlah 4, maka harus dibuat dulu subnetnya, sehingga network configuration diisi sebagai berikut.
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet dhcp
```
### 2. Kemudian install deps
```
#Revolte
apt-get update
apt-get install isc-dhcp-server -y
```
### 3. Pada Revolte, ubah config interfaces di isc-dhcp-server, tambahkan eth0
```
# /etc/default/isc-dhcp-server
INTERFACES="eth0"
```
### 4. Melakukan konfigurasi pada /etc/dhcp/dhcpd.conf
```
# /etc/dhcp/dhcpd.conf
# A2
subnet 192.208.14.140 netmask 255.255.255.252 {
}

# A3
subnet 192.208.14.144 netmask 255.255.255.252 {
}

# A4
subnet 192.202.0.0 netmask 255.255.248.0 {
    range 192.208.0.3 192.202.7.254;
    option routers 192.208.0.1;
    option broadcast-address 192.208.7.255;
    option domain-name-servers 192.208.14.134;
    default-lease-time 180;
    max-lease-time 5760;
}

# A5
subnet 192.208.8.0 netmask 255.255.252.0 {
    range 192.208.8.3 192.208.11.254;
    option routers 192.208.8.1;
    option broadcast-address 192.208.11.255;
    option domain-name-servers 192.208.14.134;
    default-lease-time 180;
    max-lease-time 5760;
}

# A6
subnet 192.208.14.148 netmask 255.255.255.252 {
}

# A7
subnet 192.208.14.152 netmask 255.255.255.252 {
}

# A8
subnet 192.208.12.0 netmask 255.255.254.0 {
    range 192.208.12.3 192.208.13.254;
    option routers 192.208.12.1;
    option broadcast-address 192.208.13.255;
    option domain-name-servers 192.208.14.134;
    default-lease-time 180;
    max-lease-time 5760;
}

# A9
subnet 192.208.14.0 netmask 255.255.255.128 {
    range 192.208.14.3 192.208.14.126;
    option routers 192.208.14.1;
    option broadcast-address 192.208.14.255;
    option domain-name-servers 192.208.14.134;
    default-lease-time 180;
    max-lease-time 5760;
}

# A10
subnet 192.208.14.132 netmask 255.255.255.252 {
}

# A11
subnet 192.208.14.136 netmask 255.255.255.252 {
}
```

## Config Relay
Relay ditempatkan pada Heiter & Frieren
### 1. Menginstall Relay
```
# Heiter Frieren
apt-get update
apt-get install isc-dhcp-relay -y
```
### 2. Melakukan konfigurasi pada isc-dhcp-relay, memasukkan Revolte(.138) sebagai server.
```
# /etc/default/isc-dhcp-relay
# What servers should the DHCP relay forward requests to?
SERVERS="192.208.14.138"

# On what interfaces should the DHCP relay (dhrelay) serve DHCP requests?
INTERFACES="eth0 eth1 eth2"

# Additional options that are passed to the DHCP relay daemon?
OPTIONS=""
```

## Config DNS (Richter)
```
# /etc/bind/named.conf.options
options {
        directory "/var/cache/bind";

        // If there is a firewall between you and nameservers you want
        // to talk to, you may need to fix the firewall to allow multiple
        // ports to talk.  See http://www.kb.cert.org/vuls/id/800113

        // If your ISP provided one or more IP addresses for stable
        // nameservers, you probably want to use them as forwarders.
        // Uncomment the following block, and insert the addresses replacing
        // the all-0's placeholder.

        forwarders {
                192.168.122.1;
        };

        //========================================================================
        // If BIND logs error messages about the root key being expired,
        // you will need to update your keys.  See https://www.isc.org/bind-keys
        //========================================================================
        //dnssec-validation auto;
        allow-query{any;};

        auth-nxdomain no;    # conform to RFC1035
				listen-on-v6 { any; };
};
```
# Problem Solution
## Soal 1
> Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi Aura menggunakan iptables, tetapi tidak ingin menggunakan MASQUERADE.
### Solusi
```
iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source $ETH0_IP -s 192.208.0.0/20
```
keterangan:
* -t nat menunjukkan bahwa aturan yang dibuat akan berada pada tabel NAT.
+ -A POSTROUTING menunjukkan bahwa aturan yang dibuat akan diletakkan pada chain POSTROUTING.
- -o eth0 menunjukkan bahwa paket yang akan dikenai aturan ini adalah paket yang keluar melalui interface eth0.
* -j SNAT menunjukkan bahwa paket yang dikenai aturan ini akan mengalami perubahan source address.
+ --to-source $ETH0_IP menunjukkan bahwa source address dari paket yang dikenai aturan ini akan diubah menjadi IP address dari interface eth0.
- -s 192.208.0.0/20 menunjukkan bahwa paket yang dikenai aturan ini adalah paket yang berasal dari semua subnet

## Soal 2
> Kalian diminta untuk melakukan drop semua TCP dan UDP kecuali port 8080 pada TCP.
### Solusi
Pada Client konfigurasikan:
```
iptables -A INPUT -p tcp ! --dport 8080 -j DROP
iptables -A INPUT -p tcp --dport 8080 -j ACCEPT
iptables -A INPUT -p udp -j DROP
```
keterangan:
* Paket TCP yang bukan menuju port 8080 akan ditolak.
+ Paket TCP yang menuju port 8080 akan diterima.
- Paket UDP akan ditolak.

### Testing
* Client
  ```
  apt-get update
  apt-get install netcat
  ```
+ Sender
  ```
  # TCP Port 8080
  nc 192.208.8.15 8080

  # TCP Port 8000
  nc 192.208.8.15 8000

  # UDP Port 8080
  nc -u 192.208.8.15 8080
  ```
- Receiver
  ```
  # TCP Port 8080
  nc -l -p 8080

  # TCP Port 8000
  nc -l -p 8000

  # UDP Port 8080
  nc -u -l -p 8080
  ```
## Soal 3
> Kepala Suku North Area meminta kalian untuk membatasi DHCP dan DNS Server hanya dapat dilakukan ping oleh maksimal 3 device secara bersamaan, selebihnya akan di drop.
### Solusi
Pada DNS dan DHCP server (Revolte Richter) lakukan konfigurasi iptables sebagai berikut.
```
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP
```
keterangan:

* --connlimit-above 3 maka paket ICMP selanjutnya akan ditolak (DROP) dari alamat sumber tersebut. -
+ --connlimit-mask 0 menunjukkan bahwa pengecekan jumlah koneksi dilakukan berdasarkan alamat IP sumber secara langsung.

## Soal 4
> Lakukan pembatasan sehingga koneksi SSH pada Web Server hanya dapat dilakukan oleh masyarakat yang berada pada GrobeForest.
### Solusi
Pada Web Server (Sein dan Stark) lakukan konfigurasi berikut.
```
iptables -A INPUT -p tcp --dport 22 -s 192.208.8.4/22 -j ACCEPT
iptables -A INPUT -p tcp --dport 22 -j DROP
```
keterangan:

* iptables -A INPUT -p tcp --dport 22 -s 192.208.8.4/22 -j ACCEPT menunjukkan bahwa paket TCP yang menuju port 22 akan diterima jika berasal dari subnet 192.208.8.4/22 (IP GrobeForest).
+ iptables -A INPUT -p tcp --dport 22 -j DROP menunjukkan bahwa paket TCP yang menuju port 22 akan ditolak.

### Testing
```
nmap 192.208.14.150 22
```
```
nc -l -p 22

nc 192.208.14.150 22
nc 192.208.8.2 22
```

## Soal 5
> Selain itu, akses menuju WebServer hanya diperbolehkan saat jam kerja yaitu Senin-Jumat pada pukul 08.00-16.00.
### Solusi
```
iptables -A INPUT -p tcp --dport 22 -m time --weekdays Mon,Tue,Wed,Thu,Fri --timestart 08:00 --timestop 16:00 -s -j ACCEPT
iptables -A INPUT -j DROP
```
keterangan:

* iptables -A INPUT -p tcp --dport 22 -m time --weekdays Mon,Tue,Wed,Thu,Fri --timestart 08:00 --timestop 16:00 -s -j ACCEPT menunjukkan bahwa paket TCP yang menuju port 22 akan diterima dalam jangka waktu Senin-Jumat pada pukul 08.00-16.00.
+ iptables -A INPUT -j DROP menunjukkan bahwa paket TCP yang menuju port 22 selain waktu sebelumnya akan ditolak.

### Testing
* Rubah Date pada node untuk hak akses
  ```
  # Monday, 18 December 2023 09:00
  date 121809002023

  # Monday, 18 December 2023 17:00
  date 121817002023

  # Sunday, 17 December 2023 09:00
  date 121709002023
  ```
+ Lakukan nmap
  ```
  nmap 192.202.1.118 22
  ```

## Soal 6
> Lalu, karena ternyata terdapat beberapa waktu di mana network administrator dari WebServer tidak bisa stand by, sehingga perlu ditambahkan rule bahwa akses pada hari Senin - Kamis pada jam 12.00 - 13.00 dilarang (istirahat maksi cuy) dan akses di hari Jumat pada jam 11.00 - 13.00 juga dilarang (maklum, Jumatan rek).
### Solusi
Pada Web Server (Sein dan Stark) tambahkan konfigurasi berikut.
```
iptables -A INPUT -p tcp --dport 22 -m time --weekdays Mon,Tue,Wed,Thu --timestart 12:00 --timestop 13:00 -j DROP
iptables -A INPUT -p tcp --dport 22 -m time --weekdays Fri --timestart 11:00 --timestop 13:00 -j DROP
```
keterangan:

* iptables -A INPUT -p tcp --dport 22 -m time --weekdays Mon,Tue,Wed,Thu --timestart 12:00 --timestop 13:00 -j DROP menunjukkan bahwa paket TCP yang menuju port 22 akan ditolak dalam jangka waktu Senin-Kamis pada pukul 12.00-13.00.
+ iptables -A INPUT -p tcp --dport 22 -m time --weekdays Fri --timestart 11:00 --timestop 13:00 -j DROP menunjukkan bahwa paket TCP yang menuju port 22 akan ditolak dalam jangka waktu Jumat pada pukul 11.00-13.00.

### Testing 
* Rubah Date pada node untuk hak akses
  ```
  # Monday, 18 December 2023 09:00
  date 121809002023

  # Monday, 18 December 2023 12:30
  date 121812302023

  # Friday, 22 December 2023 09:00
  date 122209002023

  # Friday, 22 December 2023 12:00
  date 122212002023
  ```
+ Lakukan nmap
  ```
  nmap 192.208.14.150 22
  ```

## Soal 7
> Karena terdapat 2 WebServer, kalian diminta agar setiap client yang mengakses Sein dengan Port 80 akan didistribusikan secara bergantian pada Sein dan Stark secara berurutan dan request dari client yang mengakses Stark dengan port 443 akan didistribusikan secara bergantian pada Sein dan Stark secara berurutan.
### Solusi
Initialisasi Web Server
```
apt-get install -y apache2

echo "dari [nama node]" > /var/www/html/index.html

# Konfigurasi virtual host di Apache
echo "
<VirtualHost *:80>
    ServerName 192.208.[ip node]
    DocumentRoot /var/www/html
    ErrorLog \${APACHE_LOG_DIR}/error.log
    CustomLog \${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
<VirtualHost *:443>
    ServerName 192.208.[ip node]
    DocumentRoot /var/www/html
    ErrorLog \${APACHE_LOG_DIR}/error.log
    CustomLog \${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
" > /etc/apache2/sites-available/192.208.8.2.conf

echo '
Listen 80
Listen 443

<IfModule ssl_module>
        Listen 443
</IfModule>

<IfModule mod_gnutls.c>
        Listen 443
</IfModule>
' > /etc/apache2/ports.conf

a2ensite 192.208.8.2.conf
service restart apache2
```
Tambahkan konfigurasi ini pada Router
```
iptables -A PREROUTING -t nat -p tcp -d 192.208.8.2 --dport 80 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination 192.208.8.2:80
iptables -A PREROUTING -t nat -p tcp -d 192.208.8.2 --dport 80 -j DNAT --to-destination 192.208.14.150:80

iptables -A PREROUTING -t nat -p tcp -d 192.208.14.150 --dport 443 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination 192.208.14.150:443
iptables -A PREROUTING -t nat -p tcp -d 192.208.14.150 --dport 443 -j DNAT --to-destination 192.208.8.2:443
```
keterangan:

* Aturan pertama: Setiap paket yang masuk ke alamat IP 192.208.8.2 dengan port 80 akan diarahkan ke alamat IP 192.208.8.2:80 secara bergantian setiap kedua paket. Ini akan membagi beban antara Sein (192.208.8.2:80) dan Stark (192.208.14.150:80).
+ Aturan kedua: Semua paket yang masih tiba di 192.208.8.2:80 akan dialihkan ke 192.208.14.150:80. Ini menjamin bahwa ada distribusi antara kedua server tersebut.
- Aturan ketiga: Setiap paket yang masuk ke alamat IP 192.208.14.150 dengan port 443 akan diarahkan ke alamat IP 192.208.14.150:443 secara bergantian setiap kedua paket. Ini akan membagi beban antara Sein (192.202.14.150:443) dan Stark (192.208.8.2:443).
* Aturan keempat: Semua paket yang masih tiba di 192.208.14.150:443 akan dialihkan ke 192.208.8.2:443. Ini juga menjamin distribusi beban antara kedua server.

### Testing
Lakukan curl untuk mendapatkan hasil dari setiap webserver
```
curl 192.208.8.2:80
curl 192.208.8.2:80

curl 192.208.14.150:443
curl 192.208.14.150:443
```

## Soal 8
> Karena berbeda koalisi politik, maka subnet dengan masyarakat yang berada pada Revolte dilarang keras mengakses WebServer hingga masa pencoblosan pemilu kepala suku 2024 berakhir. Masa pemilu (hingga pemungutan dan penghitungan suara selesai) kepala suku bersamaan dengan masa pemilu Presiden dan Wakil Presiden Indonesia 2024
### Solusi 
Pada Web Server (Sein dan Stark) lakukan konfigurasi berikut.
```
iptables -A INPUT -p tcp -s 192.208.14.138/30 --dport 80 -m time --datestart 2023-10-19 --datestop 2024-02-15 -j DROP
```
keterangan:

* iptables -A INPUT -p tcp -s 192.208.14.138/30 --dport 80 -m time --datestart 2023-10-19 --datestop 2024-02-15 -j DROP menunjukkan bahwa paket TCP yang menuju port 80 akan ditolak jika diakses pada waktu 2023-10-19 hingga 2024-02-15.

## Soal 9
> Sadar akan adanya potensial saling serang antar kubu politik, maka WebServer harus dapat secara otomatis memblokir alamat IP yang melakukan scanning port dalam jumlah banyak (maksimal 20 scan port) di dalam selang waktu 10 menit. (clue: test dengan nmap)
### Solusi
Pada Web Server (Sein dan Stark) lakukan konfigurasi berikut.
```
iptables -N portscan

iptables -A INPUT -m recent --name portscan --update --seconds 600 --hitcount 20 -j DROP
iptables -A FORWARD -m recent --name portscan --update --seconds 600 --hitcount 20 -j DROP

iptables -A INPUT -m recent --name portscan --set -j ACCEPT
iptables -A FORWARD -m recent --name portscan --set -j ACCEPT
```
keterangan:

* iptables -N portscan menunjukkan bahwa akan dibuat chain baru bernama portscan.
+ iptables -A INPUT -m recent --name portscan --update --seconds 600 --hitcount 20 -j DROP menunjukkan bahwa paket yang masuk akan ditolak jika alamat IP sumber sudah melakukan scanning port dalam jumlah 20 kali dalam waktu 10 menit.
- iptables -A FORWARD -m recent --name portscan --update --seconds 600 --hitcount 20 -j DROP menunjukkan bahwa paket yang akan diteruskan ke node lain akan ditolak jika alamat IP sumber sudah melakukan scanning port dalam jumlah 20 kali dalam waktu 10 menit.
* iptables -A INPUT -m recent --name portscan --set -j ACCEPT menunjukkan bahwa paket yang masuk akan diterima jika alamat IP sumber belum melakukan scanning port dalam jumlah 20 kali dalam waktu 10 menit.
+ iptables -A FORWARD -m recent --name portscan --set -j ACCEPT menunjukkan bahwa paket yang akan diteruskan ke node lain akan diterima jika alamat IP sumber belum melakukan scanning port dalam jumlah 20 kali dalam waktu 10 menit.

### Testing
Pada node Client (GrobeForest) lakukan ping sebanyak 30 paket ke webserver.
```
ping 192.208.8.13 -c 30
```

## Soal 10
> Karena kepala suku ingin tau paket apa saja yang di-drop, maka di setiap node server dan router ditambahkan logging paket yang di-drop dengan standard syslog level.
### Solusi
```
iptables -N LOGGING
iptables -A INPUT -j LOGGING
iptables -A LOGGING -j LOG --log-prefix "DROP: "
iptables -A LOGGING -j REJECT

echo'
kern.warning /var/log/iptables.log
' >> /etc/rsyslog.conf

/etc/init.d/rsyslog restart
```
keterangan:

* iptables -N LOGGING menunjukkan bahwa akan dibuat chain baru bernama LOGGING.
+ iptables -A INPUT -j LOGGING menunjukkan bahwa paket yang masuk akan diteruskan ke chain LOGGING.
- iptables -A LOGGING -j LOG --log-prefix "DROP: " menunjukkan bahwa paket yang masuk akan dicatat pada log dengan prefix DROP.
kern.warning /var/log/iptables.log menunjukkan bahwa log dengan level warning akan dicatat pada file /var/log/iptables.log.
/etc/init.d/rsyslog restart restart kembali rsyslog.

# Kendala Pengerjaan
* File konfigurasi sempat hilang disaat _progress_ sudah sekitar 60% sehingga harus mengulang dari awal yang menyebabkan waktu terkuras sangat banyak
+  Kurangnya pemahaman pada web server sebelumnya membuat pemecahannya memakan waktu lama
- _Syntax-syntax_ konfigurasi yang tidak tersedia secara langsung di modul dan check re-check syntax di internet cukup membuat repot
* Saat konfigurasi eth ternyata terdapat ip yang tidak sesuai yang sebelumnya tak terdeteksi sehingga membuat peroutingan tidak bekerja
