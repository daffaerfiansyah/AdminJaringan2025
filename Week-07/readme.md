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

## A. Konfigurasi Mikrotik pada Desktop 1
### 1. Menambahkan Routes IP Address

<div align="center">

![Image](<Assets/IMG%20(1).png>)

</div>
<p>
Masuk ke dalam mikrotik sesuai dengan IP yang telah terdaftar pada switch kemudian konfigurasi routes agar dapat terhubung sesama jaringan. Disini saya menambahkan destination addres untuk Kelompok 1 yaitu "192.168.1.0/24" dengan gateaway: "10.252.108.51". Kemudian klik Apply dan OK
</p>

### 2. Check alamat IP

> ping 192.168.1.1
<div align="center">

![Image](<Assets/IMG%20(4).png>)

</div>
<p>
PING IP Address yang telah didaftarkan pada destination addres, disini saya PING untuk kelompok 1 dengan IP: "192.168.1.1" dan berhasil.
</p>

### 3. Validasi IP

<div align="center">

![Image](<Assets/IMG%20(3).png>)

</div>
<p>
Pada tampilan routes seperti pada gambar menunjukkan setiap IP dari masing" kelompok yang telah didaftarkan berstatus "reachable" yang artinya dapat diakses dan dapat mengirimkan paket pada jaringan.
</p>


