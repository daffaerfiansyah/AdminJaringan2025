<div align="center">
  <h1 style="text-align: center;font-weight: bold">Workshop<br>Administrasi Jaringan</h1>
  <h4 style="text-align: center;">Dosen Pengampu : Dr. Ferry Astika Saputra, S.T., M.Sc.</h4>
</div>
<br />
<div align="center">
  <img src="https://upload.wikimedia.org/wikipedia/id/4/44/Logo_PENS.png" alt="Logo PENS">
  <h3 style="text-align: center;">Disusun Oleh : </h3>
  <p style="text-align: center;">
    <strong>Muhammad Daffa Erfiansyah (3123500006)</strong><br>
  </p>

<h3 style="text-align: center;line-height: 1.5">Politeknik Elektronika Negeri Surabaya<br>Departemen Teknik Informatika Dan Komputer<br>Program Studi Teknik Informatika<br>2024/2025</h3>
  <hr><hr>
</div>

## A. Rangkuman Unix and Linux

### Chapter 4: Process Control
<p>
  Bab ini membahas bagaimana sistem operasi mengelola proses. Setiap proses memiliki ruang alamat dan struktur data dalam kernel, termasuk informasi seperti PID (Process ID), PPID (Parent Process ID), serta UID dan EUID untuk hak akses pengguna.

Proses memiliki siklus hidup yang dimulai dengan fork, di mana sebuah proses menyalin dirinya untuk membuat proses baru. Sistem juga menggunakan signals untuk komunikasi antar proses, misalnya KILL, INT, dan TERM untuk menghentikan proses.

Monitoring proses dilakukan dengan perintah seperti ps, top, dan htop untuk melihat penggunaan CPU dan memori oleh proses. Ada juga kill untuk menghentikan proses, serta nice dan renice untuk mengatur prioritas eksekusi.

Sistem berkas virtual /proc digunakan untuk menyimpan informasi tentang proses. Selain itu, alat seperti strace dapat digunakan untuk menganalisis perilaku suatu proses, dan cron digunakan untuk menjadwalkan eksekusi tugas secara otomatis.
<p>

### Chapter 5: The Filesystem

<p>
  Bab ini menjelaskan struktur sistem berkas pada UNIX/Linux, yang terdiri dari namespace (hirarki direktori), API (sistem panggilan untuk manipulasi berkas), model keamanan, dan implementasi fisik di perangkat penyimpanan.

Terdapat berbagai sistem berkas seperti ext4, XFS, NTFS, dan ISO 9660 untuk CD/DVD. Setiap file memiliki path yang dapat berupa absolute atau relative. File system dapat di-mount menggunakan perintah mount, dan di-unmount menggunakan umount.

Berbagai jenis file di UNIX termasuk regular files, directories, device files, symbolic links, dan named pipes. Hak akses file dikendalikan oleh bit read (r), write (w), dan execute (x), yang dapat diubah menggunakan chmod dan chown.

Fitur tambahan seperti Access Control Lists (ACLs) memberikan kontrol yang lebih detail atas hak akses file. Selain itu, sistem berkas memiliki mekanisme seperti sticky bit, setuid, dan setgid untuk mengatur hak eksekusi.
</p>

### Chapter 6:  Software Installation and Management

<p>
  Bab ini membahas pengelolaan perangkat lunak di sistem UNIX/Linux. Instalasi sistem operasi bisa dilakukan melalui media fisik seperti USB/DVD atau melalui jaringan menggunakan PXE (Preboot Execution Environment).

Linux memiliki dua sistem manajemen paket utama:

RPM (Red Hat, CentOS, Fedora, SUSE)
DEB (Debian, Ubuntu)
Alat manajemen paket tingkat tinggi mencakup APT (Advanced Package Tool) untuk sistem berbasis Debian dan YUM untuk distribusi berbasis RPM. Repositori paket menyimpan berbagai perangkat lunak yang dapat diunduh dan diperbarui secara otomatis.

Selain itu, konfigurasi perangkat lunak bisa disesuaikan dengan lingkungan lokal atau cloud agar lebih fleksibel dan mudah dipulihkan dalam kasus kegagalan sistem.
</p>

<hr>

## Menginstall Debian Linux dengan VirtualBox melalui root terminal pada OS Linux

### 1. Check Ubuntu Version

### Perintah terminal

>lsb_release -a<br>
<div align="center">

Hasil

![Image](<Assets/IMG (18).png>)
<p>
Untuk mengecheck versi ubuntu yang sudah terinstall
</p>

</div>

### 2. Check Dependensi 
### Perintah terminal

>sudo apt --fix-broken install
<div align="center">

Hasil
![Image](<Assets/IMG (19).png>)
<p>
memperbaiki paket yang rusak atau dependensi yang belum terpenuhi pada sistem berbasis Debian/Ubuntu.
</p>

</div>

### 3. Install VirtualBox Debian menggunakan paket melalui terminal
### Perintah terminal

>sudo dpkg -i virtualbox-7.1_7.1.6-167084~Debian~bookworm_amd64.deb<br>
<div align="center">

Hasil
![Image](<Assets/IMG (12).png>)

<p>
Fungsi untuk menginstal paket VirtualBox versi 7.1.6 dari file .deb secara manual menggunakan dpkg (Debian Package Manager).
</p>

</div>

### 4. Problem Solve Error Installing
### Perintah terminal
>sudo apt install libxcb-cursor0<br>
<div align="center">
Hasil

![Image](<Assets/IMG (8).png>)

<p>
menginstal pustaka (library) libxcb-cursor0 pada sistem berbasis Debian
</p>
</div>

### 5. Menambah User VirtualBox
### Perintah terminal
>sudo usermod -aG vboxusers$<br>
<div align="center">
Hasil

![Image](<Assets/IMG (20).png>)

<p>
menambahkan pengguna saat ini ke dalam grup vboxusers, yang diperlukan agar pengguna dapat menggunakan fitur tertentu di VirtualBox, seperti akses ke perangkat USB.
</p>
</div>

### 6. Interface Installation VirtualBox Debian

<div align="center">
Hasil

![Image](<Assets/IMG (1).png>)

<p>
Jika sudah download file ISO Debian 12, berikan lokasi file ISO tersebut kolom ISO Image.
</p>
</div>

### Langkah berikutnya

<div align="center">
Hasil

![Image](<Assets/IMG (2).png>)

<p>
Gunakan password "student"
</p>
</div>

### Penggunaan RAM dan Proccessors yang dibutuhkan

<div align="center">
Hasil

![Image](<Assets/IMG (3).png>)

<p>
Untuk RAM minimalnya 2 GB dan untuk Proccessors menggunakan 2 CPU
</p>
</div>

### Penggunaan HDD yang dibutuhkan

<div align="center">
Hasil

![Image](<Assets/IMG (4).png>)

<p>
Menggunakan 10 GB untuk alokasi memory pada Harddisk
</p>
</div>

### Validasi Kebutuhan install

<div align="center">
Hasil

![Image](<Assets/IMG (5).png>)

<p>
Jika sudah sesuai dengan spesifikasi yang diinginkan lanjut klik Finish untuk memproses instalasi.
</p>
</div>

### Proses Instalasi Berjalan

<div align="center">
Hasil

![Image](<Assets/IMG (16).png>)

<p>
Tunggu Hingga Proses instalasi selesai.
</p>
</div>

### Instalasi Virtualbox Debian Linux Berhasil

<div align="center">
Hasil

![Image](<Assets/IMG (21).png>)

<p>
Proses instalasi menggunakan Root terminal pada OS Linux selesai
</p>
</div>

</div>


