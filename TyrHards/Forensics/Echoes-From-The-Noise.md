# TryHards - [Echoes From The Noise](https://tryhards.community/challenges#Echoes%20from%20the%20Noise-9)
* **Kategori:** Forensics
* **Difficulty:** Easy


## Challenge Description

> A network capture reveals suspicious HTTP traffic.
> Two files were downloaded — an audio recording and a bitmap image. One hides a password, the other holds the flag. Find both.

Files provided:
* `evidence.zip`

## Reconnaissance

### Tools yang Digunakan:
* **Wireshark** - Untuk melihat traffic jaringan.
* **Audacity** - Untuk menganalisis gelombang audio.
* **Steghide** - Untuk mengekstrak data yang ada di file gambar.

## Analisis & Eksploitasi

1. **Ekstrak file evidence.zip:**
   Saat mengekstrak file `evidence.zip`, kita mendapatkan file `capture.pcap`
   Buka file `capture.pcap` dengan Wireshark

2. **Melihat Traffic jaringan dengan Wireshark (`capture.pcap`):**
   Pada Bagian Fillter kita fillter traffic HTTP:
   Disana kita melihat ada beberapa file, ada file `recording.mav` dan `photo.bmp`.
   Kita Download file tersebut dengan cara:
   -Klik File
   -Eksport Obejct dan pilih HTTP lalu save all.

3. **Mengekstrak data yag ada di `recording.mav`**
   Buka Software `Audacity` dan pilih file `recording.mav` kalian melihatnya biasa biasa saja kan???, Sandinya tersembunyi di track visualization, kita ubah track visualizationnya ke spectrogram dan sandinya sudah kelihatan yaitu:
   
   ```text
   s1390_Lsb_k3y
   ```
   Sandi ini kita gunakan untuk membuka file gambarnya nanti.

4. **Mengekstrak data yang ada di `photo.bmp`**
   Buka Terminal dengan ``Ctrl + alt + T`` di Ubuntu, Sesuaikan dengan sistem operasi yang kalian gunakan.
   kalau belum terinstall `Steghide` install dengan perintah:
   ```bash
   sudo apt install steghide
   ```
   kalau sudah selesai, masuk ke folder dimana kalian menyimpan file `photo.bmp`nya (Contoh: Kalau filenya ada di folder Download, masuk dengan perintah `cd Downloads`. **sesuaikan dengan lokasi folder**.
   lalu jalankan perintah ini untuk mengekstrak data `photo.bmp`nya:
   ```bash
   steghide extract -sf photo.bmp
   ```
   Kalau berhasil flagnya ada di file `_flag.txt` kalian bisa lihat dengan perintah:
   ```bash
   cat _flag.txt
   ```
---
   
**Flagnya adalah:**
TryHards{st3g0_4nd_f0r3ns1cs_comb1n3d}
