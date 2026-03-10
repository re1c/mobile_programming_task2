# Tugas 2: Eksplorasi Widget Layout di Flutter

Repositori ini berisi pengerjaan Tugas 2, di mana fokus utamanya adalah membangun antarmuka pengguna (UI) menggunakan kombinasi berbagai Widget dasar pada Flutter, seperti `Column`, `Row`, dan `Container`.

## Penjelasan Komponen Widget yang Digunakan

Berikut adalah analisis dan penjelasan mengenai fungsi masing-masing *Widget* yang digunakan dalam kode aplikasi ini:

### 1. `MaterialApp`
Widget ini merupakan fondasi utama dari aplikasi Flutter yang menerapkan *Material Design*. `MaterialApp` bertindak sebagai pembungkus (*wrapper*) teratas yang mengatur tema global aplikasi (melalui parameter `ThemeData`), sistem navigasi (*routing*), dan menentukan halaman beranda awal (`home`). 

### 2. `Scaffold`
`Scaffold` mendasari kerangka struktur visual standar untuk satu halaman penuh layar. Widget ini mempermudah penyusunan UI karena secara otomatis menyediakan slot khusus untuk elemen-elemen kerangka utama sistem navigasi, seperti `AppBar` (di bagian atas layar), `body` (area konten di tengah), hingga properti melayang seperti `FloatingActionButton`.

### 3. `AppBar`
Merupakan representasi fungsi bilah navigasi aplikasi (*Application Bar*) yang diletakkan di bagian paling atas layar. Pada proyek ini, `AppBar` digunakan untuk menampilkan judul ("My first app") dan menerima kustomisasi melalui properti `centerTitle: true` agar teks terpusat secara rapi, serta mengatur latar belakang agar lebih kalem menggunakan paduan nilai `backgroundColor`.

### 4. `Column`
`Column` adalah *layout widget* fundamental yang menyusun anak-anaknya (*children*) menurun secara vertikal dari atas ke bawah. Seluruh blok elemen di halaman beranda aplikasi ini—mulai dari blok gambar luas, teks pertanyaan di tengah, hingga deretan ikon di bagian bawah—secara solid dibungkus dalam sebuah `Column` sehingga menyatu dan tidak saling tumpang tindih.

### 5. `Row`
Kebalikan dari `Column`, `Row` menyusun anak-anaknya secara horizontal dan membentang dari arah kiri ke kanan. Widget ini digunakan di bagian dalam kotak kuning terbawah guna menjejerkan tiga kelompok interaki ("Food", "Scenery", "People"). Jarak tata letaknya disempurnakan dengan konfigurasi `mainAxisAlignment: MainAxisAlignment.spaceEvenly` sehingga secara otomatis mendistribusikan spasi rasional dan merata di antara seluruh komponen.

### 6. `Container`
`Container` ibarat sebuah kotak fleksibel serbaguna (analoginya menyerupai `<div>` dalam ekosistem *web programming*). Widget ini membungkus widget lain sekaligus memberikan keleluasaan pengaturan tata letak fisik, seperti batas luar (`margin`), batas kedalaman di dalam konten (`padding`), maupun penegasan warna dasar. Pada proyek kita, `Container` lah pahlawan di balik blok-blok yang menampilkan sorotan warna *cyan*, *pink* keputihan, dan aksen kuning.

### 7. `AspectRatio`
Sesuai namanya, widget ini mengambil kendali rasio dimensi elemen. `AspectRatio(aspectRatio: 1.0)` digunakan pada foto utamanya untuk secara sistematis memaksa *container* yang membungkus gambar agar tinggi lebarnya selalu identik, menciptakan sebuah wadah kotak dengan persepsi fisik seimbang yang senantiasa harmonis 1:1.

### 8. `Center`
Sebuah *layout widget* sederhana namun krusial, berfungsi memusatkan *widget* di dalamnya secara kokoh ke tengah ruang elemen yang dimilikinya. Pada struktur program, ia digunakan untuk membungkus `Image` guna memastikannya tampil memusat tanpa tergeser saat menyesuaikan posisi kontainernya.

### 9. `Image.network`
Pengkonstruksi (*constructor*) ini difungsikan untuk mengambil dan memunculkan gambar langsung di UI secara *real-time* bersumber dari jejambat internet (`URL`). Melalui layanan seperti *picsum* di program ini, pengguna dipastikan melihat gambar yang terpanggil hanya dengan "hot-linking", menghindari pemuatan muatan gambar mentah secara berlebihan di ruang pemyimpanan internal lokal.

### 10. `Text`
Merupakan jembatan komunikasi statis utama di UI guna menarasikan untaian nilai literal ke atas layar. Di aplikasi ini, parameter `Text` banyak digabungkan dengan `TextStyle` guna mendikte kebebasan tipe font, ketebalan karakter (*font weight*), dan ukuran sehingga mampu membedakan hierarki informasi judul dibanding teks penjelasan biasa.

### 11. `Icon`
Terinspirasi dari desain fungsionalis, `Icon` bertugas untuk memanggil dan merender piktogram visual dari kustomisasi pustaka font ikon yang seragam (seperti pustaka *Material Icons* bawaan). Ikon fungsional seperti `Icons.restaurant`, `Icons.umbrella`, dan `Icons.person` memicu abstraksi visual yang mampu berbicara secara universal jauh melampaui rentetan teks, sekaligus hemat dari sisi komputasi pemuatan tampilan grafis layar.

### 12. `MediaQuery`
Meski secara struktur ia merupakan entitas pengakses kelas dan lazim digunakan sebagai `MediaQuery.of(context)`, elemen logik internal ini memitigasi isu fragmentasi ukuran perangkat dengan mengambil status lebar/tinggi sesungguhnya layar di setiap resolusi ponsel yang berbeda. Implementasi pemanggilan dimensi ukuran (*size width*) memastikan `Container` memiliki kesadaran adaptif untuk senantiasa membentang utuh merapat dengan batas maksimal lebar tampilan gawai (*device*).

---

*Proyek ini diformat sebagai pemahaman teknikal dasar tentang hierarki, modifikasi komunal dan kapabilitas rendering antarmuka berbasis kerangka Material pada instrumen pengembangan Flutter.*
