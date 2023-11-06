#Telegraf-Gambar
Solusi hosting gambar gratis, alternatif Flickr/imgur. Gunakan Halaman Cloudflare dan Telegraf.

[Bahasa Inggris](README-EN.md)|中文

## Cara menyebarkan

### Persiapkan terlebih dahulu
Satu-satunya hal yang perlu Anda persiapkan terlebih dahulu adalah akun Cloudflare (jika Anda perlu menerapkan di server Anda sendiri tanpa bergantung pada Cloudflare, silakan merujuk ke [#46](https://github.com/cf-pages/Telegraph- Gambar/masalah/46 ) )

### Tutorial langkah demi langkah
Dalam 3 langkah sederhana, Anda dapat menerapkan proyek ini dan memiliki gambar sendiri

1. Unduh atau Fork repositori ini (Catatan: Silakan gunakan fork saat ini, ada masalah dengan penerapan saat menggunakan unduhan [#14](https://github.com/cf-pages/Telegraph-Image/issues/14))

2. Buka Cloudflare Dashboard, masuk ke halaman manajemen Pages, pilih Create Project, jika pada langkah pertama Anda memilih untuk mem-fork repositori ini, pilih `Connect to Git Provider`, jika Anda memilih untuk mendownload repositori ini pada langkah pertama, lalu Pilih `Unggah Langsung`
![1](https://telegraph-image.pages.dev/file/8d4ef9b7761a25821d9c2.png)

3. Masukkan nama proyek seperti yang diminta di halaman, pilih repositori git yang akan dihubungkan (langkah pertama pilih fork) atau unggah file gudang yang baru saja Anda unduh (langkah pertama unduh repositori ini), dan klik ` Deploy Site`. Deployment siap

## Fitur
1. Penyimpanan gambar tidak terbatas, Anda dapat mengunggah gambar dalam jumlah tidak terbatas

2. Tidak perlu membeli server, server dihosting di jaringan Cloudflare, dan jika penggunaannya tidak melebihi kuota gratis Cloudflare, maka sepenuhnya gratis.

3. Tidak perlu membeli nama domain, Anda dapat menggunakan nama domain tingkat kedua gratis `*.pages.dev` yang disediakan oleh Cloudflare Pages, dan juga mendukung pengikatan nama domain khusus.

4. Mendukung API review gambar, yang dapat diaktifkan sesuai kebutuhan, setelah diaktifkan, gambar buruk akan otomatis diblokir dan tidak dapat dimuat lagi.

5. Mendukung manajemen gambar latar belakang, Anda dapat melihat pratinjau gambar yang diunggah secara online, menambahkan daftar putih, daftar hitam, dan operasi lainnya

### Ikat nama domain khusus
Di halaman custom domain, ikat nama domain yang ada di cloudflare. Nama domain yang dihosting oleh cloudflare akan secara otomatis mengubah catatan dns.
![2](https://telegraph-image.pages.dev/file/29546e3a7465a01281ee2.png)

### Aktifkan tinjauan gambar
1. Silakan buka https://moderatecontent.com/ untuk mendaftar dan mendapatkan kunci API gratis untuk memoderasi konten gambar

2. Buka halaman manajemen Halaman Cloudflare, klik `Pengaturan`, `Variabel Lingkungan`, `Tambahkan Variabel Lingkungan`

3. Tambahkan `nama variabel` sebagai `ModerateContentApiKey`, `nilai` sebagai `kunci API` yang baru saja Anda peroleh pada langkah pertama, klik `Simpan`.

Catatan: Karena perubahan akan berlaku selama penerapan berikutnya, Anda mungkin juga perlu masuk ke halaman `Penerapan` dan menerapkan ulang proyek.

Setelah mengaktifkan peninjauan gambar, pemuatan gambar pertama akan lambat karena peninjauan memerlukan waktu. Pemuatan gambar selanjutnya tidak akan terpengaruh karena cache.
![3](https://telegraph-image.pages.dev/file/bae511fb116b034ef9c14.png)

### membatasi
1. Karena file gambar sebenarnya disimpan di Telegraph, Telegraph membatasi ukuran gambar yang diunggah maksimal 5 MB.

2. Karena penggunaan jaringan Cloudflare, kecepatan memuat gambar mungkin tidak terjamin di beberapa area.

3. Fungsi Cloudflare versi gratis memiliki batas harian 100.000 permintaan (yaitu, jumlah total unggahan atau pemuatan gambar tidak boleh melebihi 100.000 kali). Jika melebihi batas, Anda mungkin perlu membeli paket Fungsi Cloudflare berbayar .Jika fungsi manajemen gambar diaktifkan, juga akan ada sejumlah operasi KV.batas, jika melebihi batas, Anda perlu membeli paket berbayar

### bersyukur
Ide dan kode disediakan oleh Hostloc @feixiang dan @wulaca

## Perbarui log
18 Januari 2023--Pembaruan fungsi manajemen gambar

1. Mendukung fungsi manajemen gambar, yang dinonaktifkan secara default. Jika Anda ingin mengaktifkannya, silakan buka latar belakang setelah penerapan dan klik `Pengaturan`->`Fungsi`->`KV Namespace Binding`->`Edit Binding`->` Isi nama variabel: `img_url` `KV namespace` Pilih ruang penyimpanan KV yang Anda buat sebelumnya, buka dan kunjungi http(s)://nama domain Anda/admin untuk membuka halaman manajemen latar belakang
| nama variabel | Ruang nama KV |
| ----------- | ----------- |
| img_url | Pilih ruang penyimpanan KV yang dibuat sebelumnya |

![](https://im.gurl.eu.org/file/a0c212d5dfb61f3652d07.png)
![](https://im.gurl.eu.org/file/48b9316ed018b2cb67cf4.png)

2. Fungsi verifikasi login baru telah ditambahkan ke halaman manajemen backend. Fungsi ini dinonaktifkan secara default. Jika Anda ingin mengaktifkannya, silakan buka backend setelah penerapan dan klik `Pengaturan`->`Variabel Lingkungan`-> `Tentukan variabel untuk lingkungan produksi`->`Edit variabel ` Tambahkan variabel yang ditunjukkan pada tabel berikut untuk mengaktifkan verifikasi login
| nama variabel | nilai |
| ----------- | ----------- |
|BASIC_USER = | <nama pengguna login halaman manajemen backend>|
|BASIC_PASS = | <Kata sandi pengguna login halaman manajemen backend>|

![](https://im.gurl.eu.org/file/dff376498ac87cdb78071.png)

Tentu saja, Anda juga tidak dapat mengatur kedua nilai ini, sehingga tidak diperlukan verifikasi saat mengakses halaman manajemen backend dan langkah login langsung dilewati.Desain ini memungkinkan Anda untuk menggunakannya bersama dengan Cloudflare Access untuk mendukung login kode verifikasi email dan login akun Microsoft. Fungsi seperti login akun Github dapat diintegrasikan dengan metode login asli pada nama domain Anda. Tidak perlu mengingat set kata sandi akun backend tambahan. Untuk cara menambahkan Akses Cloudflare, silakan lihat resminya dokumentasi Perhatikan bahwa jalur yang dilindungi mencakup /admin dan /api/manage/*

3. Statistik jumlah gambar baru
Bila fungsi manajemen gambar diaktifkan, jumlah gambar dalam rekaman dapat dilihat di bagian atas latar belakang

![](https://im.gurl.eu.org/file/b7a37c08dc2c504199824.png)

4. Menambahkan pencarian nama file gambar
Saat fungsi manajemen gambar diaktifkan, Anda dapat menggunakan nama file gambar di kotak pencarian latar belakang untuk mencari dan menemukan gambar yang perlu dikelola dengan cepat.

![](https://im.gurl.eu.org/file/faf6d59a7d4a48a555491.png)

5. Menambahkan tampilan status gambar
Ketika fungsi manajemen gambar diaktifkan, status gambar saat ini dapat dilihat di latar belakang { "ListType": "None", "TimeStamp": 1673984678274 }
ListType mewakili apakah gambar tersebut saat ini ada dalam daftar hitam putih, Tidak ada berarti tidak ada dalam daftar hitam atau daftar putih, Putih berarti ada dalam daftar putih, Blok berarti tidak ada dalam daftar hitam, dan TimeStamp adalah stempel waktu saat gambar pertama kali dimuat, jika diaktifkan Image review API maka hasil review gambar juga akan ditampilkan disini dan ditandai dengan Label

![](https://im.gurl.eu.org/file/6aab78b83bbd8c249ee29.png)

6. Menambahkan fungsi daftar hitam
Ketika fungsi manajemen gambar diaktifkan, gambar dapat ditambahkan secara manual ke daftar hitam di latar belakang. Gambar yang ditambahkan ke daftar hitam tidak akan dimuat secara normal.

![](https://im.gurl.eu.org/file/fb18ef006a23677a52dfe.png)

7. Menambahkan fungsi daftar putih
Ketika fungsi manajemen gambar diaktifkan, gambar dapat ditambahkan secara manual ke daftar putih di latar belakang. Gambar yang ditambahkan ke daftar putih akan tetap dimuat secara normal, dan hasil tinjauan gambar API dapat dilewati.

![](https://im.gurl.eu.org/file/2193409107d4f2bcd00ee.png)

8. Menambahkan fungsi penghapusan catatan
Ketika fungsi manajemen gambar diaktifkan, rekaman gambar dapat dihapus secara manual di latar belakang, yaitu gambar tidak akan lagi ditampilkan di latar belakang kecuali seseorang mengunggah dan memuat gambar itu lagi. Perhatikan bahwa karena gambar disimpan di server telegraf, kami tidak dapat menghapus gambar asli yang diunggah, pemuatan gambar hanya dapat diblokir melalui fungsi daftar hitam pada poin 6 di atas.

9. Mode berjalan program baru: mode daftar putih
Ketika fungsi manajemen gambar diaktifkan, selain mode default, pembaruan ini juga menambahkan mode operasi baru. Dalam mode ini, hanya gambar yang ditambahkan ke daftar putih yang akan dimuat, dan gambar yang diunggah perlu ditinjau dan disetujui. mencegah pemuatan gambar buruk semaksimal mungkin. Jika Anda ingin mengaktifkannya, harap atur variabel lingkungan: WhiteList_Mode=="true"

10. Menambahkan fungsi pratinjau gambar latar belakang
Saat fungsi manajemen gambar diaktifkan, gambar yang dimuat melalui nama domain Anda dapat dipratinjau di latar belakang. Klik pada gambar untuk memperbesar, memperkecil, memutar, dan operasi lainnya.

![](https://im.gurl.eu.org/file/740cd5a69672de36133a2.png)

## Sudah di-deploy, bagaimana cara memperbaruinya?
Sebenarnya updatenya sangat sederhana, Anda hanya perlu mengacu pada konten update di atas, pertama masuk ke backend Cloudflare Pages, atur variabel lingkungan yang perlu Anda gunakan terlebih dahulu dan ikat ke namespace KV, lalu buka Github dan pilih gudang yang telah Anda fork sebelumnya. Sinkronkan garpu`->`Perbarui cabang`. Tunggu sebentar. Cloudflare Pages akan secara otomatis menyebarkan kode terbaru setelah mendeteksi bahwa gudang Anda telah diperbarui.

## Beberapa batasan:
Cloudflare KV hanya memiliki 1.000 kuota tulis gratis per hari. Setiap gambar baru yang dimuat akan menempati kuota tulis ini. Jika kuota ini terlampaui, latar belakang pengelolaan gambar tidak akan dapat merekam gambar yang baru dimuat.

Hingga 100.000 operasi baca gratis per hari. Kuota ini akan terisi setiap kali gambar dimuat (jika tidak ada cache, jika nama domain Anda di-cache di Cloudflare, kuota hanya akan terisi ketika cache hilang), melebihi daftar hitam putih Fungsi lain mungkin gagal

Ada maksimal 1.000 penghapusan gratis per hari. Setiap rekaman gambar akan menempati kuota ini. Jika melebihi batas, rekaman gambar tidak dapat dihapus.

Maksimum 1.000 operasi listing gratis per hari. Setiap kali latar belakang/admin dibuka atau disegarkan, kuota ini akan terisi. Jika melebihi batas, akan dilakukan pengelolaan gambar latar belakang.

Dalam kebanyakan kasus, kuota gratis pada dasarnya cukup, dan dapat sedikit terlampaui. Jika terlampaui, maka akan segera dinonaktifkan. Setiap kuota dihitung secara terpisah. Jika suatu operasi melebihi kuota gratis, hanya operasi tersebut yang akan dinonaktifkan. Itu tidak mempengaruhi fungsi lainnya, yaitu meskipun kuota menulis bebas saya habis, fungsi membaca dan menulis saya tidak terpengaruh, dan gambar dapat dimuat secara normal, tetapi saya tidak dapat melihat gambar baru di latar belakang pengelolaan gambar.

Jika kuota gratis Anda tidak mencukupi, Anda dapat membeli Cloudflare Workers versi berbayar dari Cloudflare. Harganya mulai dari $5 per bulan dan dikenakan biaya sesuai penggunaan Anda. Tidak ada batasan kuota yang disebutkan di atas.

Selain itu, perubahan yang dilakukan pada variabel lingkungan akan berlaku selama penerapan berikutnya. Jika Anda mengubah `variabel lingkungan` dan mengaktifkan atau menonaktifkan fungsi tertentu, harap ingat untuk menerapkan ulang.

![](https://im.gurl.eu.org/file/b514467a4b3be0567a76f.png)

### Sponsor
Proyek ini diuji dengan BrowserStack.

Proyek ini didukung oleh [Cloudflare](https://www.cloudflare.com/).
