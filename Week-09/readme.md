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

## A. Topologi IP Routes

<div align="center">

![Image](<Assets/IMG%20(1).jpg>)

</div>
<p>

</p>

## B. Konfigurasi DNS Server pada Desktop 2

### 1. Menambahkan Zona Internal

> $ sudo nano /etc/bind/named.conf

<div align="center">
<h3>
Hasil
</h3>

![Image](<Assets/IMG%20(5).png>)

<p>
Tambahkan include "/etc/bind/named.conf.internal-zones"; pada baris bawah sendiri kemudian save perubahan tersebut. Package yang baru saja ditambahkan berguna untuk menyimpan konfigurasi zona tambahan khusus pada jaringan internal.
</p>

</div>

### 2. Konfigurasi pada named.conf.options

> $ sudo nano /etc/bind/named.conf.options

<div align="center">
<h3>
Hasil
</h3>

![Image](<Assets/IMG%20(6).png>)

<p>
1. Membuat ACL (Access Control List) dengan jaringan yang terhubung: 192.168.10.0/24.<br>
2. Hanya localhost dan jaringan internal-network (192.168.10.0/24) yang boleh mengirim query DNS ke server ini.<br>
3. Hanya localhost yang diizinkan melakukan zone transfer (biasanya dipakai untuk secondary DNS).<br>
4. Mengaktifkan rekursi, artinya server akan meneruskan permintaan DNS yang tidak diketahui ke server lain (misalnya untuk browsing internet).
</p>

</div>

### 3. Konfigurasi pada named.conf.internal-zones

> $ sudo nano /etc/bind/named.conf.internal-zones

<div align="center">
<h3>
Hasil
</h3>

![Image](<Assets/IMG%20(7).png>)

<p>
1. Menyimpan konfigurasi zona DNS untuk domain internal (kelompok1.home).<br>
2. Menyediakan forward dan reverse lookup untuk jaringan 192.168.10.0/24.
</p>

</div>

### 4. Konfigurasi pada default/named

> $ sudo nano /etc/default/named

<div align="center">
<h3>
Hasil
</h3>

![Image](<Assets/IMG%20(8).png>)

<p>
1. Menjalankan BIND sebagai user non-root (bind) untuk keamanan.<br>
2. Menonaktifkan IPv6, hanya mengaktifkan dukungan IPv4.
</p>

</div>

### 5. Konfigurasi pada Zone Files

> $ sudo nano /etc/bind/kelompok1.home

<div align="center">
<h3>
Hasil
</h3>

![Image](<Assets/IMG%20(9).png>)

<p>
File srv.world.lan ini adalah file zona forward lookup untuk domain lokal kelompok10.home. Ia menyimpan:<br>
1. Info DNS utama (NS)<br>
2. Info mail server (MX)<br>
3. Pemetaan hostname ke IP (A record)
</p>

</div>

### 6. Konfigurasi pada Zone Reverse Lookup

> $ sudo nano /etc/bind/192.168.10.db

<div align="center">
<h3>
Hasil
</h3>

![Image](<Assets/IMG%20(10).png>)

<p>
1. Menyatakan bahwa ns.kelompok10.home adalah name server untuk zona ini (reverse zona 192.168.10.1).<br>
2. Melakukan pemetaan IP ke nama domain:<br>
"192.168.10.10" akan dikenali sebagai ns.kelompok10.home.<br>
"192.168.10.11" akan dikenali sebagai www.kelompok10.home.<br>
</p>

</div>

### 7. Verifikasi Perubahan

> $ systemctl restart named

> $ sudo nano /etc/resolv.conf

<div align="center">
<h3>
Hasil
</h3>

![Image](<Assets/IMG%20(11).png>)

<p>
Baris nameserver "192.168.10.10" digunakan untuk mengatur DNS resolver lokal agar mengarah ke DNS server internal (192.168.10.10).
</p>

</div>

### 7. Menggunakan perintah DIG (Domain Information Groper)

> $ dig ns.kelompok10.home

<div align="center">
<h3>
Hasil
</h3>

![Image](<Assets/IMG%20(12).png>)

<p>
Gambar tersebut adalah perintah Dig (Domain Information Groper) yang digunakan untuk melakukan query DNS.
Dalam hal ini, saya meminta alamat IP dari domain ns.kelompok10.home.
</p>

</div>

### 8. Menggunakan perintah DIG -x (Domain Information Groper)

> $ dig -x 10.0.0.1

<div align="center">
<h3>
Hasil
</h3>

![Image](<Assets/IMG%20(13).jpg>)

<p>
Gambar tersebut adalah digunakan untuk melakukan pencarian (query) terhadap DNS (Domain Name System) untuk melakukan reverse lookup terhadap alamat IP yang diberikan, dalam hal ini 10.0.0.1
</p>

</div>

## C. Konfigurasi Web Server Apache pada Desktop 2

### 1. Mengatur Konfigurasi Keamanan Apache

> $ nano /etc/apache2/conf-enabled/security.conf

<div align="center">
<h3>
Hasil
</h3>

![Image](<Assets/IMG%20(14).jpg>)

<p>
 Gambar diatas adalah berisi pengaturan terkait aspek keamanan untuk server Apache, seperti pengaturan otorisasi
 pembatasan akses, header HTTP, dan lainnya.
 disini saya menambahkan ServerTokens Prod: Membatasi informasi yang diberikan oleh server tentang dirinya sendiri, hanya menampilkan nama dan versi utama produk. Ini membantu mengurangi informasi yang dapat digunakan oleh pihak yang tidak bertanggung jawab untuk mengeksploitasi kerentanannya.
</p>

</div>

### 2. Mengatur Konfigurasi Apache Aktif

> $ nano /etc/apache2/mods-enabled/dir.conf

<div align="center">
<h3>
Hasil
</h3>

![Image](<Assets/IMG%20(15).jpg>)

<p>
 DirectoryIndex: Direktif ini memberitahu Apache file apa yang harus dicari dan ditampilkan secara default ketika sebuah direktori diakses tanpa menyebutkan nama file.

index.html index.htm: Daftar file yang akan dicari oleh Apache secara berurutan. Jika ada index.html, maka itu yang ditampilkan. Jika tidak ada, maka akan mencoba index.htm.
</p>

</div>

### 3. Menambahkan domain server

> $ nano /etc/apache2/apache2.conf

<div align="center">
<h3>
Hasil
</h3>

![Image](<Assets/IMG%20(16).jpg>)

<p>
 ServerName www.kelompok10.home: Baris ini menetapkan nama host utama (FQDN) dari server Apache. Ini mencegah peringatan seperti Could not reliably determine the server's fully qualified domain name saat Apache dimulai, dan digunakan untuk merespons permintaan HTTP.
</p>

</div>

### 4. Menambahkan domain server

> $ nano /etc/apache2/sites-enabled/000-default.conf

<div align="center">
<h3>
Hasil
</h3>

![Image](<Assets/IMG%20(17).jpg>)

<p>
 ServerAdmin webmaster@kelompok10.home: Baris ini menetapkan alamat email administrator web (webmaster) yang akan ditampilkan di halaman error server (misalnya error 500) agar pengguna tahu harus menghubungi siapa jika ada masalah.
</p>

</div>

### 5. Mengakses Webserver

<div align="center">
<h3>
Hasil
</h3>

![Image](<Assets/IMG%20(19).jpg>)

<p>
 Mengakses pada browser untuk validasi webserver dapat berfungsi dengan baik dengan mengetik sesuai IP "http://192.168.10.10".
</p>

</div>

## C. Konfigurasi Mail Server
### 1. Mengatur jaringan local dan eksternal

> $ nano /etc/postfix/main.cf

<div align="center">
<h3>
Hasil
</h3>

![Image](<Assets/IMG%20(20).jpg>)

<p>
 inet_interfaces = all <br>Memungkinkan server untuk menerima koneksi dari semua jaringan yang terhubung ke server, baik itu dari localhost atau jaringan eksternal.
 
</p>

### 2. Mengatur Perilaku Server

> $ nano /etc/postfix/main.cf

<div align="center">
<h3>
Hasil
</h3>

![Image](<Assets/IMG%20(21).jpg>)

<p>
 mail_owner = postfix<br>
 Menentukan user sistem yang akan menjalankan proses Postfix.
 
</p>

</div>

### 3. Menambahkan hostname

> $ nano /etc/postfix/main.cf

<div align="center">
<h3>
Hasil
</h3>

![Image](<Assets/IMG%20(21).jpg>)

<p>
 myhostname = mail.kelompok10.home<br>
Menentukan hostname dari server email ini.
</p>

</div>

### 4. Menambahkan Jaringan

> $ nano /etc/postfix/main.cf

<div align="center">
<h3>
Hasil
</h3>

![Image](<Assets/IMG%20(22).jpg>)

<p>
 mynetworks = 127.0.0.0/8, 192.168.10.0/24<br>
Spesifik jaringan lokal yang diizinkan relay email melalui server.
</p>

</div>

### 5. Mengizinkan Jaringan

> $ nano /etc/postfix/main.cf

<div align="center">
<h3>
Hasil
</h3>

![Image](<Assets/IMG%20(23).jpg>)

<p>
 mynetworks_style = subnet<br>
Mengizinkan semua alamat dalam subnet lokal untuk mengirim email.
</p>

</div>

### 6. Menentukan Format Penyimpanan

> $ nano /etc/postfix/main.cf

<div align="center">
<h3>
Hasil
</h3>

![Image](<Assets/IMG%20(24).jpg>)

<p>
 home_mailbox = Maildir/<br>
Menentukan format penyimpanan email (Maildir).
</p>

</div>

### 7. Menetapkan Jalur

> $ nano /etc/postfix/main.cf

<div align="center">
<h3>
Hasil
</h3>

![Image](<Assets/IMG%20(25).jpg>)

<p>
 sendmail_path = /usr/sbin/postfix
<br>
menetapkan jalur untuk program sendmail yang digunakan oleh sistem untuk mengirim email.
</p>

</div>

### 8. Identifikasi SMTP

> $ nano /etc/postfix/main.cf

<div align="center">
<h3>
Hasil
</h3>

![Image](<Assets/IMG%20(26).jpg>)

<p>
 smtpd_banner = $myhostname ESMTP<br>
Banner identifikasi SMTP yang sederhana (menghilangkan informasi distro untuk keamanan).
</p>

</div>

### 9. Menggunakan ipv4

> $ nano /etc/postfix/main.cf

<div align="center">
<h3>
Hasil
</h3>

![Image](<Assets/IMG%20(27).jpg>)

<p>
 inet_protocols = ipv4<br>
Hanya menggunakan IPv4 (nonaktifkan IPv6).
</p>

</div>

### 10. Mengatur beberapa path

> $ nano /etc/postfix/main.cf

<div align="center">
<h3>
Hasil
</h3>

![Image](<Assets/IMG%20(28).jpg>)

<p>
- sendmail_path = /usr/sbin/postfix<br>
Mengatur agar sistem menggunakan Postfix sebagai pengganti perintah sendmail untuk mengirim email.<br>
- newaliases_path = /usr/bin/newaliases<br>
Menetapkan jalur perintah newaliases yang digunakan untuk memperbarui database alias email (/etc/aliases).<br>
- mailq_path = /usr/bin/mailq<br>
Menetapkan jalur perintah mailq untuk melihat antrean email yang sedang menunggu pengiriman.<br>
- setgid_group = postdrop<br>
Menetapkan grup postdrop untuk mengatur izin akses saat pengguna biasa mengirim email ke antrean Postfix (antrian mail drop).<br>
</p>

</div>

### 11. Security dan Auth

> $ nano /etc/postfix/main.cf

<div align="center">
<h3>
Hasil
</h3>

![Image](<Assets/IMG%20(29).jpg>)

<p>
Baris akhir tambahan (security & auth):

disable_vrfy_command = yes → Menonaktifkan perintah VRFY untuk keamanan.

smtpd_helo_required = yes → Memaksa client mengirim perintah HELO/EHLO.

message_size_limit = 10240000 → Batasi ukuran email 10MB.

SMTP AUTH config → Mengaktifkan otentikasi SMTP dengan Dovecot (smtpd_sasl_*).
</p>

</div>


## Kesimpulan
Konfigurasi DNS Server (BIND) pada Debian 12 bertujuan untuk membangun layanan sistem penamaan domain menggunakan perangkat lunak BIND. Proses ini mencakup instalasi paket, pengaturan file zona dan konfigurasi named.conf, serta pengujian untuk memastikan fungsi DNS berjalan dengan baik. Implementasi ini memungkinkan server berperan sebagai pengelola layanan nama domain baik untuk kebutuhan lokal maupun publik.

Konfigurasi HTTP Server (Apache2) difokuskan pada penyediaan layanan web menggunakan Apache di lingkungan Debian 12. Panduan mencakup instalasi server, pembuatan virtual host, aktivasi modul-modul penting seperti SSL, serta pengaturan direktori dan hak akses. Tujuan utamanya adalah memastikan server web dapat menyajikan konten secara optimal dan aman.

Konfigurasi Mail Server menggunakan Postfix dan Dovecot dimaksudkan untuk membangun sistem pengiriman dan penerimaan email yang lengkap. Postfix digunakan sebagai agen transfer email (MTA), sementara Dovecot sebagai agen penerima (IMAP/POP3). Panduan ini juga mencakup pengaturan pengguna, penerapan keamanan komunikasi (SSL/TLS), serta fitur proteksi tambahan seperti SPF, DKIM, dan DMARC, guna meningkatkan integritas serta keandalan sistem surat elektronik.
<p>

</p>
