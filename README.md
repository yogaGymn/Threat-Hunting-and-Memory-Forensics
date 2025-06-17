# 🛡️ Threat Hunting & Memory Forensics - Bear Cyber Hunt

## 📄 Deskripsi Umum

Dokumentasi ini berisi hasil investigasi tim Bear Cyber Hunt dalam mengikuti *ACADefence Challenge 2025*, ajang kompetisi keamanan siber yang diselenggarakan oleh acadCSIRT, bekerja sama dengan Huawei, Universitas Kristen Maranatha, dan Orang Siber. Fokus utama laporan ini adalah melakukan analisis forensik memori dan threat hunting terhadap artefak digital yang disediakan panitia, seperti file pcap, memory dump, dan JSON indikator malware.

---

## 👥 Tim

- **Prayoga Gymnastiar** - prayoga.gymnastiar15@gmail.com  
- **Agus Sudarmanto** - kukukganyong@gmail.com  
- **Syaiful Akbar Rizki Mubarok** - syaifulakbar873@gmail.com  

---

## 📌 Ringkasan Temuan

### 🔍 Tugas I
- Ditemukan pola komunikasi HTTP mencurigakan ke IP eksternal `211.234.117.141:443` dengan struktur URI acak (indikasi C2).
- Komunikasi HTTP plaintext di port HTTPS → obfuscation.
- `sample3` bukan memory dump Windows, melainkan image firmware (ESP32 / ISO9660).
- Artefak menunjukkan penggunaan `rundll32.exe`, `powershell.exe`, `iexplore.exe` → kemungkinan LOLBins abuse.

### 📦 Packet Capture (t12.pcap & t13.pcap)
- Terjadi komunikasi berulang dengan port 443 dan 4444 → indikasi C2 & reverse shell.
- IP mencurigakan dari Korea Selatan.
- Nama domain `smp-rda.samsungdm.com`.

### 💾 File attack2.json
- Malware dikaitkan dengan APT41.
- Kapabilitas: Zero-day exploit, cloud C2, espionage, financial theft.
- Tidak ditemukan korelasi langsung antara attack2.json dan sample3.

### 🛡️ Rekomendasi Mitigasi (Tugas I)
1. Segmentasi jaringan dan firewall ketat.
2. Logging & monitoring PowerShell/rundll32.exe.
3. Patch sistem dan firmware.
4. Deteksi trafik C2 abnormal.
5. Isolasi host dan forensik lanjutan.
6. Integrasi Threat Intelligence.
7. Edukasi pengguna.

---

## 🧪 Tugas II

### 💣 Artefak Infeksi
- Proses mencurigakan: `spools.exe` (masquerading), `cmd.exe` (parent aneh), `ipconfig.exe` (proses tersembunyi).
- Komunikasi HTTP eksternal ke `targetn.com` dan `in-t-e-r-n-e-t.com`.

### 🧬 Teknik Malware
- Code injection ke `explorer.exe`, `winlogon.exe`, dll.
- Downloader berbasis XML (`bootup.exe.xml`).
- Eksfiltrasi data melalui POST HTTP.

### 🔐 Rekomendasi Mitigasi (Tugas II)
1. Isolasi sistem terinfeksi.
2. Reinstall sistem.
3. Audit lalu lintas jaringan.
4. Terapkan *Least Privilege* dan eksekusi terbatas.
5. Edukasi pengguna.
6. Perbarui sistem & gunakan EDR.

---

## 🤖 Penggunaan AI
- AI digunakan untuk mendeteksi pola komunikasi tersembunyi, anomali trafik, dan solusi troubleshooting saat mengalami kendala pada tools seperti Volatility.

---

## 📚 Referensi
Daftar referensi lengkap tersedia di bagian akhir laporan, meliputi literatur digital forensik, keamanan sistem, dan threat intelligence.

---

## 📁 Struktur Berkas
