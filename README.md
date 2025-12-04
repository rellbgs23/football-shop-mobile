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

# Tugas 9
## Jelaskan mengapa kita perlu membuat model Dart saat mengambil/mengirim data JSON? Apa konsekuensinya jika langsung memetakan Map<String, dynamic> tanpa model (terkait validasi tipe, null-safety, maintainability)?
Kita juga perlu membuat model Dart untuk mencegah error saat runtime. Misalnya, jika kita tidak menggunakan model:
1. Tidak ada validasi tipe. Bisa saja backend mengirim 'price' sebagai String dan bukan int.
2. Tidak ada null-safety. Bisa saja 'name' ternyata null dari backend.
3. Sulit untuk maintain. Ketika data JSON pada backend terus bertambah, files pada proyek Flutter harus dicek satu persatu untuk diganti.
## Apa fungsi package http dan CookieRequest dalam tugas ini? Jelaskan perbedaan peran http vs CookieRequest.
### http adalah package universal yang bercirikhas:
1. mengirim GET/POST request
2. tidak menyimpan session/cookie
### CookieRequest adalah package dari pbp_djangoo_auth yang bercirikhas:
1. menyimpan cookie session Django
2. mengirim cookie tersebut di request berikutnya secara otomatis
3. handling csrf token otomatis
4. mendukung register/login/logout
Perbedaan yang jelas: http digunakan untuk public API, dan CookieRequest digunakan untuk API yang perlu authentication
## Jelaskan mengapa instance CookieRequest perlu untuk dibagikan ke semua komponen di aplikasi Flutter.
Agar session cookie tersimpan, dan bisa dipakai pada instance itu (selama user logged in terus), dan juga agar halaman manapun bisa melakukan authentication request dimanapun dan kapanpun **dengan cookierequest yang sama**.
## Jelaskan konfigurasi konektivitas yang diperlukan agar Flutter dapat berkomunikasi dengan Django. Mengapa kita perlu menambahkan 10.0.2.2 pada ALLOWED_HOSTS, mengaktifkan CORS dan pengaturan SameSite/cookie, dan menambahkan izin akses internet di Android? Apa yang akan terjadi jika konfigurasi tersebut tidak dilakukan dengan benar?
Agar Flutter dapat berkomunikasi dengan Django;
1. perlu adanya 10.0.2.2 pada allowed hosts. Jika tidak ada, Django send httpresponse 400 bad request, invalid host reader.
2. CORS perlu diaktifkan. Karena, tanpa CORS, Django akan memblokir request karena error CORS.
3. SameSite perlu diatur. Jika tidak, Django mengira user tidak logged in pada request selanjutnya.
4. Android perlu diatur izin akses internetnya. Secara default, Emulator ini tidak punya akses ke internet kecuali diaktifkan.
## Jelaskan mekanisme pengiriman data mulai dari input hingga dapat ditampilkan pada Flutter.
1. User input pada Flutter, e.g. form create product
2. Flutter kirim data (konversi dulu dari variabel Dart ke JSON) lewat http atau CookieRequest (POST).
3. Django menerima data, parse request, validasi data, simpan ke DB (kalau perlu), kirim status kembali ke Flutter.
4. Flutter menerima response, jsonDecode(), dan ubah ke model Dart (_.fromJson())
5. Kemudian, Flutter update state (setState()) dan UI diperbaharui.
## Jelaskan mekanisme autentikasi dari login, register, hingga logout. Mulai dari input data akun pada Flutter ke Django hingga selesainya proses autentikasi oleh Django dan tampilnya menu pada Flutter.
1. User input username/password, dan register
2. Flutter kirim request ke Django
3. Django validasi, save user baru, return success/fail
4. Flutter show hasil
1. User input username/password, dan login
2. Flutter kirim request ke Django
3. Django validasi, jika benar, buat session id dan send cookie ke Flutter
4. Langsung ke MyHomePage() karena user sudah login.
1. User logout
2. Flutter kirim request jke Django
3. Django hapus session di DB
4. Flutter hapus cookie
5. User redirect ke login page
## Implementasi Checklist
1. ran python manage.py startapp authentication
2. added authentication to installed apps
3. installed django-cors-headers
4. added corsheaders to installed apps, added middleware
5. added cors config, 10.0.2.2
### login stuff
6. added login on django auth, routing too
7. added auth url to project url
8. install packages to flutter
9. added cookierequest to main.dart
10. login.dart on screens
11. main.dart redirects to loginpage now
### regist and logout stuff
12. added register on django auth, routing too
13. register.dart on screens
14. added logout on django auth, routing too
15. logout func on product card
### models stuff
16. quicktype json shenanigans for dart models
17. AndroidManifest.xml on android/app/src/main uses permission internet
18. added proxy_image() on main/views.py, routing too
19. added product_entry_card.dart
20. added product_entry_list.dart
21. added product_entry_list to left drawer
22. routing all products to entry list in product_card
### details page
23. added product_detail.dart
24. routing from entry list to detail (ontap changed)
### create product
25. added create product flutter on django main, routing too
26. changed onpressed on form