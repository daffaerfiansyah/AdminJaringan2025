<div align="center">
  <h1 style="text-align: center;font-weight: bold">Workshop<br>Administrasi Jaringan</h1>
  <h4 style="text-align: center;">Dosen Pengampu : Dr. Ferry Astika Saputra, S.T., M.Sc.</h4>
</div>
<br />
<div align="center">
  <img src="https://upload.wikimedia.org/wikipedia/id/4/44/Logo_PENS.png" alt="Logo PENS">
  <br>
  <br>
  <p style="text-align: center;">
    <strong>Muhammad Daffa Erfiansyah (3123500006)</strong><br>
  </p>

<h3 style="text-align: center;line-height: 1.5">Politeknik Elektronika Negeri Surabaya<br>Departemen Teknik Informatika Dan Komputer<br>Program Studi Teknik Informatika<br>2024/2025</h3>
  <hr><hr>
</div>

## Review Konsep Jaringan

### 1. Analisa Versi HTTP, IP Address dari client maupun server, berapa durasi waktu dari client mengirimkan HTTP request hingga waktu dari server mengirimkan ke server.

### Jawaban
<div>
<p>

>Versi : HTTP/1.1<br>
<div align="center">

![Image](Assets/IMG03.png)

</div>

>IP HTTP Client : 145.254.160.237<br>

<div align="center">

![Image ](Assets/IMG02.png)


</div>

>IP HTTP Server : 65.208.228.223
<div align="center">


![Image ](Assets/IMG02.png)


</div>

>Durasi HTTP Request : 0.911310<br>
<div align="center">

![Image ](Assets/IMG04.png)

</div>

>Durasi HTTP Response : 3.955688<br>
<div align="center">

![Image ](Assets/IMG05.png)

</div>

>Durasi waktu dalam 1 sesi HTTP Response : 4.846969 - 3.955688 = 0.891281

</p>
</div>

### 2. Deskripsikan gambar pada slide 3

<div align="center">

![Image ](Assets/IMG01.jpg)

<p>Figure 23.1 Types of data deliveries slide PPT</p>
</div>

### Deskripsi
<div>
  <p>
1. Pada <b>Transport Layer</b>, komunikasi terjadi antara aplikasi di perangkat pengirim dan penerima. Data dikemas dalam segmen dengan header yang berisi port number, memastikan data sampai ke aplikasi yang tepat. Melibatkan protokol TCP dan UDP.
<br>
<br>
2. Pada <b>Network Layer</b>, data dikemas dalam bentuk paket dan dikirim dari komputer pengirim ke komputer penerima melalui internet. Melibatkan protokol IP<br>Proses yang terjadi:
Pengalamatan IP → Setiap paket diberi alamat IP sumber dan tujuan.
Routing → Paket dikirim melalui berbagai router untuk mencapai tujuan.
<br>
<br>
3. Pada <b>Data Link Layer</b>, data dikemas dalam frame dan dikirim antar perangkat jaringan (seperti switch atau router). Melibatkan protokol Ethernet, Wi-fi, atau PPP untuk komunikasi jaringan lokal. <br>
Proses yang terjadi:
Pengalamatan MAC → Frame diberi alamat MAC sumber dan tujuan untuk komunikasi dalam satu jaringan lokal.
Error Detection → Data diperiksa untuk memastikan tidak terjadi kesalahan saat transmisi.
<br>
<br>
Jadi, dalam gambar tersebut, terjadi tiga jenis proses utama:
<br>Proses ke Proses (Transport Layer)
<br>Host ke Host (Network Layer)
<br>Node ke Node (Data Link Layer)

Setiap proses ini bekerja sama untuk memastikan data dikirim dengan benar dari satu komputer ke komputer lain di jaringan.

  </p>
</div>

### 3. Rangkuman tahapan komunikasi menggunakan TCP
<div>
  <p>
  1. Three-Way Handshake (Membangun Koneksi)

Pengirim mengirim SYN ke penerima.
<br>Penerima membalas dengan SYN-ACK.
<br>Pengirim mengonfirmasi dengan ACK, koneksi terbentuk.
<br>
<br>
2. Data Transmission (Pengiriman Data)

Data dibagi menjadi segmen dan diberi sequence number.
<br>
Penerima mengirim ACK untuk setiap segmen yang diterima.
<br>
Jika segmen hilang, TCP akan mengirim ulang (retransmission).
<br>
Sliding Window digunakan untuk mengontrol jumlah data yang dikirim.
<br>
<br>
3. Four-Way Handshake (Menutup Koneksi)

Pengirim mengirim FIN, penerima membalas ACK.
Penerima mengirim FIN, pengirim membalas ACK.
Koneksi ditutup setelah TIME_WAIT selesai.


  </p>
</div>


