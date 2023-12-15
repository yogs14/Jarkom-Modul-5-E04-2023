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
| Subnet | Node | Jumlah IP | Length | IP | Subnet Mask |
| ------ | ---- | --------- | ------ | -- | ----------- |
| A1 | NAT1 - Aura | 192.208.14.128 | 2 | /30 |
| A2 | Aura - Frieren | 192.208.14.140 | 2 | /30 |
| A3 | Aura - Heiter | 192.208.14.144 | 2 | /30 |
| A4 | Heiter - TurkRegion | 192.208.0.0 | 1023 | /21 |
| A5 | Heite - Sein - GrobeForest | 192.208.8.0 | 514 | /22 |
| A6 | Frieren - Stark | 192.208.14.148 | 2 | /30 |
| A7 | Frieren - Himmel | 192.208.14.152 | 2 | /30 |
| A8 | Himmel - LaubHills | 192.208.12.0 | 256 | /23 |
| A9 | Himmel - SchwerMountain - Fern | 192.208.14.0 | 66 | /25 |
| A10 | Fern - Richter | 192.208.14.132 | 2 | /30 |
| A11 | Fern - Revolte | 192.208.14.136 | 2 | /30 |

# Configuration
## Config ETH

### Aura
### Frieren
### Heiter

