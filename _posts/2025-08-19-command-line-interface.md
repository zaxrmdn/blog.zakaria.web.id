---
title: "Command Line Interface di Linux "
date: 2025-05-25
excerpt_separator: "<!--more-->"
categories:
  - Bahasa Indonesia
  - Linux
  - Sysadmin
  - Learn Linux
tags:
  - Learn Linux 2
  - CLI
---

# Command Line Interface
Salah satu ciri khas Linux dibanding sistem operasi lain adalah penggunaan command-line interface (CLI). Administrator Linux lebih sering memakai CLI untuk tugas sehari-hari, sedangkan di platform lain biasanya menggunakan GUI (antarmuka grafis).

Di Linux, GUI bersifat opsional, bahkan sering dianggap tidak perlu pada server karena bisa mengurangi performa dan keamanan. GUI memakan banyak sumber daya hardware, terutama memori dan prosesor. Pada server, sumber daya ini sebaiknya difokuskan untuk layanan utama, seperti query database atau manajemen printer. Sementara itu, komputer desktop biasanya membutuhkan GUI agar lebih mudah digunakan.

### Kelebihan CLI:

- ***Lebih cepat*** : Eksekusi perintah bisa lebih cepat jika sudah hafal.

- ***Ringan*** : Tidak banyak memakai resource hardware, sehingga performa server lebih optimal.

- ***Bisa otomatisasi***n: Perintah bisa ditulis dalam script agar dijalankan berulang, terjadwal, dan konsisten.

### Kekurangan CLI:

- ***Sulit dipelajari*** : Harus mengingat banyak perintah dan opsi.

- ***Kurang intuitif*** : Perintah sering tidak mudah dipahami atau dihubungkan dengan fungsinya.

- ***Tidak konsisten*** : Setiap perintah bisa punya gaya berbeda, sehingga kadang membingungkan.

Command-line interface (CLI) tersedia di Linux, Windows, dan macOS. Pengguna mengetik perintah dengan sintaks tertentu, lalu sistem menjalankannya. Awalnya, cara ini bisa terasa sulit atau menakutkan, tapi akan semakin mudah dengan latihan. CLI biasanya lebih cepat dan mendukung otomatisasi yang tidak bisa dilakukan lewat GUI.

contoh:
```
rama@mysrv:~$ whoami
rama

rama@mysrv:~$ pwd
/home/rama

rama@mysrv:~$ hostname
mysrv
```

### Apa itu Shell?
`Shell` adalah program yang menyediakan CLI. Setiap shell punya sintaks sendiri atau cara penulisan perintah yang berbeda.

Beberapa shell umum di Linux:

- `Bash`: Shell default di sebagian besar distro Linux.

- `ksh` (Korn shell): Shell lama yang masih digunakan di beberapa sistem.

- `zsh` (Z shell): Shell dengan fitur tambahan dan lebih ramah pengguna.

Perbedaan utama antar shell terletak pada sintaks dan fitur kemudahan penggun

