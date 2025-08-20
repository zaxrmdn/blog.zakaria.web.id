---
title: "Berinteraksi dengan Bash di linux "
date: 2025-05-25
excerpt_separator: "<!--more-->"
categories:
  - Bahasa Indonesia
  - Linux
  - Sysadmin
  - Learn Linux
tags:
  - Learn Linux 3
  - CLI
---

> Blog sebelumnya [Learn Linux 2](
https://blog.zakaria.web.id/bahasa%20indonesia/linux/sysadmin/learn%20linux/command-line-interface/)



# Apa itu Bash

Administrasi Linux lewat command line menggunakan shell. Shell default di Linux adalah Bash, yang punya aturan penulisan perintah (sintaks) berupa:

- `Command` (perintah)

- `Option` (modifier/perintah tambahan)

- `Argument` (nilai/target perintah)

Bash punya fitur seperti tab completion (melengkapi perintah otomatis), history (riwayat perintah), serta mendukung privilege escalation (meningkatkan hak akses, misalnya dengan sudo).

Di hampir semua sistem Linux juga tersedia perintah umum, direktori standar, dan aplikasi seperti editor teks Vim dan Nano.
Dengan memahami Bash dan sintaksnya, administrasi Linux akan jadi jauh lebih mudah.

### Command shell
CLI disediakan oleh software yang disebut shell. Shell menerima input dari pengguna, memproses sintaks perintah, lalu menampilkan output kembali.

Di Linux, shell default pada sebagian besar distro adalah Bash, dan inilah yang biasanya digunakan sysadmin.
Shell lain yang juga populer di Linux:

- `ksh` (KornShell) → banyak dipakai di server Unix.

- `zsh` (Z Shell) → mendukung scripting yang kuat.

- `fish` (Friendly Interactive Shell) → lebih ramah pengguna, bahkan punya konfigurasi berbasis web.

Sebagai perbandingan:

- Windows Server juga punya shell: cmd.exe (mirip DOS lama) dan PowerShell.

- macOS saat ini menggunakan zsh sebagai shell default.

### Karakteristik Bash
Di Bash, perintah harus ditulis dengan struktur tertentu yang disebut sintaks. Setiap bagian sintaks punya nama:

- `Command`: Instruksi utama yang diberikan ke sistem.

- `Subcommand` : Instruksi tambahan yang lebih detail, - mendukung command utama.

- `Option` : Modifikasi perintah, mengubah cara perintah dijalankan (biasanya diawali dengan - atau --).

- `Argument` : Objek yang dikenai perintah. Misalnya, jika perintah untuk menghapus file, maka nama file adalah argument.

Ada dua bentuk dasar sintaks:

### `Normal command` → hanya `command` + `option` + `argument`.
Contoh:

| Command         | Penggunaan      |
| :-------------: | ------------- |
| ls              | List isi folder  |
| ls -la          | List semua (-a) isi dan dalam format panjang |
|ls /var/log      | List isi dari folder /var/log                   |
|ls -la /var/log | List semua isi dari folder /var/log dalam format panjang |



### `Command-subcommand` → `command` + `subcommand` + `option` + `argument`.
Contoh: 

| Command and Sub-Command  | Penggunaan |
| :------------: | ---------- |
|ip addr         | Menampilkan alamat ip di semua interface |
| ip addr show eth0 | Hanya menamplikan alamat ip di interface eth0 |
|ip help | Menampilkan bantuan umum perintah ip |
|ip link help | Menampilkan bantuan ip link sub command|


### Tab Completion di Bash

Bash mendukung tab completion. Caranya, ketik sebagian perintah atau nama file yang cukup unik, lalu tekan tombol Tab. Bash akan otomatis melengkapi perintah atau nama file/direktori.
👉 Manfaat: lebih cepat, mengurangi salah ketik.

### Command History di Bash

Bash juga menyimpan riwayat perintah di history file. Riwayat ini bisa dipanggil kembali untuk dijalankan ulang atau diedit.

Cara paling mudah:

Tekan ↑ (Up Arrow) → memanggil perintah terakhir.

Tekan ↓ (Down Arrow) → maju/mundur dalam daftar perintah yang pernah dipakai.

Tekan Enter setelah perintah yang diinginkan muncul.

### Tips & Trik Menggunakan Shell (Bash)

`Tab completion` → Biasakan pakai tombol Tab untuk mempercepat pengetikan perintah atau nama file, sekaligus mengurangi salah ketik.

`Gunakan history` → Kalau salah ketik dalam perintah panjang, tidak perlu mengetik ulang dari awal. Tekan ↑ (Up Arrow) untuk memanggil perintah sebelumnya, lalu gunakan ← → (Left/Right Arrow) untuk memperbaiki bagian yang salah.

`Baca perintah dari kanan ke kiri` → Saat mencari kesalahan, cek perintah dari akhir ke awal agar lebih mudah menemukan karakter yang kurang atau ganda.

`Bersihkan layar` → Gunakan perintah clear agar tampilan terminal kosong kembali, sehingga fokus pada tugas baru tanpa gangguan dari perintah lama.

> Blog selanjutnya [Learn Linux 4](
https://blog.zakaria.web.id/bahasa%20indonesia/linux/sysadmin/learn%20linux/command-line-interface/)

