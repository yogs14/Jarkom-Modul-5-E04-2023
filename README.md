# Jarkom-Modul-5-E04-2023

### Anggota Kelompok:
1. Yoga Firman Syahputra (5025221212)
2. Vidiawan Nabiel Rasyid (5025221231)


# Klusterisasi Subnet
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
|   Total  |                          | 1873 | /21 |

# Pohon IP

