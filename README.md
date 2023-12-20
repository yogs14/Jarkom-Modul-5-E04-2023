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
| Subnet | Node | IP | Jumlah IP | Length | Subnet Mask |
| ------ | ---- | --------- | ------ | -- | ----------- |
| A1 | NAT1 - Aura | 192.208.14.128 | 2 | /30 | 255.255.255.252 |
| A2 | Aura - Frieren | 192.208.14.140 | 2 | /30 | 255.255.255.252 |
| A3 | Aura - Heiter | 192.208.14.144 | 2 | /30 | 255.255.255.252 |
| A4 | Heiter - TurkRegion | 192.208.0.0 | 1023 | /21 | 255.255.248.0 |
| A5 | Heite - Sein - GrobeForest | 192.208.8.0 | 514 | /22 | 255.255.252.0 |
| A6 | Frieren - Stark | 192.208.14.148 | 2 | /30 | 255.255.255.252 |
| A7 | Frieren - Himmel | 192.208.14.152 | 2 | /30 | 255.255.255.252 |
| A8 | Himmel - LaubHills | 192.208.12.0 | 256 | /23 | 255.255.254.0 |
| A9 | Himmel - SchwerMountain - Fern | 192.208.14.0 | 66 | /25 | 255.255.255.128 |
| A10 | Fern - Richter | 192.208.14.132 | 2 | /30 | 255.255.255.252 |
| A11 | Fern - Revolte | 192.208.14.136 | 2 | /30 | 255.255.255.252 |

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
1. Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi Aura menggunakan iptables, tetapi tidak ingin menggunakan MASQUERADE.
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

2. Kalian diminta untuk melakukan drop semua TCP dan UDP kecuali port 8080 pada TCP.
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
3. Kepala Suku North Area meminta kalian untuk membatasi DHCP dan DNS Server hanya dapat dilakukan ping oleh maksimal 3 device secara bersamaan, selebihnya akan di drop.
### Solusi
Pada DNS dan DHCP server (Revolte Richter) lakukan konfigurasi iptables sebagai berikut.
```
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP
```
keterangan:

* --connlimit-above 3 maka paket ICMP selanjutnya akan ditolak (DROP) dari alamat sumber tersebut. -
+ --connlimit-mask 0 menunjukkan bahwa pengecekan jumlah koneksi dilakukan berdasarkan alamat IP sumber secara langsung.

4. Lakukan pembatasan sehingga koneksi SSH pada Web Server hanya dapat dilakukan oleh masyarakat yang berada pada GrobeForest.
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

5. Selain itu, akses menuju WebServer hanya diperbolehkan saat jam kerja yaitu Senin-Jumat pada pukul 08.00-16.00.
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
