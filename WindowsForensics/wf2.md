# 🕵️ Windows Forensic 2 - CTF Write-up

## 📄 Deskripsi

Masih melanjutkan challenge sebelumnya, kali ini kita diminta mencari tahu **kapan file yang menyimpan credential dibuka**. Kita tetap bekerja dengan file registry `NTUSER.DAT` dari image forensic yang sudah dimount sebelumnya.

- **Pertanyaan:** File yang menyimpan credential, dibuka pada tanggal berapa?
- **Flag:** `IDN_FLAG{2025-05-03 07:16:29}`
- **Author:** Aditya Firman Nugroho

---

## 🧰 Tools yang Digunakan

- [reglookup](https://www.kali.org/tools/reglookup/): Untuk membaca isi registry Windows
- `less`: Untuk navigasi dan pencarian pada output `reglookup`

---

## 🧪 Langkah Penyelesaian

### 1. Jalankan Perintah `reglookup`

Gunakan perintah berikut untuk membaca seluruh isi file registry:

```bash
reglookup NTUSER.DAT | less
```
### 2. Cari Entri Terkait

Setelah berada dalam tampilan less, gunakan fitur pencarian dengan mengetik /password_docs.txt. Ini akan langsung menyorot entri yang berkaitan dengan file tersebut.

> ![Output](screenshots/Screenshot%202025-05-06%20144529.png)

Timestamp kapan file password_docs.txt diakses akan muncul di baris sebelumnya atau di entri yang sama, tergantung struktur registry.
