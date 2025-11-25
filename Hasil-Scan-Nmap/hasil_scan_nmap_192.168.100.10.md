# 🛡️ Laporan Hasil Scanning Nmap — Metasploitable2

## 📌 Informasi Target
IP Address : 192.168.100.10
Hostname : target
Command : nmap -n -Pn -p- -A target -o hasil_scan.txt

![Pic1.png](Image/gambar1.png)
![Pic2.png](Image/gambar2.png)
![Pic3.png](Image/gambar3.png)
![gPic4.png](Image/gambar4.png)
---

# 🔍 Ringkasan Port Terbuka

| Port | Status | Service            | Keterangan |
|------|--------|--------------------|------------|
| 21 | open | ftp — vsftpd 2.3.4 | Anonymous login allowed → rawan pencurian data |
| 22 | open | ssh — OpenSSH 4.7p1 | Versi lama → rentan brute force & exploit |
| 23 | open | telnet             | Tidak terenkripsi → kredensial dapat dicuri |
| 25 | open | smtp — Postfix     | Sertifikat SSL kadaluarsa (MITM risk) |
| 53 | open | dns — ISC BIND 9.4.2 | Rawan DNS Cache Poisoning |
| 80 | open | http — Apache 2.2.8 | Halaman web Metasploitable2 |
| 111 | open | rpcbind            | Digunakan untuk pivoting |
| 139 | open | Samba 3.0.20       | Rentan RCE (CVE-2007–2447) |
| 445 | open | Samba 3.0.20       | Guest login, signing disabled |
| 512 | open | exec (rsh)         | Remote login tanpa password |
| 513 | open | login (rshd)       | Sangat berbahaya |
| 514 | open | shell (rsh)        | Login remote tidak aman |
| 1099 | open | Java RMI           | Rentan remote code execution |
| 1524 | open | bindshell          | Root backdoor shell |
| 2049 | open | NFS                | Akses filesystem rawan |
| 2121 | open | ProFTPD 1.3.1      | Reverse shell exploit tersedia |
| 3306 | open | MySQL 5.0          | Sering tanpa password |
| 3632 | open | distccd v1         | Rentan Remote Command Execution |
| 5432 | open | PostgreSQL 8.3     | Versi lama, brute force risk |
| 5900 | open | VNC                | Tidak terenkripsi |
| 6000 | open | X11                | Bisa membaca input keyboard/mouse |
| 6667 | open | UnrealIRCD         | Backdoor default tersedia |
| 6697 | open | UnrealIRCD SSL     | Eksploit tersedia |
| 7001 | open | Java RMI           | Potensi RCE |
| 8009 | open | AJP13              | LFI atau upload shell |
| 8180 | open | Apache Tomcat 5.5  | Default admin credentials |
| 8787 | open | Ruby DRb           | Potensi RCE |
| 38183 / 38320 / 38820 / 53855 | open | RPC                | Banyak layanan RPC → rawan pivoting |

---

# ⚠️ Kesimpulan Keamanan

Target **192.168.100.10** memiliki **lebih dari 30 port terbuka** dan hampir seluruh servicenya menggunakan **versi lama (tahun 2007–2010)** serta memiliki **eksploit publik**.  
Ini adalah tanda khas **Metasploitable2**, sebuah sistem untuk latihan penetration testing.

---

# 🧨 Kerentanan Paling Kritis

### 🔥 1. Remote Code Execution
- Samba 3.0.20 (CVE-2007–2447)
- distccd
- ProFTPD 1.3.1
- UnrealIRCD backdoor

**Dampak:** Eksekusi perintah sebagai root.

### 🔥 2. Credential Leak / Tanpa Password
- FTP Anonymous
- Telnet
- RSH (rlogin, rshell)

**Dampak:** Penyerang dapat login tanpa otentikasi.

### 🔥 3. Web Exploitation
- Apache 2.2.8
- Tomcat 5.5 (default credentials)

**Dampak:** Upload shell, RCE, takeover webserver.

### 🔥 4. Service Enumeration
- RPC
- NFS
- MySQL / PostgreSQL

**Dampak:** Mempermudah pivoting dan eksploitasi lanjutan.

---

# 📊 Tabel Risiko

| No | Risiko | Layanan Terdampak | Dampak |
|----|--------|-------------------|--------|
| 1 | Remote Code Execution | Samba, ProFTPD, distccd | Full system compromise |
| 2 | Credential Leak | FTP, Telnet, RSH | Password bocor |
| 3 | Web Exploitation | Apache, Tomcat | Upload malicious shell |
| 4 | Enumeration | RPC, NFS, MySQL | Pivoting |
| 5 | Outdated Services | Sebagian besar service | Exploit tersedia publik |

---
Di Buat Oleh : Sertu TTG Marthen Frikaldo Antaribaba
