# Tugas 2: Membangun Antarmuka Pengguna (UI) Dasar di Flutter

Repositori ini berisi implementasi Tugas 2 untuk praktikum Pemrograman Perangkat Bergerak. Fokus utama dari tugas ini adalah memahami dan mempraktikkan penggunaan komponen tata letak (*layouting*) dasar di Flutter, seperti `Column`, `Row`, dan `Container`, guna membangun antarmuka yang responsif dan sesuai dengan prinsip *Material Design*.

Dokumentasi ini akan membedah kode sumber pada `lib/main.dart` langkah demi langkah, menjelaskan fungsi setiap *widget* secara rinci, rasionalisasi penempatannya, dan penerapan praktik terbaik (*best practice*) dalam menata antarmuka aplikasi.

---

## Bedah Kode: `lib/main.dart`

Berikut adalah analisis komponen dari aplikasi yang dibangun, diurutkan berdasarkan alur eksekusi widget.

### 1. Titik Masuk Aplikasi (*Entry Point*)

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}
```

* **`import 'package:flutter/material.dart';`**: Baris ini mengimpor pustaka inti *Material Design* dari Flutter. Pustaka ini menyediakan sekumpulan komponen (*widget*) standar yang sudah mematuhi pedoman desain antarmuka Google (seperti tombol, *app bar*, efek bayangan, dll).
* **`void main()`**: Fungsi utama yang akan dieksekusi pertama kali saat aplikasi run-time Flutter dijalankan.
* **`runApp()`**: Fungsi ini mengambil *widget* utama (dalam hal ini `MyApp`) dan menjadikannya sebagai akar (*root*) dari *widget tree* aplikasi.
* **`const`**: Penggunaan *modifier* `const` pada `MyApp()` sangat disarankan sebagai *best practice*. Ini memberi tahu kompilator Dart bahwa *widget* ini bersifat *immutable* (tidak akan berubah). Dengan begitu, saat status aplikasi ada yang berubah, sistem Flutter tidak perlu merender ulang (*rebuild*) bagian ini, sehingga performa aplikasi menjadi jauh lebih optimal.

### 2. Konfigurasi Tema dan Rute Utama (`MyApp`)

```dart
class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        colorScheme: ColorScheme.fromSeed(seedColor: Colors.deepPurple),
        useMaterial3: true,
      ),
      home: const RowColumnPage(),
    );
  }
}
```

* **`StatelessWidget`**: `MyApp` mewarisi `StatelessWidget` karena pada level ini, aplikasi hanya bertugas menetapkan konfigurasi tema awal dan rute tanpa menyimpan data (status) yang berubah-ubah secara dinamis.
* **`MaterialApp`**: Ini adalah *widget* pembungkus utama yang menyediakan sistem dasar bagi aplikasi, seperti pengaturan tema, lokalisasi, dan alur navigasi halaman (*routing*).
* **`ThemeData` & `colorScheme`**: Bagian ini menetapkan skema warna global aplikasi. Menggunakan `ColorScheme.fromSeed()` memungkinkan Flutter secara otomatis menghasilkan palet warna lengkap (untuk mode terang/gelap) yang saling melengkapi dan harmonis, hanya dengan bermodalkan satu warna dasar (`Colors.deepPurple`).
* **`useMaterial3: true`**: Mengaktifkan pedoman *Material Design 3* secara bawaan. Ini memberikan sentuhan visual yang modern, seperti jarak komponen yang lebih proporsional dan ujung-ujung komponen yang secara *default* lebih melengkung.
* **`home`**: Menentukan *widget*/halaman pertama yang akan dimuat saat aplikasi selesai diinisialisasi; pada project ini menunjuk ke kelas `RowColumnPage`.

### 3. Kerangka Dasar Halaman: `Scaffold` dan `AppBar`

```dart
class RowColumnPage extends StatelessWidget {
  const RowColumnPage({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text(
          'My first app',
          style: TextStyle(color: Colors.black, fontWeight: FontWeight.normal),
        ),
        backgroundColor: Colors.orange[200],
        centerTitle: true,
      ),
```

* **`Scaffold`**: *Widget* ini berfungsi sebagai kerangka dasar sebuah halaman layar penuh. Ia mengatur manajemen tata letak agar komponen umum aplikasi—seperti `AppBar` (di atas), `body` (konten utama), hingga `BottomNavigationBar`—dapat ditempatkan ke *slot*-nya masing-masing secara rapi tanpa bertabrakan.
* **`AppBar`**: Menampilkan bilah navigasi statis di bagian atas layar.
    * **`title`**: Menyisipkan komponen `Text` untuk menampilkan judul halaman.
    * **`TextStyle`**: Dikustomisasi agar warna teks menjadi hitam (`Colors.black`) dengan ketebalan huruf normal (`fontWeight.normal`) sehingga terlihat lebih kasual dan tidak terlalu berat.
    * **`backgroundColor`**: Mengubah warna dasar *app bar* menggunakan palet warna *orange* yang lembut (`Colors.orange[200]`).
    * **`centerTitle: true`**: Memastikan judul selalu berada tepat di tengah. Hal ini penting untuk menjaga konsistensi tampilan lintas-perangkat (mengingat OS Android secara bawaan cenderung membuat teks rata kiri).

### 4. Menyusun Tata Letak Vertikal: `Column`

```dart
      body: Column(
        crossAxisAlignment: CrossAxisAlignment.center,
        children: <Widget>[
```

* Setelah `AppBar`, kita mulai merangkai isi antarmuka utama di dalam properti **`body`**.
* **`Column`**: *Widget* *layout* ini bertugas untuk menyusun elemen-elemen anaknya (*children*) secara vertikal dari arah atas menurun ke bawah. Seluruh susunan kotak konten yang ada di halaman beranda kita diwadahi oleh komponen ini.
* **`crossAxisAlignment.center`**: Parameter ini memaksa setiap anak di dalam struktur `Column` untuk diposisikan di tengah layar berdasarkan sumbu silangnya (sumbu horizontal).

### 5. Memuat Gambar secara Presisi dan Responsif

```dart
          AspectRatio(
            aspectRatio: 1.0,
            child: Container(
              width: MediaQuery.of(context).size.width,
              margin: const EdgeInsets.fromLTRB(20.0, 20.0, 20.0, 10.0),
              padding: const EdgeInsets.all(20.0),
              color: Colors.cyan[100],
              child: Center(
                child: Image.network(
                  'https://picsum.photos/200',
                  fit: BoxFit.cover,
                  width: 500,
                ),
              ),
            ),
          ),
```

* **`AspectRatio`**: *Widget* ini mengunci anak di dalamnya (yakni blok *Container* biru) agar selalu mempertahankan rasio dimensi bujur sangkar murni (`aspectRatio: 1.0`). Strategi ini mencegah antarmuka layarnya patah (*layout shift/jank*) saat perangkat membentang, juga mencegah gambar tampak pipih/distorsi merusak tata letak.
* **`Container`**: *Widget* krusial yang digunakan secara intensif di Flutter. Ia memadukan kemampuan *sizing* (ukuran), *positioning* (posisi), *padding*, serta pewarnaan dekoratif (*painting*).
    * Di dalamnya, **`width`** ditentukan dengan `MediaQuery.of(context).size.width`. Menggunakan *MediaQuery* adalah *best practice* dalam desain responsif karena membuat kontainer ini dinamis melebar selebar resolusi maksimal layar asal (*device*), berapapun ukurannya.
    * **`margin`** memberikan gaya jarak estetis terhadap elemen lain di luarnya (mencegah himpitan), sementara **`padding`** memberikan sisa batasan bernapas bagi ruang pelukisan di dalam lingkar luarnya. Latar dimensinya lantas diwarnai terang menggunakan paramater **`color`** `Colors.cyan[100]`.
* **`Center`**: Komposisi *layout* yang mengunci presisi suatu elemen/obyek agar tegak berdiri membentang lurus tepat pada sumbu titik berat ruang pembungkusnya.
* **`Image.network`**: Sub-sistem pembangun yang merender aset gambar langsung lewat intervensi jaringan/internet (*hot-linking* url `picsum`), sebuah praktik untuk menghindari penyimpanan *internal asset footprint* berukuran tambun apabila rilis produk menuntut ukurannya diminimalkan sejak fase prototipe.
    * Parameter **`fit: BoxFit.cover`** adalah proteksi penting untuk menyikapi resiko rupa gambar web yang resolusi aslinya sering berbeda (asimetris). Opsi 'cover' menetapkan gambar harus direnggangkan penuh menutupi area kanvas wadahnya tanpa mengurangi rasio aslinya; area berlebihnya secara otomatis disembunyikan (*clip*), memastikan gambar senantiasa artistik dan pas.

### 6. Menampilkan Ruang Penegas Baris Teks (*Text Container*)

```dart
          Container(
            width: MediaQuery.of(context).size.width,
            margin: const EdgeInsets.fromLTRB(20.0, 5.0, 20.0, 10.0),
            padding: const EdgeInsets.all(20.0),
            color: Colors.pink[100],
            child: const Text('What image is that?', style: TextStyle(fontSize: 16)),
          ),
```

* Di dalam blok `Container` kedua—ruang kuesioner pertanyaan foto—asas komposisi margin, pewarnaan (`Colors.pink[100]`), padding, serta luasan fleksibel (algoritma `MediaQuery` atas bentangan selebar layar gawai) direplikasi selaras menerusi parameter serupa dengan blok di atasnya.
* Di dalamnya bertengger antarmuka penyampaian aksara pasif yaitu **`Text`**. Melalui injeksi parametris gaya (*styling modifier*) turunan **`TextStyle`**, besaran huruf ditingkatkan menjadi sebesar *16 logical pixels*. Hal tersebut berguna agar teks secara jelas dapat menonjol (visibilitas proporsional) tanpa terlalu agresif memotong lajur area lapang antar ruang (*whitespace/padding*).

### 7. Membingkai Tata Letak Kategori Menu Penutup Secara Horizontal (`Row` dan `Icon`)

```dart
          Container(
            width: MediaQuery.of(context).size.width,
            color: Colors.yellow[200],
            padding: const EdgeInsets.all(20.0),
            margin: const EdgeInsets.fromLTRB(20.0, 5.0, 20.0, 5.0),
            child: const Row(
              mainAxisAlignment: MainAxisAlignment.spaceEvenly,
              crossAxisAlignment: CrossAxisAlignment.start,
              children: <Widget>[
                Column(children: [Icon(Icons.restaurant), Text("Food")]),
                Column(children: [Icon(Icons.umbrella), Text("Scenery")]),
                Column(children: [Icon(Icons.person), Text("People")]),
              ],
            ),
          ),
        ],
      ),
    );
  }
}
```

* Lahan kontur terbawah berpayungkan serapan aksen *kuning lembut* (`Colors.yellow[200]`). Komposisi inti blok dasar ini memecah paradigma tata letak penempatan sumbu jatuh `Column` dengan membentangkan landasan fungsional arsitektur pilar mendatar; yakni *widget layout* **`Row`**.
    * **`Row`** menyajikan pengalokasian komponen yang melintang berurutan ke arah horizontal (kiri ke kanan).
    * Elemen parameter pemisah paling vital yang dioperasikan adalah **`mainAxisAlignment: MainAxisAlignment.spaceEvenly`**. Modifikator kalkulasi mesin rander silang orientasi ruang dimensi parameter horizontal ini bakal merapikan tumpukan jarak ketiga kategori menu, mengintervensi algoritma agar setiap spasi di sela (*gutter margin*) ketiganya terdistribusi kosong/renggang persis setara (*equivalent*). Akibatnya, elemen-elemennya seimbang tanpa menumpuk pada satu sisi (*overlapping*).
* **Eksekusi Pengulangan Bersarang (*Nesting* `Column/Row`)**: Di tiap porsi perhentian kategori anak **`Row`**, ditanamkan kembali blok turunan **`Column`** sederhana untuk mewujudkan tata susun ikon abstrak yang selalu ditaruh persis secara vertikal berbaris menaungi sub-label keterangannya; menelurkan tata-kelola struktur navigasional UI modern pada umumnya.
* **Optimalisasi Muatan Grafis Vektor (`Icon`)**: Mewujudkan wujud ikon navigasi lewat pendelegasian komponen grafis (*primitive shape render class*) bernama **`Icon`**. Menggunakan referensi bawaan pedoman statis piktogram (contohnya `Icons.restaurant`, `Icons.umbrella`, dan `Icons.person`) merupakan keputusan implementasi rekayasa antarmuka standar *(best-practice)*. Abstraksi visual native gubahan Google ini jauh lebih gampang diregistrasi, nol kelambatan muatan rasio berkas (*zero footprint download metric payload*), namun ketajaman resolusinya tak pernah pecah layaknya vektor terukur rapi meski dilihat melalui kedalaman dimensi piksel tinggi perangkat Retina kekinian.

### 8. Penambahan Interaktivitas dengan *StatefulWidget* (`CounterCard`)

```dart
          const CounterCard(),
        ],
      ),
    );
  }
}

class CounterCard extends StatefulWidget {
  const CounterCard({super.key});

  @override
  State<CounterCard> createState() => _CounterCardState();
}

class _CounterCardState extends State<CounterCard> {
  int _counter = 0; // State variabel yang akan diperbarui

  void _incrementCounter() {
    setState(() {
      _counter++; // Mengubah status dan memicu render ulang (rebuild)
    });
  }

  @override
  Widget build(BuildContext context) {
    return Container(
      margin: const EdgeInsets.fromLTRB(20.0, 5.0, 20.0, 5.0),
      padding: const EdgeInsets.all(20.0),
      width: MediaQuery.of(context).size.width,
      color: Colors.cyan[100],
      child: Row(
        mainAxisAlignment: MainAxisAlignment.spaceBetween,
        children: [
          Text("Counter here: $_counter", style: const TextStyle(fontSize: 16)),
          Container(
            color: Colors.cyan[200],
            padding: const EdgeInsets.all(5.0),
            child: IconButton(
              onPressed: _incrementCounter,
              icon: const Icon(Icons.add, color: Colors.black, size: 16),
            ),
          ),
        ],
      ),
    );
  }
}
```

* Di bagian paling bawah beranda, kita memasukkan komponen **`CounterCard`**, yang mendemonstrasikan bagaimana aplikasi Flutter menangani perubahan data secara dinamis (reaktif) melalui pewarisan **`StatefulWidget`**.
* Berbeda dengan `StatelessWidget` yang tampilannya kaku statis, `StatefulWidget` dipasangkan dengan kelas **`State`** (`_CounterCardState`). Kelas ini bertugas sebagai penyimpan memori lokal/status komponen (yakni variabel integer **`_counter`**).
* **`setState()`**: Ini adalah fungsi intervensi paling penting dalam siklus hidup antarmuka dinamis Flutter. Ketika pengguna menekan tombol penambah (diatur melalui *callback* `onPressed: _incrementCounter`), fungsi `setState()` dipanggil. Fungsi ini bukan sekadar mengubah angka `_counter` di latar belakang, namun sekaligus memberi tahu *rendering engine* Flutter bahwa status penyusun data telah berubah (*dirty state*), sehingga kerangka *widget* `CounterCard` wajib digambar ulang (*rebuild*) ke layar secepat mungkin untuk menampilkan perhitungan angka terbaru.
* Di dalam *UI/build* dari `CounterCard`, struktur kotaknya mengulangi penerapan konsep dasar sebelumnya: menggunakan `Container` sebagai latar, `padding`/`margin` sebagai ruang spasi, dan `Row` dengan parameter `mainAxisAlignment: MainAxisAlignment.spaceBetween` agar label teks angka (kiri) dan tombol (kanan) saling mendorong terpisah merapat ke tepian wadahnya masing-masing.

---

Kesimpulannya, penempatan `Row` di dalam `Column` yang disusun dan dibalut di dalam `Container` pada proyek ini menunjukkan pola umum pembuatan antarmuka (UI) dasar di Flutter. Pola ini sengaja disusun untuk memisahkan setiap komponen agar kodenya lebih bersih, mudah dibaca, dan mudah untuk dimodifikasi kembali (*maintainable*). Implementasi awal ini diharapkan dapat berfungsi dengan baik sebagai fondasi yang cukup kokoh bagi pengembangan halaman atau fitur aplikasi yang lebih kompleks ke depannya.
