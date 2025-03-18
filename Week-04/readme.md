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

## A. Rangkuman DNS Hierarki

<div align="center">

![Image](<Assets/IMG%20(15).png>)

</div>
<p>
Gambar tersebut menjelaskan cara kerja DNS (Domain Name System) dalam menerjemahkan nama domain menjadi alamat IP melalui proses pencarian bertingkat. 

Proses tersebut menunjukkan bagaimana DNS bertindak sebagai "buku telepon" internet, yang menerjemahkan nama domain yang mudah diingat oleh manusia menjadi alamat IP yang digunakan oleh sistem komputer untuk komunikasi jaringan. 

Gambar tersebut memberikan alur lengkap bagaimana DNS bekerja dalam menyelesaikan permintaan domain melalui sistem hierarkis.

Proses Cara Kerja DNS (Total Request-Response)<br>
1. User meminta alamat IP untuk www.example.com.au ke Recursive DNS Server (1 permintaan).
2. Recursive DNS Server bertanya ke Root DNS Server:
"Di mana .au berada?" → (2 permintaan)
Root DNS Server mengembalikan alamat TLD .au → (1 respons).
3. Recursive DNS Server bertanya ke TLD .au Server:
"Di mana example.com.au berada?" → (3 permintaan)
TLD .au Server merespons dengan memberikan alamat Name Server dari example.com.au → (1 respons).
4. Recursive DNS Server bertanya ke Authoritative Name Server:
"Di mana www.example.com.au berada?" → (4 permintaan)
Authoritative Name Server merespons dengan memberikan IP m.n.o.p → (1 respons).
5. Recursive DNS Server mengirimkan alamat IP ke User (1 respons).

Total request dan response adalah 5(permintaan) + 5(respons) = 10 proses.
Jika menghitung permintaan awal dari User ke Recursive DNS Server sebagai tambahan, maka totalnya menjadi 11 (10+1).
</p>

## B. Instalasi dan Konfigurasi bind9

### 1. Install BIND

> $ apt -y install bind bind-utils

<div align="center">
<h3>
Hasil
</h3>

![Image](<Assets/IMG%20(1).png>)

<p>
Melakukan instalasi pada OS yang digunaka, sebelum install disarankan masuk pada root.
</p>

</div>

### 2. Konfigurasi BIND untuk Jaringan Internal

> $ nano /etc/named.conf.options

<div align="center">
<h3>
Hasil
</h3>

![Image](<Assets/IMG%20(4).png>)

<p>
Menambahkan recursion dan dns google.com sebagai contoh yaitu "8.8.8.8;" dan "8.8.4.4;".
</p>

</div>

### 3. Konfigurasi Zona Forward

> $ nano /etc/bind/named.conf.local

<div align="center">
<h3>
Hasil
</h3>

![Image](<Assets/IMG%20(5).png>)

<p>
Menambahkan domain yang saya gunakan dan memberikan akses untuk file domain saya.
</p>

</div>

### 4. Konfigurasi Zona Forward

> $ nano /etc/bind/named.conf.local

<div align="center">
<h3>
Hasil
</h3>

![Image](<Assets/IMG%20(7).png>)

<p>
Memberikan konfigurasi dengan menambahkan alamat IP yang digunakan oleh domain saya seperti pada gambar.
</p>

</div>

### 5. Konfigurasi Zona Reverse

> $ nano /etc/bind/named.conf.local

<div align="center">
<h3>
Hasil
</h3>

![Image](<Assets/IMG%20(6).png>)

<p>
Dengan file yang sama pada langkah ke 3, setelah melakukan konfigurasi zona reverse, menambahkan alamat IP yang digunakan pada domain dengan struktur terbalik pada IP yang digunakan kemudian menambahkan file db.100 untuk konfigurasi selanjutnya
</p>

</div>

### 6. Konfigurasi Zona Reverse

> $ nano /etc/bind/db.100

<div align="center">
<h3>
Hasil
</h3>

![Image](<Assets/IMG%20(8).png>)

<p>
Membuat file db.100 untuk konfigurasi domain yang digunakan dengan menambahkan 2 angka terakhir pada alamat IP agar terdeteksi pada jaringan.
</p>

</div>

### 7. Pengujian

> $ systemctl restart bind9

<div align="center">
<h3>
Hasil
</h3>

![Image](<Assets/IMG%20(3).png>)
![Image](<Assets/IMG%20(2).png>)

<p>
Restart proses bind9 setelah melakukan konfigurasi kemudian melakukan pengujian dengan melakukan ping pada terminal. Konfigurasi berhasil dilakukan.
</p>

</div>

## C. Konfigurasi Zona Files

### 1. Konfigurasi zona

> $ nano /etc/bind/named.conf.local

<div align="center">
<h3>
Hasil
</h3>

![Image](<Assets/IMG%20(10).png>)

<p>
Konfigurasi ini sama dengan langkah pertama menambahkan domain dan menambahkan file db.100.srv yang terdapat konfigurasi IP namun alamat IP yang digunakan berbeda dengan sebelumnya. in-addr.arpa digunakan untuk reverse lookup zone dan bisa disesuaikan dengan subnet jaringan Anda.
</p>

</div>

### 2. Membuat file forward zone

> $ nano /etc/bind/db.srv.world

<div align="center">
<h3>
Hasil
</h3>

![Image](<Assets/IMG%20(11).png>)

<p>
Melakukan konfigurasi domain yang digunakan, menambahkan alamat IP yang terdaftar pada domain. Berbeda dengan langkah sebelumnya, disini terdapat serial number. SOA (Start of Authority): Menentukan DNS server utama dan email admin. NS (Name Server): Menunjukkan bahwa ns.srv.world adalah name server utama. A Records: www, mail, dan ns mengarah ke alamat IP masing-masing.
</p>

</div>

### 3. Membuat file reverse zone

> $ nano /etc/bind/db.100.srv

<div align="center">
<h3>
Hasil
</h3>

![Image](<Assets/IMG%20(12).png>)

<p>
Sama seperti langkah sebelumnya, namun disini alamat IP yang ditambahkan hanya 2 digit terakhir untuk megidentifikasi domain yang telah didaftarkan. PTR Records: Digunakan untuk reverse lookup dari IP ke hostname.
</p>

</div>

### 4. Pengujian

> $ systemctl restart bind9

<div align="center">
<h3>
Hasil
</h3>

![Image](<Assets/IMG%20(13).png>)

<p>
Setelah melakukan restart bind9 langsung melakukan pengujian dengan www.srv.world. Jika berhasil maka akan terdeteksi seperti pada gambar tersebut.
</p>

</div>

## D. Verfikasi resolusi DNS

> $ systemctl restart bind9

<div align="center">
<h3>
Hasil
</h3>

![Image](<Assets/IMG%20(14).png>)

<p>
Pada proses ini adalah melakukan verifikasi terhadap konfiguras-konfigurasi yang dilakukan, jika tidak ada kendala berarti proses tersebut berhasil dilakukan.
</p>

</div>

## Kesimpulan

<p>
Konfigurasi BIND di Ubuntu 20.04 mencakup dua langkah utama, yaitu pengaturan file zona dan pengujian resolusi DNS. Langkah pertama melibatkan pembuatan file zona forward lookup (db.srv.world) dan reverse lookup (db.192.168.100) agar server DNS dapat secara otoritatif menangani permintaan penerjemahan nama domain dan alamat IP dalam jaringan internal. Setelah itu, dilakukan verifikasi resolusi DNS dengan perintah nslookup dan dig untuk memastikan bahwa server dapat menerjemahkan nama domain menjadi alamat IP (forward lookup) serta sebaliknya (reverse lookup). Jika hasil pengujian sesuai harapan, maka konfigurasi BIND telah berjalan dengan baik. Namun, jika terjadi kesalahan, perlu dilakukan pengecekan ulang terhadap konfigurasi file zona, memastikan BIND berfungsi dengan benar, serta meninjau log sistem di /var/log/syslog untuk menemukan penyebab masalah. Selain itu, agar DNS dapat bekerja optimal, konfigurasi jaringan menggunakan Netplan, NetworkManager, atau /etc/network/interfaces juga harus disesuaikan dengan kebutuhan sistem. Dengan konfigurasi yang tepat, server DNS dapat beroperasi secara efisien dalam mengelola resolusi nama dalam jaringan internal. 
</p>
