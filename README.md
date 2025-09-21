# Simulasi Virtualisasi dan SSH di VirtualBox

Project ini adalah catatan saya dalam mempelajari mata kuliah **Virtualisasi dan Cloud**.  
Fokusnya adalah membangun beberapa Virtual Machine (Ubuntu 20.04.6 & Windows 10), mengatur jaringan, dan melakukan uji konektivitas (ping dan SSH) di VirtualBox.  

---

## Lingkungan
- **Host:** Windows 11, RAM 16 GB
- **Hypervisor:** VirtualBox 7 + Extension Pack
- **Guest OS:** Ubuntu 20.04.6, Windows 10
- **Tools:** ifconfig, ipconfig, ping, ssh, PowerShell

---

## Tahapan Praktikum

### 1. Instalasi VirtualBox & VM
- Instalasi **Python Core** (dependency) & VirtualBox 7.
- Membuat VM **Ubuntu 20.04.6** (RAM 2 GB, Storage 25 GB).
- Membuat VM **Windows 10** sebagai guest tambahan.
- Clone VM Ubuntu untuk backup & recovery.

### 2. Konfigurasi Jaringan
- Awalnya semua VM menggunakan **NAT** → IP sama.
- Mengubah adaptor jaringan ke **Bridge Adapter** agar setiap VM punya IP berbeda.
- Verifikasi IP dengan:
  - `ifconfig` (Ubuntu)
  - `ipconfig` (Windows)

### 3. Uji Konektivitas
- **Tes Ping antar VM**:
  - Windows 10 → Ubuntu
  - Ubuntu → Windows 10
  - Ubuntu Clone → Ubuntu & Windows 10
- **Tes Internet**: membuka YouTube di masing-masing VM → semua sukses.
- **Resize Storage**: menambahkan 1–5 GB pada setiap VM.

### 4. Implementasi SSH
- **VM Windows 10 → VM Ubuntu**
  - Instalasi OpenSSH Server di Ubuntu → sukses login via SSH.
- **Host Windows 11 → VM Ubuntu & Windows 10**
  - Aktivasi SSH di Windows 10 (Optional Features → OpenSSH Server).
  - Remote berhasil via `ssh user@ip-address`.
- **Host PC1 → Host PC2**
  - SSH antar PC menggunakan OpenSSH di PowerShell.
- **Host → VM di host lain**
  - SSH Host PC1 ke VM (Ubuntu/Windows 10) di Host PC2.

---

## Hasil

| Client                 | IP Client       | Server                 | IP Server       | Hasil    |
|-------------------------|-----------------|------------------------|-----------------|----------|
| Windows 10 (VM PC1)     | 192.168.18.230  | Ubuntu (VM PC1)        | 192.168.18.228  | ✔ Berhasil |
| Windows 11 (Host PC1)   | 192.168.18.24   | Ubuntu (VM PC1)        | 192.168.18.228  | ✔ Berhasil |
| Windows 11 (Host PC1)   | 192.168.18.24   | Windows 10 (VM PC1)    | 192.168.18.230  | ✔ Berhasil |
| Windows 11 (Host PC2)   | (Tidak dicek)   | Windows 11 (Host PC1)  | 192.168.18.230  | ✔ Berhasil |
| Windows 11 (Host PC1)   | (Tidak dicek)   | Ubuntu (VM PC2)        | 192.168.216.225 | ✔ Berhasil |
| Windows 11 (Host PC2)   | (Tidak dicek)   | Windows 10 (VM PC1)    | 192.168.216.222 | ✔ Berhasil |

**Ringkasan:**
- Semua skenario uji koneksi (ping & SSH) berhasil.
- VM dapat terhubung dengan host dan antar-host.
- Koneksi antar-host ke VM di host lain juga berhasil.

---

## Dokumentasi
> (Tambahkan screenshot pribadi lo di folder `/images`)

- `vm-ubuntu.png` → Tampilan VM Ubuntu
- `ping-test.png` → Hasil ping antar VM
- `ssh-success.png` → SSH berhasil login

---

## Skill yang Ditunjukkan
- Instalasi VirtualBox & VM (Ubuntu + Windows 10)
- Konfigurasi jaringan VM (NAT → Bridge)
- Uji konektivitas jaringan (ping & internet)
- Implementasi SSH di Ubuntu & Windows
- Manajemen storage VM (resize disk)

---

## Kesimpulan
Melalui project ini saya mempelajari cara membangun infrastruktur virtual sederhana menggunakan VirtualBox.  
Konfigurasi jaringan (Bridge Adapter) memungkinkan komunikasi antar VM & host secara langsung.  
Implementasi SSH memberikan pemahaman tambahan mengenai keamanan komunikasi data pada lingkungan virtual.  

Project ini menjadi dasar penting untuk memahami **virtualisasi, jaringan komputer, dan keamanan komunikasi** dalam konteks cloud computing.
