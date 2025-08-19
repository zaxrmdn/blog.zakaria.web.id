---
title: "🔐 Menambahkan 2FA di Ubuntu Server dengan Microsoft Authenticator "
date: 2025-05-25
excerpt_separator: "<!--more-->"
categories:
  - Bahasa Indonesia
  - Ubuntu Server
  - Sysadmin
  - Intermediate Level
tags:
  - Documentation
  - SSH
  - 2FA
---

Tujuan dari article ini dibuat sebagai catatan saya saja, jadi background dibuatnya ini berdasarkan kebutuhan saya untuk menambahkan keamanan pada server ubuntu. Mengingat 2FA ini sudah menjadi hal yang wajib dibeberapa platform, dan mengapa kita tidak coba menambahkan metode ini untuk keamanan di infarastruktur kita terutama server linux ubuntu. Kenapa? karna jika kita hanya mengandalkan satu metode saja meskipun terbilang aman seperti lewat ssh-key bisa dibilang masih cukup membuat kita terkadang merasa khawatir. Jadi upaya yang bisa kita lakukan ialah menambah layer keamanan lagi.

Salah satu metode perlindungan tambahan yang sangat disarankan adalah Two-Factor Authentication (2FA). Di artikel ini, saya akan membahas langkah-langkah rinci bagaimana menambahkan 2FA ke Ubuntu Server dengan dukungan login menggunakan password dan OTP dari Microsoft Authenticator.

<!--more-->


# 🎯 Tujuan Akhir

- Login SSH membutuhkan password + OTP (6-digit code)

- OTP dapat dihasilkan dari HP melalui Microsoft Authenticator

- Ada kode cadangan (scratch code) untuk pemulihan darurat


# Environtment
- OS: Ubuntu Server 22.04
- Dependencies: libpam-google-authenticator
- Aplikasi Authenticator: Microsoft Authenticator (Android)  


# Step by step
## Instalasi Paket Pendukung

Login ke server Ubuntu dan install modul PAM untuk TOTP:

```
ubuntu@rama-prod:~$ sudo apt update
ubuntu@rama-prod:~$ sudo apt install libpam-google-authenticator -y 
```

## Setup Google Authernticator di satu user
Jalankan perintah berikut untuk user yang ingin diamankan:

```
ubuntu@rama-prod:~$ google-authenticator
```
Saat diminta:

```
Do you want authentication tokens to be time-based (y/n) y
```
Jawab y.

Akan muncul:

- QR code

- Secret key (16 digit)

- Codes Verification

Untuk codes verfication perlu di isi nanti

## Tambahkan ke Microsoft Authenticator

- Screenshot QR code atau catat secret key

- Buka Microsoft Authenticator

- Tambahkan akun baru → Lainnya → Scan QR atau masukkan kode manual


✅ OTP akan sinkron di semua device yang menggunakan secret key yang sama.

## Masukkan codes dari Authenticator
Di step sebelumnya kita perlu melanjutkan memasukkan code yang digenerate microsoft authenticator setiap 30 detik sekali.

```
Enter code from app (-1 to skip): 431215
Code confirmed

```
## Backup Scratch Code
Scratch code digunakan untuk recovery jika seandainya device authenticatornya tidak bisa atau hilang. Tetapi setiap code yang ada di scratch code hanya bisa digunakan sekali saja. Jika ingin menambahkan scratch code lagi perlu reset authenticatornya.

```
Your emergency scratch codes are:
  58954342
  39993186
  47413280
  64958173
  74581785

Do you want me to update your "/home/ubuntu/.google_authenticator" file? (y/n) 

```

## Opsi pengaturan tambahan
```
Do you want to disallow multiple uses of the same authentication
token? This restricts you to one login about every 30s, but it increases
your chances to notice or even prevent man-in-the-middle attacks (y/n) y

By default, a new token is generated every 30 seconds by the mobile app.
In order to compensate for possible time-skew between the client and the server,
we allow an extra token before and after the current time. This allows for a
time skew of up to 30 seconds between authentication server and client. If you
experience problems with poor time synchronization, you can increase the window
from its default size of 3 permitted codes (one previous code, the current
code, the next code) to 17 permitted codes (the 8 previous codes, the current
code, and the 8 next codes). This will permit for a time skew of up to 4 minutes
between client and server.
Do you want to do so? (y/n) y

If the computer that you are logging into isn't hardened against brute-force
login attempts, you can enable rate-limiting for the authentication module.
By default, this limits attackers to no more than 3 login attempts every 30s.
Do you want to enable rate-limiting? (y/n) y

```
## Config PAM (Pluggable Authentication Modules)
Edit file berikut:

```
ubuntu@rama-prod:~$ sudo vim /etc/pam.d/sshd
```

Tambahkan konfigurasi berikut:
```
# pam google authenticator
auth required pam_google_authenticator.so
```

## Konfigurasi SSH agar Mendukung Password + OTP

Edit konfigurasi SSH:

```
sudo vim /etc/ssh/sshd_config
```
Pastikan hanya ini yang diaktifkan:

```
PasswordAuthentication yes
KbdInteractiveAuthentication yes
UsePAM yes
ChallengeResponseAuthentication yes
```
Restart service ssh
```
sudo systemctl restart ssh

```
## Uji Login SSH
Gunakan session ssh baru atau terminal baru untuk menghindari tidak bisa login hehe (pengalaman but seriuosly!)

contoh:
```
(ubuntu@172.23.11.27) Verification code: 
(ubuntu@172.23.11.27) Password: 
Welcome to Ubuntu 22.04.3 LTS (GNU/Linux 5.15.0-130-generic x86_64)

```

# The end

Mengaktifkan 2FA dengan Microsoft Authenticator di Ubuntu Server adalah langkah mudah namun sangat efektif untuk menambah lapisan keamanan. Dengan konfigurasi ini, login ke server kamu akan jauh lebih aman dan tetap fleksibel, bahkan jika kamu menggunakan lebih dari satu HP.

Jangan lupa untuk menyimpan:

- Secret key

- Scratch codes

- Screenshot QR di tempat yang aman dan terenkripsi