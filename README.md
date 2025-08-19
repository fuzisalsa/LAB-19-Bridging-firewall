# LAB-19-Bridging-firewall
tanggal 16 Agustus 

![p](LLLLLLLLLLLLLLLLLLLLL.PNG)

# Langkah Konfigurasi Bridging Firewall di Mikrotik via terminal 

1. Buat DHCP Client ke interface yang terhubung ke internet untuk akses internet
   IP > DHCP CLIENT.

      

1. Buat Bridge untuk Admin

```bash
/interface bridge add name=bridge1
/interface bridge port add bridge=bridge1 interface=eth2
/interface bridge port add bridge=bridge1 interface=eth3
```

2. Buat Bridge untuk Client

```bash
/interface bridge add name=bridge10
/interface bridge port add bridge=bridge10 interface=eth4
/interface bridge port add bridge=bridge10 interface=eth5
```

3. Konfigurasi IP Address 

```bash
/ip address add address=192.168.10.1/24 interface=bridge1
/ip address add address=10.16.10.1/24 interface=bridge10
```
5. Buat DHCP server untuk setiap bridge interface, IP > DHCP SERVER > DHCP SETUP.
4. Tambahkan Firewall Filter untuk Membatasi Hak Akses Client, IP > FIREWALL > FILTER RULES > ADD.
   
**Blokir Client Akses ke Mikrotik**

```bash
/ip firewall filter add chain=input in-interface=bridge10 action=drop comment="Block access to Mikrotik from client"
```

**Izinkan Internet untuk Client**

```bash
/ip firewall filter add chain=forward in-interface=bridge10 out-interface=eth1 action=accept comment="Allow internet for client"
```

5. Cek Hasil
   interface clinet
   interface admin
  
# Kesimpulan

Bridging firewall di Mikrotik mengatur dua fungsi sekaligus yang dimana menggabungkan
interface ke dalam satu segment jaringan, dan membatasi 
hak akses masing-masing segment menggunakan firewall.
