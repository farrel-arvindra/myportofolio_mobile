# myportofolio_mobile

Aplikasi portofolio sederhana yang dibuat dengan Flutter.

## Tugas 7 — Widget Flutter

### 1. Widget tree dan hubungan induk-anak

*Widget tree* adalah susunan hierarkis widget yang mendeskripsikan antarmuka aplikasi Flutter. Setiap widget dapat memiliki satu atau lebih widget anak. Widget induk menentukan cara anak-anaknya disusun atau diberi tampilan, sedangkan widget anak menyediakan bagian antarmuka yang lebih kecil.

Contohnya, `MaterialApp` menjadi induk tingkat atas bagi halaman `MyHomePage`. Di halaman tersebut, `Scaffold` berisi `AppBar` dan `body`; `Column` di dalam `body` mengatur anak seperti `Row`, `SizedBox`, dan `Center`. Hubungan tersebut membentuk cabang-cabang pohon. Flutter membangun ulang bagian yang diperlukan ketika konfigurasi widget berubah.

### 2. Widget yang digunakan dalam proyek

Berikut widget yang digunakan oleh antarmuka aplikasi, termasuk widget khusus yang didefinisikan di proyek:

| Widget | Fungsi |
| --- | --- |
| `MyApp` | Widget khusus yang menjadi titik awal konfigurasi aplikasi. |
| `MaterialApp` | Menyediakan kerangka aplikasi bergaya Material, tema, judul, dan halaman awal. |
| `MyHomePage` | Widget khusus untuk menyusun halaman utama portofolio. |
| `Scaffold` | Menyediakan struktur dasar halaman, seperti `AppBar` dan area `body`. |
| `AppBar` | Menampilkan bilah atas dengan judul aplikasi. |
| `Text` | Menampilkan teks judul, informasi pengguna, sambutan, dan label menu. |
| `Padding` | Memberikan jarak di sekeliling konten atau anak widget. |
| `Column` | Menyusun anak-anak secara vertikal. |
| `Row` | Menyusun kartu informasi secara horizontal. |
| `InfoCard` | Widget khusus yang menampilkan judul dan isi informasi dalam sebuah kartu. |
| `Card` | Memberikan tampilan kartu pada informasi. |
| `Container` | Menampung dan mengatur ukuran, padding, dan isi kartu. |
| `SizedBox` | Memberi jarak tetap di antara elemen. |
| `Center` | Menempatkan konten anak di tengah ruang yang tersedia. |
| `GridView.count` | Menampilkan item menu dalam kisi dengan jumlah kolom yang ditentukan. |
| `ItemCard` | Widget khusus untuk menampilkan satu item menu yang dapat ditekan. |
| `Material` | Menyediakan permukaan Material dan warna latar untuk kartu menu. |
| `InkWell` | Menambahkan respons sentuhan dan menjalankan aksi ketika kartu ditekan. |
| `Icon` | Menampilkan ikon untuk setiap item menu. |
| `SnackBar` | Menampilkan pesan sementara setelah item menu ditekan. |

`ItemHomepage` bukan widget, melainkan kelas model data yang menyimpan nama, ikon, dan warna setiap item menu. `Theme.of(context)` dan `MediaQuery.of(context)` juga digunakan untuk membaca tema serta ukuran layar; keduanya adalah API, bukan widget yang ditampilkan langsung.

### 3. Fungsi `MaterialApp`

`MaterialApp` menyiapkan fitur umum aplikasi yang mengikuti Material Design, seperti konfigurasi tema, navigasi/rute, lokalisasi, dan halaman awal melalui properti `home`. Widget ini umum dijadikan *root widget* karena menyediakan konteks serta infrastruktur Material bagi widget-widget di bawahnya. Dalam proyek ini, `MyApp` mengembalikan `MaterialApp` dengan tema aplikasi dan `MyHomePage` sebagai halaman awal.

### 4. `StatelessWidget` dan `StatefulWidget`

- `StatelessWidget` tidak menyimpan state yang berubah selama widget hidup. Widget ini cocok jika tampilannya hanya bergantung pada konfigurasi atau data yang diterima, misalnya `MyApp`, `MyHomePage`, `InfoCard`, dan `ItemCard` dalam proyek ini.
- `StatefulWidget` dipakai jika tampilan perlu mengikuti state yang dapat berubah selama widget hidup. State disimpan pada objek `State`, lalu perubahan yang memengaruhi tampilan biasanya diberitahukan dengan `setState`.

Pilih `StatelessWidget` untuk tampilan yang tidak mengelola state lokal yang berubah. Pilih `StatefulWidget` ketika widget perlu mengelola perubahan lokal seperti pilihan, input, atau status pemuatan. Interaksi tidak otomatis mengharuskan `StatefulWidget`: `ItemCard` tetap stateless karena hanya meminta `ScaffoldMessenger` menampilkan `SnackBar`, tanpa mengubah state tampilannya sendiri.

### 5. `BuildContext`

`BuildContext` adalah referensi ke lokasi sebuah widget di dalam widget tree. Flutter memberikannya ke metode `build`, dan konteks tersebut dapat digunakan untuk mencari informasi atau layanan dari widget leluhur. Contohnya, kode proyek memakai `Theme.of(context)` untuk mengambil skema warna tema, `MediaQuery.of(context)` untuk membaca lebar layar, dan `ScaffoldMessenger.of(context)` untuk menampilkan `SnackBar`.

Karena konteks terkait dengan posisi widget, pemanggilan seperti `Theme.of(context)` hanya dapat menemukan penyedia yang berada di atas widget tersebut pada tree. Konteks bukan widget dan tidak sebaiknya disimpan untuk digunakan sembarangan setelah widget dilepas dari tree.

### 6. *Hot reload*, *hot restart*, dan *full restart*

- **Hot reload** menerapkan perubahan kode Dart ke aplikasi yang sedang berjalan tanpa memulai ulang aplikasi. Umumnya state yang sedang aktif dipertahankan sehingga perubahan UI dapat dilihat dengan cepat.
- **Hot restart** memulai ulang isolate Dart dan menjalankan kembali aplikasi dari awal. State dalam memori akan di-reset, tetapi proses aplikasi/platform tidak dimulai ulang sepenuhnya.
- **Full restart** menghentikan lalu menjalankan kembali aplikasi, termasuk proses native/platform. Ini diperlukan untuk menerapkan perubahan yang tidak dapat dimuat ulang hanya dengan memulai ulang kode Dart.

Hot reload tidak cukup jika perubahan menyangkut inisialisasi yang hanya berjalan saat startup dan perlu dijalankan ulang, atau perubahan struktur state yang tidak dapat dipertahankan dengan aman. Gunakan hot restart untuk mengulang alur Dart dari awal. Gunakan full restart, misalnya, setelah mengubah kode native Android/iOS, konfigurasi native, atau menambahkan plugin/dependensi yang memerlukan integrasi platform baru. Kebutuhan pastinya bergantung pada jenis perubahan dan dukungan tool/platform.

## AI Disclosure

Penjelasan pada bagian Tugas 7 disusun dengan bantuan AI berdasarkan kode Flutter dalam proyek ini. Pemilik proyek tetap bertanggung jawab untuk meninjau dan memastikan isi dokumentasi sesuai dengan implementasi.
