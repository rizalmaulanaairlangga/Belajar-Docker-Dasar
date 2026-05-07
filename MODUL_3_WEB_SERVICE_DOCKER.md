# WEB SERVICE DOCKER

<img src="./images/modul_3/image2.png"
style="width:6.54931in;height:3.68333in" />

Disusun Oleh:

Nama : Rizal Maulana Airlangga

Kelas : 2 S.Tr. Teknik Informatika B

NRP : 3124600033

Kelompok : B4

Modul : 3 (tiga)

**Dosen Pengampu:**

Dr. Ferry Astika Saputra, S.T., M.Sc.

**PROGRAM STUDI D4 TEKNIK INFORMATIKA**

**DEPARTEMEN TEKNIK INFORMATIKA DAN KOMPUTER**

**POLITEKNIK ELEKTRONIKA NEGERI SURABAYA**

2026\
=====

# Jawaban Pre-Lab

1.  Apa keuntungan menjalankan web server di container dibandingkan
    langsung di host?

> Container memberikan isolasi environment, deployment lebih konsisten,
> mudah dipindahkan antar server, dan dependency aplikasi tidak
> bercampur dengan host.

2.  Jelaskan perbedaan document root Apache vs Nginx.

> Apache menggunakan default document root /usr/local/apache2/htdocs/,
> sedangkan Nginx menggunakan /usr/share/nginx/html/. Folder tersebut
> adalah lokasi file website yang dilayani web server.

3.  Apa itu SSL Termination dan mengapa dilakukan di reverse proxy?

> SSL Termination adalah proses decrypt HTTPS di reverse proxy sebelum
> request diteruskan ke backend. Hal ini mempermudah manajemen
> sertifikat dan mengurangi beban backend.

4.  Apa perbedaan name-based dan IP-based virtual hosting?

> Name-based virtual hosting menggunakan satu IP untuk banyak domain
> berdasarkan hostname. IP-based virtual hosting menggunakan IP berbeda
> untuk setiap website.

5.  Mengapa self-signed certificate menghasilkan warning di browser?

> Karena sertifikat ditandatangani sendiri dan tidak diverifikasi oleh
> Certificate Authority terpercaya.

\
=

# Screenshot Wajib

## docker compose ps: 4 Service Running

## curl -k https://site1.lab:8443: Halaman Site 1<img src="./images/modul_3/image16.png"
style="width:8.15754in;height:1.7127in" />

<img src="./images/modul_3/image1.png"
style="width:5.51181in;height:2.64567in" />

## curl -k https://site2.lab:8443: Halaman Site 2

<img src="./images/modul_3/image7.png"
style="width:5.51181in;height:2.64567in" />

## curl -I http://site1.lab:8080: HTTP → HTTPS Redirect 301<img src="./images/modul_3/image4.png"
style="width:8.26285in;height:1.22929in" />

## openssl s_client output: Detail Certificate<img src="./images/modul_3/image8.png"
style="width:8.26042in;height:1.07196in" />

<img src="./images/modul_3/image14.png"
style="width:8.26042in;height:2.29184in" /><img src="./images/modul_3/image13.png" style="width:8.181in;height:2.29167in" />

## curl -k https://app.lab:8443/api/health: JSON database connected<img src="./images/modul_3/image12.png"
style="width:8.17708in;height:1.71148in" />

<img src="./images/modul_3/image15.png"
style="width:8.17708in;height:2.36446in" />

## POST /api/visitors: Response 201<img src="./images/modul_3/image19.png"
style="width:8.17708in;height:0.81771in" />

<img src="./images/modul_3/image9.png"
style="width:6.69872in;height:2.27934in" />

## GET /api/visitors: Daftar Visitor<img src="./images/modul_3/image20.png"
style="width:8.22917in;height:1.89321in" />

## Log nginx per-site<img src="./images/modul_3/image18.png"
style="width:8.08398in;height:5.08765in" />

## Log Apache per-site<img src="./images/modul_3/image18.png"
style="width:8.08481in;height:1.89583in" />

# Pertanyaan Post-Lab

1.  Bandingkan response header dari Apache vs Nginx. Header apa yang
    menunjukkan software web server?

Perbedaan terlihat pada header:

- nginx (host atau browser) Server: nginx/1.29.8 menunjukkan request
  ditangani **nginx (reverse proxy)**

<img src="./images/modul_3/image4.png" style="width:6.9758in;height:1.04175in" />

<img src="./images/modul_3/image5.png"
style="width:6.99814in;height:1.38904in" />

- Apache (lokal) Server: Apache/2.4.66 (Unix) menunjukkan backend yang
  digunakan adalah Apache.

<img src="./images/modul_3/image5.png"
style="width:7.01325in;height:1.61742in" />

Header yang menunjukkan software web server adalah Server, karena berisi
informasi jenis dan versi web server yang menangani request.

2.  Jika Nginx proxy down, apakah Apache masih bisa diakses langsung?
    Bagaimana cara testnya?

<img src="./images/modul_3/image3.png"
style="width:6.68227in;height:0.50528in" />

Tidak bisa diakses langsung, namun bisa diakses melalui Apache

<img src="./images/modul_3/image10.png"
style="width:6.48094in;height:1.61717in" />

3.  Tunjukkan bahwa X-Real-IP header diteruskan dengan benar dari Nginx
    ke Flask.<img src="./images/modul_3/image17.png"
    style="width:8.07953in;height:0.4853in" />

Header X-Real-IP berhasil diteruskan dan flask menerima IP dari client
melalui nginx.

4.  Jelaskan mengapa Flask app perlu terhubung ke dua network (web-net
    dan db-net).

Flask butuh 2 network, karena satu untuk menerima request dari nginx
(web layer) dan satu lagi untuk mengakses database (data layer). Ini
bertujuan untuk memisahkan traffic agar lebih aman dan terstruktur.

5.  Apa yang terjadi jika file server.key atau server.crt dihapus saat
    container running?

<img src="./images/modul_3/image11.png"
style="width:6.55327in;height:0.61006in" />

Jika file server.key atau server.crt dihapus saat container sedang
berjalan, layanan HTTPS masih dapat berjalan sementara. Namun, jika
container di-restart, maka nginx gagal memulai layanan HTTPS karena file
sertifikat tidak ditemukan.
