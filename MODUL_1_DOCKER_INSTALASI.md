<img src="./images/modul_1/image16.png"
style="width:6.54931in;height:3.68333in" />

Disusun Oleh:

Nama : Rizal Maulana Airlangga

Kelas : 2 S.Tr. Teknik Informatika B

NRP : 3124600033

Kelompok : B4

Modul : 1 (satu)

**Dosen Pengampu:**

Dr. Ferry Astika Saputra, S.T., M.Sc.

**PROGRAM STUDI D4 TEKNIK INFORMATIKA**

**DEPARTEMEN TEKNIK INFORMATIKA DAN KOMPUTER**

**POLITEKNIK ELEKTRONIKA NEGERI SURABAYA**

**2026**

# Jawaban Pre-Lab

1.  Sebutkan minimal 3 perbedaan antara Virtual Machine dan Container.

    1.  Virtual Machine menjalankan guest OS lengkap, sedangkan
        container berbagi kernel host

    2.  VM lebih berat dalam penggunaan resource, sedangkan container
        lebih ringan dan cepat

    3.  Booting VM membutuhkan waktu lebih lama, sedangkan container
        dapat berjalan dalam hitungan detik.

    4.  VM menggunakan hypervisor, sedangkan container menggunakan
        container runtime seperti containerd dan runc.

2.  Apa fungsi dari containerd dan runc dalam arsitektur Docker?

> containerd berfungsi sebagai container runtime tingkat tinggi yang
> mengelola lifecycle container seperti pull image, start, stop, dan
> networking. runc adalah low-level runtime yang bertugas membuat dan
> menjalankan container sesuai standar OCI.

3.  Mengapa Docker membutuhkan kernel Linux? Bagaimana Docker Desktop di
    Windows mengatasi hal ini?

> Docker menggunakan fitur kernel Linux seperti namespaces dan cgroups
> untuk isolasi dan manajemen resource container. Di Windows, Docker
> Desktop menggunakan WSL2 atau virtual machine Linux kecil agar Docker
> tetap dapat menjalankan kernel Linux.

4.  Apa keuntungan layered filesystem pada Docker Image?

> Layered filesystem memungkinkan reuse layer antar image sehingga lebih
> hemat storage, mempercepat build, dan mempercepat proses pull/push
> image.

5.  Jelaskan perbedaan antara docker run dan docker exec.

> docker run digunakan untuk membuat dan menjalankan container baru dari
> image. docker exec digunakan untuk menjalankan perintah tambahan pada
> container yang sudah berjalan.

# 

\
=

# Screenshot Wajib 

## docker version: Versi Client dan Server

<img src="./images/modul_1/image11.png"
style="width:6.10236in;height:3.16667in" />

## sudo systemctl status docker: Service Active (Running)

<img src="./images/modul_1/image15.png"
style="width:6.10236in;height:0.76389in" />

## docker run hello-world: Pesan Sukses Lengkap

<img src="./images/modul_1/image10.png" style="width:6.10236in;height:2.75in" />

## docker images: Daftar Image yang Sudah di-pull

<img src="./images/modul_1/image8.png"
style="width:6.10236in;height:1.01389in" />

## docker ps: Container nginx Berjalan dengan Port Mapping

<img src="./images/modul_1/image1.png"
style="width:6.10236in;height:0.97222in" />

## Browser Mengakses http://localhost:8080: Halaman nginx Default

<img src="./images/modul_1/image2.png"
style="width:6.10236in;height:1.95833in" />

## docker build -t pens-web:1.0 .: Proses Build Berhasil (Step Terakhir)

<img src="./images/modul_1/image12.png"
style="width:6.10236in;height:2.80556in" />

## Browser Mengakses http://localhost:9090: Halaman Custom PENS

<img src="./images/modul_1/image14.png"
style="width:4.58973in;height:1.95744in" />

# Jawaban Post-Lab

1.  Bandingkan output docker image history nginx dengan docker image
    history pens-web:1.0. Layer mana saja yang di-share?

    1.  ENTRYPOINT \["/docker-entrypoint.sh"\]

    2.  EXPOSE 80

    3.  STOPSIGNAL SIGQUIT

    4.  CMD \["nginx" "-g" "daemon off;"\]

    5.  COPY docker-entrypoint.sh

    6.  COPY 10-listen-on-ipv6-by-default.sh

    7.  COPY 15-local-resolvers.envsh

    8.  COPY 20-envsubst-on-templates.sh

    9.  COPY
        [<u>30-tune-worker-processes.sh</u>](http://30-tune-worker-processes.sh)

2.  Apa yang terjadi pada data di dalam container setelah container
    dihapus dengan docker rm? Bagaimana solusinya?

> <img src="./images/modul_1/image4.png"
> style="width:6.10236in;height:1.20833in" />

1.  Seluruh data di dalam container akan hilang permanen.

2.  Solusi yang bisa digunakan

    1.  Data disimpan di Docker, terpisah dari container

<img src="./images/modul_1/image13.png"
style="width:6.10236in;height:0.86111in" />

<img src="./images/modul_1/image6.png"
style="width:6.10236in;height:0.65278in" />

> Data masih ada

2.  Data langsung disimpan di komputer

<!-- -->

3.  Jelaskan perbedaan antara EXPOSE di Dockerfile dan flag -p pada
    docker run. Apakah EXPOSE cukup untuk membuat port dapat diakses
    dari host?

    1.  EXPOSE (di Dockerfile)

        1.  Deklarasi / dokumentasi bahwa container menggunakan port
            tertentu

        2.  Memberi informasi ke user/tool (misalnya Docker Compose)

        3.  Tidak membuka akses ke luar (host)

    2.  -p (saat docker run)

        1.  Mapping port host ke container

        2.  Membuka akses dari luar (browser, jaringan)

    3.  EXPOSE tidak cukup untuk membuat port dapat diakses dari host.
        Harus pakai -p

    4.  Percobaan

        1.  docker run -d --name web1 nginx

> <img src="./images/modul_1/image9.png"
> style="width:3.28244in;height:2.34076in" />

2.  docker run -d --name web2 -p 8080:80 nginx

> <img src="./images/modul_1/image5.png" style="width:5.64702in;height:2.0044in" />
>
> <img src="./images/modul_1/image3.png"
> style="width:6.10236in;height:0.59722in" />

4.  Mengapa menggunakan tag spesifik (misal nginx:1.26) lebih baik
    daripada nginx:latest untuk production?

    1.  Reproducible

        1.  nginx:1.26 versi tetap (Hari ini build, sukses)

        2.  nginx:latest bisa berubah kapan saja (Besok build (latest
            berubah) bisa error)

    2.  Stabilitas sistem

        1.  Versi spesifik sudah teruji di environment

        2.  latest bisa membawa perubahan (konfigurasi,dependency, dan
            breaking change)

    3.  Keamanan (security control)

        1.  Versi spesifik dapat diketahui: CVE yang berlaku, patch yang
            dipakai

        2.  Latest: tidak jelas berubah ke versi apa

    4.  Debugging lebih mudah

        1.  Kalau error: nginx:1.26 bisa reproduce

        2.  nginx:latest tidak konsisten

5.  Berapa ukuran image alpine:3.20 dibanding ubuntu:22.04? Apa
    trade-off menggunakan Alpine?

    1.  Tabel perbandingan

> <img src="./images/modul_1/image7.png"
> style="width:6.10236in;height:1.59722in" />

| Image        | Ukuran  |
|--------------|---------|
| alpine:3.20  | 12.2 MB |
| ubuntu:22.04 | 119 MB  |

> Alpine ≈ 10x lebih kecil dari Ubuntu

2.  Trade-off menggunakan Alpine

    1.  Kelebihan Alpine

        1.  Ukuran sangat kecil, pull cepat

        2.  Startup container lebih cepat

        3.  Surface attack lebih kecil (lebih aman)

        4.  Hemat storage

    2.  Kekurangan Alpine

        1.  Menggunakan musl libc (bukan glibc)

            1.  Beberapa aplikasi/library tidak kompatibel

            2.  Contoh: Python packages tertentu, Java native libs

        2.  Debugging lebih sulit

            1.  Tools terbatas (tidak selengkap Ubuntu)

            2.  Banyak package harus install manual

        3.  Ecosystem lebih kecil

            1.  Tidak semua software tersedia Kadang perlu workaround

        4.  Build lebih kompleks

            1.  Compile dependency bisa lebih ribet
