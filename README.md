# sefruit shop

# Tugas 7
## Jelaskan apa itu widget tree pada Flutter dan bagaimana hubungan parent-child (induk-anak) bekerja antar widget.
Widget tree adalah struktur 'tree' yang merepresentasikan semua widget yang menyusun tampilan aplikasi Flutter.

Parent widget menentukan struktur dan aturan layout untuk child widget e.g. Column adalah parent yang menentukan children ditumpuk vertikal.
Child widget mendapat constraints (batas ukuran) dari parent dan render sesuai aturan tersebut.
## Sebutkan semua widget yang kamu gunakan dalam proyek ini dan jelaskan fungsinya.
1. Scaffold: Framework untuk AppBar dan body
2. AppBar: Ruang yang ada di atas layar (seperti head pada html (?))
3. Padding: Padding untuk mengelilingi body
4. Column: Menyusun children dari atas ke bawah (Row, SizedBox, Center)
5. Row: Menyusun children dari kiri ke kanan (NPM, Name, Class)
6. SizedBox: Memberikan padding antar children (Vertikal 16px)
7. Center: Memastikan children ada di tengah (Selamat datang di Sefruit Shop)
8. Text: self explanatory
9. GridView.count: Menunjukkan daftar item dalam grid dengan 3 kolom
10. Card: Membuat kotak card dengan shadow (ItemCard)
11. Container: Ruang untuk menata padding, size, etc.
12. Material: Memberi bg color dari tema app
13. InkWell: Membuat widget bersifat touchable
14. Icon: Menampilkan icon
15. SnackBar: Menampilkan pesan singkat di bawah layar
16. ScaffoldMessenger: Menentukan kapan SnackBar show/hide
17. MaterialApp: Root
18. ThemeData: Theme yang bersifat global
## Apa fungsi dari widget MaterialApp? Jelaskan mengapa widget ini sering digunakan sebagai widget root.
MaterialApp berfungsi untuk menyediakan tema, routing, localization, app title, home widget, dan sbg. Ini sering dijadikan root karena MaterialApp menyediakan konteks Material lengkap. Tanpa ini, widget seperti Scaffold, AppBar, ikon Material, dan button Material tidak akan berfungsi dengan benar.
## Jelaskan perbedaan antara StatelessWidget dan StatefulWidget. Kapan kamu memilih salah satunya?
StatelessWidget bersifat statis dan hanya perlu dibuild sekali, sedangkan StatefulWidget bisa berubah selama app berjalan. Jika interface tidak perlu berubah, gunakan StatelessWidget. Jika tidak, gunakan StatefulWidget.
## Apa itu BuildContext dan mengapa penting di Flutter? Bagaimana penggunaannya di metode build?
BuildContext adalah objek yang merepresentasikan posisi widget dalam widget tree. Ini penting karena dengan context, widget bisa:
1. Mendapat screen size
2. Mendapat tema
3. Routing
4. Find parent widget melalui tree

Contoh penggunaan:
```dart
@override
Widget build(BuildContext context) {
  return Scaffold(
    appBar: AppBar(
      title: Text("Contoh", style: Theme.of(context).textTheme.headlineMedium),
    ),
  );
}
```
## Jelaskan konsep "hot reload" di Flutter dan bagaimana bedanya dengan "hot restart".
Hot reload: 
1. Apply changes ke app tanpa menghentikan state yang sedang berjalan,
2. UI langsung  (StatefulWidget tidak!)
Hot restart: Restart aplikasi dari awal (self explanatory)
## Implementasi Checklist
1. new menu.dart
2. move main.dart classes to menu.dart
3. change main.dart colorscheme to blue
4. edit menu.dart's myhomepage, add class infocard, class itemhomepage
5. add list itemhomepage at myhomepage, add class itemcard

# Tugas 8
##  Jelaskan perbedaan antara Navigator.push() dan Navigator.pushReplacement() pada Flutter. Dalam kasus apa sebaiknya masing-masing digunakan pada aplikasi Football Shop kamu?
Navigator.push() menambahkan page baru di atas page sekarang, dan kita bisa kembali ke page sekarang nanti. Navigator.pushReplacement() mengganti page sekarang dengan page baru, jadi kita tidak bisa kembali ke page sekarang.
Pada Football Shop ini, Navigator.push() digunakan untuk page yang memungkinkan user untuk "Back" nanti, sedangkan Navigator.pushReplacement() digunakan sebaiknya digunakan untuk page seperti save product.
## Bagaimana kamu memanfaatkan hierarchy widget seperti Scaffold, AppBar, dan Drawer untuk membangun struktur halaman yang konsisten di seluruh aplikasi?
Pada Football Shop ini, setiap halaman menggunakan Scaffold (untuk kerangka utama). AppBar (page title, navbar, etc) digunakan bila seperlunya saja, untuk kasus ini title pada menu.dart dan form.dart. Drawer digunakan untuk seluruh halaman, dan cukup memanngil LeftDrawer().
## Dalam konteks desain antarmuka, apa kelebihan menggunakan layout widget seperti Padding, SingleChildScrollView, dan ListView saat menampilkan elemen-elemen form? Berikan contoh penggunaannya dari aplikasi kamu.
1. Padding: Memberikan jarak. Jika jarak antarteks terlalu 'padat', aplikasi susah dibaca. e.g. padding pada form
2. SingleChildScrollView: Membuat agar page memiliki fitur scroll, jika isi page terlalu banyak (tinggal scroll down). e.g. form.dart
3. ListView: Mirip Column tapi tak perlu adanya SingleChildScrollView, dan juga mendukung lazy loading. e.g. left_drawer.dart
## Bagaimana kamu menyesuaikan warna tema agar aplikasi Football Shop memiliki identitas visual yang konsisten dengan brand toko?
Set colorScheme pada theme di main.dart
## Implementasi Checklist
1. left_drawer.dart on lib/widgets
2. routing to drawer
3. add drawer to menu.dart
4. productlist_form.dart on lib
5. create product routing on menu.dart