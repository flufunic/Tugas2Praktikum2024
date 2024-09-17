# Tugas Pertemuan 2

Fork dan clone repository ini, lalu jalankan perintah 
```
flutter pub get
```
Buatlah tampilan form yang berisi nama, nim, dan tahun lahir pada file `ui/form_data.dart`, lalu buatlah tampilan hasil dari input data tersebut pada file `ui/tampil_data.dart`

JELASKAN PROSES PASSING DATA DARI FORM MENUJU TAMPILAN DENGAN FILE `README.md`

1.	User menginputkan data berupa nama, NIM, dan tahun lahir ke dalam form di halaman input(form_data.dart). Data tersebut diambil dari tiga TextField yang masing-masing dikontrol oleh controller:
final _namaController = TextEditingController();
final _nimController = TextEditingController();
final _tahunController = TextEditingController();

Saat tombol “simpan” ditekan, data yang diinput akan diambil dari controller ini:
String nama = _namaController.text;
String nim = _nimController.text;
int tahun = int.parse(_tahunController.text);

2.	Setelah data diperoleh dari form, halaman akan berpindah menggunakan Navigator.of(context).push(). Fungsi ini digunakan untuk navigasi ke halaman lain sambil mengirimkan data:
Navigator.of(context).push(
  MaterialPageRoute(
    builder: (context) => TampilData(
      nama: nama,
      nim: nim,
      tahun: tahun,
    ),
  ),
);
Kode ini mengirimkan 3 nilai yang diteruskan ke widget TampilData.

3. Widget TampilData menerima data yang dikirimkan melalui konstruktor:
class TampilData extends StatelessWidget {
  final String nama;
  final String nim;
  final int tahun;

  const TampilData({
    Key? key,
    required this.nama,
    required this.nim,
    required this.tahun,
  }) : super(key: key);
}

Data tersebut digunakan untuk menghitung umur dan ditampilkan dalam teks:
final int umur = DateTime.now().year - tahun;
Text("Nama saya $nama, NIM $nim, dan umur saya adalah $umur tahun"),

4. Proses perpindahan dari form menuju tampilan terjadi menggunakan widget Navigator. MaterialPageRoute berfungsi untuk menampilkan halaman baru (TampilData) yang memanfaatkan data yang telah diinput pada form.
