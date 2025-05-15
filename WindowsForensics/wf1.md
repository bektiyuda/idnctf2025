# 🕵️ Windows Forensic 1 - CTF Write-up

## 📄 Deskripsi

Dalam challenge ini, peserta diberikan sebuah file hasil digital forensic imaging (`Evident.ad1`) dan file log-nya (`Evident.ad1.txt`). Berdasarkan deskripsi soal, hive-nya sudah diambil (dalam hal ini, registry file) namun peserta tetap harus melakukan mounting terhadap image `.ad1` untuk mencari informasi tambahan.

Tujuan dari challenge ini adalah menemukan nama file yang menyimpan credential.

- **Flag:** `IDN_FLAG{password_docs.txt}`  
- **Author:** Aditya Firman Nugroho

---

## 🧰 Tools yang Digunakan

- [FTK Imager](https://www.exterro.com/digital-forensics-software/ftk-imager): Untuk mounting image `.ad1`
- [reglookup](https://www.kali.org/tools/reglookup/): Untuk membaca isi file registry Windows (NTUSER.DAT)
- `grep`: Untuk melakukan filter output

---

## 🧪 Langkah Penyelesaian

### 1. Ekstraksi File

Setelah mengekstrak file `.zip`, diperoleh:
- `Evident.ad1` — file forensic image
- `Evident.ad1.txt` — file log hasil pembuatan image

> ![Deskripsi Challenge](screenshots/Screenshot%202025-05-07%20232937.png)

### 2. Analisis File `.txt`

Isi `Evident.ad1.txt` menunjukkan bahwa file image dibuat menggunakan **FTK Imager**. File ini juga mengandung daftar isi file yang terdapat dalam image `Evident.ad1`. 

Beberapa entri file yang ditemukan:
> ![Isi Evident.ad1.txt](screenshots/Screenshot%202025-05-07%20233900.png)

### 3. Mounting Image `.ad1`

Menggunakan **FTK Imager**:
- Buka menu `File > Image Mounting`
- Masukkan file `Evident.ad1` pada field Image
- Klik **Mount**

> ![Daftar File 1](screenshots/Screenshot%202025-05-07%20234325.png)  

Jika berhasil, maka akan muncul drive baru di sistem yang berisi file-file dari image tersebut.

> ![Daftar File 2](screenshots/Screenshot%202025-05-07%20234623.png)

### 4. Analisis Registry (NTUSER.DAT)

Untuk membaca registry:
```bash
reglookup NTUSER.DAT | grep -i "password"
```
Kami menggunakan tool reglookup karena file NTUSER.DAT sering mengandung data kredensial dan konfigurasi pengguna. Dengan menambahkan filter grep -i "password", berhasil ditemukan file bernama : password_docs.txt

> ![Proses Mounting di FTK Imager](screenshots/Screenshot%202025-05-06%20144230.png)